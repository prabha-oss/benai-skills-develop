---
name: n8n-main
description: Build and manage n8n workflows via REST API. Use when user says "create workflow", "build automation", "deploy to n8n", "activate workflow", "make a workflow", "set up n8n", "connect to n8n", or needs to list/update/delete/test workflows. Also use for webhook execution, checking executions, and debugging workflow runs.
---

# n8n API Skill

Build, test, and deploy n8n workflows via REST API with incremental testing.

---

## Before Starting (MANDATORY)

**You MUST read these files using the Read tool before building any workflow:**

1. **Read `pitfalls.md`** - Command format rules, common mistakes (CRITICAL)
2. **Read `build-process.md`** - Step-by-step build and pin process
3. **Load `n8n-nodes` skill** - Get correct node configurations
4. **Load `n8n-credentials` skill** - Get credentials from template

```
BEFORE ANY WORK → READ pitfalls.md → READ build-process.md → LOAD n8n-nodes skill
```

**Do NOT proceed until you have read these files.**

---

## Critical Rules (Memorize These)

### 1. ALWAYS Load n8n-nodes Skill First

**MANDATORY**: Before adding ANY node to a workflow:
1. Load the `n8n-nodes` skill to get correct node configuration
2. Use the exact `typeVersion`, `parameters`, and structure from the reference
3. If a node fails, reload `n8n-nodes` skill and check the configuration

```
BEFORE ADDING NODE → LOAD n8n-nodes SKILL → GET CONFIG → ADD NODE
```

**On Error**: If any node throws an error, ALWAYS check `n8n-nodes` skill for correct configuration before retrying.

### 2. One Node at a Time + PIN After Each

```
ADD NODE → TEST → PIN RESPONSE → ADD NEXT NODE → TEST → PIN → REPEAT
```

**NEVER add 2+ nodes without testing and pinning between them.**

### 3. PIN Everything for Speed

**After EVERY successful node test, PIN the response data immediately:**

```bash
# After test succeeds, update workflow with pinned data
curl -X PUT "${N8N_API_URL}/api/v1/workflows/{id}" \
  -H "X-N8N-API-KEY: ${N8N_API_KEY}" \
  -H "Content-Type: application/json" \
  -d '{
    "nodes": [...],
    "pinData": {
      "Node Name": [{"json": {...execution result...}}]
    }
  }'
```

**Why PIN?**
- Pinned data is used instead of executing the node again
- No external API calls on subsequent tests = FAST development
- Each node only calls external APIs once, then uses pinned data

### 4. Use Native Nodes First

| Priority | Use When |
|----------|----------|
| 1. Native node | Built-in exists (Slack, Sheets, AI Agent Node) |
| 2. HTTP Request | Native has issues OR no node exists |
| 3. Code node | Complex logic only |

### 5. No Mock Data

Never use placeholder URLs, fake IDs, or "REPLACE_ME" values. Ask user for real values.

### 6. Test with 10 Items

Always set `limit=10` or `maxResults=10` on data-fetching nodes.

---

## Build Process (Follow Exactly)

### Step 1: Load n8n-nodes Skill
Before starting, load the `n8n-nodes` skill to have all node configurations available.

### Step 2: Create Workflow with Trigger
```
1. Get trigger config from n8n-nodes skill
2. Create workflow with trigger only
3. Test trigger
4. PIN trigger response
```

### Step 3: Add Each Node (Repeat for Every Node)
```
1. Load n8n-nodes skill → get node config
2. Add ONE node to workflow
3. Test workflow
4. If ERROR → check n8n-nodes skill → fix → retry
5. If SUCCESS → PIN the response immediately
6. Move to next node
```

### Step 4: Final Verification
```
1. All nodes added and tested
2. All responses pinned
3. Workflow activated
4. Report success to user
```

---

## Pinning Data Format

When updating workflow with pinned data:

```json
{
  "name": "Workflow Name",
  "nodes": [...],
  "connections": {...},
  "pinData": {
    "Webhook": [
      {
        "json": {
          "body": {"message": "test"},
          "headers": {...}
        }
      }
    ],
    "HTTP Request": [
      {"json": {"result": "data1"}},
      {"json": {"result": "data2"}}
    ]
  }
}
```

**Rules:**
- `pinData` keys are node NAMES (not IDs)
- Value is an array of items (even for single item)
- Each item has `json` property with the data

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

## API Call Format (MUST Follow Exactly)

**CRITICAL RULES:**
1. **NEVER write JSON files to disk** - Always use API directly
2. **NEVER use `\` line continuations** - Causes "blank argument" errors
3. **NEVER use `source .env`** - Use `export $(cat .env | grep -v '^#' | xargs)` instead
4. **Always single-line commands** - Or heredoc for large JSON

**GET:**
```bash
export $(cat .env | grep -v '^#' | xargs) && curl -s "${N8N_API_URL}/api/v1/ENDPOINT" -H "X-N8N-API-KEY: ${N8N_API_KEY}" | jq .
```

**POST/PUT (small JSON):**
```bash
export $(cat .env | grep -v '^#' | xargs) && curl -s -X POST "${N8N_API_URL}/api/v1/ENDPOINT" -H "X-N8N-API-KEY: ${N8N_API_KEY}" -H "Content-Type: application/json" -d '{"key": "value"}'
```

**POST/PUT (large JSON - use heredoc):**
```bash
export $(cat .env | grep -v '^#' | xargs) && curl -s -X POST "${N8N_API_URL}/api/v1/workflows" -H "X-N8N-API-KEY: ${N8N_API_KEY}" -H "Content-Type: application/json" -d "$(cat <<'EOF'
{
  "name": "My Workflow",
  "nodes": [...],
  "connections": {},
  "settings": {"executionOrder": "v1"}
}
EOF
)"
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
  "pinData": {},
  "settings": {"executionOrder": "v1"}
}
```

---

## Reference Files

| File | Contents |
|------|----------|
| [api-reference.md](api-reference.md) | All API commands (CRUD, executions, tags, variables, source control) |
| [build-process.md](build-process.md) | Step-by-step build-test workflow, pinning data, verification |
| [pitfalls.md](pitfalls.md) | **CRITICAL**: Command format rules, common mistakes, debugging |

---

## Integration with Other Skills

| Skill | When to Use |
|-------|-------------|
| **n8n-nodes** | **ALWAYS** load before adding any node. Contains correct typeVersions, parameters, and structures for 40+ nodes |
| **n8n-credentials** | Get full node configs from template (credentials + parameters) |
| **n8n-expressions** | Expression syntax for dynamic values (`{{ $json.field }}`) |

---

## Nodes Requiring Manual UI Config

| Node | Reason | Solution |
|------|--------|----------|
| Google Sheets | OAuth document picker | Ask for spreadsheet ID/URL or manual UI |
| Google Drive | OAuth file picker | Ask for file/folder ID or manual UI |
| Notion | Database picker | Ask for database ID or manual UI |
| Airtable | Base/Table picker | Ask for base and table IDs |

---

## What to Report to User

**After successful build:**
```
✅ Workflow built and tested successfully!

Build Progress:
1. ✓ Webhook trigger - working (pinned)
2. ✓ HTTP Request - working (pinned, 10 results)
3. ✓ Google Sheets - working (pinned)

- Workflow: My Workflow
- URL: https://n8n.example.com/workflow/abc123
- Status: Active
- All data pinned for fast re-testing
```

**If manual config needed:**
```
✅ Workflow built and partially tested!

⚠ Google Sheets requires manual setup:
→ Open workflow in n8n UI
→ Select your spreadsheet
→ Save
```
