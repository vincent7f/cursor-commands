# Bug

Collect the **bug report** from the user (and any relevant context from the conversation), organize it, and save it under `docs/bugs/` as **one file per bug** with a **timestamp in the filename**.

**Output:**

- **Path**: Save under `docs/bugs/`.
- **Filename**: One file per bug, named with **date and time**: `bug_YYYYMMDD_HHmm.md` (e.g. `bug_20260221_1430.md`). Use the **current date and time** (e.g. on Windows PowerShell: `Get-Date -Format "yyyyMMdd_HHmm"`). If the user reports multiple distinct bugs in one turn, create one file per bug (e.g. `bug_20260221_1430.md`, `bug_20260221_1431.md`).
- **Content**: Organize the reported problem into sections, e.g.:
  - **Title** (one-line summary)
  - **描述 / Description** (what went wrong, expected vs actual)
  - **复现步骤 / Steps to reproduce** (if provided or inferable)
  - **环境 / Environment** (Godot version, OS, scene/script if relevant — infer or ask briefly)
  - **相关文件 / Related files** (paths mentioned or involved)
  - **状态 / Status** (e.g. `open`, `fixed` — default `open`)
  - **备注 / Notes** (extra context from the conversation)

Use a mix of Chinese and English to match how the user described the bug. If the user only gives a short description, infer from the conversation (e.g. which feature, which scene) and fill in what you can.

**Steps:**

1. Get current date and time and form the filename `bug_YYYYMMDD_HHmm.md`.
2. Ensure `docs/bugs/` exists (create the directory if needed).
3. Write the bug report to `docs/bugs/bug_YYYYMMDD_HHmm.md`.
4. Reply with the file path and a one-sentence summary (e.g. "已记录到 docs/bugs/bug_20260221_1430.md" / "Recorded to docs/bugs/bug_20260221_1430.md").

Do not ask for confirmation before writing. Run this command whenever the user wants to record a bug report.
