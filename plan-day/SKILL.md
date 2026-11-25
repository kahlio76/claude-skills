---
name: plan-day
description: Build today's plan from TickTick and the calendar and write it into the Obsidian daily note. Use when the user types /plan-day or asks to plan their day.
---

# /plan-day

Vault: `<your Obsidian vault>`; note: `Daily/YYYY-MM-DD.md` (create it if missing).
Timezone: <your timezone>.

1. Fetch in parallel: TickTick tasks due today and overdue (`list_undone_tasks_by_date` or
   `filter_tasks`), and today's calendar events (Google Calendar `list_events`).
2. Build a short plan: fixed events first by time, then tasks ordered by priority then
   due time; overdue flagged. Fit tasks into gaps; don't over-schedule (max ~5 focus tasks).
3. Write it at the TOP of the daily note as a `## Today` section, replacing an existing
   `## Today` section if present. Leave everything else in the note untouched. Use
   `- [ ] title (project)` lines so they're visibly TickTick-sourced; append ` #ticktick`
   so `/clear-tasks` won't re-send them.
4. Append a line to `Claude/Run Log.md`.
5. Reply with the plan in at most 10 lines, plus the single most important task.
