# Hooks System

> Introduced: v2.0.x (Late 2025) | Frontmatter support: v2.1.0 | Latest: v2.1.76

## What It Is

Hooks are event-driven automations that fire at specific points in Claude Code's lifecycle. When Claude is about to run a bash command, edit a file, or finish a response — hooks can intercept, validate, transform, or block the action. They're configured in `settings.json` and can be shell commands, LLM prompts, or full subagents.

## Why It Matters

Hooks turn Claude Code from interactive to automated:
- Auto-format files after every edit (Prettier, Black, gofmt)
- Block edits to protected files (.env, package-lock.json)
- Send desktop notifications when Claude needs attention
- Enforce quality gates before marking tasks complete
- Audit configuration changes for security
- Re-inject context after compaction

---

## Quick Start (60 Seconds)

Add to `~/.claude/settings.json`:

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"Claude needs attention\" with title \"Claude Code\"'"
          }
        ]
      }
    ]
  }
}
```

Now you get macOS notifications whenever Claude is waiting for input.

---

## All Hook Events (22 Events)

### Session Lifecycle

| Event | Fires when | Can block? | Matcher values |
|-------|-----------|------------|----------------|
| `SessionStart` | Session begins/resumes | Yes | `startup`, `resume`, `clear`, `compact` |
| `SessionEnd` | Session terminating | Yes | `clear`, `logout`, `prompt_input_exit`, `other` |
| `PreCompact` | Before context compaction | Yes | `manual`, `auto` |
| `PostCompact` | After context compaction completes | No | `manual`, `auto` |

### User Input

| Event | Fires when | Can block? | Matcher |
|-------|-----------|------------|---------|
| `UserPromptSubmit` | Before prompt processing | Yes | — |

### Tool Lifecycle

| Event | Fires when | Can block? | Matcher values |
|-------|-----------|------------|----------------|
| `PreToolUse` | Before tool executes | Yes | Tool name: `Bash`, `Edit`, `Write`, `mcp__server__tool` |
| `PostToolUse` | After tool succeeds | No | Tool name |
| `PostToolUseFailure` | After tool fails | No | Tool name |
| `PermissionRequest` | Permission dialog | Yes | Tool name |

### Agent Lifecycle

| Event | Fires when | Can block? | Matcher values |
|-------|-----------|------------|----------------|
| `SubagentStart` | Subagent spawned | No | Agent type: `Explore`, `Plan`, `code-reviewer` |
| `SubagentStop` | Subagent finished | No | Agent type |
| `TeammateIdle` | Teammate about to idle | Yes | — |
| `TaskCompleted` | Task marked complete | Yes | — |

### MCP Lifecycle

| Event | Fires when | Can block? | Matcher values |
|-------|-----------|------------|----------------|
| `Elicitation` | MCP server requests structured input | Yes | MCP server name |
| `ElicitationResult` | Before response sent back to MCP | Yes | MCP server name |

### System Events

| Event | Fires when | Can block? | Matcher values |
|-------|-----------|------------|----------------|
| `Stop` | Claude finishes responding | Yes | — |
| `Notification` | Notification queued | No | `permission_prompt`, `idle_prompt`, `auth_success` |
| `ConfigChange` | Config file modified | Yes | `user_settings`, `project_settings`, `local_settings` |
| `WorktreeCreate` | Worktree being created | Yes | — |
| `WorktreeRemove` | Worktree being removed | No | — |

---

## Hook Types

| Type | What it is | Tool access? | Timeout | Best for |
|------|-----------|-------------|---------|----------|
| `command` | Shell command | No (stdin/stdout) | 10 min | Formatting, validation, logging |
| `prompt` | Single LLM turn (Haiku) | No | 10 sec | Policy decisions |
| `agent` | Multi-turn subagent | Yes | 60 sec | Complex verification |

---

## Configuration

### In settings.json

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo 'Bash command about to run'"
          }
        ]
      }
    ]
  }
}
```

### Config Scope

| File | Scope |
|------|-------|
| `~/.claude/settings.json` | All projects |
| `.claude/settings.json` | This project (team-shared) |
| `.claude/settings.local.json` | Personal overrides |
| Skill/agent frontmatter | Scoped to skill lifecycle |

### Matcher Patterns (Regex)

```json
"matcher": "Bash"              // Exact: Bash tool only
"matcher": "Edit|Write"        // Regex OR: Edit or Write
"matcher": "mcp__.*"           // All MCP tools
"matcher": "mcp__github__.*"   // GitHub MCP tools only
"matcher": ""                  // All (empty = match everything)
```

