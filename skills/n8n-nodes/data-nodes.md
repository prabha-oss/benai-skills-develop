# Data & Communication Nodes

Nodes for storing data, databases, and sending messages.

## Contents
- [Auto-Create Tables](#auto-create-tables)
- [Google Sheets](#google-sheets)
- [Airtable](#airtable)
- [Notion](#notion)
- [Postgres](#postgres)
- [MySQL](#mysql)
- [Slack](#slack)
- [Gmail](#gmail)
- [Telegram](#telegram)
- [Discord](#discord)

---

## Auto-Create Tables

**Google Sheets and Airtable can create new tables/sheets if they don't exist.**

When the user requests a workflow that saves to a spreadsheet or table that doesn't exist yet:
1. Use the "create" operations first
2. Then proceed with append/update operations

---

## Google Sheets

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

## Airtable

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

## Notion

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

## Postgres

**Execute query:**
```json
{
  "id": "postgres-1",
  "name": "Postgres",
  "type": "n8n-nodes-base.postgres",
  "typeVersion": 2.6,
  "position": [650, 300],
  "parameters": {
    "operation": "executeQuery",
    "query": "SELECT * FROM users WHERE status = $1 LIMIT 10",
    "options": {
      "queryParameters": "active"
    }
  },
  "credentials": {
    "postgres": {
      "id": "cred-id",
      "name": "Postgres"
    }
  }
}
```

**Insert rows:**
```json
{
  "parameters": {
    "operation": "insert",
    "table": {
      "__rl": true,
      "mode": "list",
      "value": "users"
    },
    "columns": {
      "mappingMode": "autoMapInputData",
      "value": {}
    },
    "options": {}
  }
}
```

**Update rows:**
```json
{
  "parameters": {
    "operation": "update",
    "table": {
      "__rl": true,
      "mode": "list",
      "value": "users"
    },
    "columns": {
      "mappingMode": "defineBelow",
      "value": {
        "status": "={{ $json.status }}",
        "updated_at": "={{ $now.toISO() }}"
      },
      "matchingColumns": ["id"]
    }
  }
}
```

**Upsert (Insert or Update):**
```json
{
  "parameters": {
    "operation": "upsert",
    "table": {
      "__rl": true,
      "mode": "list",
      "value": "users"
    },
    "columns": {
      "mappingMode": "autoMapInputData",
      "value": {},
      "matchingColumns": ["email"]
    }
  }
}
```

**Operations:** `executeQuery`, `insert`, `update`, `upsert`, `select`, `deleteTable`

---

## MySQL

**Execute query:**
```json
{
  "id": "mysql-1",
  "name": "MySQL",
  "type": "n8n-nodes-base.mySql",
  "typeVersion": 2.5,
  "position": [650, 300],
  "parameters": {
    "operation": "executeQuery",
    "query": "SELECT * FROM products WHERE category = ? LIMIT 10",
    "options": {
      "queryParameters": "electronics"
    }
  },
  "credentials": {
    "mySql": {
      "id": "cred-id",
      "name": "MySQL"
    }
  }
}
```

**Insert rows:**
```json
{
  "parameters": {
    "operation": "insert",
    "table": {
      "__rl": true,
      "mode": "list",
      "value": "orders"
    },
    "columns": {
      "mappingMode": "autoMapInputData",
      "value": {}
    },
    "options": {}
  }
}
```

**Operations:** `executeQuery`, `insert`, `update`, `upsert`, `select`, `deleteTable`

---

## Slack

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

## Gmail

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

## Telegram

**Send message:**
```json
{
  "id": "telegram-1",
  "name": "Telegram",
  "type": "n8n-nodes-base.telegram",
  "typeVersion": 1.2,
  "position": [650, 300],
  "parameters": {
    "resource": "message",
    "operation": "sendMessage",
    "chatId": "={{ $json.chatId }}",
    "text": "={{ $json.message }}",
    "additionalFields": {}
  },
  "credentials": {
    "telegramApi": {
      "id": "cred-id",
      "name": "Telegram API"
    }
  }
}
```

**Send photo:**
```json
{
  "parameters": {
    "resource": "message",
    "operation": "sendPhoto",
    "chatId": "={{ $json.chatId }}",
    "file": "={{ $json.imageUrl }}",
    "additionalFields": {
      "caption": "={{ $json.caption }}"
    }
  }
}
```

**Send document:**
```json
{
  "parameters": {
    "resource": "message",
    "operation": "sendDocument",
    "chatId": "={{ $json.chatId }}",
    "file": "={{ $json.fileUrl }}",
    "additionalFields": {}
  }
}
```

**Resources:** `chat`, `callback`, `file`, `message`

**Message operations:** `sendMessage`, `sendPhoto`, `sendDocument`, `sendVideo`, `sendAudio`, `sendAnimation`, `sendSticker`, `sendLocation`, `sendMediaGroup`, `deleteMessage`, `pinChatMessage`, `unpinChatMessage`

---

## Discord

**Send message:**
```json
{
  "id": "discord-1",
  "name": "Discord",
  "type": "n8n-nodes-base.discord",
  "typeVersion": 2,
  "position": [650, 300],
  "parameters": {
    "authentication": "botToken",
    "resource": "message",
    "operation": "send",
    "guildId": {
      "__rl": true,
      "mode": "list",
      "value": "SERVER_ID"
    },
    "channelId": {
      "__rl": true,
      "mode": "list",
      "value": "CHANNEL_ID"
    },
    "content": "={{ $json.message }}"
  },
  "credentials": {
    "discordBotApi": {
      "id": "cred-id",
      "name": "Discord Bot"
    }
  }
}
```

**Send via webhook (no bot required):**
```json
{
  "parameters": {
    "authentication": "webhook",
    "content": "={{ $json.message }}",
    "options": {
      "username": "Notification Bot",
      "avatarUrl": "https://example.com/avatar.png"
    }
  },
  "credentials": {
    "discordWebhookApi": {
      "id": "cred-id",
      "name": "Discord Webhook"
    }
  }
}
```

**Connection types:**
- `botToken` - Bot Token (full API access)
- `oAuth2` - OAuth2 (user-level access)
- `webhook` - Webhook (simple message sending)

**Operations:** `send`, `get`, `getAll`, `deleteMessage`, `react`

---

## Quick Reference: Data Node typeVersions

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
