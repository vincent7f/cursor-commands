# Kill Ideas

**Implement ideas one by one** that are documented under `docs/ideas/`. After implementing **each** idea, **automatically commit once** (stage + commit with a clear message).

**Steps:**

1. **List idea files** in `docs/ideas/` (e.g. `YYYYMMDD.md`). Ignore non-markdown files. Process files in a sensible order (e.g. by date, oldest first).
2. **For each idea file**, read it and find **implementable items**, e.g.:
   - Lines under **功能点实现 / Feature implementations** that say **待实现：...** (to implement: ...).
   - Distinct bullets under **设计想法 / Design ideas** or **游戏规则 / Game rules** or **显示规则 / Display rules** that describe a concrete feature or rule to implement.
   Treat each such item as one idea. If a section has multiple bullets, each bullet can be one idea unless they are clearly one single feature.
3. **For each implementable item** (one at a time):
   - **Implement the idea** in the codebase using the item’s description and any 其他思考 / Notes in the same file.
   - **Update the idea document**: mark the item as done (e.g. change `待实现：X` to `待实现：X（已实现）`, or add `[x]` / “已实现” next to it, or add a short “实现说明”).
   - **Commit immediately**: run `git add -A`, then `git commit -m "[Cursor] Idea: <short summary in English>"` (on Windows PowerShell use one line: `git add -A; git commit -m "[Cursor] Idea: <summary>"`).
   - Then proceed to the **next** implementable idea (same file or next file).
4. If there are **no** idea files or **no** implementable items left, reply briefly (e.g. “No open ideas in docs/ideas/” / “docs/ideas/ 下暂无待实现的 idea”).
5. When done with all implementable ideas (or when the user stops), reply with a short summary: which ideas were implemented and the commit hash(es).

**Rules:**

- One idea → one implementation → one commit. Do not batch multiple ideas into a single commit unless the user asks otherwise.
- Use the idea file’s **其他思考 / Other notes** and surrounding context to locate and implement in the right place.
- Keep commit messages in English and concise (e.g. `[Cursor] Idea: probability-based card effect for Tang Monk`).

Run this command when the user wants to implement all (or the next) recorded ideas in `docs/ideas/`.
