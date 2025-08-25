# Commands for Self-Hosted AI Starter Kit

## Prerequisites

- Docker
- Docker Compose

## Getting Started

1.  **Environment Variables:**
    *   Create a `.env` file from the `.env.example` file and populate it with your desired values.

    ```bash
    cp .env.example .env
    ```

2.  **Running the Stack:**

    *   **To run all services:**

        ```bash
        docker-compose -f docker-compose.yml -f docker-compose.ollama.yml -f docker-compose.others.yml -f docker-compose.webui.yml up -d
        ```

    *   **To run only Ollama and WebUI:**

        ```bash
        docker-compose -f docker-compose.yml -f docker-compose.ollama.yml -f docker-compose.webui.yml up -d
        ```

    *   **To run only the "other" services (Postgres, n8n, Qdrant):**

        ```bash
        docker-compose -f docker-compose.yml -f docker-compose.others.yml up -d
        ```

3.  **Stopping the Stack:**

    *   **To stop all services:**

        ```bash
        docker-compose -f docker-compose.yml -f docker-compose.ollama.yml -f docker-compose.others.yml -f docker-compose.webui.yml down
        ```

    *   **To stop only Ollama and WebUI:**

        ```bash
        docker-compose -f docker-compose.yml -f docker-compose.ollama.yml -f docker-compose.webui.yml down
        ```

    *   **To stop only the "other" services:**

        ```bash
        docker-compose -f docker-compose.yml -f docker-compose.others.yml down
        ```
