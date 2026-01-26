---
name: n8n-nodes
description: Reference configurations for 20+ common n8n nodes. Use when building workflows to get correct node structure, typeVersion, and real-world parameter examples.
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

## Triggers

### 1. Webhook

```json
{
  "id": "webhook-1",
  "name": "Webhook",
  "type": "n8n-nodes-base.webhook",
  "typeVersion": 2,
  "position": [250, 300],
  "parameters": {
    "path": "my-webhook-path",
    "httpMethod": "POST",
    "responseMode": "lastNode",
    "options": {}
  },
  "webhookId": "unique-webhook-id"
}
```

**Response modes:**
- `onReceived` - Respond immediately
- `lastNode` - Wait for workflow to complete
- `responseNode` - Wait for Respond to Webhook node

---

### 2. Schedule Trigger

```json
{
  "id": "schedule-1",
  "name": "Schedule Trigger",
  "type": "n8n-nodes-base.scheduleTrigger",
  "typeVersion": 1.2,
  "position": [250, 300],
  "parameters": {
    "rule": {
      "interval": [
        {
          "field": "hours",
          "hoursInterval": 1
        }
      ]
    }
  }
}
```

**Daily at specific time:**
```json
{
  "rule": {
    "interval": [
      {
        "field": "days",
        "triggerAtHour": 9
      }
    ]
  }
}
```

---

### 3. Airtable Trigger

```json
{
  "id": "airtable-trigger-1",
  "name": "Airtable Trigger",
  "type": "n8n-nodes-base.airtableTrigger",
  "typeVersion": 1,
  "position": [250, 300],
  "parameters": {
    "pollTimes": {
      "item": [
        {
          "mode": "everyMinute"
        }
      ]
    },
    "baseId": {
      "__rl": true,
      "mode": "id",
      "value": "appXXXXXXXXXXXXXX"
    },
    "tableId": {
      "__rl": true,
      "mode": "id",
      "value": "tblXXXXXXXXXXXXXX"
    }
  },
  "credentials": {
    "airtableTokenApi": {
      "id": "cred-id",
      "name": "Airtable Token"
    }
  }
}
```

---

### 4. Gmail Trigger

```json
{
  "id": "gmail-trigger-1",
  "name": "Gmail Trigger",
  "type": "n8n-nodes-base.gmailTrigger",
  "typeVersion": 1.2,
  "position": [250, 300],
  "parameters": {
    "pollTimes": {
      "item": [
        {
          "mode": "everyMinute"
        }
      ]
    },
    "filters": {
      "includeSpamTrash": false
    }
  },
  "credentials": {
    "gmailOAuth2": {
      "id": "cred-id",
      "name": "Gmail OAuth2"
    }
  }
}
```

---

### 5. Slack Trigger

```json
{
  "id": "slack-trigger-1",
  "name": "Slack Trigger",
  "type": "n8n-nodes-base.slackTrigger",
  "typeVersion": 1,
  "position": [250, 300],
  "parameters": {
    "trigger": "onMessage",
    "channelId": {
      "__rl": true,
      "mode": "id",
      "value": "C0XXXXXXXXX"
    }
  },
  "credentials": {
    "slackOAuth2Api": {
      "id": "cred-id",
      "name": "Slack OAuth2"
    }
  }
}
```

---

## AI Nodes

### 6. AI Agent

```json
{
  "id": "ai-agent-1",
  "name": "AI Agent",
  "type": "@n8n/n8n-nodes-langchain.agent",
  "typeVersion": 1.7,
  "position": [650, 300],
  "parameters": {
    "promptType": "define",
    "text": "={{ $json.body.message }}",
    "hasOutputParser": true,
    "options": {
      "systemMessage": "You are a helpful assistant. Answer questions concisely."
    }
  }
}
```

**With tools connected:**
The AI Agent requires a chat model connected via `ai_languageModel` input.

---

### 7. OpenAI Chat Model

