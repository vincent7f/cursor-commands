# Idea

Record the user's **design ideas, feature implementations, game rules, display rules, and related thoughts** into a single markdown file for the day.

**Output:**

- **Path**: Save under `docs/ideas/`.
- **Filename**: **One file per day**, named by **date only**: `YYYYMMDD.md` (e.g. `20260112.md`). Use the **current date** (e.g. run `Get-Date -Format "yyyyMMdd"` on Windows PowerShell). If the file for that date already exists, **append** the new content to it (with a clear separator such as a time-stamped section or horizontal rule); otherwise create the new file.
- **Content**: Organize whatever the user shared in this turn (and any relevant follow-up from the conversation) into sections as appropriate, e.g.:
  - 设计想法 / Design ideas
  - 功能点实现 / Feature implementations
  - 游戏规则 / Game rules
  - 显示规则 / Display rules
  - 其他思考 / Other notes

Use a mix of Chinese and English to match how the user expressed things. If the user only gave a short prompt (e.g. "add X"), infer from the conversation what was designed or decided and record that.

**Steps:**

1. Get today's date and form the filename `YYYYMMDD.md`.
2. Ensure `docs/ideas/` exists (create the directory if needed).
3. If `docs/ideas/YYYYMMDD.md` already exists, read it and append a new section (e.g. with a time or "Session" header); otherwise start a new file.
4. Write or append the consolidated content.
5. Reply with the file path and a one-sentence summary (e.g. "已记录到 docs/ideas/20260112.md" / "Recorded to docs/ideas/20260112.md").

Do not ask for confirmation before writing. Run this command whenever the user wants to capture their ideas and decisions for the day.
