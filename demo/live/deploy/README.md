# Valkey for AI - Live Demo

Real demos backed by Valkey 9 with Bedrock Titan embeddings and Claude Haiku LLM.

## Deploy locally

```bash
git clone https://github.com/meet-bhagdev/valkeyforai.git
cd valkeyforai/demo/live/deploy

# Requires AWS credentials with Bedrock access (Titan Embeddings + Claude Haiku)
docker compose up --build
```

API runs at http://localhost:8000. Health check: `curl http://localhost:8000/api/health`

## Endpoints

| Endpoint | What it does |
|----------|-------------|
| `GET /api/health` | Ping Valkey |
| `POST /api/vector-search/setup` | Create HNSW index + embed 8 sample docs with Titan |
| `POST /api/vector-search/search` | KNN search with real 1536-dim embeddings |
| `POST /api/semantic-cache/setup` | Create cache index |
| `POST /api/semantic-cache/ask` | Check cache, call Claude on miss, cache result |
| `POST /api/rate-limit/check` | INCR + EXPIRE pipeline |
| `POST /api/rate-limit/reset` | Clear rate limit keys |

## Requirements

- Docker + Docker Compose
- AWS credentials with access to:
  - `amazon.titan-embed-text-v1` (embeddings)
  - `anthropic.claude-3-haiku-20240307-v1:0` (LLM)
