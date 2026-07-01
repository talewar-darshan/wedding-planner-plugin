---
name: wedding-planning-manager
description: >
  This skill should be used when the user gives natural-language updates
  about wedding planning progress and wants their ~~project tracker updated
  automatically — e.g. "caterer's confirmed, mark it done", "log the advance
  we paid the decorator", "add a task for booking the mandap", "what's still
  open in vendors", "assign the guest list task to my cousin". Use it for
  ongoing, day-to-day management of a wedding board (typically one created by
  the wedding-planning-setup skill) so the user never has to open the
  tracker's UI directly.
metadata:
  version: "0.1.0"
---

# Wedding Planning Manager

Translate a plain-English update about wedding planning into the correct
action(s) in the user's connected ~~project tracker.

## Step 1: Classify the request

Read the user's message and classify it as one of:

- **Status change** — something is done, started, or blocked ("caterer's
  confirmed", "we're still waiting on the venue").
- **Log / comment** — information to record against an existing item without
  necessarily changing its status ("log the advance we paid the decorator",
  "note that the pandit wants the list by Friday").
- **New task** — something to add that doesn't exist yet ("add a task for
  booking the mandap").
- **Assignment** — reassign or delegate an item ("give the guest list task
  to my cousin").
- **Query** — a question about current state ("what's still open in
  vendors", "what's overdue this week").

A single message may contain more than one of these — handle each part.

## Step 2: Find the matching item(s)

Search the connected ~~project tracker for issues whose title/summary best
matches the subject of the request (fuzzy match on keywords, not exact
string match — "caterer" should match a task titled "Shortlist and confirm a
caterer for every event..."). Prefer matches within the most relevant
category/Epic if the request implies one (e.g. "decorator" implies Vendors
or Gifts & Hampers depending on context).

If more than one item is a plausible match, or nothing matches well enough
to be confident, ask the user to confirm which item they mean rather than
guessing. Do not silently pick the first result.

## Step 3: Act

Depending on the classification:

- **Status change** — transition the issue to the appropriate status using
  the tracker's transition/update tools.
- **Log / comment** — add a comment with the information provided, verbatim
  or lightly cleaned up, without altering status unless the user also asked
  for that.
- **New task** — create it under the correct existing Epic/category. If no
  matching category exists, ask which one it belongs under (or whether to
  create a new one) before adding it.
- **Assignment** — update the assignee field. If the assignee's account
  isn't resolvable from the name given, ask for clarification (email,
  username) rather than guessing.
- **Query** — search and summarize matching issues and their current status
  in a short list. Do not fabricate items that don't exist in the tracker.

## Step 4: Confirm back briefly

After acting, tell the user in one or two lines exactly what changed (e.g.
"Marked 'Confirm caterer for all events' as Done and logged your comment
about the final headcount."). Never report an action as completed unless
the corresponding tool call actually succeeded — surface tool errors instead
of glossing over them.
