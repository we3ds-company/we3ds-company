# 🔄 WE3DS Development Workflow

> This document describes the end-to-end development process followed by all WE3DS projects — from task creation to production deployment.

---

## 🗺️ Workflow Overview

```
📋 Issue Created
      ↓
🌿 Feature Branch Created from develop
      ↓
💻 Development (with local tests)
      ↓
🔀 Pull Request Opened
      ↓
⚙️  CI Pipeline Runs (lint → test → build → security)
      ↓
👁️  Code Review (min. 1 approval)
      ↓
✅ Approved & CI Green
      ↓
🔗 Merged into develop
      ↓
🚀 Auto-deploy to Staging
      ↓
🎯 Manual Approval → Merge to main
      ↓
🏁 Deploy to Production
```

---

## 📋 Step 1 — Issue Creation

Every piece of work starts with a GitHub Issue:

- Use the correct **issue template** (bug report or feature request)
- Add labels: `bug`, `feature`, `enhancement`, `chore`, etc.
- Assign to a milestone if applicable
- Assign to the responsible developer

---

## 🌿 Step 2 — Branch Creation

Create a branch from `develop` following the naming convention:

| Work Type | Branch Name |
|---|---|
| New feature | `feature/user-authentication` |
| Bug fix | `fix/cart-total-calculation` |
| Hotfix | `hotfix/payment-timeout` |
| Maintenance | `chore/upgrade-dependencies` |
| Release | `release/v2.1.0` |

```bash
git checkout develop
git pull origin develop
git checkout -b feature/your-feature-name
```

---

## 💻 Step 3 — Development

During development:

- [ ] Write code that follows the [Code Quality](./Code-Quality.md) standards
- [ ] Write or update tests for new logic
- [ ] Keep commits small and focused (one concern per commit)
- [ ] Use conventional commit messages
- [ ] Run tests locally before pushing

```bash
# Run tests locally before pushing
php artisan test        # Laravel
dotnet test             # ASP.NET Core
npm run test            # Frontend
```

---

## 🔀 Step 4 — Pull Request

When the feature is ready:

- Open a PR from your branch to `develop`
- Fill in the PR template completely
- Link the related issue (`Closes #123`)
- Assign a reviewer
- Add appropriate labels

> [!IMPORTANT]
> Never push directly to `main` or `develop`. All changes go through Pull Requests.

---

## ⚙️ Step 5 — CI Pipeline

GitHub Actions automatically runs on every PR:

| Check | Tool |
|---|---|
| **Linting** | PHP CS Fixer / ESLint / StyleCop |
| **Static Analysis** | PHPStan / Psalm |
| **Tests** | PHPUnit / Jest / xUnit |
| **Build** | Verify project builds without errors |
| **Security Scan** | Dependabot / GitHub secret scanning |

All checks must pass before the PR can be merged.

---

## 👁️ Step 6 — Code Review

| Rule | Detail |
|---|---|
| **Min. approvals** | 1 required; 2 for critical paths |
| **Review scope** | Logic, security, performance, readability |
| **Feedback tone** | Constructive and specific |
| **Resolve all** | All review threads resolved before merge |

---

## ✅ Step 7 — Merge

Once approved and CI is green:

- Merge using **Squash and Merge** (keeps history clean)
- Delete the feature branch after merge
- The issue is automatically closed

---

## 🚀 Step 8 — Deploy

| Stage | Branch | Trigger |
|---|---|---|
| **Staging** | `develop` | Auto-deploy on merge |
| **Production** | `main` | Manual trigger after staging validation |

---

## 🛡️ GitHub Configuration

Every WE3DS repository must be configured with:

| Feature | Setting |
|---|---|
| **Branch Protection** | `main` and `develop` protected, no direct push |
| **Required Reviews** | Minimum 1 approval before merge |
| **Status Checks** | CI must pass before merge |
| **GitHub Actions** | CI/CD pipeline on PRs and main merges |
| **Dependabot** | Automatic dependency update PRs |
| **Secret Scanning** | Enabled on all repositories |
| **Issue Templates** | Bug report + feature request templates |
| **PR Template** | Checklist template for all PRs |

---

*Last updated: 2024 · WE3DS Engineering*
