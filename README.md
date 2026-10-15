# Code factory skills

Skills for Beraki's coding workflow. Each folder is one skill. The agent loads `SKILL.md` when the task matches the description. [`AGENTS.md`](AGENTS.md) is the workflow to drop into a repo.

## Install

```bash
npx skills add beraki/my-code-factory-skills
```

## Skills

### [before-and-after](before-and-after/SKILL.md)

Captures before and after screenshots and prints a PR-ready comparison table.

### [code-structure](code-structure/SKILL.md)

Actions own why and when. Services own how. Extract shared logic only after a second caller.

### [evidence-driven-testing](evidence-driven-testing/SKILL.md)

Records proof while testing. UI changes can be a video. Other changes use measured output. The recorder is `scripts/evidence.py`, and `tests/test_evidence.py` smoke-tests it.

### [new-feature](new-feature/SKILL.md)

Picks up the task, marks a Linear issue In Progress, and branches from the latest main. A worktree is only for non-blocking work other agents are doing in parallel.

### [unslop](unslop/SKILL.md)

Edits commit messages, PR text, docs, and other prose a person will read.

## Source

This pack adapts [michaelshimeles/skills](https://github.com/michaelshimeles/skills). `code-structure`, `evidence-driven-testing`, `before-and-after`, and `unslop` are unchanged, including their licenses and scripts. `new-feature`, `AGENTS.md`, and this README follow Beraki's branch and ship workflow.

Every pull request uses `gh pr create --base main`. Never `--base integration`. There is no exception.

If the repo has an integration branch, after the change merge that branch directly into integration. Do not open a pull request for that merge.

The agent never merges the pull request into main. He tests locally and comments on the PR.
