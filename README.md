# BenAI Skills

Expert automation skills for Claude Code.

## Installation

```bash
# Add marketplace
/plugin marketplace add naveedharri/benai-skills

# Install individual plugins
/plugin install n8n@benai-skills
/plugin install video@benai-skills
```

## Available Plugins

### n8n Automation

| Plugin | Command | Purpose |
|--------|---------|---------|
| n8n | `/n8n` | Complete n8n workflow automation |

**Features:**
- Build, test, and deploy workflows via REST API
- Node reference for 40+ common nodes
- JavaScript/Python Code node patterns
- Expression syntax and debugging
- Credential management via template

**Setup:** Create `.env` in your working directory:
```bash
N8N_API_URL=https://your-n8n.app.n8n.cloud
N8N_API_KEY=your-api-key
N8N_CREDENTIALS_TEMPLATE_URL=https://your-n8n.app.n8n.cloud/workflow/template-id
```

### Video Editing

| Plugin | Command | Purpose |
|--------|---------|---------|
| video | `/video` | Full video editing pipeline |

**Features:** Stitching, transitions, TikTok-style captions, teasers, transcription, title cards, graphics generation.

**Tools:** FFmpeg (CLI), Remotion (React-based rendering)

## Project Structure

```
benai-skills/
├── .claude-plugin/
│   └── marketplace.json
├── skills/
│   ├── n8n/
│   │   ├── SKILL.md
│   │   └── references/
│   └── video/
│       ├── SKILL.md
│       └── references/
├── CLAUDE.md
└── README.md
```

## Adding New Plugins

1. Create skill folder: `skills/<name>/SKILL.md`
2. Add plugin entry to `.claude-plugin/marketplace.json`:
   ```json
   {
     "name": "<name>",
     "source": "./skills/<name>",
     "description": "..."
   }
   ```

## License

MIT License
