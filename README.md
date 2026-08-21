# skills

**GitHub:** [github.com/Zolkyed/skills](https://github.com/Zolkyed/skills)

Zolkyed's personal agent skills — install into any coding agent that supports [skills.sh](https://skills.sh) (Claude Code, Codex, Copilot, OpenCode, 70+ more).

## Install

```bash
npx skills add Zolkyed/skills              # interactive: pick skill(s) + agent(s)
npx skills add Zolkyed/skills --list       # list without installing
/plugin install zolkyed-skills             # Claude Code plugin, whole set
```

## Structure

```text
skills/
└── design/
    └── frontend-design/
```

`skills/<category>/<skill-name>/SKILL.md` — YAML frontmatter (`name`, `description`) + process. The `description` is what an agent uses to decide *when* to reach for it, not just what it does.

## Adding a skill

1. Write the `SKILL.md`.
2. Add its path to `.claude-plugin/plugin.json`'s `skills` array.

## Source

Most skills started as a copy of [mattpocock/skills](https://github.com/mattpocock/skills) (MIT) — see `THIRD_PARTY_NOTICES.md`.
