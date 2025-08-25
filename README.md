# AI Stack Deployment

This repository contains three separate docker-compose files for deploying the AI stack:

1. `docker-compose.others.yml` - Contains postgres, n8n-import, n8n, and qdrant services
2. `docker-compose.ollama.yml` - Contains ollama services
3. `docker-compose.webui.yml` - Contains the open-webui service

## Prerequisites

- Docker and Docker Compose installed
- NVIDIA Docker runtime (for GPU support with Ollama)

## Setup Instructions

1. Create the shared network for inter-container communication:
   ```bash
   docker network create ai-stack-network
   ```

2. Start the services in the following order:
   ```bash
   # Start the core services (postgres, qdrant)
   docker-compose -f docker-compose.others.yml up -d postgres qdrant
   
   # Start Ollama services
   docker-compose -f docker-compose.ollama.yml up -d
   
   # Wait for Ollama to be ready, then start n8n services
   docker-compose -f docker-compose.others.yml up -d
   
   # Finally, start the WebUI
   docker-compose -f docker-compose.webui.yml up -d
   ```

## Stopping Services

To stop all services:
```bash
docker-compose -f docker-compose.webui.yml down
docker-compose -f docker-compose.ollama.yml down
docker-compose -f docker-compose.others.yml down
```

## Environment Variables

Make sure to set the required environment variables in a `.env` file:
- POSTGRES_USER
- POSTGRES_PASSWORD
- POSTGRES_DB
- N8N_ENCRYPTION_KEY
- N8N_USER_MANAGEMENT_JWT_SECRET
- N8N_DEFAULT_BINARY_DATA_MODE
- QDRANT__SERVICE__API_KEY
- WEBUI_SECRET_KEY
- OLLAMA_HOST (optional, defaults to ollama-gpu:11434)

## Service Dependencies

- open-webui depends on ollama-gpu
- n8n and n8n-import depend on postgres
- n8n depends on n8n-import
- ollama-pull-llama-gpu depends on ollama-gpu

All services communicate through the shared `ai-stack-network` network.
