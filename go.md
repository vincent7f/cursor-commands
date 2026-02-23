# Go — Fetch, Fix, and Close GitHub Issues

**Fetch open issues from the remote GitHub repository**, then **fix or implement them one by one**. For each issue: implement the fix/feature, **review the changes and check the logic**, commit, then **close the issue** on GitHub.

**Prerequisites:**

- **GitHub CLI** (`gh`) installed and logged in (`gh auth status`). If not, tell the user to install and run `gh auth login`.
- Run from the **repository root** (the repo that `gh` uses as default).

**Steps:**

0. **Create and switch to a dev branch (before any other work)**
   - Branch name: `dev-<today>`, where `<today>` is the current date `yyyyMMdd` (e.g. `dev-20260223`). **The same branch is used for the whole day** (every `/go` run on the same day uses the same branch).
   - From repo root: if the branch already exists, run `git checkout dev-<today>`; otherwise run `git checkout -b dev-<today>`. On Windows PowerShell: `$today = Get-Date -Format "yyyyMMdd"; $branch = "dev-$today"; git rev-parse --verify $branch 2>$null; if ($LASTEXITCODE -eq 0) { git checkout $branch } else { git checkout -b $branch }`.
   - All subsequent steps (fetch issues, fix, commit, close) run on this branch; **main is not modified directly**.

1. **Fetch open issues**
   - Run: `gh issue list --state open --limit 50` (or a reasonable limit).
   - Parse the output to get issue numbers and titles. If there are no open issues, reply with “No open issues” / “暂无打开的 Issue” and stop.

2. **For each open issue** (in order, e.g. by issue number):
   - **Fetch full issue**: `gh issue view <N>` to get title, body, and labels.
   - **Interpret the issue**: Use the title prefix to decide how to handle it:
     - `[Bug]` — Fix the bug in the codebase (find root cause, minimal fix).
     - `[Feature]` — Implement the feature as described (or a reasonable scope).
     - `[Idea]` — Implement the idea or document it; if implementation is small, do it; otherwise implement what’s feasible or add a short design note.
     - `[UI]` — UI-only change (layout, animation, display, alignment); implement as described.
     - `[Todo]` — General task or unspecified; implement as described or treat as feature/task.
   - **Check if already done**: Before implementing, search/inspect the codebase to see whether the described functionality is already implemented or the described bug is already fixed. If it is:
     - Do **not** make any code changes or commit.
     - Close the issue with a comment that it is already done (e.g. “Already implemented / 已实现，无需修改” or “Bug already fixed / 问题已修复，无需修改”). Use: `gh issue close <N> --comment "Already implemented/fixed in codebase; no change needed. 代码中已实现/已修复，无需修改。"`.
     - Then proceed to the **next** open issue; do not implement or commit for this one.
   - **Implement or fix** in the codebase (edit the right files, add tests if applicable) only when the above check shows it is **not** already done.
   - **Review before committing**:
     - Re-read the diff: ensure the change matches the issue and does not break existing behavior.
     - Check logic: edge cases, null/type safety, and that the fix/feature is complete.
     - Run linter on changed files if applicable (`read_lints`); fix any new errors.
   - **Commit**: `git add -A; git commit -m "[Cursor] Fix/Feat: <short summary in English> (closes #<N>)"` (on Windows PowerShell use one line). Use “Fix” for bugs, “Feat” for features/ideas when implementing code. Include `(closes #N)` so GitHub will link and close the issue when pushed.
   - **Close the issue on GitHub**: Run `gh issue close <N> --comment "Fixed in commit <hash>. <one-line summary>."` (replace `<hash>` with the actual commit hash from the previous step, and optionally add a one-line summary). If you prefer not to add a comment, use `gh issue close <N>`.
   - Then proceed to the **next** open issue (re-fetch list if needed, since one was just closed).

3. **Final reply**
   - Summarize: branch name used (`dev-<today>`), how many issues were processed, which were fixed with a commit, which were closed as already implemented (no code change), and the commit hash(es) where applicable. If any issue was skipped (e.g. unclear scope), say so and leave it open. Remind the user that changes are on the dev branch and can be merged to `main` when ready.

**Rules:**

- **Before implementing**, always check whether the issue is already satisfied by the current codebase; if so, close it as “already implemented/fixed” with a comment and do not commit.
- **One issue → one fix/implementation → one commit → then close that issue.** Do not batch multiple issues into one commit. (Issues closed as already done do not require a commit.)
- **Always review changes and logic before committing.** Do not commit without checking the diff and behavior.
- Prefer **minimal, correct changes** for bugs; for features/ideas, implement a clear subset if the issue is large.
- Commit messages: start with `[Cursor]`, use English, include `(closes #N)` for the issue being closed.

Run this command when the user wants to pull GitHub issues and work through them (fix/implement, review, commit, close) one by one.
