# BenAI Skills - n8n Automation Expertise

## What This Plugin Does

This plugin provides expert-level n8n workflow automation capabilities through a set of specialized skills. It enables building, testing, and deploying production-ready n8n workflows via the REST API.

## Available Skills

### Core Operations

| Skill | Command | Purpose |
|-------|---------|---------|
| n8n-main | `/benai-skills:n8n-main` | All workflow CRUD operations via REST API |
| n8n-credentials | `/benai-skills:n8n-credentials` | Extract node configs from template workflows |
| n8n-expressions | `/benai-skills:n8n-expressions` | Expression syntax, patterns, and debugging |
| n8n-development | `/benai-skills:n8n-development` | Code nodes, workflow patterns, node configuration |

## Configuration

All skills require a `.env` file in your working directory:

```
N8N_API_URL=https://your-n8n-instance.com
N8N_API_KEY=your-api-key
N8N_CREDENTIALS_TEMPLATE_URL=https://your-n8n-instance.com/workflow/template-id
```

The skills will automatically create this file if missing and prompt for values.

## Build Philosophy

### Node Selection Priority

**ALWAYS prefer native n8n nodes over HTTP Request or Code nodes.**

| Priority | Use When |
|----------|----------|
| 1. Native node | A built-in n8n node exists for the service (Slack, Google Sheets, OpenAI, etc.) |
| 2. HTTP Request | Native node has known limitations or bugs, OR no native node exists |
| 3. Code node | Complex logic that can't be done with built-in nodes |

**Why native nodes?**
- Pre-built authentication handling
- Tested and maintained by n8n team
- Better error messages
- Simpler configuration
- Credentials template compatibility

**When HTTP Request is acceptable:**
- Native node has a known bug or missing feature
- API endpoint not supported by native node
- Custom API not covered by any node

### Never Mock Data

**CRITICAL: Never use placeholder, fake, or mock data when building workflows.**

- Use real API endpoints, not fake URLs
- Use real webhook paths that will actually be called
- Use real credential references from the template
- If you don't have real data, ask the user for it

**Wrong:**
```json
"url": "https://api.example.com/placeholder"
"documentId": "REPLACE_WITH_REAL_ID"
"apiKey": "your-api-key-here"
```

**Right:**
```json
"url": "https://api.openai.com/v1/chat/completions"
"documentId": {"__rl": true, "mode": "id", "value": "1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms"}
"credentials": {"openAiApi": {"id": "abc123", "name": "OpenAI Production"}}
```

### Incremental Build-Test Process (MANDATORY)

**THE #1 RULE: Add ONE node → Test entire workflow → Repeat**

```
❌ WRONG: Add Node A → Add Node B → Add Node C → Test → Error → Which node failed???

✅ RIGHT: Add Node A → Test ✓ → Add Node B → Test ✓ → Add Node C → Test ✓ → Done
```

**NEVER add two or more nodes at once. ALWAYS test after each single node.**

| Step | Action | Must Do Before Next Step |
|------|--------|--------------------------|
| 1 | Create workflow with trigger only | Test - verify trigger works |
| 2 | Add ONE node | Test - verify new node in runData |
| 3 | Add next ONE node | Test - verify new node in runData |
| 4 | Repeat step 3 | Test after EVERY node |
| 5 | Report success | Only after ALL nodes individually tested |

**Why this matters:**
- If you add 3 nodes and get an error, you don't know which one failed
- Testing after each node isolates problems immediately
- Faster debugging, guaranteed working workflows

### Test with 10 Real Data Items

**Never test with just 1 item. Always use at least 10 real data items.**

| Node Type | How to Set |
|-----------|------------|
| Scraper/Apify | `maxResults: 10` |
| HTTP Request | `?limit=10` in URL |
| Database | `LIMIT 10` in query |
| Search nodes | Set limit parameter to 10 |

This reveals array handling issues, performance problems, and edge cases that single-item testing misses.

### Pin Data After Fetching

**After a node successfully fetches external data, PIN the output immediately.**

