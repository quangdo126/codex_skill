# CLAUDE.md

This repository ships an npm CLI (`codex-skill`) that installs the `codex-review` skill pack into Claude skill directories.

## Project Overview

`codex-review` provides three skills powered by OpenAI Codex CLI:
- `/codex-plan-review` — debate plans before implementation
- `/codex-impl-review` — review uncommitted changes before commit
- `/codex-think-about` — peer reasoning/debate on technical topics

## Distribution Model

- Global scope install: `~/.claude/skills/codex-review`
- Project scope install: `<project>/.claude/skills/codex-review`
- Installed by `codex-skill init -g` or `codex-skill init`

## Requirements

- Node.js >= 20
- Claude Code CLI
- OpenAI Codex CLI in PATH (`codex`)
- OpenAI API key configured for Codex

## Development Commands

```bash
node ./bin/codex-skill.js --help
node ./bin/codex-skill.js doctor
node skill-packs/codex-review/scripts/codex-runner.js version
```

There is no build system, test suite, or linter. The project is JavaScript + Markdown + JSON.

## Architecture

### CLI Layout

```text
bin/codex-skill.js
src/cli/
src/commands/
src/lib/
```

### Skill Pack Layout

```text
skill-packs/codex-review/
├── manifest.json
├── scripts/
│   └── codex-runner.js          ← single shared Node.js runner
└── skills/
    ├── codex-plan-review/
    │   ├── SKILL.md
    │   └── references/
    ├── codex-impl-review/
    │   ├── SKILL.md
    │   └── references/
    └── codex-think-about/
        ├── SKILL.md
        └── references/
```

### Core Execution Flow

1. **Skill invocation** (`/codex-plan-review`, `/codex-impl-review`, or `/codex-think-about`) follows SKILL.md step-by-step
2. **Runner resolution**: SKILL.md resolves `scripts/codex-runner.js` from project-local or global scope
3. **codex-runner.js** spawns `codex exec --json --sandbox read-only` as a detached process, polls JSONL output
4. **Review debate loop** (plan-review, impl-review): Claude Code parses Codex's `ISSUE-{N}` review → fixes/rebuts → resumes via `--thread-id` → repeats until `APPROVE` verdict or stalemate
5. **Peer debate loop** (think-about): Claude Code and Codex think independently → discuss → exchange perspectives → repeat until consensus or stalemate → present to user

### Key Design Decisions

- **Node.js runner**: `codex-runner.js` uses Node.js stdlib only — no Python/bash dependency
- **Cross-platform**: Works on Windows, macOS, and Linux
- **Prompt minimalism**: Prompts contain only file paths and context; Codex reads files/diffs itself
- **Structured output**: Review skills use `ISSUE-{N}` format with `VERDICT` block; think-about uses Key Insights / Considerations / Recommendations
- **Thread persistence**: First call creates a thread; subsequent rounds use `codex exec resume <thread_id>`
- **Stalemate detection**: Stops if same points repeat for 2 consecutive rounds with no progress
- **PID-reuse protection**: `verifyCodex()` and `verifyWatchdog()` check process cmdline before killing — prevents killing wrong process if OS reuses the PID

### codex-runner.js Exit Codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 2 | Timeout (default 3600s) |
| 3 | Turn failed |
| 4 | Stalled (no output for ~3 minutes) |
| 5 | Codex CLI not found in PATH |

## Design Principles

- Progressive disclosure: keep `SKILL.md` lean (~40–70 lines).
- Move long prompts/protocol details into `references/`.
- Single shared runner at skill-pack level, not duplicated per skill.

## Verification

1. `node bin/codex-skill.js --help` — CLI hoạt động
2. `node bin/codex-skill.js init -g --force` — install thành công
3. `node skill-packs/codex-review/scripts/codex-runner.js version` — in version `8`
4. `node bin/codex-skill.js doctor` — tất cả checks pass
5. Invoke `/codex-plan-review`, `/codex-impl-review`, `/codex-think-about` trong Claude Code
