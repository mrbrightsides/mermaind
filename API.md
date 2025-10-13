# 🔌 **MERMAIND API DOCUMENTATION**

Complete REST API reference for programmatic diagram generation and template access.

---

## 📋 **Table of Contents**

- [Overview](#overview)
- [Authentication](#authentication)
- [Rate Limiting](#rate-limiting)
- [Endpoints](#endpoints)
  - [Generate Diagram](#generate-diagram)
  - [Get Templates](#get-templates)
- [Error Handling](#error-handling)
- [Code Examples](#code-examples)
- [SDKs](#sdks)

---

## 🌟 **Overview**

The Mermaind API allows you to programmatically generate academic diagrams, access templates, and integrate Mermaind into your research workflows.

**Base URL**: `https://mermaind.app/api/v1`

**Response Format**: JSON

**Authentication**: API Key (Bearer Token)

---

## 🔐 **Authentication**

All API requests require an API key passed in the `Authorization` header.

### **Getting an API Key**

1. Visit [Mermaind App](https://mermaind.app)
2. Click "API Keys" button
3. Create new API key
4. Copy and securely store your key

### **Using Your API Key**

```bash
curl -H "Authorization: Bearer YOUR_API_KEY" \
     https://mermaind.app/api/v1/diagram
```

**⚠️ Security**: Never commit API keys to version control. Use environment variables.

```bash
export MERMAIND_API_KEY="your_api_key_here"
```

---

## ⏱️ **Rate Limiting**

**Free Tier**: 100 requests per hour per API key

**Headers**:
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1640000000
```

**429 Response** when rate limit exceeded:
```json
{
  "error": "Rate limit exceeded",
  "limit": 100,
  "reset": 1640000000,
  "retryAfter": 3600
}
```

---

## 📡 **Endpoints**

### **Generate Diagram**

Create a diagram from a natural language prompt.

#### **Request**

```http
POST /api/v1/diagram
```

**Headers**:
```
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

**Body**:
```json
{
  "prompt": "Show the peer review process for academic journals",
  "type": "flowchart",
  "style": "academic",
  "options": {
    "theme": "default",
    "width": 800,
    "height": 600
  }
}
```

**Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `prompt` | string | ✅ Yes | Natural language description of diagram |
| `type` | string | ✅ Yes | Diagram type: `flowchart`, `sequence`, `class`, `state`, `gantt`, `git` |
| `style` | string | ❌ No | Style preset: `academic`, `minimal`, `professional` (default: `academic`) |
| `options.theme` | string | ❌ No | Mermaid theme: `default`, `dark`, `forest`, `neutral` |
| `options.width` | number | ❌ No | Diagram width in pixels (default: 800) |
| `options.height` | number | ❌ No | Diagram height in pixels (default: 600) |

#### **Response**

**Success (200)**:
```json
{
  "success": true,
  "data": {
    "id": "diagram_abc123",
    "type": "flowchart",
    "mermaidCode": "flowchart TD\n  Start --> End",
    "svg": "<svg>...</svg>",
    "metadata": {
      "generatedAt": "2024-01-15T10:30:00Z",
      "processingTime": 1234,
      "aiModel": "perplexity-small"
    },
    "urls": {
      "svg": "https://mermaind.app/diagrams/abc123.svg",
      "png": "https://mermaind.app/diagrams/abc123.png",
      "pdf": "https://mermaind.app/diagrams/abc123.pdf"
    }
  }
}
```

**Error (400)**:
```json
{
  "success": false,
  "error": {
    "code": "INVALID_DIAGRAM_TYPE",
    "message": "Diagram type must be one of: flowchart, sequence, class, state, gantt, git",
    "details": {
      "provided": "invalid_type",
      "allowed": ["flowchart", "sequence", "class", "state", "gantt", "git"]
    }
  }
}
```

#### **Example Request**

```bash
curl -X POST https://mermaind.app/api/v1/diagram \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Show machine learning pipeline from data collection to deployment",
    "type": "flowchart",
    "style": "academic"
  }'
```

---

### **Get Templates**

Retrieve available academic diagram templates.

#### **Request**

```http
GET /api/v1/templates
```

**Headers**:
```
Authorization: Bearer YOUR_API_KEY
```

**Query Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `type` | string | ❌ No | Filter by diagram type |
| `category` | string | ❌ No | Filter by category: `medical`, `engineering`, `social-science`, etc. |
| `search` | string | ❌ No | Search templates by name or description |
| `limit` | number | ❌ No | Number of results (default: 50, max: 200) |
| `offset` | number | ❌ No | Pagination offset (default: 0) |

#### **Response**

**Success (200)**:
```json
{
  "success": true,
  "data": {
    "templates": [
      {
        "id": "template_001",
        "name": "Clinical Trial CONSORT",
        "description": "Standard CONSORT flow diagram for clinical trials",
        "type": "flowchart",
        "category": "medical",
        "tags": ["clinical", "trial", "research"],
        "mermaidCode": "flowchart TD\n  Enrollment --> Allocation",
        "preview": "https://mermaind.app/templates/001/preview.png",
        "usageCount": 1234,
        "createdAt": "2024-01-01T00:00:00Z"
      }
    ],
    "pagination": {
      "total": 200,
      "limit": 50,
      "offset": 0,
      "hasMore": true
    }
  }
}
```

#### **Example Request**

```bash
curl -X GET "https://mermaind.app/api/v1/templates?type=flowchart&category=medical&limit=10" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

---

## ❌ **Error Handling**

### **Error Response Format**

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": {
      "additionalInfo": "value"
    }
  }
}
```

### **Error Codes**

| Code | Status | Description |
|------|--------|-------------|
| `UNAUTHORIZED` | 401 | Invalid or missing API key |
| `RATE_LIMIT_EXCEEDED` | 429 | Too many requests |
| `INVALID_DIAGRAM_TYPE` | 400 | Unsupported diagram type |
| `INVALID_PROMPT` | 400 | Prompt is too short or invalid |
| `GENERATION_FAILED` | 500 | AI diagram generation failed |
| `RENDERING_FAILED` | 500 | Mermaid rendering failed |
| `TEMPLATE_NOT_FOUND` | 404 | Template ID doesn't exist |
| `INTERNAL_ERROR` | 500 | Unexpected server error |

### **Handling Errors**

```python
import requests

response = requests.post(
    "https://mermaind.app/api/v1/diagram",
    headers={"Authorization": f"Bearer {API_KEY}"},
    json={"prompt": "Show process", "type": "flowchart"}
)

if response.status_code == 200:
    data = response.json()
    print(f"Diagram generated: {data['data']['urls']['svg']}")
elif response.status_code == 429:
    error = response.json()['error']
    print(f"Rate limited. Retry after: {error['details']['retryAfter']} seconds")
else:
    error = response.json()['error']
    print(f"Error: {error['message']}")
```

---

## 💻 **Code Examples**

### **cURL**

```bash
# Generate diagram
curl -X POST https://mermaind.app/api/v1/diagram \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Show systematic review PRISMA flowchart",
    "type": "flowchart"
  }'

# Get templates
curl -X GET "https://mermaind.app/api/v1/templates?category=medical" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### **Python**

```python
import requests

API_KEY = "your_api_key_here"
BASE_URL = "https://mermaind.app/api/v1"

def generate_diagram(prompt, diagram_type):
    """Generate academic diagram from prompt"""
    response = requests.post(
        f"{BASE_URL}/diagram",
        headers={
            "Authorization": f"Bearer {API_KEY}",
            "Content-Type": "application/json"
        },
        json={
            "prompt": prompt,
            "type": diagram_type,
            "style": "academic"
        }
    )
    
    if response.status_code == 200:
        return response.json()['data']
    else:
        raise Exception(f"API Error: {response.json()['error']['message']}")

# Usage
diagram = generate_diagram(
    "Show machine learning pipeline from data to deployment",
    "flowchart"
)
print(f"SVG URL: {diagram['urls']['svg']}")
print(f"Mermaid Code:\n{diagram['mermaidCode']}")
```

### **JavaScript/Node.js**

```javascript
const axios = require('axios');

const API_KEY = 'your_api_key_here';
const BASE_URL = 'https://mermaind.app/api/v1';

async function generateDiagram(prompt, type) {
  try {
    const response = await axios.post(
      `${BASE_URL}/diagram`,
      {
        prompt: prompt,
        type: type,
        style: 'academic'
      },
      {
        headers: {
          'Authorization': `Bearer ${API_KEY}`,
          'Content-Type': 'application/json'
        }
      }
    );
    
    return response.data.data;
  } catch (error) {
    if (error.response) {
      console.error('API Error:', error.response.data.error.message);
    }
    throw error;
  }
}

// Usage
generateDiagram('Show PhD thesis workflow', 'flowchart')
  .then(diagram => {
    console.log('SVG URL:', diagram.urls.svg);
    console.log('Mermaid Code:', diagram.mermaidCode);
  })
  .catch(console.error);
```

### **R**

```r
library(httr)
library(jsonlite)

API_KEY <- "your_api_key_here"
BASE_URL <- "https://mermaind.app/api/v1"

generate_diagram <- function(prompt, type) {
  response <- POST(
    paste0(BASE_URL, "/diagram"),
    add_headers(
      Authorization = paste("Bearer", API_KEY),
      `Content-Type` = "application/json"
    ),
    body = toJSON(list(
      prompt = prompt,
      type = type,
      style = "academic"
    ), auto_unbox = TRUE),
    encode = "json"
  )
  
  if (status_code(response) == 200) {
    content(response)$data
  } else {
    stop(paste("API Error:", content(response)$error$message))
  }
}

# Usage
diagram <- generate_diagram(
  "Show experimental research design",
  "flowchart"
)
print(diagram$urls$svg)
```

### **Jupyter Notebook Integration**

```python
import requests
from IPython.display import SVG, display

API_KEY = "your_api_key_here"

def create_and_display_diagram(prompt, diagram_type="flowchart"):
    """Generate and display diagram in Jupyter"""
    response = requests.post(
        "https://mermaind.app/api/v1/diagram",
        headers={"Authorization": f"Bearer {API_KEY}"},
        json={"prompt": prompt, "type": diagram_type}
    )
    
    if response.status_code == 200:
        svg_content = response.json()['data']['svg']
        display(SVG(data=svg_content))
        return response.json()['data']
    else:
        print(f"Error: {response.json()['error']['message']}")

# Usage in notebook
diagram = create_and_display_diagram(
    "Show data analysis pipeline for quantitative research"
)
```

---

## 📦 **SDKs**

### **Coming Soon**

We're developing official SDKs for popular languages:

- [ ] Python SDK (`pip install mermaind`)
- [ ] JavaScript/TypeScript SDK (`npm install @mermaind/sdk`)
- [ ] R Package (`install.packages("mermaind")`)
- [ ] Julia Package
- [ ] Ruby Gem

**Want to help?** Contribute to SDK development! See [CONTRIBUTING.md](./CONTRIBUTING.md)

---

## 🔄 **Webhooks** (Coming Soon)

Configure webhooks to receive notifications when:
- Diagrams are generated
- Templates are updated
- Collaboration events occur

```json
{
  "event": "diagram.generated",
  "timestamp": "2024-01-15T10:30:00Z",
  "data": {
    "diagramId": "abc123",
    "type": "flowchart"
  }
}
```

---

## 📊 **Usage Analytics**

Track your API usage in the Mermaind dashboard:

- Total requests per day/week/month
- Response times and success rates
- Most used diagram types
- Error rate monitoring
- Cost projections (for paid plans)

Access at: [mermaind.app/dashboard/api](https://mermaind.app/dashboard/api)

---

## 🚀 **Best Practices**

### **1. Cache Responses**
```python
import requests_cache

# Cache responses for 1 hour
requests_cache.install_cache('mermaind_cache', expire_after=3600)
```

### **2. Handle Rate Limits Gracefully**
```python
import time

def generate_with_retry(prompt, type, max_retries=3):
    for attempt in range(max_retries):
        response = requests.post(...)
        
        if response.status_code == 429:
            retry_after = int(response.headers.get('Retry-After', 60))
            time.sleep(retry_after)
            continue
        
        return response.json()
```

### **3. Use Batch Processing**
```python
# Generate multiple diagrams efficiently
prompts = [
    "Show clinical trial process",
    "Show systematic review workflow",
    "Show lab experiment protocol"
]

diagrams = []
for prompt in prompts:
    diagram = generate_diagram(prompt, "flowchart")
    diagrams.append(diagram)
    time.sleep(1)  # Respect rate limits
```

### **4. Error Logging**
```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

try:
    diagram = generate_diagram(prompt, type)
    logger.info(f"Generated diagram: {diagram['id']}")
except Exception as e:
    logger.error(f"Failed to generate diagram: {str(e)}")
```

---

## 🆘 **Support**

- **API Issues**: [GitHub Issues](https://github.com/yourusername/mermaind/issues)
- **Email**: api-support@mermaind.app
- **Status Page**: [status.mermaind.app](https://status.mermaind.app)
- **Documentation**: [docs.mermaind.app](https://docs.mermaind.app)

---

## 📄 **License**

API usage subject to [Terms of Service](https://mermaind.app/terms)

---

**Built with 🔵 on Base • Empowering Academic Research Through APIs** 🚀
