---
name: scout:settings
description: Configure Scout agent settings — quality profile, execution mode, and cmux preference. Opens an interactive menu.
---

# /scout:settings — Scout Settings Menu

Opens an interactive settings menu for configuring Scout's behavior.

## On Invocation

1. Read `~/.claude/skills/scout/settings.json`. If it doesn't exist, use defaults: `{"quality":"balanced","mode":"interactive","cmux":"auto"}`
2. Walk through each setting using `AskUserQuestion`, one at a time
3. Save updated settings to `~/.claude/skills/scout/settings.json`

## Step 1: Quality Profile

Use `AskUserQuestion`:

Title: "SCOUT SETTINGS (1/3) — Quality Profile"
Description: "Controls which model each agent uses."

Show a table in the question text:

```
| Agent       | high   | balanced | budget |
|-------------|--------|----------|--------|
| Scout       | opus   | opus     | sonnet |
| Griller     | opus   | opus     | sonnet |
| Reconn      | opus   | sonnet   | sonnet |
| Architect   | opus   | opus     | sonnet |
| Slicer      | opus   | sonnet   | sonnet |
| Builder-N   | opus   | sonnet   | sonnet |
```

Options (mark current with `(current)`):
- `high` — opus everywhere (best quality, highest cost)
- `balanced` — opus for thinking, sonnet for execution (recommended)
- `budget` — sonnet everywhere (fastest, lowest cost)

## Step 2: Execution Mode

Use `AskUserQuestion`:

Title: "SCOUT SETTINGS (2/3) — Execution Mode"
Description: "Controls how much human interaction is required."

Show a table in the question text:

```
| Behavior           | interactive    | yolo                    | auto           |
|--------------------|---------------|-------------------------|----------------|
| Grill interview    | Yes           | Yes                     | Skipped        |
| Grill approval     | Yes           | Yes (last checkpoint)   | Skipped        |
| PRD approval       | Yes           | Auto                    | Auto           |
| Issue breakdown    | Yes           | Auto                    | Auto           |
| HITL issues        | Pause         | Pause                   | Treated as AFK |
```

Options (mark current with `(current)`):
- `interactive` — approval gates at every phase transition
- `yolo` — grill runs normally, then everything auto-executes
- `auto` — fully autonomous, skips grill entirely

## Step 3: cmux

Use `AskUserQuestion`:

Title: "SCOUT SETTINGS (3/3) — cmux Tab Spawning"
Description: "Controls whether agents get their own terminal tabs."

Options (mark current with `(current)`):
- `auto` — detect cmux on startup, use tabs if available
- `on` — always spawn cmux tabs (fails if cmux not running)
- `off` — always run in-process, no tabs

## Step 4: Save and Confirm

Write the updated settings to `~/.claude/skills/scout/settings.json`:

```bash
echo '{"quality":"<value>","mode":"<value>","cmux":"<value>"}' > ~/.claude/skills/scout/settings.json
```

Display the summary showing what changed:

```
Settings saved to ~/.claude/skills/scout/settings.json

  Quality: balanced → high
  Mode: interactive → yolo
  cmux: auto (unchanged)
```

Only show the arrow for values that changed. Show "(unchanged)" for values that stayed the same.
