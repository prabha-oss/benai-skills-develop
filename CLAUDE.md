# BenAI Skills - n8n Automation Expertise

## What This Plugin Does

This plugin provides expert-level n8n workflow automation capabilities through a set of specialized skills. It enables building, testing, and deploying production-ready n8n workflows via the REST API.

## Available Skills

### Core Operations

| Skill | Command | Purpose |
|-------|---------|---------|
| n8n-api | `/benai-skills:n8n-api` | All workflow CRUD operations via REST API |
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

### Incremental Build-Test Process

**Never build entire workflows at once.** Follow this mandatory process:

1. Create workflow with trigger only → Test
2. Add ONE node → Test → Verify node ran
3. Add next node → Test → Verify
4. Repeat until complete
5. Report success only after all nodes tested

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
