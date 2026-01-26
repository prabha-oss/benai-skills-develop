# Common Pitfalls

Mistakes to avoid and how to debug errors.

## Contents
- [Critical Mistakes](#critical-mistakes)
- [API Mistakes](#api-mistakes)
- [Build Process Mistakes](#build-process-mistakes)
- [Error Handling](#error-handling)
- [Debugging](#debugging)

---

## Critical Mistakes

### Using HTTP Request When Native Node Exists

❌ **Wrong**: Using HTTP Request to call Slack API when `n8n-nodes-base.slack` exists

✅ **Right**: Use native Slack node with credentials from template

**Exception**: Native node has known bug or missing feature

### Using Mock/Placeholder Data

❌ **Wrong**:
```json
"url": "https://api.example.com/placeholder"
"documentId": "REPLACE_ME"
"apiKey": "your-api-key-here"
```

✅ **Right**: Use real URLs, real IDs, real credential references from template

**If missing**: Ask user for real values, don't guess or mock

### Adding Multiple Nodes Before Testing

❌ **Wrong**: Add Node A → Add Node B → Add Node C → Test → Error (which failed?)

✅ **Right**: Add ONE node → Test → Add ONE node → Test → Repeat

---

## API Mistakes

### Using PATCH Instead of PUT

❌ **Wrong**: `curl -X PATCH /api/v1/workflows/{id}`

✅ **Right**: `curl -X PUT /api/v1/workflows/{id}`

### Trying to Activate with PUT

❌ **Wrong**: `curl -X PUT /api/v1/workflows/{id} -d '{"active": true}'`

✅ **Right**: `curl -X POST /api/v1/workflows/{id}/activate`

### Trying to Execute Manual Trigger via API

❌ **Wrong**: Expecting `POST /api/v1/workflows/{id}/run` to exist

✅ **Right**: Add webhook trigger, activate workflow, call webhook URL

### Executing Webhook Before Activating

❌ **Wrong**: `POST /webhook/path` on inactive workflow

✅ **Right**: First activate, then call webhook

### Fetching All Executions

❌ **Wrong**: `GET /api/v1/executions` (fetches everything)

✅ **Right**: `GET /api/v1/executions?limit=2` (only recent)

---

## Build Process Mistakes

### Telling User to Test Instead of Testing Yourself

❌ **Wrong**: "Workflow created! Please test it."

✅ **Right**: Test it yourself, debug failures, report only after confirmed working

### Reporting Success Without Testing

❌ **Wrong**: "Workflow is ready to use!" (without executing)

✅ **Right**: Execute workflow, verify status=success, then report

### Not Verifying Each Node Executed

❌ **Wrong**: Check only final status, assume all nodes ran

✅ **Right**: Check `runData | keys` to verify each node

### Creating New Workflows Instead of Updating

❌ **Wrong**: Create new workflow each time you add a node

✅ **Right**: Create ONE workflow, use PUT to update incrementally

### Leaving Google Sheets documentId Empty

❌ **Wrong**: Creating workflow with empty `documentId.value` and executing

✅ **Right**: Get spreadsheet ID from user, or warn about manual UI config

---

## Error Handling

### Common API Errors

| Status | Meaning | Solution |
|--------|---------|----------|
| 401 | Unauthorized | Check API key is valid |
| 404 | Not found | Check workflow/execution ID exists |
| 400 | Bad request | Validate JSON structure |
| 409 | Conflict | Workflow name may be duplicate |
| "method not allowed" | Wrong HTTP method | Use PUT for updates, POST for activate |

### WorkflowHasIssuesError

If execution fails with `WorkflowHasIssuesError`:

1. Check for nodes with incomplete configuration (empty required fields)
2. Common cause: Google Sheets without documentId selected
3. User must open workflow in n8n UI to complete configuration

### Google Sheets Configuration

**Placeholder (will cause error if executed):**
```json
{
  "documentId": {"__rl": true, "mode": "list", "value": ""},
  "sheetName": {"__rl": true, "mode": "list", "value": ""}
}
```

**If user provides spreadsheet URL:**
```json
{
  "documentId": {"__rl": true, "mode": "id", "value": "SPREADSHEET_ID_FROM_URL"},
  "sheetName": {"__rl": true, "mode": "name", "value": "Sheet1"}
}
```

---

## Debugging

### List Recent Executions (limit to 2)

```bash
export $(cat .env | grep -v '^#' | xargs) && curl -s "${N8N_API_URL}/api/v1/executions?limit=2" -H "X-N8N-API-KEY: ${N8N_API_KEY}" | jq '.data[] | {id, status, startedAt, workflowId}'
```

### Get Error Details

```bash
export $(cat .env | grep -v '^#' | xargs) && curl -s "${N8N_API_URL}/api/v1/executions/{EXECUTION_ID}?includeData=true" -H "X-N8N-API-KEY: ${N8N_API_KEY}" | jq '.data.resultData.error'
```

### Check Which Nodes Ran

```bash
export $(cat .env | grep -v '^#' | xargs) && curl -s "${N8N_API_URL}/api/v1/executions/{EXECUTION_ID}?includeData=true" -H "X-N8N-API-KEY: ${N8N_API_KEY}" | jq '.data.resultData.runData | keys'
```

### Get Node Output Data

```bash
export $(cat .env | grep -v '^#' | xargs) && curl -s "${N8N_API_URL}/api/v1/executions/{EXECUTION_ID}?includeData=true" -H "X-N8N-API-KEY: ${N8N_API_KEY}" | jq '.data.resultData.runData["Node Name"]'
```
