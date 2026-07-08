---
name: improve-codebase-architecture
description: Find a tangled cluster and propose deepening it into one testable module.
---

# improve-codebase-architecture

Find one tangled cluster and propose deepening it into a single testable module.

1. **Read.** Open GLOSSARY.md for the shared vocabulary before you look at code.
2. **Scan.** Find mixed concerns, like physics tangled into the render loop in index.html.
3. **Cut.** Pick one clean boundary to pull into the pure core (createGame, nextState, collides).
4. **Propose.** Name what moves behind game.js and its interface. Write the proposal only, do not edit code.

A boundary you can wrap a `node --test` around is the goal.