```json
{
  "id": "openai-chat-1",
  "name": "OpenAI Chat Model",
  "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
  "typeVersion": 1.2,
  "position": [450, 500],
  "parameters": {
    "model": {
      "__rl": true,
      "mode": "list",
      "value": "gpt-4o",
      "cachedResultName": "gpt-4o"
    },
    "options": {
      "temperature": 0.7
    }
  },
  "credentials": {
    "openAiApi": {
      "id": "cred-id",
      "name": "OpenAI API"
    }
  }
}
```

**Models:** `gpt-4o`, `gpt-4o-mini`, `gpt-4-turbo`, `gpt-3.5-turbo`

---

### 8. OpenAI Embeddings

```json
{
  "id": "embeddings-1",
  "name": "Embeddings OpenAI",
  "type": "@n8n/n8n-nodes-langchain.embeddingsOpenAi",
  "typeVersion": 1.1,
  "position": [450, 500],
  "parameters": {
    "model": "text-embedding-3-small",
    "options": {}
  },
  "credentials": {
    "openAiApi": {
      "id": "cred-id",
      "name": "OpenAI API"
    }
  }
}
```

---

## Data Nodes

### Auto-Create Tables When Not Found

**Google Sheets and Airtable can create new tables/sheets if they don't exist.**

When the user requests a workflow that saves to a spreadsheet or table that doesn't exist yet:
1. Use the "create" operations first
2. Then proceed with append/update operations

---

### 9. Google Sheets

**Create new spreadsheet:**
```json
{
  "id": "sheets-create-1",
  "name": "Create Spreadsheet",
  "type": "n8n-nodes-base.googleSheets",
  "typeVersion": 4.5,
  "position": [450, 300],
  "parameters": {
    "operation": "create",
    "title": "={{ $json.spreadsheetName ?? 'New Spreadsheet' }}",
    "sheetName": "Sheet1",
    "options": {}
  },
  "credentials": {
    "googleSheetsOAuth2Api": {
      "id": "cred-id",
      "name": "Google Sheets OAuth2"
    }
  }
}
```

**Create new sheet (tab) in existing spreadsheet:**
```json
{
  "parameters": {
    "resource": "sheet",
    "operation": "create",
    "documentId": {
      "__rl": true,
      "mode": "id",
      "value": "existing-spreadsheet-id"
    },
    "title": "New Sheet Tab",
    "options": {}
  }
}
```

**Append rows:**
```json
{
  "id": "sheets-1",
  "name": "Google Sheets",
  "type": "n8n-nodes-base.googleSheets",
  "typeVersion": 4.5,
  "position": [850, 300],
  "parameters": {
    "operation": "append",
    "documentId": {
      "__rl": true,
      "mode": "id",
      "value": "1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms"
    },
    "sheetName": {
      "__rl": true,
      "mode": "name",
      "value": "Sheet1"
    },
    "columns": {
      "mappingMode": "autoMapInputData",
      "value": {}
    },
    "options": {}
  },
  "credentials": {
    "googleSheetsOAuth2Api": {
      "id": "cred-id",
      "name": "Google Sheets OAuth2"
    }
  }
}
```

**Update rows:**
```json
{
  "parameters": {
    "operation": "update",
    "documentId": {
      "__rl": true,
      "mode": "id",
      "value": "SPREADSHEET_ID"
    },
    "sheetName": {
      "__rl": true,
      "mode": "name",
      "value": "Sheet1"
    },
    "columns": {
      "mappingMode": "defineBelow",
      "value": {
        "id": "={{ $json.id }}",
        "status": "={{ $json.status }}"
      },
      "matchingColumns": ["id"]
    }
  }
}
```

---

### 10. Airtable

