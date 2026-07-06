# AGENTS.md — Retrospective System

## Project Overview

A Claude Code command (`/复盘`) and skill suite for extracting maximum value from completed conversations. After finishing an important task, the agent scans the entire conversation, identifies notable moments across 7 domains, performs domain-specific deep analysis using retro-<domain> skills, cross-references existing knowledge assets, and persists findings as structured memory files.

## Key Commands & Skills

- `/复盘` — Main entry point. Full 4-stage retrospective workflow with degradation paths.
- `retro-experiment` — ML experiment retro: 7 evaluation dimensions, 9 anti-patterns
- `retro-data` — Data processing retro: 5 dimensions, 10 anti-patterns
- `retro-coding` — Code quality retro: 6 dimensions, 9 anti-patterns
- `retro-research` — Research/search retro: 5 dimensions, 8 anti-patterns
- `retro-debugging` — Debugging retro: 5 dimensions, 8 anti-patterns
- `retro-design` — Architecture/design retro: 5 dimensions, 10 anti-patterns

## Architecture

All skills follow a unified structure: scope + evaluation dimensions + anti-patterns table + solidified-patterns table + critical questions (critical + positive + anti-evidence guidance). The system maintains balance between problem identification and positive pattern recognition.

## Conventions

- Memory files follow `feedback_`/`reference_`/`action_` naming convention
- Skill files are stored at `~/.claude/skills/retro-<domain>/SKILL.md`
- Command file at `~/.claude/commands/复盘.md`
- Design documentation in `docs/design.md`

## Related Files

- `.claude/commands/复盘.md` — Command implementation
- `.claude/skills/retro-*/SKILL.md` — Domain skill implementations
- `docs/design.md` — Full design document
- `docs/adversarial-review-round*.md` — Review records
