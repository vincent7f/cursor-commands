# Build Model

Analyze the **current codebase** to derive a **game model** (entities, state, systems, data flow, and key structures), then save it as a single markdown document under `docs/models/`. The file must include the **current Git commit ID** used for the analysis.

**Output:**

- **Path**: Save under `docs/models/`.
- **Model file**: Filename must include the current **timestamp**: `model_YYYYMMDD_HHmm.md` (e.g. `model_20260221_1430.md`). Use the system date/time (e.g. on Windows PowerShell: `Get-Date -Format "yyyyMMdd_HHmm"`).
- **Diagram file**: Same timestamp, name `model_YYYYMMDD_HHmm_diagram.md` — a markdown file that contains a **Mermaid diagram** (in a fenced code block ` ```mermaid `) so the model can be viewed visually (e.g. on GitHub or in Mermaid-capable editors).
- **Model content**: A structured game model document that includes:
  - **Metadata**: `git_commit_id` (full commit hash from `git rev-parse HEAD` at analysis time), timestamp, and optional one-line summary.
  - **Entities**: Player, enemies, cards, treasures (法宝), status effects—what they are and where they are defined (scripts/data).
  - **State**: Global and per-scene state (e.g. GameManager vars, combat state, map state).
  - **Systems**: Combat, map, rewards, shop, rest, localization—how they interact and which scripts/scenes own them.
  - **Data flow**: Key transitions (e.g. main menu → map → battle → reward → map), where data is read/written (e.g. deck, gold, treasures).
  - **Data sources**: JSON/data files (cards, enemies, treasures, maps, translations) and how they are loaded.

Use clear sections and subsections; tables or bullet lists are fine. Use a mix of Chinese and English as fits the project. Base the model **only on the current code** (and referenced data files), not on plans or docs unless they reflect implemented behavior.

**Diagram content (Mermaid):** Generate a diagram that visualizes the model, e.g.:
- **Flowchart** of scene/state flow: main_menu → map → battle | rest | shop → reward → map → … (victory/game_over).
- **Graph** of main entities (Player, Enemy, Card, Treasure, GameManager) and systems (Combat, Map, Reward, Tavern, Rest) with short labels; optional arrows for “uses” or “owns”.
Use `flowchart LR` or `flowchart TB` (or `graph`) and standard Mermaid syntax so it renders correctly. The diagram file should start with a brief title (e.g. `# Game Model Diagram — YYYYMMDD_HHmm`) and then a single ` ```mermaid ` code block containing the diagram.

**Steps:**

1. Get the current **Git commit ID**: run `git rev-parse HEAD` and record the result.
2. Get the current **timestamp** and form the base name `model_YYYYMMDD_HHmm`.
3. Ensure `docs/models/` exists (create the directory if needed).
4. Analyze the codebase (e.g. `src/`, `data/`, key scenes in `scenes/`, autoloads in `project.godot`) to extract entities, state, systems, and data flow.
5. Write the consolidated model document to `docs/models/<base_name>.md`, with the **first section** containing at least: `git_commit_id`, timestamp, and (optional) one-line summary.
6. **Generate the diagram file**: Write `docs/models/<base_name>_diagram.md` containing a title and one Mermaid code block that depicts the game model (scene flow and/or entities–systems relationship) for visual review.
7. **Auto-commit**: Run `git add -A`, then `git commit -m "[Cursor] Build model: <base_name>"` (e.g. on Windows PowerShell: `git add -A; git commit -m "[Cursor] Build model: model_20260221_1430"`). If there is nothing to commit (working tree clean), say so in the reply; otherwise include the new commit hash in the reply.
8. Reply with the paths to both the model file and the diagram file, the commit ID used for analysis, and (if a commit was made) the new commit hash (e.g. "已保存到 docs/models/model_20260221_1430.md 与 model_20260221_1430_diagram.md，分析 commit: abc1234，已提交: def5678" / "Saved to ... .md and ... _diagram.md, analysis commit: abc1234, committed: def5678").

Do not ask for confirmation before writing the files.