**Create new table:**
```json
{
  "id": "airtable-create-table-1",
  "name": "Create Airtable Table",
  "type": "n8n-nodes-base.airtable",
  "typeVersion": 2.1,
  "position": [450, 300],
  "parameters": {
    "resource": "table",
    "operation": "create",
    "baseId": {
      "__rl": true,
      "mode": "id",
      "value": "appXXXXXXXXXXXXXX"
    },
    "name": "={{ $json.tableName ?? 'New Table' }}",
    "fields": [
      {
        "name": "Name",
        "type": "singleLineText"
      },
      {
        "name": "Email",
        "type": "email"
      },
      {
        "name": "Status",
        "type": "singleSelect",
        "options": {
          "choices": [
            { "name": "Active" },
            { "name": "Inactive" }
          ]
        }
      }
    ]
  },
  "credentials": {
    "airtableTokenApi": {
      "id": "cred-id",
      "name": "Airtable Token"
    }
  }
}
```

**Airtable field types:** `singleLineText`, `multilineText`, `email`, `url`, `number`, `currency`, `percent`, `date`, `dateTime`, `checkbox`, `singleSelect`, `multipleSelects`, `attachment`

**Create record:**
```json
{
  "id": "airtable-1",
  "name": "Airtable",
  "type": "n8n-nodes-base.airtable",
  "typeVersion": 2.1,
  "position": [650, 300],
  "parameters": {
    "operation": "create",
    "baseId": {
      "__rl": true,
      "mode": "id",
      "value": "appXXXXXXXXXXXXXX"
    },
    "tableId": {
      "__rl": true,
      "mode": "id",
      "value": "tblXXXXXXXXXXXXXX"
    },
    "columns": {
      "mappingMode": "defineBelow",
      "value": {
        "Name": "={{ $json.name }}",
        "Email": "={{ $json.email }}",
        "Status": "Active"
      }
    },
    "options": {}
  },
  "credentials": {
    "airtableTokenApi": {
      "id": "cred-id",
      "name": "Airtable Token"
    }
  }
}
```

---

### 11. Notion

**Create page:**
```json
{
  "id": "notion-1",
  "name": "Notion",
  "type": "n8n-nodes-base.notion",
  "typeVersion": 2.2,
  "position": [650, 300],
  "parameters": {
    "resource": "page",
    "operation": "create",
    "databaseId": {
      "__rl": true,
      "mode": "id",
      "value": "database-id-here"
    },
    "propertiesUi": {
      "propertyValues": [
        {
          "key": "Name",
          "title": "={{ $json.title }}"
        },
        {
          "key": "Status",
          "select": "In Progress"
        }
      ]
    }
  },
  "credentials": {
    "notionApi": {
      "id": "cred-id",
      "name": "Notion API"
    }
  }
}
```

---

## Communication Nodes

### 12. Slack

**Send message:**
```json
{
  "id": "slack-1",
  "name": "Slack",
  "type": "n8n-nodes-base.slack",
  "typeVersion": 2.2,
  "position": [650, 300],
  "parameters": {
    "resource": "message",
    "operation": "post",
    "channel": {
      "__rl": true,
      "mode": "name",
      "value": "#general"
    },
    "text": "={{ $json.message }}",
    "otherOptions": {}
  },
  "credentials": {
    "slackApi": {
      "id": "cred-id",
      "name": "Slack API"
    }
  }
}
```

---

### 13. Gmail

**Send email:**
```json
{
  "id": "gmail-1",
  "name": "Gmail",
  "type": "n8n-nodes-base.gmail",
  "typeVersion": 2.1,
  "position": [650, 300],
  "parameters": {
    "operation": "send",
    "sendTo": "={{ $json.email }}",
    "subject": "={{ $json.subject }}",
    "message": "={{ $json.body }}",
    "options": {}
  },
  "credentials": {
    "gmailOAuth2": {
      "id": "cred-id",
      "name": "Gmail OAuth2"
    }
  }
}
```

