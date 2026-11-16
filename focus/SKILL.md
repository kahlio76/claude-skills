---
name: focus
description: Start a focus block. Sets a timer that fires a Clawd notification when it ends and builds a Spotify playlist for the session. Use when the user types /focus, optionally with minutes and a vibe (e.g. "/focus 50 lofi"), or says they want to start a focus/study block.
---

# /focus

Arguments: `[minutes] [vibe...]`. Defaults: 25 minutes, vibe "instrumental focus music".
Parse loosely: a bare number is minutes, everything else is the vibe. If the user names a
course or task ("/focus 50 calc homework"), keep it as the label and use the default vibe.

## Steps

1. **Start the timer first**, so the music step can't delay it. Run in the background with
   Bash `run_in_background: true` (do not poll it; you are re-invoked when it exits):

   ```bash
   sleep $((MINUTES * 60)) && /opt/homebrew/bin/terminal-notifier \
     -title "Focus block done" -message "LABEL: MINUTES min complete. Take a break." \
     -sound Hero -contentImage ~/.claude/icons/clawd.png -group claude-focus
   ```

   Set the Bash `timeout` high enough to cover the block (max 600000 ms is for foreground
   only; background commands are not limited by it).

2. **Make the playlist** with `mcp__claude_ai_Spotify__generate_playlist` (load it via
   ToolSearch `select:` first if its schema is not available). Prompt it with the vibe and
   a length close to the block (about 3 minutes per track). If the user gave no vibe, use
   instrumental/lofi/ambient with no lyrics, since lyrics hurt reading and proofs.

3. **Open it** if the result includes a Spotify URI or URL: `open "<uri>"`. Otherwise give
   the link.

4. **Reply in 2 lines max**: the end time (clock time, e.g. "ends 3:45 PM"), and the
   playlist name. No pep talk.

## Rules

- Do not touch macOS Focus/Do Not Disturb or any other app; only the timer and Spotify.
- If the user types `/focus stop`, kill the pending timer with TaskStop and confirm in one line.
- If Spotify fails, still keep the timer running and say the playlist step failed.
