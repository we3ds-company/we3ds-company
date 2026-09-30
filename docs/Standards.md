# 📐 WE3DS Repository Standards

> This document defines the standards every WE3DS repository must follow to ensure consistency, quality, and maintainability across all projects.

---

## 📁 Required Repository Structure

Every WE3DS repository must contain the following files and directories:

```
repository-root/
├── README.md                        # Project overview, setup, and usage
├── LICENSE                          # License file
├── .env.example                     # Environment variable template (no real secrets)
├── .gitignore                       # Git ignore rules
├── CONTRIBUTING.md                  # Contribution guidelines
├── SECURITY.md                      # Security policy and reporting
├── .github/
│   ├── workflows/                   # GitHub Actions CI/CD pipelines
│   ├── ISSUE_TEMPLATE/              # Bug report & feature request templates
│   └── pull_request_template.md    # PR checklist template
├── docs/                            # Extended documentation
└── tests/                           # Test suites
```

---

## 📋 README Standard

Every README must include:

| Section | Description |
|---|---|
| **Project Name & Description** | Clear one-line summary of what the project does |
| **Tech Stack** | Languages, frameworks, and tools used |
| **Prerequisites** | System requirements before setup |
| **Installation** | Step-by-step local setup instructions |
| **Environment Variables** | What `.env` keys are needed and what they mean |
| **Usage** | How to run, test, and build the project |
| **API Reference** | Link to API docs or inline documentation |
| **Contributing** | Link to `CONTRIBUTING.md` |
| **License** | License name and link |

---

## 🌿 Git Workflow

### Branch Strategy

| Branch | Purpose |
|---|---|
| `main` | Production-ready code only |
| `develop` | Integration branch for features |
| `feature/short-description` | New feature development |
| `fix/short-description` | Bug fixes |
| `hotfix/short-description` | Critical production fixes |
| `release/v1.x.x` | Release preparation |
| `chore/short-description` | Maintenance tasks |

### Commit Convention

All commits must follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(scope): short description

[optional body]
[optional footer]
```

**Allowed types:**

| Type | Use For |
|---|---|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation changes |
| `style` | Formatting, no logic change |
| `refactor` | Code restructuring |
| `test` | Adding or updating tests |
| `chore` | Build tools, dependencies |
| `perf` | Performance improvements |
| `ci` | CI/CD configuration changes |

**Examples:**

```
feat(auth): add JWT refresh token support
fix(cart): correct total calculation with discounts
docs(readme): update installation instructions
chore(deps): upgrade Laravel to 11.x
```

---

## 🔀 Pull Request Rules

> [!IMPORTANT]
> No code is merged into `main` or `develop` without a reviewed and approved Pull Request.

**PR Requirements:**

- [ ] Linked to a GitHub Issue
- [ ] Descriptive title following commit convention
- [ ] PR description explains **what** changed and **why**
- [ ] All CI checks pass (lint, tests, build)
- [ ] At least **1 approval** required before merge
- [ ] No unresolved review comments
- [ ] Branch is up to date with target branch

---

## 👁️ Code Review

| Standard | Detail |
|---|---|
| **Turnaround** | Reviews completed within 24 hours |
| **Focus areas** | Logic, security, performance, readability |
| **Tone** | Constructive, specific, and respectful |
| **Blocking** | Only block for correctness or security issues |
| **Suggestions** | Label non-blocking comments as `nit:` |

---

## 🧪 Testing

| Level | Expectation |
|---|---|
| **Unit Tests** | All business logic and service methods covered |
| **Feature Tests** | All API endpoints tested |
| **Regression Tests** | Every bug fix has a test to prevent recurrence |
| **CI Gate** | Tests must pass before merge is allowed |

---

## ⚙️ CI/CD Pipeline

Every repository must have a GitHub Actions pipeline that runs on every PR and push to `main`/`develop`:

```
Trigger (PR / Push)
      ↓
Install Dependencies
      ↓
Lint & Static Analysis
      ↓
Run Tests
      ↓
Build Check
      ↓
Security Scan
      ↓
✅ Pass → Allow Merge
❌ Fail → Block Merge
```

---

## 🚀 Deployment

| Environment | Branch | Trigger |
|---|---|---|
| **Production** | `main` | Manual approval after CI |
| **Staging** | `develop` | Auto-deploy on merge |
| **Preview** | `feature/*` | Optional per-PR previews |

---

*Last updated: 2024 · WE3DS Engineering*
