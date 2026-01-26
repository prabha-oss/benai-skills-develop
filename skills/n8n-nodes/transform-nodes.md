# Transform & Utility Nodes

Nodes for data transformation, logic, and workflow control.

## Contents
- [Set](#set)
- [If](#if)
- [Switch](#switch)
- [Merge](#merge)
- [Code](#code)
- [HTTP Request](#http-request)
- [Wait](#wait)
- [Split In Batches](#split-in-batches)
- [Respond to Webhook](#respond-to-webhook)
- [Connection Patterns](#connection-patterns)

---

## Set

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

## If

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

## Switch

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

## Merge

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

## Code

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

## HTTP Request

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

## Wait

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

## Split In Batches

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

## Respond to Webhook

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
