# Go — Fetch, Fix, and Close GitHub Issues

**Fetch open issues from the remote GitHub repository**, then **fix or implement them one by one**. For each issue: implement the fix/feature, **review the changes and check the logic**, commit, then **close the issue** on GitHub.

**Prerequisites:**

- **GitHub CLI** (`gh`) installed and logged in (`gh auth status`). If not, tell the user to install and run `gh auth login`.
- Run from the **repository root** (the repo that `gh` uses as default).

**Steps:**

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
   - **Implement or fix** in the codebase (edit the right files, add tests if applicable).
   - **Review before committing**:
     - Re-read the diff: ensure the change matches the issue and does not break existing behavior.
     - Check logic: edge cases, null/type safety, and that the fix/feature is complete.
     - Run linter on changed files if applicable (`read_lints`); fix any new errors.
   - **Commit**: `git add -A; git commit -m "[Cursor] Fix/Feat: <short summary in English> (closes #<N>)"` (on Windows PowerShell use one line). Use “Fix” for bugs, “Feat” for features/ideas when implementing code. Include `(closes #N)` so GitHub will link and close the issue when pushed.
   - **Close the issue on GitHub**: Run `gh issue close <N> --comment "Fixed in commit <hash>. <one-line summary>."` (replace `<hash>` with the actual commit hash from the previous step, and optionally add a one-line summary). If you prefer not to add a comment, use `gh issue close <N>`.
   - Then proceed to the **next** open issue (re-fetch list if needed, since one was just closed).

3. **Final reply**
   - Summarize: how many issues were processed, which issue numbers were fixed/closed, and the commit hash(es). If any issue was skipped (e.g. unclear scope), say so and leave it open.

**Rules:**

- **One issue → one fix/implementation → one commit → then close that issue.** Do not batch multiple issues into one commit.
- **Always review changes and logic before committing.** Do not commit without checking the diff and behavior.
- Prefer **minimal, correct changes** for bugs; for features/ideas, implement a clear subset if the issue is large.
- Commit messages: start with `[Cursor]`, use English, include `(closes #N)` for the issue being closed.

Run this command when the user wants to pull GitHub issues and work through them (fix/implement, review, commit, close) one by one.
