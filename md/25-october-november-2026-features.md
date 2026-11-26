# Claude Code October–November 2026: New Features & Capabilities

*Last Updated: November 26, 2026*
*Baseline: v2.1.332 (Current Stable)*
*Covers: v2.1.284 → v2.1.332 (~56 releases since the September 2026 snapshot)*

---

## Overview

October and November 2026 brought Claude Code's biggest platform expansion since the v2.1 agent framework: **Code Review went GA**, **Dynamic Workflows / multi-agent orchestration entered public beta on the API**, **Code Mode reached all major cloud platforms**, and the model lineup shifted again with **Claude Fable 5.2** and the **Opus 5.5 default**. Alongside the headline features came a heavy stability push — v2.1.332 alone shipped 93 bug fixes.

---

## 🚀 Major Features

### 1. Code Review — General Availability (October 15, 2026)

**What it is:**
AI-powered pull request review, promoted from preview to GA. Reviews run automatically when PRs open, on every push, or on demand.

**Key Capabilities:**
- **Three review levels** — Quick (routine codebases), Standard (default), Deep (critical repositories)
- **Trigger options** — on PR open/ready-for-review, on every push, or manually via an `@claude review` comment
- **Faster** — 6–10 minutes per review, down from ~20 minutes in preview
- **Measured impact** — Anthropic's internal testing: merged PRs doubled (Jun–Sep) while reverts fell 40%

**Availability:** Team and Enterprise plans. Admins enable code review per repository and choose the trigger; locally, `/code-review` drives the same engine (with an `ultra` tier for deep multi-agent cloud review of a branch or PR).

---

### 2. Dynamic Workflows & Multi-Agent Orchestration (Public Beta, October 9, 2026)

**What it is:**
Agents write and run **coordination scripts** that orchestrate many subagents deterministically — in parallel, in pipelines, or in loops. The lead agent authors a JavaScript program using primitives like `agent()`, `parallel()`, and `pipeline()`; the harness executes it and fans work out to subagents.

**Two routes:**

| Route | Status | Scale |
|-------|--------|-------|
| **Claude Code (local CLI)** — the `Workflow` tool | GA (research preview since May 2026) | Up to 1,000 agents per run, ~16 concurrent |
| **Claude Managed Agents (API)** — `multiagent: "multiagent_20261001"` beta header | Public Beta (Oct 9, 2026) | Up to 1,000 subagents per run, 64 concurrent threads |

**Example coordination script (local Workflow tool):**
```javascript
export const meta = {
  name: 'review-changes',
  description: 'Review changed files across dimensions, verify each finding',
  phases: [{ title: 'Review' }, { title: 'Verify' }],
}
const results = await pipeline(
  DIMENSIONS,
  d => agent(d.prompt, { phase: 'Review', schema: FINDINGS_SCHEMA }),
  review => parallel(review.findings.map(f => () =>
    agent(`Adversarially verify: ${f.title}`, { phase: 'Verify' })))
)
```

**Opt-in model:** Workflows can spawn dozens of agents and consume significant tokens, so the user must explicitly opt in — via the **"ultracode"** keyword in a prompt, a session-level ultracode toggle, or by directly asking for a workflow.

**Common workflow shapes:** understand (parallel readers → structured map), design (judge panel of N approaches), review (find → adversarially verify), research (multi-modal sweep → synthesize), migrate (discover → transform in worktrees → verify).

---

### 3. Code Mode on Cloud Platforms (v2.1.331, November 23, 2026)

**What it is:**
Code Mode — the persistent script environment with direct command execution — is now generally available on managed cloud platforms, not just local and self-hosted sessions.

**Platforms:**
- Amazon Bedrock
- Google Cloud Agent Platform (Vertex)
- Microsoft Foundry
- Claude Platform on AWS

Sessions resumed with `--resume`/`--continue` keep their permission mode's script limits; worktree state and prompt cache are preserved across cloud sessions.

---

### 4. MCP Server Skills (Beta, v2.1.332, November 24–25, 2026)

**What it is:**
Skills can now be served directly by configured MCP servers. They appear in the `/` menu namespaced as `server:skill`, while local skills keep their plain names.

**How to use:**
- Configure MCP servers as usual; their skills auto-populate the skill menu
- `/skill-doctor` shows which skills come from MCP servers

**Status:** Beta — behavior subject to change.

---

### 5. Built-In Charting — Easel (v2.1.330, November 20, 2026)