---

## Exit Code Protocol

| Exit Code | Effect |
|-----------|--------|
| **0** | Allow. stdout added to Claude's context |
| **2** | Block. stderr shown as reason |
| **Other** | Allow. stderr logged in verbose mode only |

Hooks receive JSON on stdin with event details and tool input.

---

## Real-World Workflows

### Workflow 1: Auto-Format After Every Edit

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | xargs npx prettier --write 2>/dev/null; exit 0"
          }
        ]
      }
    ]
  }
}
```

### Workflow 2: Block Protected Files

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "FILE=$(jq -r '.tool_input.file_path'); case \"$FILE\" in *.env*|*credentials*|*package-lock.json) echo \"Protected file: $FILE\" >&2; exit 2;; esac; exit 0"
          }
        ]
      }
    ]
  }
}
```

### Workflow 3: Re-inject Context on Compaction

```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "compact",
        "hooks": [
          {
            "type": "command",
            "command": "echo 'REMINDER: Use Bun not npm. Run bun test before commits. Current sprint: auth refactor.'"
          }
        ]
      }
    ]
  }
}
```

### Workflow 4: Quality Gate with Agent Hook

```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "prompt",
            "prompt": "Are all requested tasks complete? Return {\"ok\": true} if yes, {\"ok\": false, \"reason\": \"...\"} if no."
          }
        ]
      }
    ]
  }
}
```

### Workflow 5: Re-inject Context After Compaction (PostCompact)

```json
{
  "hooks": {
    "PostCompact": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "echo 'CONTEXT RESTORED: Key project details — use Bun, run tests before commits, current sprint: auth refactor.'"
          }
        ]
      }
    ]
  }
}
```

### Workflow 6: Intercept MCP Elicitation

```json
{
  "hooks": {
    "Elicitation": [
      {
        "matcher": "sentry",
        "hooks": [
          {
            "type": "command",
            "command": "echo 'MCP server requesting input — logging for audit' >> ~/mcp-elicitation.log; exit 0"
          }
        ]
      }
    ]
  }
}
```

### Workflow 7: Audit Config Changes

```json
{
  "hooks": {
    "ConfigChange": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$(date): config changed\" >> ~/claude-config-audit.log"
          }
        ]
      }
    ]
  }
}
```

---

## How It Interacts With Other Features

| Feature | Interaction |
|---------|-------------|
| **Skills** | Skills can define hooks in frontmatter (active only during skill) |
| **Worktrees** | `WorktreeCreate`/`WorktreeRemove` hooks automate setup/cleanup |
| **Agent Teams** | `TeammateIdle` and `TaskCompleted` enforce quality gates |
| **MCP** | PreToolUse can match `mcp__server__tool` patterns |
| **Subagents** | `SubagentStop` includes `last_assistant_message` field |
| **Permissions** | PreToolUse hooks are separate from permission rules (both can deny) |
| **Plugins** | Plugins can define hooks in `hooks/hooks.json` |

---

## Gotchas & Tips

1. **Shell profile breaks JSON** — if `.zshrc` has `echo` statements, they prepend to hook output. Guard with `if [[ $- == *i* ]]`.

2. **Exit 2 blocks AND shows reason** — stderr becomes the deny message. Exit 0 to add context without blocking.

3. **Stop hooks fire on every response** — not just task completion. Don't run expensive checks on every response.

4. **Async hooks can't block** — `"async": true` runs in background. Use for fire-and-forget only (logging, linting).

5. **Make scripts executable** — `chmod +x hooks/*.sh`. Use absolute paths: `"$CLAUDE_PROJECT_DIR"/.claude/hooks/script.sh`.

6. **statusLine and fileSuggestion** hooks require workspace trust (security fix in v2.1.51).

7. **Debug hooks** — `claude --debug "hooks"` shows hook execution details.

---

## Version History

| Version | Date | Change |
|---------|------|--------|
| v2.0.x | Late 2025 | Basic hook system introduced |
| v2.1.0 | Jan 2026 | Hooks in skill/agent frontmatter |
| v2.1.47 | Feb 2026 | Hook execution stability fixes |
| v2.1.49 | Feb 2026 | `SubagentStop` includes `last_assistant_message` |
| v2.1.50 | Feb 2026 | `WorktreeCreate`, `WorktreeRemove`, `ConfigChange` events |
| v2.1.51 | Feb 2026 | `statusLine`/`fileSuggestion` require workspace trust |
| v2.1.76 | Mar 2026 | `PostCompact`, `Elicitation`, `ElicitationResult` events added |
