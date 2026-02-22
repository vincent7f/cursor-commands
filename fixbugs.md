# Fix Bugs

**Fix bugs one by one** that are documented under `docs/bugs/`. After fixing **each** bug, **automatically commit once** (stage + commit with a clear message).

**Steps:**

1. **List bug files** in `docs/bugs/` (e.g. `bug_YYYYMMDD_HHmm.md`). Ignore `.gitkeep` and non-markdown files.
2. **For each bug file** (in a sensible order, e.g. by filename/timestamp):
   - Read the file. If **状态 / Status** is already `fixed` (or equivalent), skip it.
   - If status is `open` (or absent):
     - **Fix the bug** in the codebase using the bug’s 描述、复现步骤、相关文件、备注.
     - **Update the bug document**: set 状态 / Status to `fixed`, and optionally add a short “修复说明” (e.g. which file/change fixed it).
     - **Commit immediately**: run `git add -A`, then `git commit -m "[Cursor] Fix: <short bug title or summary in English>"` (on Windows PowerShell use one line: `git add -A; git commit -m "[Cursor] Fix: <summary>"`).
     - Then proceed to the **next** bug file (if any).
3. If there are **no** bug files or **no open** bugs, reply briefly (e.g. “No open bugs in docs/bugs/” / “docs/bugs/ 下暂无待修复的 bug”).
4. When done with all open bugs, reply with a short summary: which bugs were fixed and the commit hash(es).

**Rules:**

- One bug → one fix → one commit. Do not batch multiple bug fixes into a single commit unless the user asks otherwise.
- Use the bug document’s **相关文件 / Related files** and **备注 / Notes** to locate and change the right code.
- Keep commit messages in English and concise (e.g. `[Cursor] Fix: deduct card cost before playing to prevent over-spend`).

Run this command when the user wants to fix all (or the next) recorded bugs in `docs/bugs/`.