**What it is:**
A built-in mod that renders charts in the conversation when you ask for them, and automatically parses MCP metrics tool results into visualizations.

**Use cases:** plotting benchmark results, usage dashboards from MCP metrics servers, quick data exploration without leaving the terminal.

---

### 6. Enterprise Sign-In via Admin Console (v2.1.330, November 20, 2026)

**What it is:**
Organizations can authenticate Claude Code users through the Anthropic Enterprise Admin Console — SSO, centralized license control, and audit logging.

```bash
claude auth login   # now offers org admin-console sign-in
```

Also in this area: stronger self-hosted runner controls and new VS Code workflow automation tools (v2.1.330 shipped 142 changes total).

---

### 7. Ultrathink at xhigh Effort (v2.1.316, October 31, 2026)

**What changed:**
- The `ultrathink` keyword now runs at a new **xhigh** effort level (and renders as rainbow text in VS Code chat)
- New per-subagent effort controls
- Opt out entirely with `CLAUDE_CODE_DISABLE_ULTRATHINK=1`

---

### 8. New Hook: PreSkillShellCommand (v2.1.331, November 23, 2026)

**What it is:**
Fires as skills load, letting you refuse (or silently approve) inline shell commands that a skill wants to run — a guardrail against risky commands baked into third-party skills.

```json
{
  "hooks": {
    "PreSkillShellCommand": [
      { "matcher": "*", "hooks": [{ "type": "command", "command": "./check-skill-cmd.sh" }] }
    ]
  }
}
```

---

## 🤖 Model Lineup Changes (Fall 2026)

| Model | Date | Notes |
|-------|------|-------|
| **Claude Opus 5.5** | Default since v2.1.280 (Sep 22) | 1M context, $4/$20 per Mtok, xhigh effort default; Pro & Team Standard now default to Opus |
| **Claude Sonnet 5.5** | GA Sep 2026+ | $3/$15 per Mtok; new default on Microsoft Foundry and Pro plans |
| **Claude Fable 5.2** | November 9, 2026 | Current default Fable model, 1M context |
| **Claude Fable 5.1** | September 1, 2026 | Superseded by 5.2 |
| **Claude Opus 4.8** | May 28, 2026 | Still GA; **fast mode on Opus 4.8 deprecated** — expires November 30, 2026 (no fallback after) |

**Cloud platform routing updates (v2.1.332):**
- Vertex: `sonnet` → Sonnet 5.5, `opus` → Opus 5.5; new `VERTEX_REGION_CLAUDE_5_5_SONNET` env var; fast mode available in global/us/eu regions (since v2.1.322, Nov 10)
- Microsoft Foundry: default model → Sonnet 5.5; Opus 4/4.1 marked retired
- Bedrock: terminal/VS Code sessions moved to Sonnet 5/5.5 auto mode; Monitor tool supported since v2.1.310 (Oct 23)

---

## ⚠️ Breaking Changes & Deprecations

| Change | Version | Action Required |
|--------|---------|-----------------|
| **Fast mode on Opus 4.8 expires Nov 30, 2026** | v2.1.315+ | Migrate to Opus 5.5 (fast mode supported) |
| **`computer-use` is now a reserved skill name** on Macs with computer use enabled | v2.1.332 | Rename any custom skill/command with that name |
| **OAuth token prefix** for self-hosted runners can now be `oat02-` (was only `oat01-`) | v2.1.332 | Update proxy rules and log scrubbers |
| **OpenTelemetry `service.name`** for desktop sessions changed to `claude-code-desktop` | v2.1.332 | Update dashboards, or set `OTEL_SERVICE_NAME=claude-code` |
| **"Routines" renamed** — `/schedule`, permission prompts, and `/loop` cloud offers now say "cloud scheduled task" | v2.1.332 | Terminology only; `/routines` still aliases |
| **WebSearch budget model changed** — 200-call fixed limit → 100-call hourly refill | v2.1.290 (Oct 5) | Long research sessions no longer hit a hard wall |

---

## 🔧 New Settings & Environment Variables

| Variable | Version | Purpose |
|----------|---------|---------|
| `CLAUDE_CODE_MAX_MCP_DESCRIPTION_LENGTH` | v2.1.280 | Override the 2,048-char MCP tool description cap |
| `CLAUDE_CODE_DISABLE_ULTRATHINK` | v2.1.316 | Disable the `ultrathink` keyword |
| `CLAUDE_CODE_DISABLE_RESPONSE_COMPRESSION` | v2.1.331 | Request uncompressed API responses (proxy debugging) |
| `VERTEX_REGION_CLAUDE_5_5_SONNET` | v2.1.332 | Pin the Vertex region for Sonnet 5.5 |
| `ANTHROPIC_DEFAULT_SONNET_MODEL` | v2.1.332 | Override the default Sonnet on Microsoft Foundry |

