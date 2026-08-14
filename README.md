# skills

**GitHub:** [github.com/Zolkyed/skills](https://github.com/Zolkyed/skills)

Zolkyed's agent skills — install into any coding agent that supports the [skills](https://skills.sh) ecosystem (Claude Code, Codex, Cursor, GitHub Copilot, and 70+ more).

## Source

Most skills under `skills/engineering/`, `skills/productivity/`, and `skills/misc/` (everything except `skills/engineering/example-skill/`, which is original) started as a copy of [mattpocock/skills](https://github.com/mattpocock/skills), MIT licensed. Copied as a base to customize, not used verbatim forever — see `THIRD_PARTY_NOTICES.md` for the full license text and what was and wasn't copied.

## Install

Two ways in — pick one, don't do both:

**[skills.sh](https://skills.sh) — copies editable skill files into your project:**

```bash
npx skills add Zolkyed/skills
```

Interactive picker: choose which skill(s) and which agent(s) to install to.

```bash
npx skills add Zolkyed/skills --skill example-skill -a claude-code   # non-interactive
npx skills add Zolkyed/skills --list                                # list without installing
```

**Claude Code plugin — installs the whole set as a managed, read-only bundle:**

```bash
/plugin install zolkyed-skills
```

(Requires this repo to be added as a plugin marketplace first — see `.claude-plugin/marketplace.json`.)

## What's here

```text
skills/
├── engineering/    # code-review, tdd, diagnosing-bugs, to-spec, wayfinder, ...
├── productivity/    # grill-me, handoff, teach, writing-for-agents, ...
└── misc/           # git-guardrails-claude-code, setup-pre-commit, ...
```

Each category has its own `README.md` listing what's inside and why.

## Structure

```text
skills/
└── <category>/
    └── <skill-name>/
        └── SKILL.md
```

Each `SKILL.md` needs YAML frontmatter with `name` and `description`. The `description` is what an agent uses to decide *when* to reach for the skill — be specific about the trigger, not just what it does.

## Adding or customizing a skill

1. `skills/<category>/<skill-name>/SKILL.md` — frontmatter + process.
2. Add its path to `.claude-plugin/plugin.json`'s `skills` array.
3. Optionally add it to `skills.sh.json`'s `groupings` for the interactive picker's category display.
4. If you substantially rewrite a skill that started as a copy from upstream, note it in `THIRD_PARTY_NOTICES.md`.
