---
name: decide
description: Put open decisions to the user as numbered decisions with lettered options and a recommendation, answerable as "1B 2A". Use when work hits choices that belong to the user (behaviour, scope, naming, dependencies, trade-offs), or the user says "decide".
---

A **decision** is a choice that changes what gets built and that the user would want to own. Facts are your job: look them up before asking. A choice with an obvious conventional default is not a decision: take the default and note it in one line under the block.

Where `grilling` interviews the user about a whole plan in rounds, `decide` is the quick stop mid-work: every open decision at once, one reply, back to work.

## Steps

1. Collect every open decision blocking the work. Ground each in the code: read the relevant files so the options name real modules, patterns and costs. Done when each one is something only the user can settle.
2. Present them all in one block, in the format below, ordered so that a decision whose options depend on another comes after it.
3. Stop and wait for the reply.
4. Parse it: `1B 2D` picks options; `recs` takes every recommendation; `recs except 3A` takes all but the named ones; `later` on a number parks that decision; free text on a number overrides it. Restate the final picks in one line, then continue.

## Format

```
**1. <decision title>**
<one or two sentences: what's at stake here>
- **A** <option>: <what it costs, what it gains>
- **B** <option>: <what it costs, what it gains>
➡️ **Rec: B**, <the reason, tied to this codebase>

**2. <decision title>**
...

Reply like `1B 2A`, `recs`, or `later` for any you want to park. Add a note after any number.
```

Give two to four options per decision, each a real, buildable path. Each line names the concrete cost: files touched, dependency added, behaviour change, follow-up work. The recommendation commits to one letter, with the reason a senior maintainer of this repo would accept.

Use the project's domain language from `GLOSSARY.md`, and respect ADRs in the area: a decision an ADR already settled is not open.
