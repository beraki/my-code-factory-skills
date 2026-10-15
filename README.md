# Code factory skills

This pack is the agent workflow for Beraki's product repos. Each folder is one skill, and `SKILL.md` is the file the agent loads. [`AGENTS.md`](AGENTS.md) is that same workflow in a form you can copy into a product repo.

## Install

```bash
npx skills add beraki/my-code-factory-skills
```

That installs the skill folders. It does not copy `AGENTS.md` into the product repo. Do that step yourself.

## Drop AGENTS.md into a product repo

From the product repo root, save this pack's `AGENTS.md` as `AGENTS.md`:

```bash
curl -fsSL https://raw.githubusercontent.com/beraki/my-code-factory-skills/main/AGENTS.md -o AGENTS.md
```

If you already have a checkout of this pack, copy the file instead:

```bash
cp /path/to/my-code-factory-skills/AGENTS.md ./AGENTS.md
```

The agent reads that file when it works in the product repo. When this pack's workflow changes, replace the product repo's `AGENTS.md` with the new copy. Add that repo's check commands at the bottom of the copied file.

## Workflow

Follow this order.

1. Pick up the task. If it is a Linear issue, mark it In Progress before branching. Example key: BER-12.

2. Pull the latest main. The branch name is `feature/short-description`, or `KEY/short-description` when there is a ticket. Example: `BER-12/short-description`.

   ```bash
   git checkout main
   git pull
   git checkout -b feature/short-description
   ```

   With a ticket:

   ```bash
   git checkout -b BER-12/short-description
   ```

3. A worktree is only for when other agents are doing non-blocking work in parallel. If the work overlaps or would block, stop and ask. Do not make a worktree the default. Before adding one, check open PRs with `gh pr list` and `gh pr diff <n> --name-only`, and check uncommitted work in the checkout.

4. Build with the code-structure skill. Actions own why and when. Services own how. Extract only after a second caller.

5. Caveman is always on for agent replies and for text the agent writes: commit messages, PR bodies, and chat. Apply it to those texts even where the caveman skill says commits and PR bodies stay plain prose.

6. When the work is done, open a pull request for Beraki to review. Every pull request uses `gh pr create --base main`. Never `--base integration`. There is no exception.

   ```bash
   gh pr create --base main
   ```

   The PR body includes a short checklist: what changed, how to test, and a Linear link if any.

7. If the repo has an integration branch, after the change merge that branch directly into integration. Do not open a pull request for that merge.

   ```bash
   git checkout integration
   git pull
   git merge <feature-branch>
   git push
   ```

8. The agent never merges the pull request into main. Beraki tests locally and comments on the PR.

9. A UI change requires a screenshot or a video on the PR. Use before-and-after when the proof is a page or element comparison.

Run unslop on text a person will read before you commit or post it: commit messages, the PR title and body, docs, code comments, and the closing reply.

## Skills

These are the skills in this pack.

### [before-and-after](before-and-after/SKILL.md)

Captures before and after screenshots of a page or element and prints a comparison table for the PR.

### [caveman](caveman/SKILL.md)

Terse voice for agent output. Answer first, drop filler, keep every technical fact. Always on for replies, commit messages, PR bodies, and chat. Apache-2.0 license in the folder.

### [code-structure](code-structure/SKILL.md)

Actions own why and when. Services own how. Extract shared logic only after a second caller.

### [evidence-driven-testing](evidence-driven-testing/SKILL.md)

Records proof while testing. The recorder is `scripts/evidence.py`. `tests/test_evidence.py` smoke-tests it. The workflow above does not require this skill on every task.

### [new-feature](new-feature/SKILL.md)

Starts a task. Mark a Linear issue In Progress, branch from the latest main, and use a worktree only for non-blocking parallel work.

### [unslop](unslop/SKILL.md)

Cuts AI tells from commit messages, PR text, docs, code comments, and replies before you commit or post them.

## Source

This pack adapts [michaelshimeles/skills](https://github.com/michaelshimeles/skills), and caveman is from [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) (Apache-2.0).
