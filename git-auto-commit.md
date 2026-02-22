# Auto-commit to Git

Stage all changes and commit to Git with a message starting with `[Cursor]`.

1. Run: `git add -A`
2. Run: `git commit -m "[Cursor] <short description of changes in English>"`
   - On Windows PowerShell, use one line: `git add -A; git commit -m "[Cursor] <description>"`
3. If there is nothing to commit (working tree clean), reply that there was nothing to commit; otherwise perform the commit and show the commit hash.

Do not ask for confirmation. Use a brief, clear description for the commit message (e.g. "Add damage float numbers", "Fix enemy name encoding").

---

**Reminder for AI:** After each modification (edits, new files, or fixes), run this command (or `/git-auto-commit`) to automatically stage and commit changes to Git, unless the user explicitly asks not to.
