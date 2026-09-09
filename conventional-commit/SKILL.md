---
name: conventional-commit
description: "Use when the user wants to commit staged git changes, says \"commit this\", \"write a commit message\", or mentions conventional commit format. Proposes one Conventional-Commits-style message (type(scope): description.) and waits for explicit approval before running git commit — never commits or stages files on its own."
---

# Conventional Git Commit

Propose a commit message, get approval, then commit. Never skip the approval step. Never run `git add` — assume staging is already done; if nothing is staged, say so and stop.

## Format
`<type>(<scope>): <description>.`
- type: feat, fix, docs, style, refactor, perf, test, build, ci, or chore/revert as needed
- scope: include it by default — derive it from the main file/dir/module touched (e.g. `auth`, `api`, `ci`). Only omit the scope when the change genuinely doesn't map to one area (it spans the whole repo, or touches many unrelated parts equally) — don't drop it just to save a few characters.
- description: one line, past tense (e.g. "fixed", "added", "updated" — not "fix", "add", "update"), ends with a period — this skill always uses past tense and adds the period, unlike the usual Conventional Commits spec which uses imperative mood and no period

## Steps
1. Run `git diff --staged --stat`. Empty → tell the user nothing's staged, stop.
2. Infer type/scope from the stat output (paths, extensions, counts) — don't pull the full diff unless the stat alone leaves the type or scope genuinely unclear.
3. Show exactly one suggested message, with at most one short clause of reasoning if it's not obvious. Do not commit yet.
4. If the user objects, propose a different message that addresses the feedback, not a reworded guess. Repeat until approved.
5. On explicit approval, commit:
   - No co-author: `git commit -m "<message>"`
   - Co-author (only if the user's request named one, with an email or handle): `git commit -m "<message>" -m "Co-Authored-By: Name <email>"`
   Default is no co-author.

Keep the exchange lean — no restating the diff, no multi-paragraph explanation, just the message.