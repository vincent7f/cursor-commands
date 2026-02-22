# Todo

Collect the **to-do / requirements to implement** from the user (and any relevant context from the conversation), organize them, and save under `docs/todos/` with **one file per day** (all todos for the same day go in that day's file).

**Output:**

- **Path**: Save under `docs/todos/`.
- **Filename**: **One file per day**, named by **date only**: `YYYYMMDD.md` (e.g. `20260221.md`). Use the **current date** (e.g. on Windows PowerShell: `Get-Date -Format "yyyyMMdd"`). If the file for that date already exists, **append** the new content to it (with a clear separator such as a time-stamped section or horizontal rule); otherwise create a new file.
- **Content**: Organize the requested todos into sections, e.g.:
  - **待实现需求 / To-do** (list of items to implement; use bullets or checklist `- [ ]`)
  - **优先级 / Priority** (if mentioned: high / medium / low, or 高/中/低)
  - **相关模块 / Related** (e.g. combat, map, card, UI — infer from context)
  - **备注 / Notes** (dependencies, acceptance criteria, or extra context)

Use a mix of Chinese and English to match how the user expressed things. If the user only gives a short prompt (e.g. "add X"), infer from the conversation what needs to be done and record it.

**Steps:**

1. Get today's date and form the filename `YYYYMMDD.md`.
2. Ensure `docs/todos/` exists (create the directory if needed).
3. If `docs/todos/YYYYMMDD.md` already exists, read it and append a new section (e.g. with a time or "Session" header); otherwise start a new file.
4. Write or append the consolidated todo content.
5. Reply with the file path and a one-sentence summary (e.g. "已记录到 docs/todos/20260221.md" / "Recorded to docs/todos/20260221.md").
6. **Auto-commit**: Run `git add -A`, then `git commit -m "[Cursor] Todo: <short description in English>"` (e.g. on Windows PowerShell: `git add -A; git commit -m "[Cursor] Todo: <description>"`). If there is nothing to commit (working tree clean), say so in the reply; otherwise include the commit hash in the reply.

Do not ask for confirmation before writing. Run this command whenever the user wants to record implementation todos or requirements for the day.
