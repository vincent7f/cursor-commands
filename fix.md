# Fix

**Deep analysis and minimal fix** based on the information provided by the user (text description and/or screenshots). Find the **root cause**, apply the **smallest safe change** that fixes the issue without affecting existing functionality, then **auto-commit** to Git.

**Input:**

- User provides a **description** of the problem (what went wrong, expected vs actual, steps if any).
- User may attach **screenshots** (or other images) — use them to understand UI state, errors, or visual issues.

**Steps:**

1. **Gather context**
   - Read and summarize the user’s text description (symptoms, steps, environment).
   - If screenshots are attached, analyze them (error text, UI layout, console output, etc.) and incorporate into the analysis.

2. **Root-cause analysis**
   - Identify **where** the problem originates (which script, scene, data file, or flow).
   - Distinguish **root cause** from **symptoms**. Prefer fixing the cause, not only the symptom, unless a minimal symptom fix is explicitly safer.
   - Consider: parsing/encoding, missing/null checks, wrong types, logic errors, missing signal connections, scene/node paths, autoload order, or data/JSON issues.

3. **Minimal fix**
   - Change **only what is necessary** to fix the root cause.
   - Do **not** refactor unrelated code, rename variables for style, or add features.
   - Preserve **existing behavior** elsewhere; avoid breaking other scenes or flows.
   - Prefer targeted edits (e.g. one file, few lines) over broad changes.

4. **Verify**
   - After editing, run linter on changed files if applicable (`read_lints`).
   - Resolve any new linter/compile errors introduced by the fix.

5. **Auto-commit**
   - Run: `git add -A`, then `git commit -m "[Cursor] Fix: <short English summary of the fix>"`
   - On Windows PowerShell use one line: `git add -A; git commit -m "[Cursor] Fix: <summary>"`
   - If there is nothing to commit (working tree clean), say so in the reply; otherwise confirm the commit and, if useful, include the commit hash.

6. **Reply**
   - Briefly state: **what the root cause was**, **what you changed** (file(s) and key change), and that the fix was committed (or that there was nothing to commit).

**Rules:**

- **Root cause first**: Prefer fixing the underlying cause; avoid band-aids (e.g. hiding errors or working around a bug in another system) unless that is the only safe minimal option.
- **Minimal diff**: No unnecessary edits. Do not “improve” or “clean up” unrelated code in the same pass.
- **No regressions**: The fix must not break existing behavior. If unsure, restrict the change to the failing path or add a null/type check instead of changing global behavior.
- **One fix, one commit**: Single logical fix per run; commit message should describe that fix in English.

Run this command when the user describes a problem (with or without screenshots) and wants a **targeted, root-cause fix** with automatic Git commit.
