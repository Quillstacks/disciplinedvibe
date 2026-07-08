---
name: ubiquitous-language
description: Keep one shared language across chat, code, tests, and GLOSSARY.md, with no synonyms.
---

# ubiquitous-language

Speak one language everywhere. The words in the chat, the names in the code, the
labels in the tests, and the terms in GLOSSARY.md must all be the same words.

1. **Read.** Open GLOSSARY.md and take the agreed terms as the single source of truth
   (obstacle, hitbox, spawn rate, and the pure core: createGame, nextState, collides).
2. **Match.** When you name a variable, function, test, or issue, use the GLOSSARY.md
   word. If the code and the chat disagree, the code is wrong; rename it.
3. **Catch drift.** Whenever a new noun or verb appears in conversation, stop and ask:
   is this a new term (add it to GLOSSARY.md) or a synonym for an existing one (drop it)?
4. **Fix on sight.** Rename any stray synonym across code and tests in the same change,
   so one thing never has two names.

If you have to translate between a chat word and a code word, the language is broken.