**Send and wait for approval:**
```json
{
  "parameters": {
    "operation": "sendAndWait",
    "sendTo": "approver@example.com",
    "subject": "Approval Required: {{ $json.title }}",
    "message": "={{ $json.details }}",
    "approvalOptions": {
      "values": {
        "approvalType": "double"
      }
    },
    "options": {
      "limitWaitTime": {
        "values": {
          "resumeUnit": "minutes",
          "resumeAmount": 60
        }
      }
    }
  }
}
```

---

## Transform Nodes

### 14. Set

**Add/modify fields:**
```json
{
  "id": "set-1",
  "name": "Set",
  "type": "n8n-nodes-base.set",
  "typeVersion": 3.4,
  "position": [450, 300],
  "parameters": {
    "mode": "manual",
    "duplicateItem": false,
    "assignments": {
      "assignments": [
        {
          "id": "uuid-1",
          "name": "fullName",
          "value": "={{ $json.firstName }} {{ $json.lastName }}",
          "type": "string"
        },
        {
          "id": "uuid-2",
          "name": "processed",
          "value": true,
          "type": "boolean"
        }
      ]
    },
    "includeOtherFields": true,
    "options": {}
  }
}
```

---

### 15. If

**Conditional branching:**
```json
{
  "id": "if-1",
  "name": "If",
  "type": "n8n-nodes-base.if",
  "typeVersion": 2.2,
  "position": [450, 300],
  "parameters": {
    "conditions": {
      "options": {
        "caseSensitive": true,
        "leftValue": "",
        "typeValidation": "strict",
        "version": 2
      },
      "conditions": [
        {
          "id": "condition-1",
          "leftValue": "={{ $json.status }}",
          "rightValue": "active",
          "operator": {
            "type": "string",
            "operation": "equals"
          }
        }
      ],
      "combinator": "and"
    },
    "options": {}
  }
}
```

---

### 16. Switch

**Multiple branches:**
```json
{
  "id": "switch-1",
  "name": "Switch",
  "type": "n8n-nodes-base.switch",
  "typeVersion": 3.2,
  "position": [450, 300],
  "parameters": {
    "mode": "rules",
    "rules": {
      "values": [
        {
          "outputKey": "high",
          "conditions": {
            "options": { "version": 2, "caseSensitive": true, "typeValidation": "strict" },
            "conditions": [
              {
                "leftValue": "={{ $json.priority }}",
                "rightValue": "high",
                "operator": { "type": "string", "operation": "equals" }
              }
            ],
            "combinator": "and"
          },
          "renameOutput": true
        },
        {
          "outputKey": "low",
          "conditions": {
            "options": { "version": 2, "caseSensitive": true, "typeValidation": "strict" },
            "conditions": [
              {
                "leftValue": "={{ $json.priority }}",
                "rightValue": "low",
                "operator": { "type": "string", "operation": "equals" }
              }
            ],
            "combinator": "and"
          },
          "renameOutput": true
        }
      ]
    },
    "options": {}
  }
}
```

---

### 17. Merge

**Combine by position:**
```json
{
  "id": "merge-1",
  "name": "Merge",
  "type": "n8n-nodes-base.merge",
  "typeVersion": 3,
  "position": [650, 300],
  "parameters": {
    "mode": "combine",
    "combineBy": "combineByPosition",
    "options": {
      "includeUnpaired": true
    }
  }
}
```

**Choose branch:**
```json
{
  "parameters": {
    "mode": "chooseBranch",
    "numberInputs": 2
  }
}
```

---

### 18. Code

**JavaScript:**
```json
{
  "id": "code-1",
  "name": "Code",
  "type": "n8n-nodes-base.code",
  "typeVersion": 2,
  "position": [450, 300],
  "parameters": {
    "language": "javaScript",
    "mode": "runOnceForAllItems",
    "jsCode": "const results = [];\n\nfor (const item of $input.all()) {\n  results.push({\n    json: {\n      ...item.json,\n      processed: true,\n      timestamp: new Date().toISOString()\n    }\n  });\n}\n\nreturn results;"
  }
}
```

