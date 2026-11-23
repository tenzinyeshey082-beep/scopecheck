---
name: scopecheck
description: Keeps a coding task in scope. Inspect existing changes, nearby code and tests first, reuse what already works, make the smallest complete change, then run checks and review the diff. Use when asked to fix, add or change code without over-engineering.
argument-hint: "<coding task>"
disable-model-invocation: true
---

# Scopecheck

Task: $ARGUMENTS

If the task above is empty, ask the user what they want changed and stop.

Work through these steps in order. Keep the change as small as it can be
while still solving the whole task.

## 1. Look before you edit

- Run `git status` and `git diff` to see uncommitted work. Treat any change
  you did not make as the user's: never revert, reformat or overwrite it.
- Find the code the task touches and read it, plus its callers and
  neighbours in the same folder.
- Find the tests that cover that code and note how they are run.
- Search for an existing helper, component, util or pattern that already
  does what the task needs (Grep for likely names, read similar features).

## 2. Decide the smallest complete change

- Prefer reusing or extending what exists over writing something new.
- Add a new file, helper or abstraction only if nothing existing fits and
  you can name the concrete problem it solves.
- Add a new dependency only if the standard library and current
  dependencies cannot reasonably do the job. Say why in your reply.
- Do not refactor, rename or restyle code the task does not need.
- "Smallest" still means complete: handle the edge cases the task implies
  (empty, missing, null, zero, error, very long input, first/last item).

## 3. Make the change

- Follow the surrounding code's style, naming and structure.
- Touch only the lines the task needs. Leave unrelated user edits intact.
- Update or add tests when behaviour changes and the project has tests.

## 4. Check your work

- Run the relevant tests, type checks, linters or build the project uses.
  If something cannot be run, say so instead of claiming it passes.
- Read the full `git diff`. Remove anything that is not needed for the
  task: debug output, stray files, unused imports, speculative options.
- Confirm no unrelated user changes were altered.

## 5. Report

Reply briefly with: what changed and why, what existing code you reused,
anything new you added and the reason, which checks ran and their results,
and anything left unverified.
