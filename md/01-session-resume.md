# Session Resume & Persistence

> Introduced: v1.0.0 (February 2025) | Latest enhancements: v2.1.53

## What It Is

Session resume lets you pick up Claude Code conversations exactly where you left off. Every session is automatically saved to disk — including full message history, tool results, and checkpoints. You can continue the most recent session, browse and resume any past session, or fork a session to explore alternative approaches without losing the original.

## Why It Matters

Long coding tasks rarely finish in one sitting. Session resume means you can:
- Start a feature at work, continue at home
- Explore a risky approach, then fork back to safety if it fails
- Resume PR-linked sessions when reviewers leave feedback
- Keep 50+ named sessions organized across projects

---

## Quick Start (60 Seconds)

```bash
# Start a session, work on something, then exit
claude
> implement oauth2 flow
> exit

# Continue where you left off
claude -c

# Browse all sessions interactively
claude -r

# Resume a specific named session
claude -r "oauth-work"
```

---

## All CLI Flags

| Flag | Short | Description |
|------|-------|-------------|
| `--continue` | `-c` | Continue most recent session in current directory |
| `--resume [name]` | `-r` | Interactive picker, or resume by name/ID |
| `--fork-session` | — | Create new session ID while preserving history |
| `--from-pr [number]` | — | Resume session linked to a GitHub PR |
| `--session-id <uuid>` | — | Use a specific session UUID |
| `--no-session-persistence` | — | Disable saving (only with `-p` print mode) |

---

## Configuration

Sessions are stored automatically. No configuration needed.

**Storage location:**
```
~/.claude/projects/<directory-hash>/<session-id>/
```

**Disable persistence (scripting only):**
```bash
claude -p --no-session-persistence "one-off query"
```

---

## Real-World Workflows

### Workflow 1: Multi-Day Feature Development

```bash
# Day 1: Start the feature
claude
> implement user authentication with JWT
> [work for 2 hours]
> /rename jwt-auth

# Day 2: Pick up where you left off
claude -r jwt-auth
> now add refresh token rotation
> [continue for 1 hour]

# Day 3: Resume again
claude -c    # continues jwt-auth (most recent)
```

### Workflow 2: Fork to Try an Alternative

```bash
# Working on approach A
claude -r jwt-auth
> [halfway through implementation]

# Want to try approach B without losing A
claude -c --fork-session
> actually, let's try passport.js instead
> [explore for 30 minutes, decide it's worse]
> exit

# Original session A is untouched
claude -r jwt-auth
> [continue with original approach]
```

### Workflow 3: Resume from PR Feedback

```bash
# Create PR with Claude
claude
> fix the race condition in session handler
> [Claude commits and creates PR]

# Later, reviewer leaves feedback
claude --from-pr 142
> address the reviewer's comments about error handling
```

---

## Session Picker Navigation

When you run `claude -r` (interactive picker):

| Key | Action |
|-----|--------|
| Up/Down | Navigate sessions |
| Enter | Resume selected |
| P | Preview session content |
| R | Rename session |
| / | Search/filter |
| A | Toggle: current directory vs all projects |
| B | Filter to current git branch |
| Esc | Exit |

The picker shows up to **50 sessions** (expanded from 10 in v2.1.47).

---

## How It Interacts With Other Features

| Feature | Interaction |
|---------|-------------|
| **Worktrees** | Each worktree has separate session history. `-r` in worktree shows only worktree sessions |
| **Agent Teams** | In-process teammates are NOT preserved on resume. Must respawn |
| **Checkpoints** | Preserved per session. `Esc Esc` rewinds within the resumed session |
| **CLAUDE.md** | Reloaded on each resume — changes take effect immediately |
| **Auto Memory** | Memory is global, survives resume and fork |
| **Remote Control** | Can `/rc` a resumed session to continue from another device |
| **tmux** | `tmux attach` + `claude -c` = resume from SSH |

---

## Gotchas & Tips

1. **Don't resume the same session in two terminals** — messages interleave and corrupt history. Use `--fork-session` instead.

2. **Sessions are directory-scoped** — you can't resume a session from `/project-a/` while in `/project-b/`. Use `claude -r` with `A` to see all projects.

3. **Permission modes reset on resume** — if you used `--permission-mode` originally, set it again or configure in `settings.json`.

4. **Context compaction** — large sessions may compress history. Put persistent instructions in `CLAUDE.md`, not in conversation.

5. **Name your sessions** — `/rename auth-refactor` makes them easy to find later. Unnamed sessions show the first prompt as the title.

6. **Fork creates a separate session** — the fork and original are both listed in the picker. Clean up forks you don't need.

---

## Version History

| Version | Date | Change |
|---------|------|--------|
| v1.0.0 | Feb 2025 | Basic `-c` and `-r` session continue/resume |
| v2.0.0 | Sept 2025 | Checkpoint system integrated with sessions |
| v2.1.0 | Jan 2026 | `/teleport` to move sessions to web |
| v2.1.41 | Jan 2026 | `/rename` command, session naming |
| v2.1.47 | Feb 2026 | Picker expanded to 50 sessions, title persistence after resume, large message support |
| v2.1.49 | Feb 2026 | `--fork-session` and `--from-pr` flags |
| v2.1.51 | Feb 2026 | Remote Control integration with sessions |
