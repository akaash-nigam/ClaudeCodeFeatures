# Agent Teams & Background Agents

> Introduced: v2.1.x (February 5, 2026) — Research Preview | Latest: v2.1.53

## What It Is

Agent Teams let you spawn multiple Claude instances (teammates) that work in parallel on different parts of a task. A lead session coordinates the work through a shared task list and mailbox. Each teammate has its own context window and can work independently. Background agents are a simpler variant — fire-and-forget subagents that run concurrently while you continue working.

## Why It Matters

Some tasks are embarrassingly parallel: reviewing security, performance, and tests on the same PR. Agent teams let you:
- 3 reviewers examine a PR simultaneously (security, perf, tests)
- One agent refactors backend while another updates frontend
- Background agents run linting/testing while you keep coding
- Cut wall-clock time by 3x on parallel-friendly tasks

---

## Quick Start (60 Seconds)

### Agent Teams

```bash
# Enable agent teams (required — research preview)
export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1
claude

# Or in settings.json
{
  "env": { "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1" }
}
```

Then in Claude Code:

```
Create an agent team with 3 reviewers for the latest PR:
- Security reviewer: focus on auth and data leaks
- Performance reviewer: focus on N+1 queries and memory
- Test reviewer: focus on coverage gaps and edge cases
```

### Background Agents (Simpler)

```
Run a background agent to check test coverage while I continue working.
```

Background agents run in the current session and return results when done.

---

## Agent Teams Workflow

### Step 1: Create Team
Ask Claude to create a team. It spawns:
- **Lead session** (you) — coordinates
- **Teammate sessions** — independent Claude instances
- **Shared task list** — visible to all
- **Mailbox** — for inter-agent messaging

### Step 2: Assign Tasks
```
Assign the frontend review to the UX reviewer.
Let each teammate self-claim available tasks.
```

### Step 3: Navigate Between Teammates
```
Shift+Down    → Cycle through teammates
Shift+Down    → Back to lead (wraps around)
Type message  → Send to currently focused teammate
```

### Step 4: Monitor Progress
```
Show me the task list and status of all teammates.
```

### Step 5: Shutdown
```
Ask the researcher teammate to shut down.
Clean up the team.    # Only works after all teammates are stopped
```

---

## Display Modes

| Mode | Setup | Best for |
|------|-------|----------|
| `in-process` (default) | None | Any terminal. Teammates share one window |
| `tmux` | `brew install tmux` | Split panes, see all agents at once |
| `auto` | — | Uses tmux if available, else in-process |

```bash
claude --teammate-mode tmux     # Force tmux mode
claude --teammate-mode auto     # Auto-detect (default)
```

In tmux mode, each teammate gets its own pane. iTerm2 uses native split panes.

---

## Background Agents

Simpler than teams — no coordination, just fire-and-forget:

```
Run a background agent to:
1. Find all TODO comments in the codebase
2. Categorize by priority
3. Create a summary
```

Background agents:
- Run concurrently in your session
- Pre-approve permissions upfront
- Return results when done
- Can be killed with **Ctrl+F** (two presses to confirm)

### Background vs Team

| | Background Agent | Team Teammate |
|---|---|---|
| Context | Shares session | Own context window |
| Communication | Returns summary | Mailbox + task list |
| Coordination | None | Lead coordinates |
| Use case | One-off tasks | Parallel sustained work |

---

## Configuration

### Define Custom Agents

```json
// CLI flag
claude --agents '{"reviewer": {"description": "Reviews code", "prompt": "You are a code reviewer"}}'

// Or in settings.json
{
  "agents": {
    "security-reviewer": {
      "description": "Security-focused reviewer",
      "prompt": "Focus on OWASP top 10, auth, data leaks",
      "model": "opus"
    }
  }
}
```

### Worktree Isolation for Teammates

```
Spawn a teammate with worktree isolation to refactor the auth module.
```

Each teammate can work in its own worktree, preventing file conflicts.

### Permissions

- Teammates inherit lead's permissions at spawn
- Can override per teammate after spawning (Shift+Down → Shift+Tab)
- `--dangerously-skip-permissions` applies to all teammates

---

## Real-World Workflows

### Workflow 1: Parallel PR Review (3 Reviewers)

```
Create an agent team for PR #142:

Reviewer 1 (Security):
- Check auth flows, token handling, input validation
- Look for injection risks, data leaks

Reviewer 2 (Performance):
- Profile hotspots, check for N+1 queries
- Review algorithm efficiency, memory usage

Reviewer 3 (Tests):
- Verify coverage, check edge cases
- Look for flaky tests, missing assertions

Have each reviewer report findings, then synthesize a final review.
```

### Workflow 2: Parallel Feature Implementation

```
Create a team:
- Backend agent: Add new /api/notifications endpoint with tests
- Frontend agent: Build NotificationBell component with Storybook
- Each should work in a worktree to avoid conflicts
```

### Workflow 3: Background Linting While Working

```
> Run a background agent to lint all TypeScript files and fix auto-fixable issues.
> [continue working on your feature]
> [background agent returns: "Fixed 23 lint issues across 8 files"]
```

---

## How It Interacts With Other Features

| Feature | Interaction |
|---------|-------------|
| **Worktrees** | Teammates can each work in isolated worktrees |
| **Session Resume** | Teammates are NOT preserved on resume (must respawn) |
| **Hooks** | `TeammateIdle` and `TaskCompleted` hooks for quality gates |
| **MCP Servers** | Teammates inherit lead's MCP servers |
| **Skills** | Teammates can invoke skills available to lead |
| **Plugins** | Teammates inherit enabled plugins |
| **Permissions** | Inherited from lead at spawn, overridable per teammate |

---

## Gotchas & Tips

1. **Research preview** — requires `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`. Expect rough edges.

2. **Teammates lose history on resume** — `/resume` does NOT restore teammates. You'll need to respawn them.

3. **Non-overlapping work** — give teammates distinct, non-overlapping tasks. Same-file edits without worktrees will conflict.

4. **3-5 teammates optimal** — coordination overhead increases beyond 5. Token usage scales linearly.

5. **Detailed spawn prompts** — teammates don't inherit conversation history. Include specific file paths, line references, and full context in their spawn prompt.

6. **One team per session** — can't spawn multiple teams. Teammates can't spawn their own teams (no nesting).

7. **tmux cleanup** — if cleanup fails, check with `tmux ls` and `tmux kill-session -t <name>`.

8. **Ctrl+F** — two presses to kill all background agents. Single press shows confirmation.

9. **Shift+Down wraps** — after last teammate, cycles back to lead.

10. **Split panes** — not supported in VS Code integrated terminal or Windows Terminal. Use in-process mode.

---

## Version History

| Version | Date | Change |
|---------|------|--------|
| v2.0.x | Late 2025 | Subagent system (Explore, Plan) — precursor |
| Feb 5, 2026 | v2.1.x | Agent Teams research preview announced |
| v2.1.45 | Feb 2026 | Agent Teams fixes on Bedrock, Vertex, Foundry |
| v2.1.47 | Feb 2026 | Ctrl+F to kill background agents, concurrent agent fixes |
| v2.1.49 | Feb 2026 | Background agents (`background: true`), `isolation: worktree` |
| v2.1.50 | Feb 2026 | `claude agents` subcommand, worktree hooks for agents |
| v2.1.53 | Feb 2026 | Bulk agent kill (Ctrl+F) notification fix, teammate navigation |
