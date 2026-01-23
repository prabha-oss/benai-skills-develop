# BenAI Skills Plugin

A Claude Code plugin that enables seamless n8n workflow automation with three complementary skills.

## Features

- **n8n:mcp**: READ operations via n8n MCP tools (list, get, search, validate, execute)
- **n8n:api**: WRITE operations via REST API (create, update, delete, activate workflows)
- **n8n:credentials**: Credential management via template workflow

## Installation

### Option 1: Local Development/Testing

Load the plugin directly with the `--plugin-dir` flag:

```bash
claude --plugin-dir /path/to/benai-skills
```

### Option 2: Install from Directory

1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/benai-skills.git ~/.claude/plugins/benai-skills
   ```

2. The plugin will be automatically detected by Claude Code.

## Setup

The first time you use any skill, the plugin will automatically create a `.env` file in your current working directory and guide you through the setup process.

### Step 1: n8n API Configuration

Provide your n8n instance URL and API key:
- URL: Your n8n instance (e.g., `https://your-n8n.app.n8n.cloud`)
- API Key: Generated in n8n at Settings -> API -> Create API Key

These values are saved to `.env` in your current working directory.

### Step 2: n8n MCP Server Setup

Add the n8n MCP server to your Claude configuration:

**For Claude Desktop** (`~/Library/Application Support/Claude/claude_desktop_config.json`):
```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["-y", "@n8n/mcp-server"],
      "env": {
        "N8N_API_URL": "https://your-n8n.app.n8n.cloud",
        "N8N_API_KEY": "your-api-key"
      }
    }
  }
}
```

**For Claude Code** (`~/.claude/settings.json`):
```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["-y", "@n8n/mcp-server"],
      "env": {
        "N8N_API_URL": "https://your-n8n.app.n8n.cloud",
        "N8N_API_KEY": "your-api-key"
      }
    }
  }
}
```

After adding, restart Claude.

### Step 3: Credentials Template Workflow

Create a workflow in n8n that contains nodes with your configured credentials. This template is used to extract credential references for new workflows.

Example template structure:
```
[Slack Node] -> [Google Sheets Node] -> [OpenAI Node]
```

Each node should have working credentials configured. The workflow doesn't need to be active.

Provide the full workflow URL (copy from your browser when viewing the workflow).

## Configuration

All configuration is stored in `.env` in your project directory:

```bash
# BenAI n8n Skills Configuration
N8N_API_URL=https://your-n8n.app.n8n.cloud
N8N_API_KEY=your-api-key
N8N_MCP_CONFIGURED=true
N8N_CREDENTIALS_TEMPLATE_URL=https://your-n8n.app.n8n.cloud/workflow/your-template-id
```

## Usage

### n8n:mcp Skill

READ operations and workflow execution:

```
/benai-skills:n8n:mcp

# Examples:
"List all my workflows"
"Get details for workflow abc123"
"Search for Slack nodes"
"Validate my workflow"
"Execute the webhook workflow"
```

### n8n:api Skill

WRITE operations via REST API:

```
/benai-skills:n8n:api

# Examples:
"Create a new workflow that sends Slack messages"
"Update workflow abc123"
"Activate my workflow"
"Delete the test workflow"
```

### n8n:credentials Skill

Credential management:

```
/benai-skills:n8n:credentials

# Examples:
"What credentials are available?"
"Get Slack credentials for a new node"
"Create a workflow with proper credentials"
```

## Skills Overview

| Skill | Purpose | Required Setup |
|-------|---------|----------------|
| n8n:mcp | READ operations, execution | Steps 1 & 2 |
| n8n:api | WRITE operations | Step 1 |
| n8n:credentials | Credential management | All steps |

## Project Structure

```
benai-skills/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── n8n/
│       ├── api/
│       │   └── SKILL.md
│       ├── mcp/
│       │   └── SKILL.md
│       └── credentials/
│           └── SKILL.md
├── .gitignore
├── LICENSE
└── README.md
```

## License

MIT License - see [LICENSE](LICENSE) for details.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## Support

For issues and feature requests, please open an issue on GitHub.
