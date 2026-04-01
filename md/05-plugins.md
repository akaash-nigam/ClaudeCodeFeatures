# Plugins

> Introduced: v1.0.33 (April 2025) | Latest enhancements: v2.1.51

## What It Is

Plugins are distributable bundles that package skills, agents, hooks, MCP servers, and LSP configs into a single installable unit. A plugin is a directory with a `.claude-plugin/plugin.json` manifest. You can install plugins from marketplaces, load them from local directories, or create your own. Plugin skills are namespaced (`/plugin-name:skill-name`) to prevent conflicts.

## Why It Matters

Without plugins, you'd manually copy skills, hooks, and MCP configs between projects. Plugins let you:
- Share your team's coding standards as an installable package
- Install community tools (linters, formatters, language servers) in one step
- Bundle MCP servers with their configuration
- Version and distribute your automation

---

## Quick Start (60 Seconds)

```bash
# Create a minimal plugin
mkdir -p my-plugin/.claude-plugin
cat > my-plugin/.claude-plugin/plugin.json << 'EOF'
{
  "name": "my-plugin",
  "description": "My first Claude Code plugin",
  "version": "1.0.0"
}
EOF

# Add a skill
mkdir -p my-plugin/skills/hello
cat > my-plugin/skills/hello/SKILL.md << 'EOF'
---
description: Say hello
---
Greet the user warmly.
EOF

# Test it
claude --plugin-dir ./my-plugin

# Inside Claude Code
/my-plugin:hello
```

---

## Plugin Directory Structure

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json          # Manifest (required)
├── skills/                  # Skills (optional)
│   └── code-review/
│       └── SKILL.md
├── agents/                  # Custom subagents (optional)
│   └── security-reviewer.md
├── hooks/                   # Event hooks (optional)
│   └── hooks.json
├── .mcp.json                # MCP server configs (optional)
├── .lsp.json                # LSP server configs (optional)
├── settings.json            # Default settings (optional)
├── commands/                # Legacy commands (optional)
├── README.md
└── LICENSE
```

**Important:** Only `plugin.json` goes inside `.claude-plugin/`. Everything else is at the plugin root.

---

## Configuration

### plugin.json (Manifest)

```json
{
  "name": "my-plugin",
  "description": "What this plugin does",
  "version": "1.0.0",
  "author": {
    "name": "Your Name",
    "email": "you@example.com"
  },
  "homepage": "https://github.com/user/plugin",
  "repository": "https://github.com/user/plugin",
  "license": "MIT"
}
```

### CLI Flags

```bash
# Load plugin locally (development)
claude --plugin-dir ./my-plugin

# Load multiple plugins
claude --plugin-dir ./plugin-one --plugin-dir ./plugin-two
```

### Interactive Commands

```
/plugin install <name>       # Install from marketplace
/plugin uninstall <name>     # Remove plugin
/plugin list                 # List installed
/plugin enable <name>        # Enable
/plugin disable <name>       # Disable
/plugin update [name]        # Update
```

### Enable/Disable in settings.json

```json
{
  "enabledPlugins": {
    "swift-lsp@claude-plugins-official": true,
    "my-local-plugin": true,
    "inactive-plugin": false
  }
}
```

Format: `plugin-name@marketplace` or just `plugin-name` for local plugins.

### Marketplace Configuration

Add custom marketplaces:

```json
{
  "extraKnownMarketplaces": [
    "https://github.com/myorg/plugin-marketplace/raw/main/plugins.json"
  ]
}
```

Marketplace JSON format:

```json
{
  "owner": { "name": "Your Team" },
  "plugins": [
    {
      "name": "team-standards",
      "source": "https://github.com/team/standards-plugin",
      "description": "Team coding standards and review tools",
      "tags": ["code-review", "standards"]
    }
  ]
}
```

---

## What You Can Bundle

### Skills
```
skills/code-review/SKILL.md
```
Invoked as `/my-plugin:code-review` (namespaced).

### Custom Agents
```
agents/security-reviewer.md
```
Frontmatter: `name`, `description`, `model`, `permissions`, `tools`, `hooks`.

### Hooks (hooks/hooks.json)
```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [{ "type": "command", "command": "npm run lint:fix" }]
      }
    ]
  }
}
```

### MCP Servers (.mcp.json)
```json
{
  "plugin-api": {
    "type": "stdio",
    "command": "${CLAUDE_PLUGIN_ROOT}/bin/server",
    "args": ["--config", "${CLAUDE_PLUGIN_ROOT}/config.json"]
  }
}
```

Use `${CLAUDE_PLUGIN_ROOT}` for plugin-relative paths.

### LSP Servers (.lsp.json)
```json
{
  "go": {
    "command": "gopls",
    "args": ["serve"],
    "extensionToLanguage": { ".go": "go" }
  }
}
```

---

## Real-World Workflows

### Workflow 1: Team Standards Plugin

```bash
mkdir -p team-standards/.claude-plugin
cat > team-standards/.claude-plugin/plugin.json << 'EOF'
{"name": "team-standards", "description": "Engineering standards", "version": "1.0.0"}
EOF

