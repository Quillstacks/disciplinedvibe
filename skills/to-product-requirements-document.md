---
name: to-product-requirements-document
description: Turn an aligned conversation into a product requirements document.
---

# to-product-requirements-document

Summarise the design concept we reached into a Product Requirements Document.
Write it to `issues/PRD.md`.

Structure:

- **Problem** — the problem the user faces, in one short paragraph.
- **Solution** — the approach, in one short paragraph.
- **User stories** — a short list of "as a <role>, I want <goal>, so that <reason>".
- **Implementation decisions** — the concrete choices we agreed on.
- **Testing decisions** — how each story will be verified.
- **Out of scope** — what we explicitly decided NOT to do, and why. This is the
  definition of done.

Do not write implementation code. The PRD records the destination, not the route.
