---
name: domain-modeling
description: Build the shared vocabulary for the game and record it in GLOSSARY.md.
---

# domain-modeling

Pin down the words we use for the game so the code and tests all say the same thing.

1. **List.** Collect the nouns and verbs from the chat and the code: obstacle,
   hitbox, duck, ramp, spawn rate, run length.
2. **Define.** Give each term one plain line: what it means and where it lives
   (createGame, nextState, collides).
3. **Record.** Write these lines into GLOSSARY.md, one term per line.
4. **Fix.** Find synonyms (two words, one thing) and clashes (one word, two
   things), then pick one winner and drop the rest.

One word, one meaning, everywhere.
