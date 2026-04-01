# Remote Control

> Introduced: v2.1.51 (February 24, 2026) — Research Preview | Latest: v2.1.53

## What It Is

Remote Control lets you control a Claude Code session running on your local machine from any other device — your phone, tablet, or another computer's browser. The session runs locally (your filesystem, MCP servers, and tools stay on your machine), while the remote device just sends messages and displays results. Think SSH, but for Claude Code conversations.

## Why It Matters

You start a complex refactor at your desk, then need to step away. With Remote Control:
- Continue the conversation from your phone on the couch
- Monitor a long-running agent from your iPad
- Check on Claude's progress from a coffee shop
- No VPN or SSH setup needed — just a URL or QR code

---

## Quick Start (60 Seconds)

```bash
# Navigate to your project
cd ~/my-project

# Start Remote Control
claude remote-control

# Output:
# Session URL: https://claude.ai/code/sessions/abc123
# [QR code displayed]
# Press spacebar to toggle QR code
```

On your phone: scan the QR code or open the URL. You're now controlling the session.

### From an Existing Session

```
# Already in a Claude Code session?
/remote-control
# or shorter:
/rc
```

---

## Requirements

| Requirement | Details |
|-------------|---------|
| **Plan** | Pro or Max (not API keys, not Team/Enterprise) |
| **Auth** | Must be logged in (`claude` → `/login`) |
| **Workspace trust** | Run `claude` in project directory once to accept trust |
| **Network** | Local machine must stay on and connected |

---

## CLI Flags

```bash
claude remote-control              # Start new Remote Control session
claude remote-control --verbose    # Debug logging
claude remote-control --sandbox    # Enable filesystem/network isolation
claude remote-control --no-sandbox # Disable sandboxing (default)
```

---

## How It Works

```
Your Laptop                    Anthropic API                  Your Phone
┌──────────┐    HTTPS/TLS     ┌──────────┐    HTTPS/TLS     ┌──────────┐
│ Claude   │ ───────────────► │  Message  │ ◄─────────────── │ Browser/ │
│ Code CLI │ ◄─────────────── │  Router   │ ───────────────► │ Claude   │
│          │   (polls)        │           │   (sends)        │ App      │
│ Local FS │                  └──────────┘                   └──────────┘
│ MCP      │
│ Tools    │
└──────────┘
```

Key points:
- **No inbound ports** — your machine only makes outbound HTTPS requests
- **Local execution** — Claude runs on your machine, not in the cloud
- **TLS encrypted** — all traffic through Anthropic's API
- **Multiple short-lived credentials** — each scoped to a single purpose

---

## Connecting from Another Device

Three ways to connect:

1. **QR Code** — press spacebar in terminal to toggle. Scan with phone camera.

2. **Session URL** — copy `https://claude.ai/code/sessions/<id>` to any browser.

3. **Claude App** — open [claude.ai/code](https://claude.ai/code) or the mobile app. Remote sessions show a computer icon with green dot when online.

---

## Real-World Workflows

### Workflow 1: Desk to Couch

```bash
# At desk
cd ~/my-project
claude
> add authentication to the login form
> [Claude starts working]
> /rename "Auth implementation"
> /rc

# On couch (phone)
# Scan QR code
# Continue: "Now add rate limiting to the login endpoint"
# Session stays in sync
```

### Workflow 2: Long-Running Task Monitor

```bash
# Start a big refactor
claude
> refactor the entire test suite from Jest to Vitest
> /rc

# Go grab lunch, check from phone periodically
# See Claude's progress, answer permission prompts
# Come back to desk with work done
```

### Workflow 3: Start Locally, Continue on Laptop B

```bash
# Machine A (desktop)
claude remote-control

# Machine B (laptop, browser)
# Open session URL
# Full access to Machine A's filesystem through Claude
# Continue coding as if you were at Machine A
```

---

## Remote Control vs Other Remote Options

| | Remote Control | SSH + tmux | Claude on Web |
|---|---|---|---|
| **Runs on** | Your machine | Your machine | Anthropic cloud |
| **Local files** | Full access | Full access | No access |
| **MCP servers** | Your local servers | Your local servers | Cloud only |
| **Setup** | One command | SSH + tmux config | None |
| **Network** | HTTPS only (outbound) | SSH port needed | Browser only |
| **Plan required** | Pro/Max | None | Pro/Max |

**Choose Remote Control when:** you need local file/tool access without SSH setup.
**Choose SSH + tmux when:** you want full terminal access, not just Claude.
**Choose Claude on Web when:** you don't need local filesystem access.

---

## Configuration

### Enable for All Sessions

```
/config
# Toggle "Enable Remote Control for all sessions" to true
```

### Name Sessions for Easy Discovery

```
/rename "Payment refactor"
/rc
# Now "Payment refactor" shows up on all your devices
```

---

## How It Interacts With Other Features

| Feature | Interaction |
|---------|-------------|
| **Session Resume** | Can `/rc` a resumed session. Session history carries across devices |
| **MCP Servers** | Local MCP servers remain available remotely (runs locally) |
| **Skills** | All skills available remotely (stored locally) |
| **Plugins** | Plugin tools accessible in remote sessions |
| **Agent Teams** | Can monitor and communicate with team from remote |
| **Worktrees** | Worktree sessions can be remote-controlled |
| **Hooks** | All hooks fire normally (run locally) |

---

## Gotchas & Tips

1. **Terminal must stay open** — Remote Control is a local process. Closing the terminal ends the session. Use `tmux` or `screen` to keep it alive.

2. **Machine must stay awake** — if your laptop sleeps, Remote Control stops. Disable sleep: `caffeinate -d` on macOS.

3. **Network interruption** — if offline >10 minutes, session times out. Restart with `claude remote-control`.

4. **One connection at a time** — each local session supports one remote connection.

5. **Not for collaboration** — designed for single-user, multi-device use. Not simultaneous multi-user.

6. **Name your sessions** — `/rename` before `/rc` makes sessions easy to find across devices.

7. **Pro/Max only** — won't work with API keys or Team/Enterprise plans.

---

## Version History

| Version | Date | Change |
|---------|------|--------|
| v2.1.51 | Feb 24, 2026 | Remote Control launched (research preview) |
| v2.1.52 | Feb 24, 2026 | VS Code extension crash fix related to Remote Control |
| v2.1.53 | Feb 25, 2026 | Session cleanup fix, stability improvements |
