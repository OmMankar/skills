# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A personal collection of Claude Code Agent Skills (see README.md: "Skills for my ai agent"). There is no build, test, or lint step — the content is Markdown, and the "runtime" is Claude Code itself loading a skill.

## Layout

One directory per skill, each containing a `SKILL.md`. The directory name is the skill's invocation name (`conventional-commit/SKILL.md` → `/conventional-commit`).

## SKILL.md contract

Every `SKILL.md` starts with YAML frontmatter:

```yaml
---
name: <kebab-case, must match the directory name>
description: "<when to use this skill — the only text loaded into context every turn, so it must be specific about triggers>"
---
```

The body is the instructions loaded only when the skill runs. Keep it imperative and short: the description does the routing, the body does the work.

## Using a skill from this repo

Skills here are not auto-loaded by Claude Code. To make one available, symlink or copy its directory into `~/.claude/skills/` (user-level) or a project's `.claude/skills/`.

## Committing

`conventional-commit/SKILL.md` describes this repo's own commit convention: `<type>(<scope>): <description>.` — past tense, trailing period, scope derived from the directory touched.
