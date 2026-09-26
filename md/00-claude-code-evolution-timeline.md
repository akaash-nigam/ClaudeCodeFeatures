# Claude Code: The Complete Evolution Timeline

**v0.2 (2024) → v2.1.283 (September 26, 2026)**

From a simple terminal chatbot to a multi-agent development platform with enterprise-grade coordination in 20 months.

---

## Architecture Evolution

```
  v1.0 (Feb 2025)          v2.0 (Sept 2025)          v2.1 (Jan-Mar 2026)
  ┌─────────────┐          ┌─────────────┐           ┌──────────────────┐
  │  Terminal    │          │  Terminal    │           │  Terminal / IDE   │
  │  Chat + Edit │   ──►   │  + VS Code   │    ──►   │  + Mobile/Remote  │
  │  + Bash      │          │  + Checkpts  │           │  + Agent Teams    │
  │             │          │  + Thinking  │           │  + Worktrees      │
  └─────────────┘          └─────────────┘           │  + Skills/Hooks   │
   Single model             Multi-model               │  + Plugins/MCP    │
   Stateless                Persistent                │  + Memory/Sched.  │
   Manual only              Semi-autonomous           └──────────────────┘
                                                       Multi-agent + Remote
                                                       + 1M Context
```

---

## Phase 1: Initial Launch (February - September 2025)

### v1.0.0 Preview (February 2025)
The first public release. A terminal-based AI coding assistant.

| Feature | Description |
|---------|-------------|
| **Core CLI** | Chat with Claude directly in terminal |
| **File Editing** | Edit files with natural language commands |
| **Bash Integration** | Run shell commands with permission prompts |
| **Git Integration** | Commit, diff, branch operations |
| **Permission System** | Allow/deny tool access per session |
| **CLAUDE.md** | Project-level instructions file |
| **Session Persistence** | Basic `-c` (continue) and `-r` (resume) |

### v1.0.0 GA (May 2025)
General availability alongside Claude Opus 4 and Claude Sonnet 4.

| Feature | Description |
|---------|-------------|
| **Multi-Model Support** | Choose between Opus, Sonnet, Haiku |
| **Web Browsing** | Fetch and analyze web content |
| **Claude Agent SDK** | Headless mode (`-p` flag) for scripting |
| **Context Compaction** | Auto-compress conversation when context fills |

### v1.0.x Series (March - September 2025)
Rapid feature additions through the first year.

| Month | Features Added |
|-------|---------------|
| **March 2025** | Vim/Emacs keybindings, custom commands (`.claude/commands/`), thinking mode, auto-compaction |
| **April 2025** | Image support, @-mentions, concurrent queries, network tools |
| **May 2025** | MCP server support (v1.0.52), plugin system (v1.0.33+) |
| **Jun-Sept** | Incremental improvements through v1.0.128 |

---

## Phase 2: IDE & Autonomy (September - December 2025)

### v2.0.0 (September 29, 2025) — Major Architectural Shift
Complete reimagining. Designed for autonomous, multi-hour sessions.

| Feature | Description |
|---------|-------------|
| **VS Code Extension** | Native IDE integration with sidebar, inline diffs |
| **Checkpoint System** | Automatic snapshots every prompt. `Esc Esc` to rewind. 30-day retention |
| **Extended Thinking** | Tab key toggles deep reasoning mode |
| **Prompt History** | Ctrl+R to search past prompts |
| **Default Model** | Claude Sonnet 4.5 (new at launch) |
| **Subagents** | Delegate subtasks to specialized agents (Explore, Plan) |
| **Revamped Terminal** | Better display for autonomous operations |

### v2.0.x Series (October - December 2025)
76 incremental releases stabilizing the new architecture.

---

## Phase 3: Agent Framework (January 2026)

### v2.1.0 (January 7, 2026) — 1,096 Commits
The skills and hooks overhaul.

| Feature | Description |
|---------|-------------|
| **Skills System** | `SKILL.md` with YAML frontmatter, hot-reload, forked context, custom agents |
| **Hooks in Frontmatter** | Skills and agents can define their own hooks |
| **Shift+Enter** | Newlines in prompts without configuration |
| **/teleport** | Move sessions to claude.ai/code (web) |
| **MCP list_changed** | Dynamic tool updates from MCP servers |
| **Language Config** | Configure Claude's response language |
| **Wildcard Permissions** | `Bash(*-h*)` pattern matching |

