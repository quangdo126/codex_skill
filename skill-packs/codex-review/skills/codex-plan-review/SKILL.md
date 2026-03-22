---
name: codex-plan-review
description: Review/debate plans before implementation between Claude Code and Codex CLI.
---

# Codex Plan Review

## Purpose
Use this skill to adversarially review a plan before implementation starts.

## When to Use
After creating a plan but before implementing code. Reviews plan quality — not a substitute for `/codex-impl-review` code review. Typical flow: plan → `/codex-plan-review` → refine → implement.

## Prerequisites
- A Markdown plan file exists (e.g. `plan.md`) with headings for sections, steps, or phases.

## Runner

```bash
RUNNER="{{RUNNER_PATH}}"
SKILLS_DIR="$(dirname "$(dirname "$RUNNER")")"
```

## Workflow
1. **Collect inputs**: Auto-detect context and announce defaults before asking anything.
   - **plan-path**: Scan CWD for `plan.md`, `PLAN.md`; also search `docs/` up to 3 levels for `*plan*.md`. If single match → use it. If multiple → list and ask user. If none → ask user for path.
   - **effort**: Default `high` for plan review (plans typically cover significant scope).
   - Announce detected plan path and effort. Proceeding — reply to override.
   - Set `PLAN_PATH` and `EFFORT`. Block only if plan file cannot be found or resolved.
2. Run pre-flight checks (see `references/workflow.md` §1.5).
3. Init session: `node "$RUNNER" init --skill-name codex-plan-review --working-dir "$PWD"` → parse `SESSION_DIR`.
4. Render prompt: `echo '{"PLAN_PATH":"/abs/path","USER_REQUEST":"...","SESSION_CONTEXT":"...","ACCEPTANCE_CRITERIA":"..."}' | node "$RUNNER" render --skill codex-plan-review --template round1 --skills-dir "$SKILLS_DIR"`.
5. Start round 1: `echo "$PROMPT" | node "$RUNNER" start "$SESSION_DIR" --effort "$EFFORT"` → validate JSON output.
6. Poll: `node "$RUNNER" poll "$SESSION_DIR"` — returns JSON with `status`, `review.blocks`, `review.verdict`, and `activities`. Report **specific activities** from the activities array (e.g. which files Codex is reading, what topic it is analyzing). NEVER report generic "Codex is running" — always extract concrete details.
7. Parse `review.blocks` from poll JSON — each block has `id`, `category`, `severity`, `location`, `problem`, `evidence`, `suggested_fix`. Use `review.raw_markdown` as fallback.
8. Apply valid fixes to the plan, **save the plan file**, rebut invalid points with evidence.
9. Render rebuttal: `echo '{"PLAN_PATH":"...","SESSION_CONTEXT":"...","FIXED_ITEMS":"...","DISPUTED_ITEMS":"..."}' | node "$RUNNER" render --skill codex-plan-review --template rebuttal --skills-dir "$SKILLS_DIR"`.
10. **Resume**: `echo "$PROMPT" | node "$RUNNER" resume "$SESSION_DIR" --effort "$EFFORT"` → validate JSON. **Go back to step 6 (Poll).** Repeat steps 6→7→8→9→10 until `APPROVE`, stalemate, or hard cap (5 rounds).
11. Finalize: `echo '{"verdict":"..."}' | node "$RUNNER" finalize "$SESSION_DIR"`.
12. Cleanup: `node "$RUNNER" stop "$SESSION_DIR"`. Return final debate summary, residual risks, and final plan path.

### Effort Level Guide
| Level    | Depth             | Best for                        | Typical time |
|----------|-------------------|---------------------------------|--------------|
| `low`    | Surface check     | Quick sanity check              | ~2-3 min     |
| `medium` | Standard review   | Most day-to-day work            | ~5-8 min     |
| `high`   | Deep analysis     | Important features              | ~10-15 min   |
| `xhigh`  | Exhaustive        | Critical/security-sensitive     | ~20-30 min   |

## Required References
- Detailed execution steps: `references/workflow.md`
- Prompt templates: `references/prompts.md`
- Output contract: `references/output-format.md`

## Rules
- If Claude Code plan mode is active, stay in plan mode during the debate. Otherwise, operate normally.
- Do not implement code in this skill.
- Do not claim consensus without explicit `VERDICT: APPROVE` or user-accepted stalemate.
- Preserve traceability: each accepted issue maps to a concrete plan edit.
- **Runner manages all session state** — do NOT manually read/write `rounds.json`, `meta.json`, or `prompt.txt` in the session directory.
- **No manual file I/O** — Claude NEVER writes files to the session directory. All session state is managed by runner commands (`init`, `start`, `poll`, `resume`, `finalize`, `stop`).
