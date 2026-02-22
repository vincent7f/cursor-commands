# Review Today

Review **today's conversation** and produce a single consolidated markdown document that covers:

1. **Design ideas** – any design decisions, product or UX ideas discussed.
2. **Feature implementations** – what was built or changed (with file/component references where relevant).
3. **Game rules** – combat, damage types, status effects, map, progression, etc.
4. **Display / UI rules** – floating numbers, colors, animations, map roads, localization, etc.

**Output:**

- **Path**: Save the document under `docs/reviews/`.
- **Filename**: Must include the current **timestamp** (e.g. `review_YYYYMMDD_HHmm.md`). Use the system date/time to generate it (e.g. run `Get-Date -Format "yyyyMMdd_HHmm"` on Windows PowerShell).
- **Format**: Clear sections and subsections; use tables or lists where they help. Write in a mix of Chinese and English as fits the project (e.g. terms and rules in Chinese where that was used in the conversation).

**Conflict rule:** If any part of the conversation contradicts an earlier statement (e.g. “use X” then “use Y instead”), **the later requirement wins**. Note in the doc where you applied this (e.g. “以后续修改为准”).

**Steps:**

1. Scan the full conversation (and any referenced docs like `docs/feature_log_*.md`, `docs/design/floating_numbers.md`) for the above four areas.
2. Generate the timestamp and filename.
3. Ensure `docs/reviews/` exists (create it if needed).
4. Write the consolidated `.md` file to `docs/reviews/<filename_with_timestamp>.md`.
5. Reply with the file path and a one-sentence summary of what was recorded.

Do not ask for confirmation before writing the file.
