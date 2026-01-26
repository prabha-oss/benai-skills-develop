---
name: n8n-nodes
description: Reference configurations for 20+ common n8n nodes. ALWAYS use when building workflows to get correct node JSON structure, typeVersion, and parameter examples. Use for Webhook, Schedule, AI Agent, OpenAI, Google Sheets, Airtable, Slack, Gmail, Notion, HTTP Request, Set, If, Switch, Merge, Code nodes and connection patterns.
---

# n8n Nodes Reference

Working configurations for the most commonly used n8n nodes. Copy these as your base when building workflows.

---

## Node Selection Priority

**ALWAYS prefer native nodes over HTTP Request or Code nodes.**

| Priority | Use When |
|----------|----------|
| 1. Native node | Built-in node exists for the service |
| 2. HTTP Request | Native node has known issues OR no node exists |
| 3. Code node | Complex logic that can't be done with built-in nodes |

---

## Quick Reference: typeVersion

Always use the correct typeVersion:

| Node | typeVersion | Node | typeVersion |
|------|-------------|------|-------------|
| Webhook | 2 | HTTP Request | 4.2 |
| Schedule Trigger | 1.2 | Set | 3.4 |
| AI Agent | 1.7 | If | 2.2 |
| OpenAI Chat Model | 1.2 | Switch | 3.2 |
| Google Sheets | 4.5 | Merge | 3 |
| Airtable | 2.1 | Code | 2 |
| Slack | 2.2 | Wait | 1.1 |
| Gmail | 2.1 | Split In Batches | 3 |
| Notion | 2.2 | Respond to Webhook | 1.1 |

---

## Auto-Create Tables

Google Sheets and Airtable can create new tables/sheets if they don't exist:
1. Use "create" operation first
2. Then proceed with append/update operations

See [data-nodes.md](data-nodes.md) for create configurations.

---

## Reference Files

| File | Contents |
|------|----------|
| [triggers.md](triggers.md) | Webhook, Schedule, Airtable, Gmail, Slack triggers |
| [ai-nodes.md](ai-nodes.md) | AI Agent, OpenAI Chat Model, Embeddings + connection patterns |
| [data-nodes.md](data-nodes.md) | Google Sheets, Airtable, Notion, Slack, Gmail (with create operations) |
| [transform-nodes.md](transform-nodes.md) | Set, If, Switch, Merge, Code, HTTP Request, Wait, Respond to Webhook |

---

## Basic Connection Pattern

```json
{
  "connections": {
    "Source Node Name": {
      "main": [[{ "node": "Target Node Name", "type": "main", "index": 0 }]]
    }
  }
}
```

**If Node (two branches):**
```json
{
  "connections": {
    "If": {
      "main": [
        [{ "node": "True Branch", "type": "main", "index": 0 }],
        [{ "node": "False Branch", "type": "main", "index": 0 }]
      ]
    }
  }
}
```

**AI Agent with Model:**
```json
{
  "connections": {
    "OpenAI Chat Model": {
      "ai_languageModel": [[{ "node": "AI Agent", "type": "ai_languageModel", "index": 0 }]]
    }
  }
}
```
