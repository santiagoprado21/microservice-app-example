# Branching Strategy for Developers

## 🧩 Strategy Type

**Simplified Git Flow + Trunk-Based Practices**

Developers follow a simplified Git Flow, incorporating Trunk-Based Development principles, focused on continuous integration, short-lived branches, and controlled deployments.

---

## 🌳 Branch Structure

- Main branches:
  - `master` (production-ready, stable releases)
  - `dev` (integration and staging branch)
- Development branches:
  - `feature/*` created from `dev`
- No `release/*`, `hotfix/*`, or `support/*` branches

---

## 🔄 Development Flow

1. Create a `feature/feature-name` branch from `dev`
2. Develop the functionality
3. Open a Pull Request (PR) into `dev`
4. Perform code review
5. Run automated tests and CI validations
6. If everything passes, merge into `dev`
7. When `dev` is stable and tested, open a PR into `master`
8. Merge into `master` to create a new production release

---

## ⚙️ Continuous Integration

- Each microservice has its own CI pipeline:
  - `auth-api-ci.yml`
  - `frontend-ci.yml`
  - `log-message-processor-ci.yml`
  - `todos-api-ci.yml`
  - `users-api-ci.yml`
- CI pipelines are triggered on every push or PR to `dev`
- On merge to `dev`:
  - Build Docker image
  - Validate build and tests
  - Push Docker image with a random tag to Azure Container Registry (ACR)
- On merge to `master`:
  - Build Docker image
  - Push Docker image with the `latest` tag to ACR

---

## 🚀 Deployment

- A deployment pipeline (`cd.yml`) runs automatically when a microservice pipeline completes successfully.
- The deployment pipeline:
  - Connects via SSH to an Azure Virtual Machine (VM)
  - Executes a deployment script using Docker Compose
  - Pulls the updated images and restarts the services

---

## ✅ Strategy Characteristics

- Frequent integration into `dev`
- Short-lived feature branches
- Controlled promotion from `dev` to `master`
- Automated testing and deployments
- Simple and efficient workflow, adapted for microservices

---

## 🎯 Why Is This Strategy Suitable for Developers?

- It's a **microservices-based project**
- The team is **small**
- **Continuous integration and delivery** are required
- **Test automation** and **automated deployments** are in place
- Reduces complexity while maintaining release stability
