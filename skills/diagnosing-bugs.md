---
name: diagnosing-bugs
description: Find and fix the root cause of a bug, not the symptom.
---

# diagnosing-bugs

Trace a bug to its root cause in the pure core (createGame, nextState, collides)
and fix that, not the surface symptom.

1. **Reproduce.** Write a failing test that triggers the bug. Run `node --test`
   and watch it fail.
2. **Minimise.** Cut the test to the smallest input that still fails. Name what
   you see using GLOSSARY.md.
3. **Find the cause.** State the likely cause in one sentence. Add a log to
   confirm it before you change anything.
4. **Fix.** Change the cause, remove the log, and run `node --test` until green.

A patch that hides the cause creates two new bugs.
