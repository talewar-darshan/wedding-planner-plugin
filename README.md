# Wedding Planner

Turns any project tracker into a wedding planning system: spin up a full
board of epics and tasks in one shot, then run it day-to-day in plain
English instead of clicking through the tracker's UI.

Built after using this exact workflow (in Jira) to plan a real multi-event
Indian wedding — the board structure here is the anonymized version of that
board.

## Components

| Skill | Purpose |
|---|---|
| `wedding-planning-setup` | Creates the full board (11 default categories, 25 default tasks) in your connected project tracker, tailored to which of those categories actually apply to your wedding. |
| `wedding-planning-manager` | Lets you update the board with plain-English messages — "caterer's confirmed, mark it done", "log the advance we paid the decorator", "what's still open in vendors" — instead of opening the tracker. |

## Setup

1. Connect a project tracker (Jira, Linear, Asana, Trello, or similar) as an
   MCP connector/integration before using this plugin. See `CONNECTORS.md`
   for how the generic `~~project tracker` reference works.
2. No other configuration is required — the blueprint is bundled in
   `skills/wedding-planning-setup/references/blueprint.md`.

## Usage

**Set up the board:**
> "Set up a wedding planning board for me"
> "Turn my wedding into a project in Linear"

Claude will confirm which categories apply to your wedding, whether to use
the default tasks or adjust them, and which project to create/use — then
create everything.

**Run it day-to-day:**
> "Caterer's confirmed, mark it done"
> "Log the ₹50k advance we paid the decorator"
> "Add a task for booking the mandap under Rituals"
> "What's still open in Vendors?"

## Customization

This plugin references tools generically (e.g. `~~project tracker`) so it
works with whatever tracker you already use. See `CONNECTORS.md` for
details, or run it through the plugin customizer to hard-wire it to a
specific tool.

The default blueprint assumes a multi-event Indian wedding (Sangeet,
Rituals & Ceremony Logistics, etc.) — drop, rename, or extend categories in
`skills/wedding-planning-setup/references/blueprint.md` to match your own
traditions.