**Python:**
```json
{
  "parameters": {
    "language": "pythonNative",
    "mode": "runOnceForAllItems",
    "pythonCode": "results = []\n\nfor item in _input.all():\n    results.append({\n        \"json\": {\n            **item.json,\n            \"processed\": True\n        }\n    })\n\nreturn results"
  }
}
```

---

## Utility Nodes

### 19. HTTP Request

```json
{
  "id": "http-1",
  "name": "HTTP Request",
  "type": "n8n-nodes-base.httpRequest",
  "typeVersion": 4.2,
  "position": [450, 300],
  "parameters": {
    "method": "POST",
    "url": "https://api.example.com/endpoint",
    "authentication": "genericCredentialType",
    "genericAuthType": "httpHeaderAuth",
    "sendHeaders": true,
    "headerParameters": {
      "parameters": [
        {
          "name": "Content-Type",
          "value": "application/json"
        }
      ]
    },
    "sendBody": true,
    "specifyBody": "json",
    "jsonBody": "{\n  \"key\": \"{{ $json.value }}\"\n}",
    "options": {}
  },
  "credentials": {
    "httpHeaderAuth": {
      "id": "cred-id",
      "name": "API Key"
    }
  }
}
```

---

### 20. Wait

**Time interval:**
```json
{
  "id": "wait-1",
  "name": "Wait",
  "type": "n8n-nodes-base.wait",
  "typeVersion": 1.1,
  "position": [450, 300],
  "parameters": {
    "resume": "timeInterval",
    "amount": 5,
    "unit": "seconds"
  }
}
```

**Wait for webhook:**
```json
{
  "parameters": {
    "resume": "webhook",
    "responseData": "allEntries",
    "options": {}
  }
}
```

---

### 21. Split In Batches

```json
{
  "id": "batch-1",
  "name": "Split In Batches",
  "type": "n8n-nodes-base.splitInBatches",
  "typeVersion": 3,
  "position": [450, 300],
  "parameters": {
    "batchSize": 10,
    "options": {}
  }
}
```

---

### 22. Respond to Webhook

```json
{
  "id": "respond-1",
  "name": "Respond to Webhook",
  "type": "n8n-nodes-base.respondToWebhook",
  "typeVersion": 1.1,
  "position": [850, 300],
  "parameters": {
    "respondWith": "json",
    "responseBody": "={{ JSON.stringify({ success: true, data: $json }) }}",
    "options": {}
  }
}
```

---

## Connection Patterns

### Basic Linear Connection

```json
{
  "connections": {
    "Webhook": {
      "main": [[{ "node": "Set", "type": "main", "index": 0 }]]
    },
    "Set": {
      "main": [[{ "node": "Google Sheets", "type": "main", "index": 0 }]]
    }
  }
}
```

### If Node (Two Branches)

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

### AI Agent with Model

```json
{
  "connections": {
    "Webhook": {
      "main": [[{ "node": "AI Agent", "type": "main", "index": 0 }]]
    },
    "OpenAI Chat Model": {
      "ai_languageModel": [[{ "node": "AI Agent", "type": "ai_languageModel", "index": 0 }]]
    }
  }
}
```

---

## Quick Reference: typeVersion

Always use the correct typeVersion from this list:

| Node | typeVersion |
|------|-------------|
| Webhook | 2 |
| Schedule Trigger | 1.2 |
| AI Agent | 1.7 |
| OpenAI Chat Model | 1.2 |
| Google Sheets | 4.5 |
| Airtable | 2.1 |
| Slack | 2.2 |
| Gmail | 2.1 |
| Notion | 2.2 |
| HTTP Request | 4.2 |
| Set | 3.4 |
| If | 2.2 |
| Switch | 3.2 |
| Merge | 3 |
| Code | 2 |
| Wait | 1.1 |
| Split In Batches | 3 |
| Respond to Webhook | 1.1 |
