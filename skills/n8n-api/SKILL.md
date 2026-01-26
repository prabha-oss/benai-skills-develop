---
name: n8n-api
description: Build and manage n8n workflows via REST API. Use when user says "create workflow", "build automation", "deploy to n8n", "activate workflow", "make a workflow", "set up n8n", "connect to n8n", or needs to list/update/delete/test workflows. Also use for webhook execution, checking executions, and debugging workflow runs.
---

# n8n API Skill

Build, test, and deploy n8n workflows via REST API with incremental testing.

---

## Critical Rules (Memorize These)

### 1. One Node at a Time
```
ADD ONE NODE → TEST → ADD ONE NODE → TEST → REPEAT
```
**NEVER add 2+ nodes without testing between them.**

### 2. Use Native Nodes First
| Priority | Use When |
|----------|----------|
| 1. Native node | Built-in exists (Slack, Sheets, AI Agent Node) |
| 2. HTTP Request | Native has issues OR no node exists |
| 3. Code node | Complex logic only |

### 3. No Mock Data
Never use placeholder URLs, fake IDs, or "REPLACE_ME" values. Ask user for real values.

### 4. Test with 10 Items
Always set `limit=10` or `maxResults=10` on data-fetching nodes.

### 5. Pin After Fetch
After external data fetch succeeds → PIN the data immediately for faster subsequent tests.

---

## API Methods Quick Reference

| Operation | Method | Endpoint |
|-----------|--------|----------|
| Create | POST | `/api/v1/workflows` |
| Update | **PUT** (not PATCH!) | `/api/v1/workflows/{id}` |
| Activate | **POST** | `/api/v1/workflows/{id}/activate` |
| Deactivate | **POST** | `/api/v1/workflows/{id}/deactivate` |
| Delete | DELETE | `/api/v1/workflows/{id}` |
| Execute | POST | `/webhook/{path}` (must be active) |

---

## Pre-Flight Checklist

Before any operation, check `.env` in working directory:

```
N8N_API_URL=https://your-n8n.app.n8n.cloud
N8N_API_KEY=your-api-key
N8N_CREDENTIALS_TEMPLATE_URL=https://your-n8n/workflow/template-id
```

If `.env` missing, create it automatically. If values empty, ask user.

---

## API Call Format

```bash
export $(cat .env | grep -v '^#' | xargs) && curl -s "${N8N_API_URL}/api/v1/ENDPOINT" -H "X-N8N-API-KEY: ${N8N_API_KEY}" | jq .
```

For POST/PUT:
```bash
export $(cat .env | grep -v '^#' | xargs) && curl -s -X POST "${N8N_API_URL}/api/v1/ENDPOINT" -H "X-N8N-API-KEY: ${N8N_API_KEY}" -H "Content-Type: application/json" -d 'JSON_DATA'
```

---

## Workflow JSON Structure

```json
{
  "name": "Workflow Name",
  "nodes": [
    {
      "id": "unique-node-id",
      "name": "Node Display Name",
      "type": "n8n-nodes-base.nodeName",
      "typeVersion": 1,
      "position": [250, 300],
      "parameters": {},
      "credentials": {}
    }
  ],
  "connections": {
    "Source Node Name": {
      "main": [[{"node": "Target Node Name", "type": "main", "index": 0}]]
    }
  },
  "settings": {"executionOrder": "v1"}
}
```

---

## Build Process Summary

1. Create workflow with trigger only → Test
2. Add ONE node → Test → Verify in runData
3. PIN data if external fetch
4. Repeat step 2-3 for each node
5. Report only after all nodes tested

**For detailed step-by-step process**: See [build-process.md](build-process.md)

---

## Reference Files

| File | Contents |
|------|----------|
| [api-reference.md](api-reference.md) | All API commands (CRUD, executions, tags, variables, source control) |
| [build-process.md](build-process.md) | Step-by-step build-test workflow, pinning data, verification |
| [pitfalls.md](pitfalls.md) | Common mistakes, error handling, debugging |

---

## Nodes Requiring Manual UI Config

| Node | Reason | Solution |
|------|--------|----------|
| Google Sheets | OAuth document picker | Ask for spreadsheet ID/URL or manual UI |
| Google Drive | OAuth file picker | Ask for file/folder ID or manual UI |
| Notion | Database picker | Ask for database ID or manual UI |
| Airtable | Base/Table picker | Ask for base and table IDs |

---

## Integration with Other Skills

- **n8n-credentials**: Get full node configs from template (credentials + parameters + typeVersion)
- **n8n-nodes**: Reference configurations for common nodes
- **n8n-expressions**: Expression syntax for dynamic values

---

## What to Report to User

**After successful build:**
```
✅ Workflow built and tested successfully!

Build Progress:
1. ✓ Webhook trigger - working
2. ✓ Scraper - working (10 results)
3. ✓ Google Sheets - working

- Workflow: My Workflow
- URL: https://n8n.example.com/workflow/abc123
- Status: Active
```

**If manual config needed:**
```
✅ Workflow built and partially tested!

⚠ Google Sheets requires manual setup:
→ Open workflow in n8n UI
→ Select your spreadsheet
→ Save
```
