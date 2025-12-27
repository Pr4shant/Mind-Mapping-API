# MindGraph API

MindGraph API allows you to generate and explore mind graphs from text. You can create graphs, view existing nodes, and expand them incrementally.

## Dashboard

Monitor your API usage with the built-in dashboard. Open `dashboard.html` in your browser and enter your API key to view:

- Total requests and success/failure rates
- Token usage (prompt and completion tokens)
- Rate limiting statistics
- Daily usage trends (last 30 days)
- Estimated billing costs

**Access the dashboard:** Open `dashboard.html` in your web browser.

---

## Endpoints

### Generate Graph
**POST** `/v1/graph`

### Get Analytics (Admin)
**GET** `/v1/analytics`

### Get User Analytics
**GET** `/v1/user/analytics`

Returns usage statistics for the authenticated user including:
- Total requests, successful/failed requests
- Token usage breakdown
- Rate limiting information
- Daily usage data (last 30 days)

---

## Base URL

```
https://mindgraph-api.onrender.com/v1/graph
```

---

## Authentication

All requests require an **API key**. Include it in the header:

```
Authorization: Bearer YOUR_API_KEY
```

---

## Request

**POST JSON body:**

```json
{
  "text": "Your text here",
  "graph": {
    "nodes": [],
    "links": []
  }
}
```

* `text`: The new text to analyze.
* `graph`: Optional. Pass your previous graph to preserve state.

---

## Response

Returns a JSON object:

```json
{
  "nodes": [
    { "id": "thought:innovate", "label": "", "category": "thought" }
  ],
  "links": [
    { "source": "thought:innovate", "target": "emotion:excitement" }
  ]
}
```
---

## Usage Examples

### Bash / macOS

```bash
curl -X POST https://mindgraph-api.onrender.com/v1/graph \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "Let's go",
    "graph": { "nodes": [], "links": [] }
  }'
```

### Windows (CMD)

```bat
curl -X POST https://mindgraph-api.onrender.com/v1/graph ^
  -H "Authorization: Bearer YOUR_API_KEY" ^
  -H "Content-Type: application/json" ^
  -d "{\"text\":\"Let's go\",\"graph\":{\"nodes\":[],\"links\":[]}}"
```

---

## Getting the API Key

Email me at - prashant.unravel@gmail.com with the subject "Get MindGraph API Key" to receive your API key.

---

## Using the API

Store your API key securely and use it in API requests:

```
Authorization: Bearer YOUR_API_KEY
```

* index.html has a simple example of how to call the API using JavaScript's fetch function.
* dashboard.html provides a dashboard to monitor your API usage and statistics. 

---

## Notes

* Always pass your **previous graph state** if you want incremental updates.
* Keep API keys private; do not commit them to public repositories.
* For frontend integration, you can use the **fetch API** in JavaScript:

```js
fetch("https://mindgraph-api.onrender.com/v1/graph", {
  method: "POST",
  headers: {
    "Authorization": "Bearer YOUR_API_KEY",
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    text: "Let's go",
    graph: { nodes: [], links: [] }
  })
})
.then(res => res.json())
.then(console.log);
```

---

## License

MIT
