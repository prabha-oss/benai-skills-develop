---
name: n8n-development
description: Write JavaScript and Python code for n8n Code nodes. Use when building custom logic, data transformation, API calls, filtering, aggregation, or complex operations. Use for $input.all(), $input.first(), returning items, debugging code nodes, and workflow patterns like error handling, pagination, and data enrichment.
---

# n8n Development Skill

Write effective JavaScript and Python code for n8n Code nodes.

---

## The Golden Rule

**Code nodes use plain JavaScript/Python - NOT expression syntax!**

```javascript
// WRONG - expression syntax in Code node
const name = {{ $json.name }};

// CORRECT - plain JavaScript
const name = $input.first().json.name;
```

---

## JavaScript vs Python

| Aspect | JavaScript | Python |
|--------|------------|--------|
| Default | Yes | Requires Python executor |
| Performance | Faster startup | Better for data science |
| Syntax | `$input.all()` | `_input.all()` |

---

## Quick Reference

### JavaScript

```javascript
// Input
const items = $input.all();
const first = $input.first().json;
const field = $input.first().json.fieldName;

// Other nodes
const data = $('Node Name').first().json;

// Environment
const key = $env.API_KEY;

// Return (MUST be array)
return [{ json: { result: 'value' } }];
```

### Python

```python
# Input
items = _input.all()
first = _input.first().json
field = _input.first().json["fieldName"]

# Return (MUST be list)
return [{"json": {"result": "value"}}]
```

---

## Common Mistakes

| Mistake | Wrong | Correct |
|---------|-------|---------|
| Not returning array | `return { json: {} }` | `return [{ json: {} }]` |
| Missing json wrapper | `return [{ name: 'John' }]` | `return [{ json: { name: 'John' } }]` |
| Expression syntax | `{{ $json.body }}` | `$input.first().json.body` |
| Forgetting await | `fetch(url).json()` | `(await fetch(url)).json()` |

---

## Node Must-Haves

```json
{
  "id": "unique-id",
  "name": "Descriptive Name",
  "type": "n8n-nodes-base.nodeName",
  "typeVersion": 2,
  "position": [x, y],
  "parameters": {}
}
```

---

## Reference Files

| File | Contents |
|------|----------|
| [javascript.md](javascript.md) | Complete JavaScript reference: input/output, filtering, aggregation, HTTP requests, dates, debugging |
| [python.md](python.md) | Python syntax, data processing, JSON handling, error handling |
| [node-config.md](node-config.md) | Node configurations (Webhook, HTTP, Set, If, Switch, Merge) + workflow patterns |
