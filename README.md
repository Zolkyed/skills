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
├── coding/
│   ├── code-review/
│   ├── codebase-design/
│   ├── create-issue/
│   ├── diagnosing-bugs/
│   ├── finish-issue/
│   ├── improve-codebase-architecture/
│   ├── prepare-pr/
│   ├── retry-issue/
│   ├── skill-creator/
│   ├── start-issue/
│   └── tdd/
├── cybersecurity/
│   ├── assess-web-application-vulnerabilities/
│   ├── audit-dependency-vulnerabilities/
│   ├── detect-exposed-secrets/
│   ├── review-source-vulnerabilities/
│   └── secure-software-engineering/
├── productivity/
│   ├── caveman/
│   ├── find-skills/
│   └── grill-me/
├── web-scraping/
│   ├── crawl-large-sites/
│   ├── extract-structured-data/
│   ├── map-website-apis/
│   ├── scrape-browser-sites/
│   └── scrape-static-sites/
└── webdev/
    ├── accessibility/
    ├── frontend-design/
    ├── frontend-engineering/
    ├── playwright/
    └── prototype/
```

`skills/<category>/<skill-name>/SKILL.md` — YAML frontmatter (`name`, `description`) + process. The `description` is what an agent uses to decide *when* to reach for it, not just what it does.

## Adding a skill

1. Write the `SKILL.md`.
2. Add its path to `.claude-plugin/plugin.json`'s `skills` array.

## Source

Imported skills retain their upstream licenses and attribution in `THIRD_PARTY_NOTICES.md`.
