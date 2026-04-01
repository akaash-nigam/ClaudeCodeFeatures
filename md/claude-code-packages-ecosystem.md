# Claude Code Package Ecosystem (Feb 2026)

*Companion to: claude-code-use-cases-comprehensive.md*
*9,000+ plugins across 43+ marketplaces; 8,600+ MCP servers tracked*

---

## 1. Top Plugins

### Tier 1: Must-Know

| Plugin | Stars | What It Does | Install |
|--------|-------|-------------|---------|
| **[Superpowers](https://github.com/obra/superpowers)** | ~42K | Enforces TDD (red-green-refactor), systematic 4-phase debugging, Socratic brainstorming, code review. 20+ battle-tested skills. Deletes code written before tests. | `/plugin marketplace add obra/superpowers-marketplace` then `/plugin install superpowers@superpowers-marketplace` |
| **[everything-claude-code](https://github.com/affaan-m/everything-claude-code)** | ~49K | Complete config collection: agents, skills, hooks, commands, rules, MCPs. Anthropic hackathon winner. | Clone and adopt configs |
| **[Claude-Mem](https://github.com/thedotmack/claude-mem)** | Popular | Long-term memory -- captures everything Claude does, compresses with AI, injects relevant context into future sessions. | `/plugin marketplace add thedotmack/claude-mem` then `/plugin install claude-mem` |
| **[Repomix](https://repomix.com/guide/claude-code-plugins)** | Popular | Packs your entire repo into a single AI-friendly file for analysis. | Via plugin marketplace |
| **[Taskmaster](https://github.com/eyaltoledano/claude-task-master)** | Popular | AI-powered task management; ~70% token reduction in Core mode. | Install during setup |
| **[Frontend Design](https://github.com/anthropics/claude-plugins-official)** | Official | Bold design choices, typography, animations, color palettes. Auto-invoked for frontend work. | `/plugin install frontend-design@claude-code-plugins` |

### Tier 2: Deep Trilogy (Pierce Lamb)

3-part workflow that turns vague ideas into working, tested code:

| Plugin | What It Does |
|--------|-------------|
| **[/deep-project](https://github.com/piercelamb/deep-plan)** | Transforms vague software ideas into individual, ready-to-be-planned components |
| **[/deep-plan](https://github.com/piercelamb/deep-plan)** | Transforms components into detailed implementation plans via research, interviews, multi-LLM review |
| **/deep-implement** | Implements code from /deep-plan sections with TDD, code review, and git workflow |

### Tier 3: Notable

| Plugin | What It Does |
|--------|-------------|
| **Hyperpowers** (withzombies/hyperpowers) | Fork of Superpowers with beads task tracking |
| **Gemini Tools** (paddo/claude-tools) | Integrates Gemini model capabilities into Claude Code |
| **Connect-Apps** (ComposioHQ) | Links Claude to 500+ SaaS apps (GitHub, Slack, Gmail, Notion, Jira). Handles auth automatically. |
| **Local-Review** (Composio) | Parallel local diff code reviews using multiple agents with confidence scoring |
| **Code Intelligence (LSP)** | Built-in Language Server Protocol for jump-to-definition, find-references, type errors |

---

## 2. MCP Servers

### Databases

| Server | Install Command |
|--------|----------------|
| **PostgreSQL** (Bytebase dbhub) | `claude mcp add db -- npx -y @bytebase/dbhub --dsn "postgresql://user:pass@localhost:5432/db"` |
| **Supabase** | `claude mcp add supabase --env SUPABASE_ACCESS_TOKEN=token -- npx -y @supabase/mcp-server` |
| **MongoDB** (Official) | `claude mcp add mongodb -- npx -y @mongodb-js/mongodb-mcp-server --connectionString "mongodb+srv://..."` |
| **Redis** (Official) | `claude mcp add redis -- npx -y @redis/mcp-server --url redis://localhost:6379` |
| **SQLite** | `claude mcp add sqlite -- npx -y @modelcontextprotocol/server-sqlite /path/to/db.sqlite` |
| **AnyDB** (universal) | `claude mcp add anydb -- npx -y anydb-mcp` |

### Code & Version Control

| Server | Install Command |
|--------|----------------|
| **GitHub** (Official) | `claude mcp add --transport http github https://api.githubcopilot.com/mcp/` |
| **Git** | `claude mcp add git -- npx -y @modelcontextprotocol/server-git` |
| **GitLab** | `claude mcp add gitlab -- npx -y @modelcontextprotocol/server-gitlab` |

### Project Management

| Server | Install Command |
|--------|----------------|
| **Jira/Confluence** (Atlassian) | `claude mcp add --transport sse atlassian https://mcp.atlassian.com/v1/sse` |
| **Linear** | `claude mcp add linear -- npx -y @linear/mcp-server` |
| **Asana** | `claude mcp add --transport sse asana https://mcp.asana.com/sse` |
| **Notion** (Official) | `claude mcp add --transport http notion https://mcp.notion.com/mcp` |

### Search & Documentation

| Server | Stars | Install Command |
|--------|-------|----------------|
| **Context7** (Upstash) | ~46K | `claude mcp add context7 -s user -- npx -y @upstash/context7-mcp` |
| **Brave Search** | Official | `claude mcp add brave-search --env BRAVE_API_KEY=key -- npx -y @modelcontextprotocol/server-brave-search` |
| **Perplexity** | Official | `claude mcp add perplexity --env PERPLEXITY_API_KEY=key -- npx -y @perplexity-ai/mcp-server` |
| **Fetch** (web content) | Official | `claude mcp add fetch -- npx -y @modelcontextprotocol/server-fetch` |
| **MCP Omnisearch** | Community | `claude mcp add omnisearch -- npx -y mcp-omnisearch` (Tavily, Brave, Kagi, Perplexity unified) |

### Browser Automation

| Server | Install Command |
|--------|----------------|
| **Playwright** (Microsoft) | `claude mcp add playwright -- npx -y @playwright/mcp@latest` |
| **Puppeteer** | `claude mcp add puppeteer -- npx -y @modelcontextprotocol/server-puppeteer` |
| **Browserbase** (cloud) | `claude mcp add browserbase -- npx -y @browserbasehq/mcp-server` |

### Communication

| Server | Install Command |
|--------|----------------|
| **Slack** | `claude mcp add slack -- npx -y @modelcontextprotocol/server-slack` (needs SLACK_BOT_TOKEN + SLACK_TEAM_ID) |

### Cloud & Infrastructure

| Server | Install Command |
|--------|----------------|
| **AWS** (45+ services) | `claude mcp add aws-core -- npx -y @awslabs/mcp-server-aws` |
| **Cloudflare** | `claude mcp add cloudflare -- npx -y @cloudflare/mcp-server-cloudflare` |
| **Terraform** (HashiCorp) | `claude mcp add --transport http terraform http://localhost:8080/mcp` |
| **Kubernetes** | `claude mcp add kubernetes -- npx -y kubernetes-mcp-server@latest` |
| **Docker** | `claude mcp add docker -- npx -y docker-mcp-server` |

### Payments & Commerce

| Server | Install Command |
|--------|----------------|
| **Stripe** (Official) | `claude mcp add --transport http stripe https://mcp.stripe.com` |
| **PayPal** (Official) | `claude mcp add --transport http paypal https://mcp.paypal.com/mcp` |
| **HubSpot** (CRM) | `claude mcp add --transport http hubspot https://mcp.hubspot.com/anthropic` |

### Design

| Server | Stars | Install Command |
|--------|-------|----------------|
| **Figma** (Official) | ~13K | `claude mcp add --transport http figma https://mcp.figma.com/mcp` |

### Monitoring

| Server | Install Command |
|--------|----------------|
| **Sentry** (Official) | `claude mcp add --transport http sentry https://mcp.sentry.dev/mcp` |

### Thinking & Reasoning

| Server | Install Command |
|--------|----------------|
| **Sequential Thinking** | `claude mcp add sequential-thinking -- npx -y @modelcontextprotocol/server-sequentialthinking` |
| **Memory** (knowledge graph) | `claude mcp add memory -- npx -y @modelcontextprotocol/server-memory` |

### Filesystem & Local

| Server | Install Command |
|--------|----------------|
| **Filesystem** | `claude mcp add filesystem -- npx -y @modelcontextprotocol/server-filesystem ~/Projects ~/Documents` |
| **Desktop Commander** | `claude mcp add desktop-commander -- npx -y @wonderwhy-er/desktop-commander` |

### Productivity

| Server | Install Command |
|--------|----------------|
| **Airtable** | `claude mcp add airtable --env AIRTABLE_API_KEY=key -- npx -y airtable-mcp-server` |
| **Google Maps** | `claude mcp add google-maps --env GOOGLE_MAPS_API_KEY=key -- npx -y @modelcontextprotocol/server-google-maps` |
| **Time** (timezone) | `claude mcp add time -- npx -y @modelcontextprotocol/server-time` |

### Key MCP Commands Reference

| Command | Description |
|---------|-------------|
| `claude mcp add <name> -- <command>` | Add a stdio server |
| `claude mcp add --transport http <name> <url>` | Add a remote HTTP server |
| `claude mcp add --scope user <name> ...` | Add globally across all projects |
| `claude mcp add --scope project <name> ...` | Add to shared `.mcp.json` for team |
| `claude mcp list` | List all configured servers |
| `claude mcp remove <name>` | Remove a server |
| `/mcp` (inside Claude Code) | Check status, authenticate OAuth servers |

---

## 3. Orchestration & Multi-Agent Frameworks

| Tool | Stars | What It Does | Install |
|------|-------|-------------|---------|
| **[claude-flow](https://github.com/ruvnet/claude-flow)** | 14K | Multi-agent swarms, RAG, 87 MCP tools, hive-mind intelligence. V2 Alpha. | `npm install -g claude-flow@alpha` |
| **[wshobson/agents](https://github.com/wshobson/agents)** | 29K | 72 plugins, 112 agents, 146 skills, 79 tools across 23 categories | Clone and configure |
| **[ccpm](https://github.com/automazeio/ccpm)** | 7K | Project management via GitHub Issues + git worktrees. `/pm:` commands. | Clone, use slash commands |
| **[oh-my-claudecode](https://github.com/Yeachan-Heo/oh-my-claudecode)** | 7K | 28 agents, 40+ skills, 31 hooks, 3-tier model routing (Haiku/Sonnet/Opus) | `npm install -g oh-my-claude-sisyphus` |
| **[claude-squad](https://github.com/smtg-ai/claude-squad)** | 6K | Manages multiple agents in tmux + git worktrees. Yolo mode. Works with Aider, Codex, Gemini too. | `brew install smtg-ai/tap/claude-squad` |
| **[ccswarm](https://github.com/nwiizo/ccswarm)** | 110 | Rust-native, specialized agent pools (Frontend/Backend/DevOps/QA), terminal UI | `cargo install ccswarm` |
| **[agentic-flow](https://github.com/ruvnet/agentic-flow)** | 440 | 66 agents, 213 MCP tools, 60-70% cost savings with intelligent LLM routing | Via npm |

---

## 4. GitHub Actions (Official Anthropic)

| Action | Stars | What It Does |
|--------|-------|-------------|
| **[claude-code-action](https://github.com/anthropics/claude-code-action)** | 5.8K | General-purpose: answer questions, implement code, review PRs on `@claude` mention |
| **[claude-code-security-review](https://github.com/anthropics/claude-code-security-review)** | 3K | OWASP Top 10 security scanning on code changes |
| **[claude-code-base-action](https://github.com/anthropics/claude-code-base-action)** | -- | Foundation for building custom Claude Code GitHub Actions |

---

## 5. SDKs & Programmatic Access

| Package | What It Does | Install |
|---------|-------------|---------|
| **@anthropic-ai/claude-code** | Official CLI | `npm install -g @anthropic-ai/claude-code` |
| **@anthropic-ai/claude-agent-sdk** | Build custom agents programmatically | `npm install @anthropic-ai/claude-agent-sdk` |
| **@botanicastudios/claude-code-sdk-ts** | Fluent TypeScript SDK with streaming, callbacks | `npm install @botanicastudios/claude-code-sdk-ts` |

---

## 6. Monitoring & Cost Tracking

| Tool | Stars | What It Does | Install |
|------|-------|-------------|---------|
| **[ccusage](https://github.com/ryoppippi/ccusage)** | 11K | Analyze usage by date/session/project from local JSONL. Monthly + 5-hour block reports. | `npm install -g ccusage` or `brew install ryoppippi/tap/ccusage` |
| **[Claude-Code-Usage-Monitor](https://github.com/Maciek-roboblog/Claude-Code-Usage-Monitor)** | 7K | Real-time CLI monitor with burn rate, projections, warnings, P90 calculator | Clone and run (Python) |
| **[SigNoz](https://github.com/SigNoz/signoz)** | 26K | Open-source observability (DataDog alternative) with dedicated Claude Code dashboard template | Docker/Helm or SigNoz Cloud |

---

## 7. Configuration & Setup Tools

| Tool | Stars | What It Does | Install |
|------|-------|-------------|---------|
| **[claude-code-templates](https://github.com/davila7/claude-code-templates)** | 21K | CLI for configuring agents, commands, MCPs. 100+ AI agents. Interactive web UI. | `npx claude-code-templates@latest` |
| **[claude-code-spec-workflow](https://github.com/Pimzino/claude-code-spec-workflow)** | 3.4K | Automated spec-driven dev (Requirements -> Design -> Tasks -> Code) | `npm install -g @pimzino/claude-code-spec-workflow` |
| **[Claude-Code-Development-Kit](https://github.com/peterkrueck/Claude-Code-Development-Kit)** | 1.3K | Context at scale: hooks, MCP servers, sub-agents for large projects | Clone and integrate |
| **[rulesync](https://github.com/dyoshikawa/rulesync)** | 800 | Sync configs across Claude Code, Cursor, Gemini CLI bidirectionally | `npm install -g rulesync` |
| **[claude-code-skill-factory](https://github.com/alirezarezvani/claude-code-skill-factory)** | 520 | Build and deploy production-ready skills, agents, commands at scale | Clone and use |
| **[ccexp](https://github.com/nyatinte/ccexp)** | 250 | Terminal UI for exploring Claude Code configs, memory files, subagent settings | `npx ccexp` |

---

## 8. Slash Command Collections

| Collection | Size | Link |
|-----------|------|------|
| **danielrosehill/Claude-Slash-Commands** | 357 commands | [GitHub](https://github.com/danielrosehill/Claude-Slash-Commands) |
| **qdhenry/Claude-Command-Suite** | 148 commands, 54 agents | [GitHub](https://github.com/qdhenry/Claude-Command-Suite) |
| **wshobson/commands** | 57 commands (15 workflows + 42 tools) | [GitHub](https://github.com/wshobson/commands) |
| **hikarubw/claude-commands** | Curated daily dev workflows | [GitHub](https://github.com/hikarubw/claude-commands) |
| **vincenthopf/My-Claude-Code** | Essential daily commands and workflows | [GitHub](https://github.com/vincenthopf/My-Claude-Code) |

---

## 9. Discovery Platforms

| Platform | Scale | URL |
|----------|-------|-----|
| **Anthropic Official Marketplace** | Curated | `/plugin` > Discover (inside Claude Code) |
| **[SkillHub](https://www.skillhub.club/)** | 7,000+ skills | skillhub.club |
| **[PulseMCP](https://www.pulsemcp.com/servers)** | 8,600+ MCP servers | pulsemcp.com |
| **[Build with Claude](https://www.buildwithclaude.com/)** | Growing | buildwithclaude.com |
| **[SkillsMP](https://skillsmp.com)** | Growing | skillsmp.com |
| **[claude-plugins.dev](https://claude-plugins.dev/)** | Community | claude-plugins.dev |
| **[Awesome Claude](https://awesomeclaude.ai/)** | Visual directory | awesomeclaude.ai |
| **[MCP Registry](https://registry.modelcontextprotocol.io/)** | Official | registry.modelcontextprotocol.io |
| **[mcp.so](https://mcp.so/)** | Community | mcp.so |
| **[awesome-mcp-servers](https://github.com/wong2/awesome-mcp-servers)** | Comprehensive | GitHub |

---

## 10. Awesome Lists (Meta-Directories)

| Repository | Stars | Focus |
|-----------|-------|-------|
| **[hesreallyhim/awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code)** | 25K | The definitive list: skills, hooks, commands, orchestrators, plugins |
| **[ccplugins/awesome-claude-code-plugins](https://github.com/ccplugins/awesome-claude-code-plugins)** | -- | Slash commands, subagents, MCP servers, hooks |
| **[ComposioHQ/awesome-claude-plugins](https://github.com/ComposioHQ/awesome-claude-plugins)** | -- | Plugins with custom commands, agents, hooks, MCPs |
| **[karanb192/awesome-claude-skills](https://github.com/karanb192/awesome-claude-skills)** | -- | 50+ verified skills for TDD, debugging, git, docs |
| **[wong2/awesome-mcp-servers](https://github.com/wong2/awesome-mcp-servers)** | -- | Comprehensive MCP server list (cross-platform) |

---

## 11. Recommended Quick-Start

### High-Impact MCP Servers (install these first)

```bash
# Live documentation for any library
claude mcp add context7 -s user -- npx -y @upstash/context7-mcp

# Structured problem-solving for architecture decisions
claude mcp add sequential-thinking -s user -- npx -y @modelcontextprotocol/server-sequentialthinking

# GitHub integration
claude mcp add github -s user -- npx -y @modelcontextprotocol/server-github

# Browser automation for testing
claude mcp add playwright -s user -- npx -y @playwright/mcp@latest

# File access control
claude mcp add filesystem -s user -- npx -y @modelcontextprotocol/server-filesystem ~/Projects ~/Documents ~/Desktop
```

### Top Plugin

```
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace
```

### Cost Monitoring

```bash
npm install -g ccusage
ccusage  # View your usage report
```

### Configuration Explorer

```bash
npx claude-code-templates@latest  # Interactive setup wizard
```

---

## 12. Top 15 by GitHub Stars

| Rank | Tool | Stars | Category |
|------|------|-------|----------|
| 1 | everything-claude-code | ~49K | Config collection |
| 2 | Context7 MCP | ~46K | Documentation MCP |
| 3 | Superpowers plugin | ~42K | TDD/debugging plugin |
| 4 | wshobson/agents | ~29K | Agent orchestration |
| 5 | SigNoz | ~26K | Observability |
| 6 | awesome-claude-code | ~25K | Awesome list |
| 7 | claude-code-templates | ~21K | Config/CLI |
| 8 | claude-flow | ~14K | Multi-agent swarms |
| 9 | Figma MCP | ~13K | Design integration |
| 10 | ccusage | ~11K | Cost tracking |
| 11 | ccpm | ~7K | Project management |
| 12 | oh-my-claudecode | ~7K | Multi-agent orchestration |
| 13 | Claude-Code-Usage-Monitor | ~7K | Cost monitoring |
| 14 | claude-squad | ~6K | Multi-agent terminal |
| 15 | claude-code-action | ~6K | GitHub Actions |
