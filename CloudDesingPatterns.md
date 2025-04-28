# Cloud Design Patterns

This document describes two cloud design patterns applied in the project: **External Configuration Store** and **Gateway Aggregation**. Their implementations, advantages, and concrete examples within the system are detailed below.

## 🛠️ External Configuration Store

This pattern is based on externalizing the configuration of services outside the source code, enabling greater flexibility and maintainability.

### 📦 Implementation

It is implemented through the `docker-compose.yaml` file, where environment variables are defined for each service:

```yaml
# Configuration for users-api service
users-api:
  environment:
    - SERVER_PORT=8083
    - JWT_SECRET=PRFT

# Configuration for auth-api service
auth-api:
  environment:
    - ZIPKIN_URL=http://zipkin:9411/api/v2/spans
    - AUTH_API_PORT=8000
    - USERS_API_ADDRESS=http://users-api:8083
    - JWT_SECRET=PRFT

# Configuration for todos-api service
todos-api:
  environment:
    - TODO_API_PORT=8082
    - JWT_SECRET=PRFT
    - REDIS_HOST=redis-queue
    - REDIS_PORT=6379
    - REDIS_CHANNEL=log_channel
```

### ✅ Advantages

- Separation between configuration and code.
- Allows changes to configurations without recompiling or redeploying.
- Supports multiple environments (development, testing, production).
- Facilitates centralized configuration management.

## 🌐 Gateway Aggregation

This pattern involves having a single entry point (frontend) for the client, which distributes requests to the corresponding services, aggregates their responses, and delivers a single response back to the user.

### 📦 Implementation

The frontend is also configured in the `docker-compose.yaml`:

```yaml
frontend:
  environment:
    - AUTH_API_ADDRESS=http://auth-api:8000
    - TODOS_API_ADDRESS=http://todos-api:8082
```

### 🔁 Request Flow

- The client sends a request to the frontend (Vue.js).
- The frontend validates authentication via `auth-api`.
- If authenticated, it fetches task data from `todos-api`.
- It can also retrieve user information from `users-api`.
- The frontend aggregates the information and returns a complete response to the client.

### ✅ Advantages

- The client interacts with a single endpoint.
- Centralizes authentication logic.
- Enables data aggregation from multiple services.
- Improves security by hiding internal architecture.
- Simplifies error handling and response transformation.
