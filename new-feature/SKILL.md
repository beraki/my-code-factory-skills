---
name: new-feature
description: Pick up a task, mark a Linear issue In Progress, and branch from the latest main before writing code. Use at the start of every feature, fix, or task. A worktree is only for non-blocking work other agents are doing in parallel. If the work overlaps or would block, stop and ask.
---

# New feature

Caveman is always on for agent replies and for text the agent writes: commit messages, PR bodies, and chat. Apply it to those texts even where the caveman skill says commits and PR bodies stay plain prose.

1. Pick up the task. If it is a Linear issue, mark it In Progress before branching. Example key: BER-12.

2. Pull the latest main. Branch name is `feature/short-description`, or `<LINEAR-KEY>/short-description` when there is a ticket (example: `BER-12/short-description`).

   ```bash
   git checkout main
   git pull
   git checkout -b feature/short-description
   ```

   With a ticket:

   ```bash
   git checkout main
   git pull
   git checkout -b BER-12/short-description
   ```

3. A worktree is only for when other agents are doing non-blocking work in parallel. If the work overlaps or would block, stop and ask. Do not make a worktree the default.

   Before adding a worktree, check open PRs with `gh pr list` and `gh pr diff <n> --name-only`, and check any uncommitted work in the checkout. Overlap means stop.

4. Build by following the code-structure skill (actions own why and when, services own how, extract only after a second caller).

5. When the work is done, open a PR for Beraki to review. Every pull request uses `gh pr create --base main`. Never `--base integration`. There is no exception.

   ```bash
   gh pr create --base main
   ```

   The agent never merges the pull request into main. He tests locally and comments on the PR.

   If the repo has an integration branch, after the change merge that branch directly into integration. Do not open a pull request for that merge.

   ```bash
   git checkout integration
   git pull
   git merge <feature-branch>
   git push
   ```

   The PR body includes a short checklist (what changed, how to test, Linear link if any):

   ```markdown
   ## Checklist

   - [ ] What changed
   - [ ] How to test
   - [ ] Linear link, if any
   ```

   A UI change requires a screenshot or a video on the PR. Use before-and-after when the proof is a page or element comparison.

6. Run unslop on text a person will read before you commit or post it: commit messages, the PR title and body, docs, code comments, and the closing reply.
