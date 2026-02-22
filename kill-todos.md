# Kill Todos

**Implement todos one by one** that are documented under `docs/todos/`. After implementing **each** todo, **automatically commit once** (stage + commit with a clear message).

**Steps:**

1. **List todo files** in `docs/todos/` (e.g. `YYYYMMDD.md`). Ignore `.gitkeep` and non-markdown files. Process files in a sensible order (e.g. by date).
2. **For each todo file**, read it and find **unchecked** items (lines like `- [ ] **...**` or `- [ ] ...` under 待实现需求 / To-do).
3. **For each unchecked item** (one at a time):
   - **Implement the todo** in the codebase using the item’s description and the file’s 相关模块、备注.
   - **Update the todo document**: change that item from `- [ ]` to `- [x]`, and optionally add a short “实现说明” under the item or in 备注 (e.g. which file/change).
   - **Commit immediately**: run `git add -A`, then `git commit -m "[Cursor] Todo: <short summary in English>"` (on Windows PowerShell use one line: `git add -A; git commit -m "[Cursor] Todo: <summary>"`).
   - Then proceed to the **next** unchecked todo (same file or next file).
4. If there are **no** todo files or **no** unchecked items, reply briefly (e.g. “No open todos in docs/todos/” / “docs/todos/ 下暂无待实现的 todo”).
5. When done with all unchecked todos (or when the user stops), reply with a short summary: which todos were implemented and the commit hash(es).

**Rules:**

- One todo → one implementation → one commit. Do not batch multiple todos into a single commit unless the user asks otherwise.
- Use the todo file’s **相关模块 / Related** and **备注 / Notes** to locate and implement in the right place.
- Keep commit messages in English and concise (e.g. `[Cursor] Todo: show full card layout on upgrade screen`).

Run this command when the user wants to implement all (or the next) recorded todos in `docs/todos/`.
