# New — Create GitHub Issue

Create a new issue on the **remote GitHub repository** and post it to the repo’s Issues. The issue is filed into one of three groups by **title prefix**: `[Bug]`, `[Feature]`, or `[Idea]`.

**Groups and prefixes:**

| Group   | Title prefix | Use for |
|--------|---------------|--------|
| bug    | `[Bug]`       | Bugs, defects, things that are broken or wrong |
| feature| `[Feature]`   | New features, enhancements, improvements |
| idea   | `[Idea]`      | Design ideas, suggestions, future possibilities |

**Steps:**

1. **Get issue content from the user**
   - **Group**: One of `bug`, `feature`, `idea`. Infer from the user’s message (e.g. “report a bug: …”, “new feature: …”, “idea: …”) or ask once: “请选择类型：bug / feature / idea” (or “Choose type: bug / feature / idea”).
   - **Title**: Short issue title (without the prefix). If the user only gives a sentence, use it as the title (you will add the prefix).
   - **Body** (optional): Longer description. If the user provided details, use them; otherwise leave body empty or a single line.

2. **Build the issue**
   - **Final title**: `[Bug] <title>` or `[Feature] <title>` or `[Idea] <title>` (no extra space inside brackets).
   - **Body**: User’s description, or a one-line summary, or “—”.

3. **Create the issue on GitHub**
   - Ensure **GitHub CLI** (`gh`) is available and the user is logged in (`gh auth status`). If not, tell the user to install/configure `gh` and run `gh auth login`.
   - **Encoding (important on Windows)**: Passing non-ASCII (e.g. Chinese) in the shell command line can cause **title mojibake** on Windows PowerShell. Always use **temp files in UTF-8** for both title and body, then pass them so that `gh` receives correct bytes:
     1. Write the **final title** (one line, no trailing newline) to `.cursor/tmp_issue_title.txt` in **UTF-8**.
     2. Write the **body** to `.cursor/tmp_issue_body.txt` in **UTF-8**.
     3. From the **repository root**, run (PowerShell):  
        `$title = Get-Content -Path ".cursor/tmp_issue_title.txt" -Encoding UTF8 -Raw; $title = $title.Trim(); gh issue create --title $title --body-file ".cursor/tmp_issue_body.txt"`
     4. After success, delete both `.cursor/tmp_issue_title.txt` and `.cursor/tmp_issue_body.txt`.
   - Use the current repo (default for `gh` when run inside the repo). If the user wants a different repo, they must say so; otherwise use the default.

4. **Reply to the user**
   - On success: show the issue URL (from `gh` output) and a one-line summary, e.g. “已在 GitHub 创建 Issue: [Bug] xxx — <url>” / “Created GitHub issue: [Bug] xxx — <url>”.
   - On failure: report the error and suggest checking `gh auth status` and network.

**Rules:**

- Always add exactly one prefix to the title: `[Bug]`, `[Feature]`, or `[Idea]`.
- Do not create a local file under `docs/bugs/` or `docs/ideas/` for this command; this command only creates a **remote GitHub issue**.
- Prefer inferring group and title from the user’s message; only ask when unclear.

Run this command when the user wants to open a new issue on GitHub (e.g. “/new bug: title here” or “/new create a feature issue …”).
