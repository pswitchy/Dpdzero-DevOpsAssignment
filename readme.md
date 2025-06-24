# DevOps Internship Assignment - Nginx Reverse Proxy with Docker

This project sets up a multi-container environment using Docker Compose. It includes two backend microservices (one in Go, one in Python) and an Nginx reverse proxy that routes traffic to them based on the URL path.

## Prerequisites

- Docker
- Docker Compose

## Setup and Running the System

1.  Clone this repository.
2.  Navigate to the project's root directory.
3.  Run the following single command to build the images and start all services:

    ```bash
    docker-compose up --build
    ```

The system will be accessible at `http://localhost:8080`.

## How It Works

- **Docker Compose:** Orchestrates the three services (`service1`, `service2`, `nginx`).
- **Nginx Reverse Proxy:** Acts as the single entry point on `localhost:8080`.
  - Requests to `http://localhost:8080/service1/...` are routed to the Go service.
  - Requests to `http://localhost:8080/service2/...` are routed to the Python service.
- **Networking:** All services are on a Docker bridge network, allowing them to communicate using their service names (e.g., `service1`, `service2`).

## Verifying the Setup

You can test the endpoints using `curl` or your web browser:

- **Test Service 1 (Go):**
  ```bash
  # Ping endpoint
  curl http://localhost:8080/service1/ping
  # Expected output: {"service":"1","status":"ok"}

  # Hello endpoint
  curl http://localhost:8080/service1/hello
  # Expected output: {"message":"Hello from Service 1"}
   ```

- **Test Service 2 (Python):**
   ```bash
   # Ping endpoint
   curl http://localhost:8080/service2/ping
   # Expected output: {"service":"2","status":"ok"}

   # Hello endpoint
   curl http://localhost:8080/service2/hello
   # Expected output: {"message":"Hello from Service 2"}
   ```
- **Check Nginx Logs:**
   You can view the custom-formatted Nginx logs to see successful routing:
   ```bash
   docker logs nginx-proxy
   ```


## Bonus Features Implemented
Health Checks: Both service1 and service2 have health checks configured in docker-compose.yml. Nginx will only start after both backend services report a healthy status.
Logging Clarity: Nginx is configured with a custom log format to include timestamps and request paths for clearer monitoring.
Clean Docker Setup: Used multi-stage builds for the Go service to create a minimal final image and leveraged official uv images for an efficient Python setup.