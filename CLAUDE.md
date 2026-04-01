# Scout Skills — Development Guide

## Repo Location

Canonical location: `/Users/iyk/Developer/scout-skills/`

All skills are symlinked into `~/.claude/skills/` — edits through the symlinks write directly to this repo.

## Adding a New Skill

1. Create the skill directory in the repo:
   ```
   skills/<new-skill-name>/SKILL.md
   ```
2. Symlink it into Claude Code:
   ```bash
   ln -sf "$(pwd)/skills/<new-skill-name>" ~/.claude/skills/<new-skill-name>
   ```
3. Commit and push from the repo.

## Editing Existing Skills

Edit via the symlinks at `~/.claude/skills/<name>/` or directly in the repo at `skills/<name>/`. Both point to the same files.

After editing, commit from the repo:
```bash
cd /Users/iyk/Developer/scout-skills
git add -A && git commit -m "description" && git push origin main
```

## Important Conventions

- **Never move the repo** — 16 symlinks in `~/.claude/skills/` will break silently.
- **`settings.json` is gitignored** — these are user-specific runtime config files (quality profile, execution mode). They live in the skill directories but are not committed.
- **Don't copy files into `~/.claude/skills/<name>/`** — always work through the symlinks. Copying creates a real directory that shadows the symlink and causes divergence.
- **Check `git status` periodically** — catch untracked runtime files before they get committed accidentally.
- **Knowledge skills are bundled but independent** — skills like `/react-best-practices` or `/flutter-expert` work standalone outside Scout. If one needs independent versioning later, extract it to its own repo and replace with a symlink.

## Repo Structure

```
scout-skills/
├── CLAUDE.md              ← you are here
├── README.md              ← public-facing docs, install guide
├── .gitignore             ← excludes settings.json
├── docs/
│   ├── DESIGN.md          ← architecture and design decisions
│   └── scout-overview.html ← visual HTML overview page
└── skills/
    ├── scout/             ← orchestrator (core)
    ├── reconn/            ← research agent (core)
    ├── execute-issues/    ← builder orchestrator (core)
    ├── grill-me/          ← interrogation protocol (core)
    ├── write-a-prd/       ← PRD writer (core)
    ├── prd-to-issues/     ← issue breakdown (core)
    ├── ui-designer/       ← design orchestrator (core)
    ├── agent-device/      ← on-device interaction (core)
    ├── senior-architect/  ← system design (knowledge)
    ├── flutter-expert/    ← Flutter best practices (knowledge)
    ├── react-native-best-practices/  (knowledge)
    ├── rn-animations-performance/    (knowledge)
    ├── using-react-native-skia/      (knowledge)
    ├── react-best-practices/         (knowledge)
    ├── expressjs-best-practices/     (knowledge)
    └── fastify-best-practices/       (knowledge)
```

## Symlink Health Check

Verify all symlinks are intact:
```bash
for skill in scout reconn execute-issues grill-me write-a-prd prd-to-issues ui-designer agent-device senior-architect flutter-expert react-native-best-practices rn-animations-performance using-react-native-skia react-best-practices expressjs-best-practices fastify-best-practices; do
  target="$HOME/.claude/skills/$skill"
  if [ -L "$target" ]; then
    echo "OK: $skill"
  elif [ -d "$target" ]; then
    echo "WARN: $skill is a real directory, not a symlink"
  else
    echo "MISSING: $skill"
  fi
done
```
