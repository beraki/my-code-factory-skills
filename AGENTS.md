# Agent workflow

Follow these steps for every task. Drop this file into a repo as `AGENTS.md`.

1. Pick up the task. If it is a Linear issue, mark it In Progress before branching. Example key: BER-12. Use the new-feature skill.

2. Pull the latest main. Branch name is `feature/short-description`, or `<LINEAR-KEY>/short-description` when there is a ticket (example: `BER-12/short-description`).

   ```bash
   git checkout main
   git pull
   git checkout -b feature/short-description
   ```

   With a ticket:

   ```bash
   git checkout -b BER-12/short-description
   ```

3. A worktree is only for when other agents are doing non-blocking work in parallel. If the work overlaps or would block, stop and ask. Do not make a worktree the default.

   Before adding a worktree, check open PRs with `gh pr list` and `gh pr diff <n> --name-only`, and check any uncommitted work in the checkout. Overlap means stop.

4. Build by following the code-structure skill (actions own why and when, services own how, extract only after a second caller).

5. When the work is done, open a PR for Beraki to review. He tests locally and leaves comments. The agent never merges, including after Greptile. If the repo has an integration branch used for deployment, the PR base is integration. If it does not, the PR base is main.

   ```bash
   gh pr create --base integration
   ```

   Use `--base main` when the repo has no integration branch used for deployment.

   The PR body includes a short checklist (what changed, how to test, Linear link if any):

   ```markdown
   ## Checklist

   - [ ] What changed
   - [ ] How to test
   - [ ] Linear link, if any
   ```

   A UI change requires a screenshot or a video on the PR. Use before-and-after when the proof is a page or element comparison.

6. Greptile (greploop) and unslop still run. They do not grant merge permission. Use greploop-apps when Greptile skips the PR for too many files. A clean Greptile review is not permission to merge.

Run unslop on text a person will read before you commit or post it: commit messages, the PR title and body, docs, code comments, and the closing reply.

## Skill sources

| Skill | Source |
|---|---|
| `new-feature` | this pack, written for Beraki's workflow |
| `code-structure`, `evidence-driven-testing` | this pack, copied from [michaelshimeles/skills](https://github.com/michaelshimeles/skills) |
| `before-and-after` | this pack, copied from michaelshimeles/skills, vendored from [vercel-labs/before-and-after](https://github.com/vercel-labs/before-and-after) |
| `greploop` | this pack, copied from michaelshimeles/skills, vendored from [greptileai/skills](https://github.com/greptileai/skills) |
| `greploop-apps` | this pack, copied from michaelshimeles/skills |
| `unslop` | this pack, copied from michaelshimeles/skills, vendored from [cursor/plugins (pstack)](https://github.com/cursor/plugins/tree/main/pstack/skills/unslop) |