mkdir -p team-standards/skills/review
cat > team-standards/skills/review/SKILL.md << 'EOF'
---
name: review
description: Review code against team standards
allowed-tools: Read, Grep
---
Check code against our standards:
- Functions < 20 lines
- No console.log in production code
- All async functions have error handling
- API responses use our standard format
EOF

# Everyone on the team installs
claude --plugin-dir ./team-standards
```

### Workflow 2: Full-Stack Plugin with MCP + Hooks

```
fullstack-plugin/
├── .claude-plugin/plugin.json
├── .mcp.json                    # Database connection
├── hooks/hooks.json             # Auto-format on save
├── skills/
│   ├── migrate/SKILL.md         # Database migrations
│   └── deploy/SKILL.md          # Deployment steps
└── agents/
    └── db-reviewer.md           # Database query reviewer
```

### Workflow 3: Publish to Marketplace

```bash
# 1. Create plugin repo
gh repo create my-plugin --public

# 2. Push plugin code
cd my-plugin && git init && git add . && git commit -m "Initial" && git push

# 3. Add to marketplace
# Edit marketplace plugins.json to include your plugin URL

# 4. Team installs
claude
> /plugin install my-plugin
```

---

## How It Interacts With Other Features

| Feature | Interaction |
|---------|-------------|
| **Skills** | Plugin skills are namespaced: `/plugin:skill` |
| **Hooks** | Plugins define hooks in `hooks/hooks.json` |
| **MCP** | Plugins can bundle MCP servers (auto-start on enable) |
| **Agent Teams** | Teammates inherit enabled plugins from lead |
| **Remote Control** | Plugins active in remote sessions (run locally) |
| **Worktrees** | Plugins discovered in worktree directories |
| **Settings** | Plugin `settings.json` applies when enabled (currently: `agent` key only) |

---

## Gotchas & Tips

1. **Skill namespacing** — plugin skills use `/plugin-name:skill-name`, not just `/skill-name`. The plugin name must match the manifest `name` field.

2. **`${CLAUDE_PLUGIN_ROOT}`** — use this for all paths in MCP configs, hooks, and agents. Absolute paths break when others install your plugin.

3. **Plugin settings are limited** — only the `agent` key is supported in plugin `settings.json` currently.

4. **Git timeout** — plugin installation clones from git. Increase timeout with `CLAUDE_CODE_PLUGIN_GIT_TIMEOUT_MS=120000` (default: 30s → now 120s in v2.1.51).

5. **Don't nest** — put skills, hooks, agents at the plugin root, NOT inside `.claude-plugin/`.

6. **Version pinning** — marketplaces can pin specific versions for stability (v2.1.51+).

---

## Version History

| Version | Date | Change |
|---------|------|--------|
| v1.0.33 | Apr 2025 | Plugin system introduced, marketplace integration |
| v2.0.x | Late 2025 | Plugin hooks and agent support |
| v2.1.0 | Jan 2026 | Plugin skills with SKILL.md frontmatter |
| v2.1.45 | Feb 2026 | `enabledPlugins` and `extraKnownMarketplaces` from CLI |
| v2.1.45 | Feb 2026 | Plugin agent skills loading by bare name |
| v2.1.51 | Feb 2026 | Custom npm registries, version pinning, git timeout 120s |
| v2.1.51 | Feb 2026 | Plugin `settings.json` for default configuration |
