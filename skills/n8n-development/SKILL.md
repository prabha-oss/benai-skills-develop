---
name: n8n-development
description: Write JavaScript and Python code for n8n Code nodes. Use when building custom logic, data transformation, API calls, or complex workflow operations that go beyond built-in nodes.
---

# n8n Development Skill

Write effective JavaScript and Python code for n8n Code nodes, configure nodes properly, and build robust workflow patterns.

---

## Part 1: Code Node Fundamentals

### JavaScript vs Python

| Aspect | JavaScript | Python |
|--------|------------|--------|
| Default | Yes | Requires Python executor |
| Performance | Faster startup | Better for data science |
| Libraries | Built-in n8n helpers | NumPy, Pandas available |
| Syntax | `$input.all()` | `_input.all()` |

### The Golden Rule

**Code nodes use plain JavaScript/Python - NOT expression syntax!**

```javascript
// WRONG - expression syntax in Code node
const name = {{ $json.name }};
const data = {{ $json.body }};

// CORRECT - plain JavaScript
const name = $input.first().json.name;
const data = $input.first().json.body;
```

---

## Part 2: JavaScript in Code Nodes

### Accessing Input Data

```javascript
// Get all input items
const items = $input.all();

// Get first item
const firstItem = $input.first();

// Get item data
const data = $input.first().json;
const name = $input.first().json.name;

// Get specific field from first item
const email = $input.first().json.body.email;
```

### Returning Data

**Every Code node MUST return an array of items.**

```javascript
// Return single item
return [{ json: { result: 'success' } }];

// Return multiple items
return [
  { json: { id: 1, name: 'First' } },
  { json: { id: 2, name: 'Second' } }
];

// Transform and return all items
return $input.all().map(item => ({
  json: {
    ...item.json,
    processed: true,
    timestamp: new Date().toISOString()
  }
}));
```

### Working with All Items

```javascript
// Process each item
const results = [];
for (const item of $input.all()) {
  results.push({
    json: {
      original: item.json.name,
      uppercase: item.json.name.toUpperCase()
    }
  });
}
return results;

// Using map (cleaner)
return $input.all().map(item => ({
  json: {
    original: item.json.name,
    uppercase: item.json.name.toUpperCase()
  }
}));
```

### Filtering Items

```javascript
// Filter items
return $input.all().filter(item => item.json.status === 'active');

// Filter and transform
return $input.all()
  .filter(item => item.json.score > 80)
  .map(item => ({
    json: {
      name: item.json.name,
      passed: true
    }
  }));
```

### Aggregating Data

```javascript
// Sum values
const total = $input.all().reduce((sum, item) => sum + item.json.amount, 0);
return [{ json: { total } }];

// Group by field
const grouped = {};
for (const item of $input.all()) {
  const key = item.json.category;
  if (!grouped[key]) grouped[key] = [];
  grouped[key].push(item.json);
}
return [{ json: grouped }];

// Count items
const count = $input.all().length;
return [{ json: { count } }];
```

### Accessing Other Nodes

```javascript
// Get data from specific node
const httpData = $('HTTP Request').first().json;
const allHttpItems = $('HTTP Request').all();

// Get data from previous node
const prevData = $input.first().json;

// Check if node has data
if ($('HTTP Request').all().length > 0) {
  // Node has output
}
```

### Environment Variables

```javascript
// Access environment variables
const apiKey = $env.API_KEY;
const baseUrl = $env.BASE_URL;

// Use in API calls
const response = await fetch(`${$env.API_URL}/endpoint`, {
  headers: { 'Authorization': `Bearer ${$env.API_KEY}` }
});
```

### Making HTTP Requests

```javascript
// GET request
const response = await fetch('https://api.example.com/data');
const data = await response.json();
return [{ json: data }];

// POST request
const response = await fetch('https://api.example.com/users', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ name: 'John', email: 'john@example.com' })
});
const result = await response.json();
return [{ json: result }];

// With error handling
try {
  const response = await fetch('https://api.example.com/data');
  if (!response.ok) {
    throw new Error(`HTTP ${response.status}: ${response.statusText}`);
  }
  const data = await response.json();
  return [{ json: { success: true, data } }];
} catch (error) {
  return [{ json: { success: false, error: error.message } }];
}
```

