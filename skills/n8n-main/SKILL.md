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
2. **Read `build-process.md`** - Step-by-step build and test process

```
BEFORE ANY WORK → READ pitfalls.md → READ build-process.md
```

**Do NOT proceed until you have read these files.**

---

## Critical Rules (Memorize These)

### 1. Fetch Database Schema First

**When workflow involves an existing database (Airtable, Google Sheets, Notion, etc.):**

1. Create a temp workflow with a trigger + schema fetch node
2. Execute it to get the actual field names
3. Use those exact field names when building the main workflow
4. Delete the temp workflow or reuse it

```
USER PROVIDES DATABASE → FETCH SCHEMA FIRST → USE EXACT FIELD NAMES
```

**Why:** Field names must match exactly (case-sensitive, space-sensitive). Never guess or ask user to create fields - work with what exists.

### 2. Load Node Config Just-In-Time

**Only load `n8n-nodes` skill when you're about to add THAT specific node:**

1. About to add Webhook? → Load n8n-nodes, read triggers.md
2. About to add Airtable? → Load n8n-nodes, read data-nodes.md
3. About to add AI Agent? → Load n8n-nodes, read ai-nodes.md

```
ABOUT TO ADD NODE → LOAD n8n-nodes SKILL → READ relevant .md file → ADD NODE
```

**On Error**: If any node throws an error, check n8n-nodes skill for correct configuration.

### 3. One Node at a Time

```
ADD NODE → TEST → ADD NEXT NODE → TEST → REPEAT
```

**NEVER add 2+ nodes without testing between them.**

### 4. Use Native Nodes First

| Priority | Use When |
|----------|----------|
| 1. Native node | Built-in exists (Slack, Sheets, AI Agent Node) |
| 2. HTTP Request | Native has issues OR no node exists |
| 3. Code node | Complex logic only |

### 5. No Mock Data

Never use placeholder URLs, fake IDs, or "REPLACE_ME" values. Ask user for real values.

### 6. Test with 2 Items

Always set `limit=2` or `maxResults=2` on data-fetching nodes for fast testing.

---

## Build Process (Follow Exactly)

### Step 0: Fetch Schema (If Database Involved)

If workflow writes to Airtable, Google Sheets, Notion, etc.:
```
1. Create temp workflow: Webhook + getSchema/getAll node
2. Execute to fetch actual field names
3. Store field names for use in main workflow
4. Delete temp workflow (or reuse as main workflow)
```

### Step 1: Create Workflow with Trigger
```
1. Load n8n-nodes skill → read triggers.md
2. Create workflow with trigger only
3. Test trigger
```

### Step 2: Add Each Node (Repeat for Every Node)
```
1. Load n8n-nodes skill → read relevant .md file for this node type
2. Add ONE node to workflow
3. Test workflow
4. If ERROR → check n8n-nodes skill → fix → retry
5. If SUCCESS → move to next node
```

### Step 3: Final Verification
```
1. All nodes added and tested
2. Workflow activated
3. Report success to user
```

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

### Handle Missing .env or Empty Values

1. **If `.env` doesn't exist**: Create it automatically with empty values
2. **If ANY value is empty**: Ask user for ALL configuration in a single prompt:

```
n8n Configuration Required

Please provide your n8n configuration:

1. n8n Instance URL
   Your n8n server address (e.g., https://your-n8n.app.n8n.cloud)

2. n8n API Key
   Found at: Settings -> API -> Create API Key

3. Credentials Template Workflow URL
   A workflow containing nodes with your configured credentials
   (e.g., https://your-n8n.app.n8n.cloud/workflow/abc123)
```

Update `.env` with all values using the Edit tool before proceeding.

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
  "settings": {"executionOrder": "v1"}
}
```

---

## Reference Files

| File | Contents |
|------|----------|
| [api-reference.md](api-reference.md) | All API commands (CRUD, executions, tags, variables, source control) |
| [build-process.md](build-process.md) | Step-by-step build-test workflow, verification |
| [pitfalls.md](pitfalls.md) | **CRITICAL**: Command format rules, common mistakes, debugging |

---

## Integration with Other Skills

| Skill | When to Use |
|-------|-------------|
| **n8n-nodes** | Load just-in-time when adding a specific node type. Read the relevant .md file (triggers.md, data-nodes.md, ai-nodes.md, transform-nodes.md) |
| **n8n-credentials** | Get credential configs from template workflow |
| **n8n-expressions** | Expression syntax for dynamic values (`{{ $json.field }}`) |

---

## Working with Existing Databases

When user provides a database ID (Airtable base, Google Sheet, Notion DB):

1. **Fetch schema first** - Get actual field names via API
2. **Use exact field names** - Case and space sensitive
3. **Work with what exists** - Don't ask user to create fields

| Database | How to Get Schema |
|----------|-------------------|
| Airtable | `getSchema` operation on base |
| Google Sheets | `getAll` first row or create and check headers |
| Notion | `getDatabase` to see properties |
| Postgres/MySQL | `executeQuery` with `DESCRIBE table` or `information_schema` |

---

## What to Report to User

**After successful build:**
```
✅ Workflow built and tested successfully!

Build Progress:
1. ✓ Webhook trigger - working
2. ✓ HTTP Request - working (2 results)
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