```
Add Scraper → Test → SUCCESS → PIN DATA → Add Next Node → Test (uses pinned data - instant!)
```

**Why:** Avoids repeated API calls, saves cost, speeds up development, ensures consistent test data.

**Pin these nodes:** Scrapers, HTTP requests to external APIs, AI/LLM nodes, any slow/expensive operation.

### Single Workflow Rule

- Create ONE workflow (POST)
- Update incrementally (PUT)
- Never create new workflows for fixes
- Same workflow ID throughout build

### Template-Based Configuration

Always copy FULL node configurations from the credentials template:
- `type` - exact node type
- `typeVersion` - version from template
- `parameters` - all settings
- `credentials` - authentication

## Key API Patterns

### Correct Methods

| Operation | Method | Endpoint |
|-----------|--------|----------|
| Create | POST | `/api/v1/workflows` |
| Update | **PUT** | `/api/v1/workflows/{id}` |
| Activate | **POST** | `/api/v1/workflows/{id}/activate` |
| Execute | POST | `/webhook/{path}` |

### Common Mistakes to Avoid

- Using PATCH instead of PUT for updates
- Using PUT with `{active: true}` instead of `/activate` endpoint
- Trying to execute manual trigger workflows via API
- Building all nodes then testing (build incrementally!)
- Fetching all executions (always use `?limit=2`)

## Expression Essentials

### The Golden Rule

All dynamic content requires double curly braces: `{{ expression }}`

### Webhook Data Location

**Critical**: Webhook data lives under `.body`:
```
{{ $json.body.fieldName }}  ← Correct
{{ $json.fieldName }}       ← Wrong (won't work)
```

### Cross-Node References

```javascript
{{ $node["Node Name"].json.field }}
{{ $('Node Name').item.json.field }}
```

## Code Node Patterns

### JavaScript Return Format

Always return array of objects with `json` key:
```javascript
return [{ json: { result: "value" } }];
```

### Data Access

```javascript
// Get all items
const items = $input.all();

// Get first item
const first = $input.first();

// Webhook data
const body = $input.first().json.body;
```

## Workflow Patterns

### 1. Webhook Processing
Webhook → Process → Respond

### 2. Data Scraping
Trigger → Scrape → Transform → Store

### 3. AI Pipeline
Trigger → Fetch Data → AI Analysis → Output

### 4. Scheduled Sync
Schedule → Fetch Source → Transform → Update Target

## Testing Requirements

After EVERY node addition:

```bash
# 1. Activate
curl -X POST "${N8N_API_URL}/api/v1/workflows/{id}/activate"

# 2. Execute
curl -X POST "${N8N_API_URL}/webhook/{path}" -d '{}'

# 3. Check status
curl "${N8N_API_URL}/api/v1/executions?limit=1" | jq '.data[0].status'

# 4. Verify node ran
curl "${N8N_API_URL}/api/v1/executions/{id}?includeData=true" | jq '.data.resultData.runData | keys'
```

**Do NOT proceed until status = "success" and new node appears in runData.**

## Error Debugging

### WorkflowHasIssuesError
Node has incomplete configuration. Check required fields.

### Method Not Allowed
Wrong HTTP method. Use PUT for updates, POST for activate.

### Execution Errors
```bash
curl "${N8N_API_URL}/api/v1/executions/{id}?includeData=true" | jq '.data.resultData.error'
```

## Best Practices Summary

1. **Always test after each node** - No exceptions
2. **Copy full node configs from template** - Not just credentials
3. **Use correct API methods** - PUT for update, POST for activate
4. **Limit execution queries** - Always `?limit=2`
5. **Report only after confirmed working** - Never "please test this"
6. **Explain manual steps when required** - With clear reasoning

## MCP Server Integration

If the n8n MCP server is available, prefer using MCP tools for:
- Node discovery: `search_nodes`, `get_node`
- Validation: `validate_node`, `validate_workflow`
- Templates: `search_templates`, `get_template`

Fall back to REST API skills when MCP is unavailable or for operations MCP doesn't support.
