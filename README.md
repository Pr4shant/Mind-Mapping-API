# MINDMAP API

### URL: https://mindgraphs.vercel.app/

### Example: https://mindgraphs.vercel.app/?application_id=test_app&actor_id=test&actor_domain_id=test&actor_domain_type=test&mindmap_domain_id=test&mindmap_domain_type=memory&api_key=api_key&text=let%27s%20go

### 📡 API Endpoint
- **POST /v1/mindmap** - Handles mindmap graph requests
- **Authentication**: API key required
- **Rate Limit**: 20 requests/minute

### 🔄 Processing Logic
The endpoint implements exactly what you requested:

1. **Fetch existing graph** from DB using application_id and actor_id
2. **If text provided**:
   - Generate new graph 
   - Merge with existing graph (existing `build_graph_from_subthoughts()`)
   - Save merged result to DB
   - Return `is_new: true`
3. **If no text**:
   - Return existing graph from DB (if present)
   - Return empty graph if no existing record
   - Return `is_new: false`

### 📋 Input/Output Formats

**Request:**
```json
{
  "application_id": "app_456",
  "actor": {
    "actor_id": "actor_789",
    "domain_id": "user_42",
    "domain_type": "user"
  },
  "mindmap": {
    "domain_id": "memory_2026_01_13",
    "domain_type": "memory",
    "text": "optional - omit to fetch only"
  }
}
```

**Response:**
```json
{
  "graph": {
    "nodes": [...],
    "links": [...]
  },
  "is_new": true,
  "message": "New graph generated and merged with existing graph"
}
```

### Use in Production
```bash
curl -X POST http://mindgraph-api.onrender.com/v1/mindmap \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "application_id": "app_456",
    "actor": {
      "actor_id": "actor_789",
      "domain_id": "user_42",
      "domain_type": "user"
    },
    "mindmap": {
      "domain_id": "memory_2026_01_13",
      "domain_type": "memory",
      "text": "your text here"
    }
  }'
```

## ✨ Key Features

✅ **Persistent Storage** - All graphs saved to Supabase
✅ **Graph Merging** - New graphs automatically merged with existing
✅ **LLM Integration** - Uses your existing LLM functions
✅ **Authentication** - API key protection
✅ **Rate Limiting** - 20 requests/minute per key
✅ **Analytics Tracking** - All requests logged
✅ **Error Handling** - Proper error responses (401, 422, 429, 500)
✅ **Performance** - O(1) database lookups with indices
✅ **Documentation** - 7 comprehensive guides included

## 🎯 Usage Examples

### Generate New Graph
```json
{
  "application_id": "app_456",
  "actor": {"actor_id": "actor_789", "domain_id": "user_42", "domain_type": "user"},
  "mindmap": {
    "domain_id": "memory_2026_01_13",
    "domain_type": "memory",
    "text": "I went to the park and saw birds flying"
  }
}
```
**Response**: `is_new: true` with generated graph

### Add to Existing Graph
```json
{
  "application_id": "app_456",
  "actor": {"actor_id": "actor_789", "domain_id": "user_42", "domain_type": "user"},
  "mindmap": {
    "domain_id": "memory_2026_01_13",
    "domain_type": "memory",
    "text": "I also saw something"
  }
}
```
**Response**: `is_new: true` with merged graph

### Fetch Without Text
```json
{
  "application_id": "app_456",
  "actor": {"actor_id": "actor_789", "domain_id": "user_42", "domain_type": "user"},
  "mindmap": {
    "domain_id": "memory_2026_01_13",
    "domain_type": "memory"
  }
}
```
**Response**: `is_new: false` with existing graph

---
Happy mindmapping! 





