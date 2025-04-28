# Branching Strategy for Developers

## 🧩 Strategy Type

**Trunk-Based Development (TBD)**

Developers follow a Trunk-Based Development strategy focused on continuous integration, short-lived branches, and rapid deployment.

---

## 🌳 Branch Structure

- Main branch: `master` (production branch)
- Development branches: `feature/*` created from `master`
- Each microservice can have its own `feature/*` branches
- No `develop`, `release`, `hotfix`, or `support` branches

---

## 🔄 Development Flow

1. Create a `feature/feature-name` branch from `master`
2. Develop the functionality
3. Open a Pull Request to `master`
4. Perform code review
5. Run automated tests and CI validations
6. If everything passes, merge into `master`

---

## ⚙️ Continuous Integration

- Each microservice has its own CI pipeline:
  - `auth-api-ci.yml`
  - `frontend-ci.yml`
  - `log-message-processor-ci.yml`
  - `todos-api-ci.yml`
  - `users-api-ci.yml`
- Tests and validations are triggered on each push or PR

---

## 🚀 Deployment

- Automatic deployment is triggered when:
  - Changes are merged into `master`
  - All CI tests pass successfully
  - The central CD pipeline (`cd.yml`) runs successfully

---

## ✅ TBD Characteristics Met

- Frequent integration into `master`
- Short-lived branches
- No parallel maintenance branches
- Automated testing and deployments
- Simple, direct, and efficient workflow

---

## 🎯 Why Is This Strategy Suitable for Developers?

- It's a **microservices project**
- The team is **small**
- **Continuous delivery** is required
- **Test automation** is in place
- Avoids the complexity of flows like Git Flow
