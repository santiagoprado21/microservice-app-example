# Branching Strategy for Operations

## 🧩 Strategy Type

**Trunk-Based Development (TBD)**

This strategy also applies to the operations area in this project, as the entire deployment and automation process follows the same approach as development: continuous integration into a single main branch (master), without support or maintenance branches.

---

## 🌳 Branch Structure

- Single main branch: `master`
- Temporary, short-lived branches for `feature/*`
- There are no:
  - Maintenance branches (`maintenance/*`)
  - Support branches (`support/*`)
  - Release branches (`release/*`)
  - Hotfix branches (`hotfix/*`)

---

## ✅ TBD Characteristics Present in Operations

- Frequent integration into `master`
- Short-lived branches focused on a single functionality or fix
- Continuous Deployment (CD)
- Automation through pipelines triggered from `master`
- No parallel maintenance or support branches

---

## 🧾 Evidence in the Codebase

- `cd.yml` defines automatic deployment from `master`
- No maintenance, support, or release branches are observed
- All infrastructure (CI/CD) code is managed from `master`
- Fixes are also handled through `feature/*` branches

---

## 🛠️ Operations Process

1. Create `feature/*` branches if infrastructure or deployment modifications are needed.
2. Integrate changes into `master` via Pull Requests (PRs).
3. If all automated tests pass, deployment is executed automatically.
4. No separate flows for infrastructure or operations: everything lives in the same trunk (`master`).

---

## 🎯 Why Is This Strategy Suitable for Operations?

- It's a **microservices-based project**
- The team is **small**, avoiding unnecessary complexity
- **Frequent and fast deployments** are required
- **Automated testing** is implemented
- No need for support branches or separate maintenance flows