### Working with Dates

```javascript
// Current date
const now = new Date();
const isoString = now.toISOString();

// Using Luxon (available in n8n)
const { DateTime } = require('luxon');
const today = DateTime.now().toFormat('yyyy-MM-dd');
const nextWeek = DateTime.now().plus({ days: 7 }).toISO();

// Parse date string
const parsed = DateTime.fromISO($input.first().json.dateString);
const formatted = parsed.toFormat('dd/MM/yyyy');

return [{ json: { today, nextWeek, formatted } }];
```

### Error Handling

```javascript
// Try-catch pattern
try {
  const data = $input.first().json;
  if (!data.required_field) {
    throw new Error('Missing required_field');
  }
  // Process data
  return [{ json: { success: true, result: data.required_field } }];
} catch (error) {
  // Return error info instead of failing
  return [{ json: { success: false, error: error.message } }];
}

// Validate input
const item = $input.first().json;
if (!item.email || !item.email.includes('@')) {
  throw new Error('Invalid email address');
}
```

### Common JavaScript Patterns

```javascript
// Deduplicate array
const unique = [...new Set($input.all().map(i => i.json.email))];
return unique.map(email => ({ json: { email } }));

// Flatten nested arrays
const nested = $input.first().json.items; // [[1,2], [3,4]]
const flat = nested.flat();
return [{ json: { flat } }];

// Sort items
const sorted = $input.all().sort((a, b) =>
  a.json.name.localeCompare(b.json.name)
);
return sorted;

// Merge objects
const merged = Object.assign({},
  $('Node1').first().json,
  $('Node2').first().json
);
return [{ json: merged }];

// Safe property access
const city = $input.first().json?.user?.address?.city ?? 'Unknown';
return [{ json: { city } }];
```

---

## Part 3: Python in Code Nodes

### Basic Python Syntax

```python
# Access input data
items = _input.all()
first_item = _input.first()
data = _input.first().json

# Return data
return [{"json": {"result": "success"}}]
```

### Processing Items

```python
# Transform all items
results = []
for item in _input.all():
    results.append({
        "json": {
            "original": item.json["name"],
            "upper": item.json["name"].upper()
        }
    })
return results

# List comprehension
return [
    {"json": {"name": item.json["name"].upper()}}
    for item in _input.all()
]
```

### Filtering in Python

```python
# Filter items
active_items = [
    item for item in _input.all()
    if item.json.get("status") == "active"
]
return [{"json": item.json} for item in active_items]
```

### Data Processing with Python

```python
# Sum values
total = sum(item.json["amount"] for item in _input.all())
return [{"json": {"total": total}}]

# Group by category
from collections import defaultdict
grouped = defaultdict(list)
for item in _input.all():
    grouped[item.json["category"]].append(item.json)
return [{"json": dict(grouped)}]
```

### Working with JSON

```python
import json

# Parse JSON string
data = json.loads(_input.first().json["json_string"])

# Stringify object
json_str = json.dumps({"key": "value"})

return [{"json": {"parsed": data, "stringified": json_str}}]
```

### Date Handling in Python

```python
from datetime import datetime, timedelta

# Current date
now = datetime.now()
iso_string = now.isoformat()

# Parse date
date_str = _input.first().json["date"]
parsed = datetime.fromisoformat(date_str)

# Add days
next_week = now + timedelta(days=7)

return [{"json": {
    "now": iso_string,
    "next_week": next_week.isoformat()
}}]
```

### Error Handling in Python

```python
try:
    data = _input.first().json
    if "required_field" not in data:
        raise ValueError("Missing required_field")

    result = process_data(data)
    return [{"json": {"success": True, "result": result}}]
except Exception as e:
    return [{"json": {"success": False, "error": str(e)}}]
```

---

