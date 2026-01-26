# Trigger Nodes

Starting points for workflow execution.

## Contents
- [Webhook](#webhook)
- [Schedule Trigger](#schedule-trigger)
- [Airtable Trigger](#airtable-trigger)
- [Gmail Trigger](#gmail-trigger)
- [Slack Trigger](#slack-trigger)

---

## Webhook

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

## Schedule Trigger

**Every hour:**
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

## Airtable Trigger

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

## Gmail Trigger

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

## Slack Trigger

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
