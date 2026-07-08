---
name: codebase-design
description: Design a deep module: a lot of behaviour behind a small, simple interface.
---

# codebase-design

Design a deep module: hide a lot of behaviour behind a small, simple interface.

1. **Name one job.** Write one sentence for what this module does. One job only.
2. **Check GLOSSARY.md.** Reuse the shared names from GLOSSARY.md so the interface fits the domain.
3. **Draft the small interface.** Write only the signatures that hide the work, like `createGame`, `nextState`, `collides`. Nothing extra.
4. **Prove it is testable.** Confirm each signature runs under `node --test` with no canvas and no DOM. If not, shrink it.
5. **Implement behind it.** Now write the code inside those functions. Keep the interface fixed.

A deep module hides a lot behind a little.
