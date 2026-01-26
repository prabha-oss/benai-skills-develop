---
name: n8n-nodes
description: Reference configurations for 40+ common n8n nodes. ALWAYS use when building workflows to get correct node JSON structure, typeVersion, and parameter examples. Use for Webhook, Schedule, Form, Chat triggers, AI Agent, OpenAI, Anthropic, Google Sheets, Airtable, Postgres, MySQL, Slack, Gmail, Telegram, Discord, Notion, HTTP Request, Set, If, Switch, Filter, Sort, Merge, Code nodes and connection patterns.
---

# n8n Nodes Reference

Working configurations for the most commonly used n8n nodes. Copy these as your base when building workflows.

---

## Before Using Nodes (MANDATORY)

**You MUST read the appropriate reference file using the Read tool before adding any node:**

| Adding This Type | Read This File First |
|------------------|---------------------|
| Webhook, Schedule, Form, Chat triggers | `triggers.md` |
| AI Agent, OpenAI, Anthropic, Memory, Vector Store | `ai-nodes.md` |
| Google Sheets, Airtable, Postgres, Slack, Gmail, Telegram | `data-nodes.md` |
| Set, If, Switch, Filter, Code, HTTP Request, Merge, Loops | `transform-nodes.md` |

```
BEFORE ADDING NODE → READ the matching reference file → GET exact config → ADD node
```

**Do NOT guess node configurations. Always read the reference file first.**

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

### Triggers
| Node | typeVersion |
|------|-------------|
| Webhook | 2 |
| Schedule Trigger | 1.2 |
| Form Trigger | 2.2 |
| Chat Trigger | 1.1 |
| Airtable Trigger | 1 |
| Gmail Trigger | 1.2 |
| Slack Trigger | 1 |
| Telegram Trigger | 1.1 |
| Google Sheets Trigger | 1 |

### AI / LangChain
| Node | typeVersion |
|------|-------------|
| AI Agent | 3.1 |
| OpenAI Chat Model | 1.2 |
| Anthropic Chat Model | 1.3 |
| OpenAI Embeddings | 1.1 |
| Simple Memory | 1.3 |
| Simple Vector Store | 1.3 |

### Data & Communication
| Node | typeVersion |
|------|-------------|
| Google Sheets | 4.5 |
| Airtable | 2.1 |
| Notion | 2.2 |
| Postgres | 2.6 |
| MySQL | 2.5 |
| Slack | 2.2 |
| Gmail | 2.1 |
| Telegram | 1.2 |
| Discord | 2 |

### Transform & Utility
| Node | typeVersion |
|------|-------------|
| Set | 3.4 |
| If | 2.2 |
| Switch | 3.2 |
| Filter | 2.3 |
| Sort | 1 |
| Split Out | 1 |
| Merge | 3 |
| Code | 2 |
| HTTP Request | 4.4 |
| Wait | 1.1 |
| Split In Batches | 3 |
| Respond to Webhook | 1.1 |

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
| [triggers.md](triggers.md) | Webhook, Schedule, Form, Chat, Airtable, Gmail, Slack, Telegram, WhatsApp, HubSpot, Stripe, Shopify, Postgres, Google Sheets triggers |
| [ai-nodes.md](ai-nodes.md) | AI Agent, OpenAI/Anthropic Chat Models, Embeddings, Memory, Vector Store + connection patterns |
| [data-nodes.md](data-nodes.md) | Google Sheets, Airtable, Notion, Postgres, MySQL, Slack, Gmail, Telegram, Discord |
| [transform-nodes.md](transform-nodes.md) | Set, If, Switch, Filter, Sort, Split Out, Merge, Code, HTTP Request, Wait, Respond to Webhook, **Looping Patterns** |

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

**Split In Batches Loop (items loop back):**
```json
{
  "connections": {
    "Loop Over Items": {
      "main": [
        [],
        [{ "node": "Process Item", "type": "main", "index": 0 }]
      ]
    },
    "Process Item": {
      "main": [[{ "node": "Loop Over Items", "type": "main", "index": 0 }]]
    }
  }
}
```

See [transform-nodes.md](transform-nodes.md) for more looping patterns (pagination, retry, etc.).
