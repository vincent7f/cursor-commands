# Kill All

Run the following commands **in this exact order**, one after the other, until each phase is finished (or has nothing left to do):

1. **/fixbugs** — Fix all open bugs in `docs/bugs/` (one fix → one commit per bug). Complete every open bug before moving on.
2. **/kill-todos** — Implement all unchecked todos in `docs/todos/` (one implementation → one commit per todo). Complete every unchecked todo before moving on.
3. **/kill-ideas** — Implement all implementable ideas in `docs/ideas/` (one implementation → one commit per idea). Complete every implementable idea before moving on.

**Rules:**

- Do **not** skip or reorder the phases. Always do fixbugs → kill-todos → kill-ideas.
- Within each phase, follow that command’s full workflow (see `/fixbugs`, `/kill-todos`, `/kill-ideas`). Each item still gets its own commit.
- At the end, give a short summary: how many bugs fixed, how many todos and ideas implemented, and the relevant commit hashes (or “no open items” for a phase).

Run this command when the user wants to process all recorded bugs, todos, and ideas in one go.