### v2.1.41-44 (January 2026)
| Feature | Description |
|---------|-------------|
| **Auth Subcommands** | `claude auth login/status/logout` |
| **Session Naming** | `/rename` command for sessions |
| **Opus 4.6 Model** | New model with effort levels |
| **Windows ARM64** | Native binary support |

---

## Phase 4: Multi-Agent & Remote (February 2026)

### v2.1.45-46 (February 17-18, 2026)
| Feature | Description |
|---------|-------------|
| **Sonnet 4.6** | New fast model with full 1M context |
| **Plugin Enhancements** | `enabledPlugins`, `extraKnownMarketplaces` from CLI |
| **Spinner Tips** | `spinnerTipsOverride` setting |
| **MCP Connector** | MCP support for claude.ai |

### v2.1.47 (February 18, 2026) — Major Stability Release
70+ bug fixes. The quality release.

| Category | Fixes |
|----------|-------|
| **Memory** | LSP diagnostic leaks, shell buffer accumulation, WASM interpreter leaks |
| **Files** | Trailing blank line preservation, Unicode curly quotes, Windows line endings |
| **Sessions** | Title persistence after resume, picker expanded to 50, large message support |
| **Git** | Read-only commands no longer trigger FSEvents, custom agents in worktrees |
| **Windows** | MSYS2/Cygwin output, bold text shifting, CWD tracking cleanup |
| **UI** | Input flicker, CJK alignment, hyperlinks on wrapped lines |

### v2.1.49 (February 19, 2026) — Worktrees & Background Agents
| Feature | Description |
|---------|-------------|
| **`--worktree` / `-w`** | Isolated git worktrees for parallel development |
| **Background Agents** | `background: true` for fire-and-forget subagents |
| **`isolation: worktree`** | Each subagent gets its own worktree |
| **Ctrl+F** | Kill all background agents (two-press confirmation) |
| **Sonnet 4.5 1M Deprecated** | Replaced by Sonnet 4.6 |

### v2.1.50 (February 20, 2026) — Worktrees Go First-Class
| Feature | Description |
|---------|-------------|
| **WorktreeCreate/Remove Hooks** | Automate worktree lifecycle |
| **`claude agents`** | New CLI subcommand to list agents |
| **LSP `startupTimeout`** | Configurable timeout for language servers |
| **1M Context in Fast Mode** | Opus 4.6 fast mode now includes full 1M window |
| **Multiple Memory Fixes** | Tool results >50KB to disk, completed task cleanup |

### v2.1.51 (February 24, 2026) — Remote Control Launch
| Feature | Description |
|---------|-------------|
| **`claude remote-control`** | Control local sessions from phone/browser |
| **QR Code Access** | Scan to connect from mobile |
| **Plugin Registries** | Custom npm registries, version pinning |
| **Managed Settings** | macOS plist, Windows Registry support |
| **Security** | statusLine/fileSuggestion hooks require workspace trust |

### v2.1.52-56 (February 24-25, 2026)
Rapid stability fixes for Remote Control, worktrees, Windows crashes, VS Code extension.

---

## Phase 5: Scheduling, Memory & Context (March 2026)

### v2.1.57-65 (Late February - Early March 2026)
Incremental improvements and stability fixes.

| Feature | Description |
|---------|-------------|
| **Auto-Memory** | Persistent file-based memory system across conversations |
| **`/context` Command** | Actionable suggestions for optimizing context usage |
| **`/color` Command** | Visually distinguish parallel sessions with colors |
| **Memory Timestamps** | Last-modified dates on memory files for freshness reasoning |
| **`autoMemoryDirectory`** | Configurable directory for auto-memory storage |

### v2.1.66-70 (March 2026) — Scheduling & Effort Control
| Feature | Description |
|---------|-------------|
| **`/loop` Command** | Session-scoped recurring task scheduler (cron under the hood) |
| **`/effort` Command** | Set model reasoning effort level per session |
| **Desktop Scheduled Tasks** | Persistent tasks in desktop app (survive restarts) |
| **One-Time Reminders** | Natural language single-fire reminders |
| **CronCreate/List/Delete** | Underlying scheduling tools for `/loop` |

