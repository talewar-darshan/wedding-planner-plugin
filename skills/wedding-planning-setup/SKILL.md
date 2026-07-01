---
name: wedding-planning-setup
description: >
  This skill should be used when the user asks to "set up a wedding planning
  board", "create a wedding project tracker", "help me plan my wedding in
  Jira/Linear/Asana", "turn my wedding into a project", "bootstrap a wedding
  board", or otherwise wants to stand up a structured wedding planning system
  from scratch in their project tracker.
metadata:
  version: "0.1.0"
---

# Wedding Planning Setup

Bootstrap a full wedding planning board in the user's connected ~~project
tracker (Jira, Linear, Asana, or similar), using the bundled blueprint as a
starting structure.

## Step 1: Confirm a tracker is connected

Check which ~~project tracker tools are currently available. If none are
connected, tell the user they need to connect a project tracker (Jira,
Linear, Asana, etc.) before this skill can create anything, and stop here.

## Step 2: Load the blueprint

Read `references/blueprint.md` in this skill's directory. It contains 11
default categories (Epics) and their default tasks, written for a
multi-event Indian wedding.

## Step 3: Tailor the blueprint to this wedding

Do not assume every category applies. Ask the user, in one message:

- Which of the 11 categories apply to their wedding (list them briefly) —
  let them drop ones that don't fit (e.g. Sangeet, Rituals & Ceremony
  Logistics are specific to certain traditions) and name any missing ones.
- Whether they want the default task list under each category as-is, or
  want to add/remove specific tasks.
- Whether to create a brand-new project in ~~project tracker, or add this
  structure into an existing project — ask for the project name/key if
  ambiguous.

Do not proceed to creation until this is confirmed.

## Step 4: Create the structure

For each confirmed category:

1. Create it as an Epic (or the tracker's equivalent top-level grouping
   issue type) using the confirmed category name as the summary/title.
2. Create each task under that category as a Task/Story, linked to the
   parent Epic using whatever linking mechanism the tracker's tools expose
   (epic link, parent field, etc).

Do not invent extra tasks beyond what the blueprint or the user specified.
If a tracker tool call fails (e.g. missing required field, invalid project),
report the exact error rather than silently skipping the item.

## Step 5: Report back

Summarize what was created: number of Epics, number of Tasks, and a link to
the board/project if the tracker's tools return one. Mention that the
companion `wedding-planning-manager` skill can be used going forward to
update this board in plain English instead of opening the tracker UI.
