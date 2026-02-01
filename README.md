# BenAI Skills

Expert automation skills for Claude Code.

## Installation

```bash
# Add marketplace
/plugin marketplace add naveedharri/benai-skills

# Install
/plugin install benai-skills
```

Or for local development:
```bash
claude --plugin-dir /path/to/benai-skills
```

## Available Skills

### n8n Automation

| Skill | Command | Purpose |
|-------|---------|---------|
| n8n | `/benai-skills:n8n` | Complete n8n workflow automation |

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

| Skill | Command | Purpose |
|-------|---------|---------|
| video | `/benai-skills:video` | Full video editing pipeline |

**Features:** Stitching, transitions, TikTok-style captions, teasers, transcription, title cards, graphics generation.

**Tools:** FFmpeg (CLI), Remotion (React-based rendering)

## Project Structure

```
benai-skills/
├── .claude-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── skills/
│   ├── n8n/
│   │   ├── SKILL.md
│   │   ├── scripts/
│   │   ├── references/
│   │   └── assets/
│   └── video/
│       ├── SKILL.md
│       ├── scripts/
│       ├── references/
│       └── assets/
├── CLAUDE.md
└── README.md
```

## Adding New Skills

Following the [Agent Skills Specification](https://agentskills.io/specification):

1. Create folder: `skills/<skill-name>/`
2. Add `SKILL.md` with frontmatter and instructions
3. Optional: Add `scripts/`, `references/`, `assets/` folders

## License

MIT License
