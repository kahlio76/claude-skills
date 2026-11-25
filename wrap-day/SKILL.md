---
name: wrap-day
description: End-of-day close out. Summarise completed TickTick tasks, roll overdue ones to tomorrow, and write a wrap section in the Obsidian daily note. Use when the user types /wrap-day or says they're done for the day.
---

# /wrap-day

Vault: `<your Obsidian vault>`; note: `Daily/YYYY-MM-DD.md`. Timezone: <your timezone>.

1. Fetch tasks completed today (`list_completed_tasks_by_date`) and still-open tasks due
   today or earlier (`list_undone_tasks_by_date`).
2. Move the open ones to tomorrow with `batch_update_tasks` (keep times, keep priority).
   Do this directly; it is reversible and the point of the command. Track roll counts in `Claude/Command State.md` in the vault (read it first, update it after). If a task has been
   rolled 3+ times, don't move it; list it as "stuck" in the reply instead.
3. Append `## Wrap` to the daily note: done count, a bullet list of what got done, and
   what rolled. Do not modify other sections.
4. Append a line to `Claude/Run Log.md`.
5. Reply in at most 6 lines: done, rolled, stuck, and one suggestion for tomorrow.
