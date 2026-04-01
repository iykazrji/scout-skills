# Scout Skills — Development Guide

## Repo Location

`~/.claude/skills/scout/` — this is both the git repo and the skill directory. No symlinks needed.

## Structure

```
~/.claude/skills/scout/
├── SKILL.md                 ← main /scout orchestrator
├── settings.md              ← /scout:settings sub-skill
├── settings.json            ← user config (gitignored)
├── overview.html            ← visual overview page
├── CLAUDE.md                ← you are here
├── README.md                ← public docs
├── .gitignore
├── docs/
│   ├── DESIGN.md
│   └── scout-overview.html
├── reconn/SKILL.md          ← /scout:reconn
├── execute-issues/SKILL.md  ← /scout:execute-issues
├── grill-me/SKILL.md        ← /scout:grill-me
├── write-a-prd/SKILL.md     ← /scout:write-a-prd
├── prd-to-issues/SKILL.md   ← /scout:prd-to-issues
├── ui-designer/             ← /scout:ui-designer
├── agent-device/            ← /scout:agent-device
├── senior-architect/        ← /scout:senior-architect
├── flutter-expert/          ← /scout:flutter-expert
├── react-native-best-practices/
├── rn-animations-performance/
├── using-react-native-skia/
├── react-best-practices/
├── expressjs-best-practices/
└── fastify-best-practices/
```

## Invocation

- `/scout` — runs the main orchestrator (SKILL.md at repo root)
- `/scout:reconn` — runs the reconn sub-skill
- `/scout:settings` — opens settings menu
- `/scout:grill-me`, `/scout:write-a-prd`, etc.

## Adding a New Skill

1. Create the directory: `~/.claude/skills/scout/<new-skill>/SKILL.md`
2. Commit and push:
   ```bash
   cd ~/.claude/skills/scout
   git add <new-skill> && git commit -m "feat: add <new-skill>" && git push origin main
   ```
3. It's immediately available as `/scout:<new-skill>`

## Editing Skills

Edit files directly — they're real files, not symlinks. Commit from the repo:
```bash
cd ~/.claude/skills/scout
git add -A && git commit -m "description" && git push origin main
```

## Conventions

- **`settings.json` is gitignored** — user-specific runtime config (quality profile, execution mode).
- **Check `git status` periodically** — catch untracked runtime files before they get committed.
- **Knowledge skills are bundled but independent** — sub-skills like `/scout:react-best-practices` work standalone for code review, refactoring, or general guidance.
