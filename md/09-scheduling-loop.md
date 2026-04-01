# Scheduling & /loop

> Introduced: v2.1.66 (March 2026) | Latest: v2.1.76

## What It Is

Claude Code now has a built-in scheduling system. The `/loop` command runs prompts or slash commands on a recurring interval within your active session. For persistent scheduling that survives restarts, the Desktop app offers scheduled tasks. Under the hood, both use cron expressions with 1-minute granularity.

## Why It Matters

Before scheduling, you had to manually re-ask Claude to check on things:
- "Did the deploy finish?" (ask every 5 minutes)
- "Any new PR comments?" (ask every 30 minutes)
- "Is the build green?" (ask before merging)

Now Claude handles recurring checks automatically while you work.

---

## Quick Start (60 Seconds)

```
/loop 5m check if the deployment finished
```

Claude creates a cron job that fires every 5 minutes, checks deploy status, and reports back.

---

## /loop Command

### Syntax

```
/loop <interval> <prompt or /command>
/loop <prompt> every <interval>       # interval at end also works
/loop <prompt>                        # defaults to 10 minutes
```

### Interval Units

| Unit | Example | Notes |
|------|---------|-------|
| `s` (seconds) | `/loop 30s check status` | Rounded up to nearest minute (cron limit) |
| `m` (minutes) | `/loop 5m run tests` | Most common |
| `h` (hours) | `/loop 2h check PRs` | Good for babysitting |
| `d` (days) | `/loop 1d security check` | Daily recurring |

### Examples

```
/loop 5m check if the deployment finished
/loop 30m /review-pr 1234
/loop 2h monitor the server status
/loop check the build status                 # every 10 minutes (default)
/loop run /code-review every 20 minutes      # natural language interval
```

### How It Works Internally

1. Parses interval → converts to cron expression
2. Schedules job with unique 8-character ID
3. Scheduler checks every second for due tasks
4. Tasks fire between conversational turns (not mid-response)
5. Results appear as low-priority messages in your session

---

## One-Time Reminders

For single-fire events, use natural language instead of `/loop`:

```
remind me at 3pm to push the release branch
in 45 minutes, check whether the integration tests passed
at 5:30pm, run the migration script
```

One-time reminders auto-delete after firing.

---

## Managing Scheduled Tasks

### List Tasks

```
what scheduled tasks do I have?
```

Or Claude uses the `CronList` tool internally.

### Cancel Tasks

```
cancel the deploy check job
stop the PR review loop
```

Claude uses `CronDelete` with the task's 8-character ID.

### Limits

| Constraint | Value |
|-----------|-------|
| Max tasks per session | 50 |
| Auto-expiry | 3 days for recurring tasks |
| Minimum interval | 1 minute (cron granularity) |
| Missed fires | Fires once when Claude becomes idle (no catch-up) |

---

## Desktop Scheduled Tasks (Persistent)

For tasks that must survive session restarts, the Claude Code Desktop app (macOS/Windows) offers persistent scheduled tasks:

| Feature | /loop (CLI) | Desktop Scheduled Tasks |
|---------|------------|------------------------|
| Persistence | Session-scoped (dies on exit) | Survives restarts |
| Platform | CLI, IDE, Desktop | Desktop app only |
| Configuration | `/loop` command | Visual schedule UI |
| Frequency | Any interval | Daily, weekly, custom times |
| Session | Runs in current session | Each fires as fresh session |

### Desktop Setup

1. Open Claude Code Desktop app
2. Navigate to Scheduled Tasks
3. Configure frequency, time, and prompt
4. Tasks run automatically on schedule

For Linux (no Desktop app), use `claude -p` in a system cron job:

```bash
# crontab -e
0 9 * * 1-5 claude -p "run test suite and report results" >> ~/claude-cron.log 2>&1
```

---

## Cron Expression Reference

If you need precise control, the underlying cron format is:

```
┌───────────── minute (0-59)
│ ┌───────────── hour (0-23)
│ │ ┌───────────── day of month (1-31)
│ │ │ ┌───────────── month (1-12)
│ │ │ │ ┌───────────── day of week (0-6, Sun=0)
│ │ │ │ │
* * * * *
```

| Expression | Meaning |
|-----------|---------|
| `*/5 * * * *` | Every 5 minutes |
| `0 9 * * *` | Daily at 9am |
| `0 9 * * 1-5` | Weekdays at 9am |
| `30 14 15 3 *` | March 15 at 2:30pm |
| `0 */2 * * *` | Every 2 hours |

Times are always in your **local timezone**.

---

## Real-World Workflows

### Workflow 1: Babysit a Deploy

```
/loop 5m check if the GitHub Actions deploy workflow completed for main branch. If it failed, show me the error.
```

### Workflow 2: PR Review Monitor

```
/loop 30m /review-pr 456
```

Every 30 minutes, runs the code review skill on PR #456 and reports new findings.

### Workflow 3: Build Status Dashboard

```
/loop 10m check CI status for all open PRs and summarize which are green, failing, or pending
```

---

## How It Interacts With Other Features

| Feature | Interaction |
|---------|-------------|
| **Skills** | `/loop 5m /skill-name` runs any skill on a schedule |
| **MCP Servers** | Scheduled prompts can use MCP tools (Sentry, GitHub, etc.) |
| **Agent Teams** | Teammates can have their own loops |
| **Remote Control** | Loops continue while controlling from phone |
| **Session Resume** | Loops are NOT preserved across session resume (session-scoped) |
| **Hooks** | No direct hook integration — loops are prompt-level |

---

## Gotchas & Tips

1. **Session-scoped** — loops die when you exit Claude Code. Use Desktop scheduled tasks for persistence.

2. **No catch-up** — if Claude is busy when a loop fires, it runs once when idle (doesn't queue multiple missed runs).

3. **3-day auto-expiry** — recurring tasks auto-delete after 3 days to prevent zombie jobs.

4. **Odd intervals rounded** — `7m` or `90m` get rounded to the nearest clean cron value.

5. **Low priority** — loop results fire between your conversational turns, never interrupting mid-response.

6. **Requires v2.1.72+** — check with `claude --version`.

---

## Version History

| Version | Date | Change |
|---------|------|--------|
| v2.1.66 | Mar 2026 | `/loop` command introduced |
| v2.1.68 | Mar 2026 | Desktop scheduled tasks (macOS/Windows) |
| v2.1.72 | Mar 2026 | One-time reminders, natural language intervals |
| v2.1.76 | Mar 2026 | Stability fixes, improved cron parsing |