### v2.1.71-74 (March 2026) — 1M Context & Fast Mode
| Feature | Description |
|---------|-------------|
| **1M Token Context** | Default for Opus 4.6 on Max, Team, Enterprise plans |
| **Fast Mode** | `/fast` toggle for faster output (same model, lower latency) |
| **Model Fallback Names** | Human-friendly names in fallback notifications |
| **Session Quality Surveys** | Enterprise `feedbackSurveyRate` setting |

### v2.1.75-76 (March 14, 2026) — MCP Elicitation & Sparse Checkout
| Feature | Description |
|---------|-------------|
| **MCP Elicitation** | MCP servers can request structured input via interactive dialogs |
| **Elicitation Hooks** | `Elicitation` and `ElicitationResult` hook events |
| **`PostCompact` Hook** | Fires after context compaction completes |
| **Session Naming** | `-n` / `--name` CLI flag for display names at startup |
| **Sparse Checkout** | `worktree.sparsePaths` for fast startup in large monorepos |
| **Deferred Tool Fix** | ToolSearch tools retain schemas after compaction |

---

## Phase 6: Channels, Security Hardening & Performance (March 17-25, 2026)

### v2.1.77 (March 17, 2026) — Output Limits & Agent Messaging
| Feature | Description |
|---------|-------------|
| **64K Default Output** | Opus 4.6 default max output raised to 64K tokens; upper bound 128K for Opus/Sonnet 4.6 |
| **`allowRead` Sandbox** | Re-allow read access within `denyRead` regions |
| **`/copy N`** | Copy the Nth-latest assistant response |
| **`/branch` (renamed /fork)** | `/fork` → `/branch` (alias still works) |
| **Agent SendMessage** | `resume` parameter removed from Agent tool — use `SendMessage({to: agentId})` to continue agents |
| **Background Bash Limits** | Background tasks killed if output exceeds 5GB |
| **Security Fix** | PreToolUse hooks returning `"allow"` no longer bypass `deny` permission rules |
| **Performance** | `--resume` up to 45% faster, ~100-150MB less peak memory; macOS startup ~60ms faster |

### v2.1.78 (March 17, 2026) — StopFailure Hook & Streaming
| Feature | Description |
|---------|-------------|
| **`StopFailure` Hook** | Fires when turn ends due to API error (rate limit, auth failure) |
| **`${CLAUDE_PLUGIN_DATA}`** | Persistent plugin state that survives updates |
| **Plugin Agent Frontmatter** | `effort`, `maxTurns`, `disallowedTools` support for plugin-shipped agents |
| **Line-by-Line Streaming** | Response text streams line-by-line as generated |
| **`ANTHROPIC_CUSTOM_MODEL_OPTION`** | Env var to add custom entry to `/model` picker |
| **tmux Notifications** | Terminal notifications pass through tmux with `allow-passthrough on` |
| **Security Fix** | Silent sandbox disable now shows visible startup warning |

### v2.1.79 (March 18, 2026) — Console Auth & Turn Duration
| Feature | Description |
|---------|-------------|
| **`--console` Auth** | `claude auth login --console` for Anthropic Console (API billing) |
| **Turn Duration Toggle** | "Show turn duration" in `/config` menu |
| **[VSCode] /remote-control** | Bridge VS Code session to claude.ai/code for browser/phone |
| **[VSCode] AI Session Titles** | Tabs get AI-generated titles from first message |
| **Performance** | Startup memory reduced by ~18MB |

### v2.1.80 (March 19, 2026) — Rate Limits & Channels Preview
| Feature | Description |
|---------|-------------|
| **Rate Limit in Statusline** | `rate_limits` field for 5-hour and 7-day usage windows |
| **Inline Plugin Sources** | `source: 'settings'` — declare plugins directly in settings.json |
| **Skill Effort Override** | `effort` frontmatter in skills overrides model effort level |
| **`--channels` (Preview)** | MCP servers can push messages into your session |
| **Performance** | ~80MB saved on startup in large repos (250K+ files) |

### v2.1.81 (March 20, 2026) — Bare Mode & Channel Permissions
| Feature | Description |
|---------|-------------|
| **`--bare` Flag** | Scripted `-p` calls skip hooks, LSP, plugins, skills, auto-memory |
| **Channel Permission Relay** | Channel servers can forward tool approval prompts to your phone |
| **MCP OAuth CIMD** | Support for Client ID Metadata Document (SEP-991) |
| **Worktree Resume** | Resuming a session in a worktree switches back to that worktree |

