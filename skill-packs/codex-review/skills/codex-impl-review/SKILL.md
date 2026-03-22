---
name: codex-impl-review
description: Have Codex CLI review uncommitted code changes or branch diff against a base branch. Claude applies valid fixes, rebuts invalid points, and iterates until consensus or user-approved stalemate.
---

# Codex Implementation Review

## Purpose
Use this skill to run adversarial review on uncommitted changes before commit, or on branch changes before merge.

## When to Use
After writing code, before committing. Use for uncommitted working-tree changes or comparing a branch against base. For security-sensitive code, run `/codex-security-review` alongside this.

## Prerequisites
- **Working-tree mode** (default): working tree has staged or unstaged changes.
- **Branch mode**: current branch differs from base branch (has commits not in base).

## Runner

```bash
RUNNER="{{RUNNER_PATH}}"
SKILLS_DIR="{{SKILLS_DIR}}"
```

## Workflow
1. **Collect inputs**: Auto-detect context and announce defaults before asking anything.
   - **scope** (detected first): Run `git status --short | grep -v '^??'` — non-empty output → `working-tree`. Else run `git rev-list @{u}..HEAD` — non-empty → `branch`. If both conditions true, use `working-tree`. If neither, ask user.
   - **effort** (adapts to detected scope): If scope=`branch`, count `git diff --name-only @{u}..HEAD`; else count `git diff --name-only`. Result <10 → `medium`, 10–50 → `high`, >50 → `xhigh`; default `high` if undetectable.
   - Announce: "Detected: scope=`$SCOPE`, effort=`$EFFORT` (N files changed). Proceeding — reply to override scope, effort, or both."
   - Set `SCOPE` and `EFFORT`. Only block for inputs that remain undetectable.
2. Run pre-flight checks (see `references/workflow.md` §1.5).
3. **Init session**: `node "$RUNNER" init --skill-name codex-impl-review --working-dir "$PWD"` → parse `SESSION_DIR` from output `CODEX_SESSION:<path>`.
4. **Render prompt**: `echo '{"USER_REQUEST":"...","SESSION_CONTEXT":"..."}' | node "$RUNNER" render --skill codex-impl-review --template <template> --skills-dir "$SKILLS_DIR"` (template = `working-tree-round1` or `branch-round1`; add `"BASE_BRANCH":"..."` for branch mode).
5. **Start**: `echo "$PROMPT" | node "$RUNNER" start "$SESSION_DIR" --effort "$EFFORT"` → validate JSON `{"status":"started","round":1}`.
6. **Poll**: `node "$RUNNER" poll "$SESSION_DIR"` → returns JSON with `status`, `review.blocks`, `review.verdict`, and `activities`. Report **specific activities** from the activities array (e.g. which files Codex is reading, what topic it is analyzing). NEVER report generic "Codex is running" — always extract concrete details.
7. **Apply/Rebut**: Read issues from poll JSON `review.blocks[]` — each has `id`, `title`, `severity`, `category`, `location`, `problem`, `evidence`, `suggested_fix`. Fix valid issues in code; rebut invalid findings with evidence. Use `review.raw_markdown` as fallback.
8. **Render rebuttal**: `echo '{"USER_REQUEST":"...","SESSION_CONTEXT":"...","FIXED_ITEMS":"...","DISPUTED_ITEMS":"..."}' | node "$RUNNER" render --skill codex-impl-review --template rebuttal-working-tree --skills-dir "$SKILLS_DIR"` (or `rebuttal-branch` + `"BASE_BRANCH":"..."` for branch mode).
9. **Resume**: `echo "$PROMPT" | node "$RUNNER" resume "$SESSION_DIR" --effort "$EFFORT"` → validate JSON. **Go back to step 6 (Poll).** Repeat steps 6→7→8→9 until `review.verdict.status === "APPROVE"`, stalemate, or hard cap (5 rounds).
10. **Finalize**: `echo '{"verdict":"...","scope":"..."}' | node "$RUNNER" finalize "$SESSION_DIR"`.
11. **Cleanup**: `node "$RUNNER" stop "$SESSION_DIR"`. Return final review summary, residual risks, and recommended next steps.

### Effort Level Guide
| Level    | Depth             | Best for                        | Typical time |
|----------|-------------------|---------------------------------|-------------|
| `low`    | Surface check     | Quick sanity check              | ~2-3 min |
| `medium` | Standard review   | Most day-to-day work            | ~5-8 min |
| `high`   | Deep analysis     | Important features              | ~10-15 min |
| `xhigh`  | Exhaustive        | Critical/security-sensitive     | ~20-30 min |

## Required References
- Detailed execution: `references/workflow.md`
- Prompt templates: `references/prompts.md`
- Output contract: `references/output-format.md`

## Rules
- If invoked during Claude Code plan mode, exit plan mode first — this skill requires code editing.
- Codex reviews only; it does not edit files.
- Preserve functional intent unless fix requires behavior change.
- Every accepted issue must map to a concrete code diff.
- If stalemate persists, present both sides and defer to user.
- **Runner manages all session state** — do NOT manually read/write `rounds.json`, `meta.json`, or `prompt.txt` in the session directory.
