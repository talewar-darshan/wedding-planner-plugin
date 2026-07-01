# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool you have
connected in that category. This plugin is tool-agnostic — it describes
workflows in terms of categories rather than one specific product, so it
works with whichever tracker you already use.

## Connectors for this plugin

| Category         | Placeholder           | Common options                  |
| ----------------- | --------------------- | -------------------------------- |
| Project tracker   | `~~project tracker`   | Jira, Linear, Asana, Trello, Monday |

To use this plugin, connect any project-tracker MCP server/connector before
running the setup skill. No specific tracker is required — whatever you
connect is what the plugin will read from and write to.
