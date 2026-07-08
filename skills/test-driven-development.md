---
name: test-driven-development
description: Implement a change with the red, green, refactor loop.
---

# test-driven-development

Implement the task using test-driven development.

1. **Red.** Write or locate a single failing test that specifies the next small
   behaviour. Run `node --test` and confirm it fails for the right reason.
2. **Green.** Write the minimum code to make that test pass. Run `node --test`.
3. **Refactor.** With the bar green, tidy the code without changing behaviour.
   Run `node --test` again.

Make one small change at a time and run the tests after each. Do not edit the
test to fit broken code; fix the code. When done, show the diff for review.