## Part 4: Node Configuration Patterns

### Webhook Node Configuration

```json
{
  "type": "n8n-nodes-base.webhook",
  "typeVersion": 2,
  "parameters": {
    "path": "my-webhook-path",
    "httpMethod": "POST",
    "responseMode": "responseNode",
    "options": {}
  }
}
```

**Key settings:**
- `path`: Unique URL path (no leading slash)
- `httpMethod`: GET, POST, PUT, DELETE
- `responseMode`: `onReceived` (immediate) or `responseNode` (wait for Respond node)

### HTTP Request Node

```json
{
  "type": "n8n-nodes-base.httpRequest",
  "typeVersion": 4.2,
  "parameters": {
    "method": "POST",
    "url": "https://api.example.com/endpoint",
    "authentication": "genericCredentialType",
    "genericAuthType": "httpHeaderAuth",
    "sendHeaders": true,
    "headerParameters": {
      "parameters": [
        { "name": "Content-Type", "value": "application/json" }
      ]
    },
    "sendBody": true,
    "bodyParameters": {
      "parameters": [
        { "name": "key", "value": "={{ $json.value }}" }
      ]
    }
  }
}
```

### Set Node (Add/Modify Fields)

```json
{
  "type": "n8n-nodes-base.set",
  "typeVersion": 3.4,
  "parameters": {
    "mode": "manual",
    "duplicateItem": false,
    "assignments": {
      "assignments": [
        {
          "id": "field1",
          "name": "newField",
          "value": "={{ $json.existingField }}",
          "type": "string"
        }
      ]
    },
    "includeOtherFields": true
  }
}
```

### If Node (Conditional)

```json
{
  "type": "n8n-nodes-base.if",
  "typeVersion": 2,
  "parameters": {
    "conditions": {
      "options": {
        "caseSensitive": true,
        "leftValue": "",
        "typeValidation": "strict"
      },
      "conditions": [
        {
          "leftValue": "={{ $json.status }}",
          "rightValue": "active",
          "operator": {
            "type": "string",
            "operation": "equals"
          }
        }
      ],
      "combinator": "and"
    }
  }
}
```

### Switch Node (Multiple Branches)

```json
{
  "type": "n8n-nodes-base.switch",
  "typeVersion": 3,
  "parameters": {
    "mode": "rules",
    "rules": {
      "rules": [
        {
          "outputKey": "high",
          "conditions": {
            "conditions": [
              {
                "leftValue": "={{ $json.priority }}",
                "rightValue": "high",
                "operator": { "type": "string", "operation": "equals" }
              }
            ]
          }
        },
        {
          "outputKey": "low",
          "conditions": {
            "conditions": [
              {
                "leftValue": "={{ $json.priority }}",
                "rightValue": "low",
                "operator": { "type": "string", "operation": "equals" }
              }
            ]
          }
        }
      ]
    }
  }
}
```

### Loop Over Items Node

```json
{
  "type": "n8n-nodes-base.splitInBatches",
  "typeVersion": 3,
  "parameters": {
    "batchSize": 10,
    "options": {}
  }
}
```

### Merge Node

```json
{
  "type": "n8n-nodes-base.merge",
  "typeVersion": 3,
  "parameters": {
    "mode": "combine",
    "mergeByFields": {
      "values": [
        { "field1": "id", "field2": "userId" }
      ]
    },
    "options": {}
  }
}
```

**Merge modes:**
- `append`: Combine all items from both inputs
- `combine`: Match items by field values
- `chooseBranch`: Select one input based on condition

---

## Part 5: Workflow Patterns

### Pattern 1: Webhook + Process + Respond

```
[Webhook] -> [Code/Set] -> [Respond to Webhook]
```

Standard request-response pattern. Set webhook `responseMode: "responseNode"`.

### Pattern 2: Fan-out/Fan-in

```
                  -> [Process A] -
[Split Items] -|                   |-> [Merge] -> [Output]
                  -> [Process B] -
```

Process items in parallel branches, then combine results.

### Pattern 3: Error Handling Branch

