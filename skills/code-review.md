---
name: code-review
description: Review a diff twice, once for standards and once for spec, in a fresh context.
---

# code-review

Read the diff fresh and report what is wrong.

1. **Clear.** Drop all prior context first, so you read the diff with no memory of writing it.
2. **Standards.** Check the diff against the rules in AGENTS.md and the terms in GLOSSARY.md. The core in game.js must stay free of canvas and DOM.
3. **Spec.** Check the diff does what the issue acceptance line or the PRD asked, no more and no less.
4. **Report.** List every problem you found in one message.

Report the problems, do not rewrite the code.