*v2.1.82 — Skipped (no release)*

### v2.1.83 (March 25, 2026) — Drop-in Policies, Transcript Search & New Hooks
| Feature | Description |
|---------|-------------|
| **`managed-settings.d/`** | Drop-in directory for team policy fragments (merge alphabetically) |
| **`CwdChanged` Hook** | Fires when working directory changes (e.g., direnv integration) |
| **`FileChanged` Hook** | Fires when files change (reactive environment management) |
| **`sandbox.failIfUnavailable`** | Exit with error when sandbox can't start |
| **Transcript Search** | Press `/` in transcript mode (Ctrl+O), `n`/`N` to step through matches |
| **`Ctrl+X Ctrl+E`** | Open external editor (readline-native binding) |
| **Image Chips** | Pasted images insert `[Image #N]` chip at cursor for positional referencing |
| **Agent `initialPrompt`** | Agents can auto-submit a first turn via frontmatter |
| **`/status` While Responding** | Works during streaming instead of being queued |
| **Interrupt Restore** | Interrupting before response auto-restores your input for editing |
| **`TaskOutput` Deprecated** | Use `Read` on background task output file instead |
| **Keybinding Changes** | Stop agents: Ctrl+F → Ctrl+X Ctrl+K; both rebindable via keybindings.json |
| **`WebFetch` User Agent** | Now identifies as `Claude-User` for robots.txt allowlisting |
| **Security Fix** | `--mcp-config` CLI flag no longer bypasses `allowedMcpServers` policy |
| **Performance** | Non-streaming cap raised 21K→64K tokens; timeout 120s→300s; caffeinate leak fixed |

---

## Phase 7: Agent Memory & Enterprise Coordination (May - September 2026)

### v2.1.84-150 (May - August 2026)
Incremental improvements building toward enterprise features.

| Month | Milestone | Key Improvements |
|-------|-----------|------------------|
| **May 2026** | Dreaming feature | Agent memory consolidation, duplicate merging, stale entry removal |
| **June 2026** | Performance focus | Session startup optimizations, improved context compaction efficiency |
| **July 2026** | Reliability hardening | Better error recovery, enhanced MCP stability, improved network handling |
| **August 2026** | Terminal enhancements | New terminal output controls, verbose/silent mode options, logging improvements |

### v2.1.283 (September 26, 2026) — Enterprise Coordination Release

The major capability expansion for large teams and complex projects.

| Feature | Description |
|---------|-------------|
| **Claude Opus 5.5 Default** | New flagship model with 1M context (from 200K), improved mouse controls, better multi-file reasoning, 5x throughput |
| **Project Coordination (Beta)** | Coordinate parallel threads within one project, shared memory system, project-wide libraries, cross-repo management |
| **Fast Mode Cloud Optimization** | 3x faster output in cloud and self-hosted environments, maintained quality, perfect for iterative development |
| **Plugin Evaluation Tool** | Run plugins against test cases, baseline comparison, regression detection, HTML reports for validation |
| **Enhanced Terminal Controls** | Fine-grained output control, customizable shell environment per session, enhanced debugging options |
| **Improved Policy Management** | Stricter permission controls, audit logging for compliance, role-based access control (RBAC) for teams |
| **Faster Startup & Resume** | 2-5 second improvements, 95%+ session recovery success rate across conversations |
| **Better Multi-session Reliability** | Improved consistency across concurrent conversations, plugins, MCP servers, background agents, remote control |

### Model Strategy (September 2026 Onward)
- **Default**: Claude Opus 5.5 (complex refactoring, large-scale changes, architecture design, 1M context)
- **Alternative**: Claude Sonnet 5 (quick tasks, CI/CD automation, tight latency requirements)
- **Legacy Support**: Claude Haiku 4.5 (constrained environments, simple operations)

### Project Coordination Features (Beta)
```yaml
# .claude/project-config.yaml example
coordination:
  enabled: true
  sharedMemory: 
    path: ./project-memory
    autoSync: true
  threads:
    - name: feature-builder
      worktree: true
    - name: test-writer
      worktree: true
    - name: reviewer
      readonly: true
  library:
    path: ./claude-lib
    autoReload: true
```

---

## Key Milestones at a Glance

