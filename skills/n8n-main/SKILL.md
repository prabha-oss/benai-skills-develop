---
name: n8n-main
description: Build and manage n8n workflows via REST API. Use when user says "create workflow", "build automation", "deploy to n8n", "activate workflow", "make a workflow", "set up n8n", "connect to n8n", or needs to list/update/delete/test workflows. Also use for webhook execution, checking executions, and debugging workflow runs.
---

# n8n API Skill

Build, test, and deploy n8n workflows via REST API with incremental testing.

---

## IMMEDIATELY When Skill Loads (DO THIS NOW)

**As soon as this skill loads, DO THESE STEPS AUTOMATICALLY - don't wait for user input:**

### Step 1: Read Reference Files NOW
```
Use the Read tool IMMEDIATELY to read these files:
1. Read pitfalls.md (in this skill's directory)
2. Read build-process.md (in this skill's directory)
```

**DO NOT ask the user what they want to build. READ THE FILES FIRST.**

### Step 2: Check .env Configuration
```
Read the .env file in the working directory to verify:
- N8N_API_URL is set
- N8N_API_KEY is set
- N8N_CREDENTIALS_TEMPLATE_URL is set
```

If any values are missing, ask the user for ALL of them in a single prompt.

### Step 3: Create a Todo List

**After understanding the user's request, create a todo list using TaskCreate.** Break down the workflow into individual tasks:

```
Example todo list for "Scrape leads and save to Airtable":

1. [ ] Fetch Airtable schema to get field names
2. [ ] Create workflow with Webhook trigger → Test
3. [ ] Add Apify scraper node → Test
4. [ ] Add AI Agent node for lead scoring → Test
5. [ ] Add Airtable create node → Test
6. [ ] Final verification and cleanup
```

**Update task status as you work:**
- Mark task `in_progress` when starting
- Mark task `completed` when done and tested
- If blocked, create new task for the blocker

```
SKILL LOADS → READ FILES IMMEDIATELY → CHECK .env → THEN respond to user
```

**The user should NOT have to ask you to read the files. Do it automatically.**

---

## Critical Rules (Memorize These)

### 1. USE THE TOOLS THE USER SPECIFIES (CRITICAL - NEVER IGNORE OR DEFER)

**If the user mentions specific tools, nodes, or services - YOU MUST USE THEM. No exceptions. No deferring.**

```
❌ WRONG: User says "use Apify" → You use HTTP Request to scrape
❌ WRONG: User says "use FullEnrich" → You skip it citing "complexity"
❌ WRONG: User says "use FullEnrich" → You "defer it for later"
❌ WRONG: User says "use OpenAI" → You use Anthropic instead
❌ WRONG: Hit a technical issue → Give up and say "can be added later"

✅ RIGHT: User says "use Apify" → You use Apify node
✅ RIGHT: User says "use FullEnrich" → You add FullEnrich AND MAKE IT WORK
✅ RIGHT: User says "use OpenAI" → You use OpenAI Chat Model
✅ RIGHT: Hit a technical issue → Debug it, fix it, make it work
```

**Rules:**
- If user mentions a tool → IT MUST BE IN THE WORKFLOW
- If user doesn't specify → Use your best judgment
- If unsure about a tool → ASK the user, don't skip it
- NEVER substitute a different tool for what the user requested
- NEVER defer a user-requested tool "for later" - implement it NOW
- NEVER skip a tool citing "complexity" or "API issues" - work through it
- If you hit errors → Debug and fix, don't give up

**This is the #1 rule. Skipping, deferring, or making excuses about user-requested tools breaks trust.**

### 2. Only Use Nodes From Credentials Template (Unless User Requests)

**NEVER add nodes that require authentication unless:**
1. The node exists in the user's credentials template, OR
2. The user explicitly asks to use that specific tool/service

```
❌ WRONG: Add Apify node without checking if it's in credentials template
❌ WRONG: Add FullEnrich node because you think it would be useful
❌ WRONG: Add any 3rd party auth node without user explicitly requesting it

✅ RIGHT: Check credentials template first → Only use nodes that are configured
✅ RIGHT: User says "use Apify" → Check template → If missing, ask user to add it
✅ RIGHT: Need a tool not in template? → Ask user if they want to add it
```

**Before using ANY node that requires authentication:**
1. Load `n8n-credentials` skill
2. Fetch the credentials template
3. Check if the node type exists in the template
4. If NOT in template AND user didn't request it → DON'T USE IT
5. If NOT in template AND user requested it → Ask user to add it to template first

**Why:** Nodes without configured credentials will fail. Don't waste time building workflows with unconfigured nodes.

### 3. Node Discovery Flow

**When you need to add a node, follow this sequence:**

```
1. LOAD n8n-nodes skill
2. CHECK if node is documented (triggers.md, data-nodes.md, ai-nodes.md, transform-nodes.md)
3. LIST available operations for that node
4. If DATABASE node → FETCH SCHEMA first to get field names
5. USE the appropriate operation with correct config
```

**Example - Adding Airtable node:**
```
1. Load n8n-nodes skill → Read data-nodes.md
2. Find Airtable section → See operations: create, delete, get, search, update, upsert, getSchema
3. Need to write data? → First use getSchema to get field names
4. Then use create/update with exact field names from schema
```

### 4. Fetch Database Schema First

**When workflow involves an existing database (Airtable, Google Sheets, Notion, etc.):**

1. Add a schema fetch node to get actual field names
2. Execute to see exact field names (case-sensitive, space-sensitive)
3. Use those exact field names when writing data
4. Work with existing fields - don't ask user to create new ones

```
USER PROVIDES DATABASE → FETCH SCHEMA → USE EXACT FIELD NAMES
```

| Database | Schema Operation |
|----------|------------------|
| Airtable | `getSchema` on base resource |
| Google Sheets | `getAll` first row to see headers |
| Notion | `getDatabase` to see properties |
| Postgres/MySQL | `executeQuery` with `DESCRIBE table` |

### 5. One Node at a Time

```
ADD NODE → TEST → ADD NEXT NODE → TEST → REPEAT
```

**NEVER add 2+ nodes without testing between them.**

### 6. Use Native Nodes First

| Priority | Use When |
|----------|----------|
| 1. Native node | Built-in exists (Slack, Sheets, etc.) |
| 2. **AI Agent node** | For ANY AI/LLM task (prefer over HTTP Request to OpenAI/Anthropic) |
| 3. HTTP Request | Native has issues OR no node exists AND not an AI task |
| 4. Code node | Complex logic only |

**For AI tasks: ALWAYS use AI Agent node + Chat Model, NOT HTTP Request to OpenAI API.**

### 7. No Mock Data

Never use placeholder URLs, fake IDs, or "REPLACE_ME" values. Ask user for real values.

### 8. Test with 2 Items

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