---

## 🛡️ Security & Reliability Highlights

- **Email-leak prevention** (v2.1.317, Nov 2) — new validation stops tools from leaking your email without explicit permission
- **Gateway diagnostics** (v2.1.331) — `claude doctor` now includes an API connectivity section; OIDC group extraction via `oidc.groups_jsonpath`
- **macOS computer-use safety** (v2.1.332) — updated safety rules; some actions refused, typing deliberately slower
- **93 bug fixes in v2.1.332** — named-pipe hangs (20s timeout), Code Mode script memory loss, git credentials lost on runner restart, rewind deleting files after failed restores, frozen Ctrl+R history picker, MCP stdout floods freezing the terminal
- **OpenTelemetry** — `gen_ai.*` trace spans on `claude_code.llm_request` (v2.1.300), `assistant_response` event (v2.1.331)

---

## 📊 Feature Maturity Status (as of November 26, 2026)

| Feature | Status | Recommendation |
|---------|--------|-----------------|
| Code Review | **GA** | Enable per-repo on Team/Enterprise |
| Code Mode on cloud platforms | **GA** | Use on Bedrock/Vertex/Foundry |
| Enterprise Admin Console sign-in | **GA** | Adopt for centralized identity |
| Easel charting | **GA** | Ask for charts; MCP metrics auto-render |
| Dynamic Workflows (Managed Agents API) | **Public Beta** | `multiagent_20261001` beta header |
| MCP Server Skills | **Beta** | Expect changes |
| Fast mode on Opus 4.8 | **Deprecated** | Dead after Nov 30 — migrate now |

---

## 📅 Release Digest (Version by Version)

| Version | Date | Highlights |
|---------|------|-----------|
| v2.1.290 | Oct 5 | WebSearch hourly-refill budget; 100+ image session fix |
| v2.1.300 | Oct 14 | 88 changes; OpenTelemetry `gen_ai.*` spans; virtual text in prompt box; agent transcript viewing |
| v2.1.310 | Oct 23 | Monitor tool on Bedrock/Vertex/Foundry; 26 fixes incl. compaction loops |
| v2.1.315 | Oct 30 | Fast-mode-on-Opus-4.8 deprecation begins; pooled group budgets |
| v2.1.316 | Oct 31 | ultrathink → xhigh effort; `CLAUDE_CODE_DISABLE_ULTRATHINK`; subagent effort controls |
| v2.1.317 | Nov 2 | Email-leak prevention; NTFS/exFAT tool-call fix |
| v2.1.322 | Nov 10 | Fast mode on Vertex (global/us/eu) |
| v2.1.330 | Nov 20 | Enterprise sign-in; Easel charting; VS Code workflow tools; 142 changes |
| v2.1.331 | Nov 23 | Code Mode GA on cloud platforms; `PreSkillShellCommand` hook; `claude doctor` connectivity section |
| v2.1.332 | Nov 24–25 | MCP server skills (beta); model routing updates; breaking changes; 93 fixes |

---

## 💡 Pro Tips

1. **Say "ultracode"** when you want Claude to orchestrate a multi-agent workflow for a substantive task — it's the explicit opt-in for Workflow-scale fan-out
2. **Migrate off Opus 4.8 fast mode before November 30** — after expiry, requests error with no fallback
3. **Use `/code-review ultra <PR#>`** for deep multi-agent cloud review of critical changes
4. **Audit third-party skills** with the `PreSkillShellCommand` hook before their inline shell commands run
5. **Rename any `computer-use` custom skill** before upgrading to v2.1.332 on a Mac

---

## 📚 Resources

- **Official Changelog**: https://code.claude.com/docs/en/changelog
- **What's New**: https://code.claude.com/docs/en/whats-new
- **Code Review GA announcement**: https://claude.com/resources/articles/code-review-is-now-generally-available
- **Release Notes**: https://support.claude.com/en/articles/12138966-release-notes
- **Community Discussion**: GitHub Discussions in akaash-nigam/ClaudeCodeFeatures

---

## Questions?

For feedback or questions about October–November 2026 features, open an issue in the [ClaudeCodeFeatures repository](https://github.com/akaash-nigam/ClaudeCodeFeatures).
