# 🎯 Skills

Skills are small, reusable instructions you hand the agent one at a time. Each file
in this folder is **one job**: a short recipe the agent follows so it stays
disciplined instead of guessing. You invoke a skill by name and the agent does that
one thing, well.

Think of them as the steps of a craft: first you agree on *what* to build, then you
name things, plan, design, build with tests, and review. The skills below follow
that order.

## 🔌 How to make them usable in opencode

opencode reads slash-commands from one of these folders, and the **filename becomes
the command** (`code-review.md` → `/code-review`):

| Scope | Folder |
|---|---|
| Just this project | `.opencode/commands/` (in the folder where you run `opencode`) |
| Everywhere | `~/.config/opencode/commands/` |

Copy the skills you want into one of those folders:

```bash
# per project (run from your vibe folder)
mkdir -p .opencode/commands && cp /path/to/disciplinedvibe/skills/*.md .opencode/commands/

# or globally, for every project
mkdir -p ~/.config/opencode/commands && cp /path/to/disciplinedvibe/skills/*.md ~/.config/opencode/commands/
```

Then in opencode type `/` and you'll see them. Invoke one, e.g.:

```
/askuserquestion
/test-driven-development
```

## 🧭 The sequence

Work top to bottom. You will not use every skill on every task — small changes skip
straight to build-and-review — but this is the full arc.

| # | Skill | What it does | When |
|---|---|---|---|
| 1 | `/askuserquestion` | Interviews you until you both agree on the plan | Start of anything non-trivial |
| 2 | `/ubiquitous-language` | Keeps one set of words across chat, code, tests, `GLOSSARY.md` | Whenever a new term appears |
| 3 | `/domain-modeling` | Collects the game's nouns and verbs into `GLOSSARY.md` | First time you name the domain |
| 4 | `/to-product-requirements-document` | Writes the agreed plan into `issues/PRD.md` | Once alignment is reached |
| 5 | `/to-issues` | Slices the PRD into small, grabbable pieces of work | Before you start building |
| 6 | `/codebase-design` | Designs one deep module: small interface, lots hidden behind it | Before building a new piece |
| 7 | `/prototype` | A throwaway spike to answer one design question, then deleted | When a design choice is unclear |
| 8 | `/test-driven-development` | Red → green → refactor, one small change at a time | The actual building |
| 9 | `/code-review` | Re-reads the diff fresh, against standards and against the spec | After each change |
| 10 | `/diagnosing-bugs` | Traces a bug to its root cause and fixes that, not the symptom | When something breaks |
| 11 | `/improve-codebase-architecture` | Finds a tangled cluster and proposes extracting it | When the code gets messy |
| 12 | `/write-a-skill` | Writes a new skill in this same style | When you want a new recipe |

A typical run: **1 → 4 → 5**, then loop **6/8 → 9** for each slice, reaching for
**7, 10, 11** only when you need them.

## 🧩 How this pairs with opencode's Plan and Build modes

opencode ships with two built-in modes you switch between with the **Tab** key:

- **Plan** — read-only. The agent can look and think but **cannot edit files or run
  commands** without asking. This is where you *decide*.
- **Build** — the default. All tools on. This is where you *make changes*.

Line the skills up with the mode:

| Mode (press **Tab**) | Skills to run |
|---|---|
| 🧠 **Plan** (read-only, decide) | `/askuserquestion`, `/domain-modeling`, `/to-product-requirements-document`, `/to-issues`, `/codebase-design`, `/improve-codebase-architecture` |
| 🔨 **Build** (edits on, make it) | `/ubiquitous-language`, `/prototype`, `/test-driven-development`, `/diagnosing-bugs`, `/code-review` |

The rhythm: **stay in Plan mode** while you interview, model, and slice the work —
nothing gets written, so you can think freely and cheaply. When the plan is solid,
press **Tab** to switch to **Build mode** and run the build-and-review loop. If you
find yourself editing code before you have a plan, that is the signal to Tab back to
Plan and run `/askuserquestion` first.

> One skill at a time. Alignment before code. One word, one meaning, everywhere.
