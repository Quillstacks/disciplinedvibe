---
name: askuserquestion
description: Interview the user relentlessly about a plan until you reach a shared understanding.
---

# askuserquestion

Interview me relentlessly about every aspect of this plan until we reach a shared
understanding. The goal is not a document, it is alignment: a design concept we
both hold.

Rules:

1. First, explore the codebase enough to ask informed questions. If a question
   can be answered by reading the code, read it instead of asking.
2. Ask questions one at a time. Wait for my answer before the next one.
3. For every question, propose your own recommended answer and say why.
4. Walk down each branch of the decision tree, resolving dependencies one by one.
   Surface the awkward questions a non-expert would forget (edge cases,
   retroactive data, failure behaviour, out-of-scope boundaries).
5. Do not write a plan or any code yet. Keep going until you have no open
   questions, then say so.

Stop when alignment is reached, not before.