| Date | Version | Milestone |
|------|---------|-----------|
| Nov 2024 | — | MCP protocol announced by Anthropic |
| Feb 2025 | v1.0.0 | Claude Code preview launch |
| May 2025 | v1.0.0 GA | General availability + Agent SDK |
| Sept 29, 2025 | v2.0.0 | VS Code extension + Checkpoints + Thinking mode |
| Jan 7, 2026 | v2.1.0 | Skills overhaul + Hooks in frontmatter |
| Feb 5, 2026 | v2.1.x | Agent Teams (research preview) |
| Feb 17, 2026 | v2.1.45 | Sonnet 4.6 released |
| Feb 18, 2026 | v2.1.47 | Major stability release (70+ fixes) |
| Feb 19, 2026 | v2.1.49 | Worktrees + Background agents |
| Feb 24, 2026 | v2.1.51 | Remote Control launch |
| Feb 25, 2026 | v2.1.56 | Stability fixes |
| Early Mar 2026 | v2.1.6x | Auto-Memory, /context, /color |
| Mar 2026 | v2.1.7x | /loop scheduling, /effort, 1M context default |
| Mar 14, 2026 | v2.1.76 | MCP Elicitation, sparse checkout, session naming |
| Mar 17, 2026 | v2.1.77 | 64K/128K output limits, Agent SendMessage, security fix |
| Mar 17, 2026 | v2.1.78 | StopFailure hook, line-by-line streaming, plugin agents |
| Mar 18, 2026 | v2.1.79 | Console auth, VS Code /remote-control, turn duration |
| Mar 19, 2026 | v2.1.80 | Rate limits in statusline, --channels preview, skill effort |
| Mar 20, 2026 | v2.1.81 | --bare mode, channel permission relay, worktree resume |
| Mar 25, 2026 | v2.1.83 | Drop-in policies, CwdChanged/FileChanged hooks, transcript search |

---

## Feature Introduction Order

```
Feb 2025  ████ Core CLI, Permissions, Sessions, CLAUDE.md
Mar 2025  ████ Vim mode, Custom Commands, Thinking, Auto-compact
Apr 2025  ████ Images, @-mentions, Concurrent queries
May 2025  ████ MCP Servers, Plugins, Multi-model, SDK
Sept 2025 ████████ VS Code, Checkpoints, Subagents (v2.0)
Jan 2026  ██████ Skills overhaul, Hooks frontmatter, Teleport (v2.1)
Feb 2026  ████████████ Agent Teams, Worktrees, Remote Control, Sonnet 4.6
Mar 2026  ██████████████ Memory, /loop, 1M, Elicitation, Channels, Transcript Search
May 2026  ████ Dreaming (Agent Memory), Performance focus
Sept 2026 ██████████████████ Opus 5.5 default, Project Coordination (Beta), Fast Mode, Plugin Eval, Terminal Controls
```

---

## What Changed Fundamentally at Each Major Version

### v1.0 → v2.0: From Tool to Partner
- **Before**: You tell Claude what to do, step by step
- **After**: Claude works autonomously for hours. Checkpoints let you rewind if it goes wrong. VS Code shows changes in real-time.

### v2.0 → v2.1: From Single Agent to Platform
- **Before**: One Claude instance, one conversation
- **After**: Multiple agents working in parallel across isolated worktrees. Skills as reusable modules. Hooks for automation. Remote access from any device. Plugin ecosystem for sharing.

---

## See Also: Feature Deep-Dives

| # | Feature | File |
|---|---------|------|
| 01 | Session Resume | `01-session-resume.md` |
| 02 | MCP Servers | `02-mcp-servers.md` |
| 03 | Skills & Custom Commands | `03-skills-custom-commands.md` |
| 04 | Hooks System | `04-hooks-system.md` |
| 05 | Plugins | `05-plugins.md` |
| 06 | Agent Teams & Background Agents | `06-agent-teams-background-agents.md` |
| 07 | Worktree Isolation | `07-worktree-isolation.md` |
| 08 | Remote Control | `08-remote-control.md` |
| 09 | Scheduling & /loop | `09-scheduling-loop.md` |
| 10 | Auto-Memory System | `10-auto-memory.md` |
| 11 | Context, Effort & Fast Mode | `11-context-effort-fast-mode.md` |
| 12 | Memory Architecture for Fleets | `12-memory-architecture-design.md` |
| 24 | September 2026 Features | `24-september-2026-features.md` |
