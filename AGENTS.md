# Development Instructions

## What this repo is

A collection of `SKILL.md` files, installable into any coding agent via `npx skills add Zolkyed/skills` or as a Claude Code plugin. Not a codebase — a content repo.

## Adding a skill

- One folder per skill: `skills/<category>/<skill-name>/SKILL.md`.
- Frontmatter needs `name` + a `description` specific enough that an agent can decide *when* to reach for it, not just what it does.
- Register the new skill's path in `.claude-plugin/plugin.json`'s `skills` array.
- Keep skills small, single-purpose, and composable — a skill that tries to do five things is five skills.

## Git

- Work only in the current worktree.
- Never work directly on `main`.
- Use Conventional Commits.

## Safety

- Never commit secrets or credentials referenced inside a skill's example commands.
- Ask before merging PRs.