```
[Main Process] --success--> [Continue]
       |
       +--error--> [Error Handler] -> [Notify]
```

Configure node with `continueOnFail: true` and check for errors.

### Pattern 4: Retry with Backoff

```json
{
  "type": "n8n-nodes-base.httpRequest",
  "retryOnFail": true,
  "maxTries": 3,
  "waitBetweenTries": 1000
}
```

### Pattern 5: Pagination Loop

```
[HTTP Request] -> [Check Has More] --yes--> [Update Page] -> [HTTP Request]
                        |
                        +--no--> [Aggregate Results]
```

For APIs that return paginated results.

### Pattern 6: Conditional Execution

```
[Webhook] -> [If Condition] --true--> [Action A]
                   |
                   +--false--> [Action B]
```

### Pattern 7: Data Enrichment

```
[Get Base Data] -> [Loop] -> [Fetch Details] -> [Merge] -> [Output]
```

Fetch main records, then enrich each with additional API calls.

### Pattern 8: Scheduled Sync

```
[Schedule Trigger] -> [Get New Records] -> [If Has Records] -> [Process] -> [Update Sync Timestamp]
```

---

## Part 6: Common Code Node Mistakes

### Mistake 1: Not Returning Array

```javascript
// WRONG - returns single object
return { json: { result: 'done' } };

// CORRECT - returns array of items
return [{ json: { result: 'done' } }];
```

### Mistake 2: Missing json Wrapper

```javascript
// WRONG - missing json property
return [{ name: 'John' }];

// CORRECT - wrapped in json
return [{ json: { name: 'John' } }];
```

### Mistake 3: Using Expression Syntax

```javascript
// WRONG - expression syntax
const data = {{ $json.body }};

// CORRECT - Code node syntax
const data = $input.first().json.body;
```

### Mistake 4: Forgetting Async/Await

```javascript
// WRONG - fetch returns Promise
const response = fetch('https://api.example.com');
const data = response.json(); // Error!

// CORRECT - await the Promise
const response = await fetch('https://api.example.com');
const data = await response.json();
return [{ json: data }];
```

### Mistake 5: Not Handling Empty Input

```javascript
// WRONG - crashes if no input
const name = $input.first().json.name;

// CORRECT - check first
const items = $input.all();
if (items.length === 0) {
  return [{ json: { error: 'No input data' } }];
}
const name = items[0].json.name;
```

### Mistake 6: Modifying Input Directly

```javascript
// WRONG - modifies original
const item = $input.first();
item.json.newField = 'value';
return [item];

// CORRECT - create new object
const item = $input.first();
return [{
  json: {
    ...item.json,
    newField: 'value'
  }
}];
```

---

## Part 7: Debugging Code Nodes

### Console Logging

```javascript
// Log to execution output
console.log('Input data:', JSON.stringify($input.first().json, null, 2));

// Log all items
console.log('Item count:', $input.all().length);
for (const item of $input.all()) {
  console.log('Item:', item.json);
}

// Always return something
return $input.all();
```

### Inspect Data Structure

```javascript
// Return input structure for debugging
return [{
  json: {
    itemCount: $input.all().length,
    firstItem: $input.first()?.json,
    allKeys: Object.keys($input.first()?.json || {}),
    rawInput: $input.all().map(i => i.json)
  }
}];
```

### Step-by-Step Debugging

```javascript
const results = { steps: [] };

// Step 1
const input = $input.first().json;
results.steps.push({ step: 1, input });

// Step 2
const processed = input.name?.toUpperCase();
results.steps.push({ step: 2, processed });

// Step 3
const final = { name: processed, timestamp: new Date().toISOString() };
results.steps.push({ step: 3, final });

return [{ json: results }];
```

---

## Quick Reference

### JavaScript Code Node

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

### Python Code Node

```python
# Input
items = _input.all()
first = _input.first().json
field = _input.first().json["fieldName"]

# Return (MUST be list)
return [{"json": {"result": "value"}}]
```

### Node Must-Haves

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
