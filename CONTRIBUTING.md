# 🤝 Contributing to WE3DS

Thank you for your interest in contributing to WE3DS projects. This guide explains how we work and what we expect from contributors.

---

## 📋 Before You Start

- Check the existing [Issues](https://github.com/we3ds-company/we3ds-company/issues) to see if your idea or bug is already being tracked
- For major changes, open an issue first to discuss the proposal before writing code
- Read our [Standards](./docs/Standards.md), [Code Quality](./docs/Code-Quality.md), and [Workflow](./docs/Workflow.md) documents

---

## 🌿 Branching

Always branch from `develop`, never from `main`:

```bash
git checkout develop
git pull origin develop
git checkout -b feature/your-feature-name
```

Use the correct branch prefix:

| Type | Prefix |
|---|---|
| New feature | `feature/` |
| Bug fix | `fix/` |
| Documentation | `docs/` |
| Maintenance | `chore/` |

---

## ✍️ Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(scope): short description
fix(scope): short description
docs(scope): short description
```

**Examples:**

```
feat(auth): add password reset flow
fix(cart): resolve total calculation on discount
docs(readme): add installation instructions
```

---

## 🔀 Pull Requests

1. Open a PR from your branch to `develop`
2. Use the PR template — fill it in completely
3. Link the related issue: `Closes #123`
4. Assign a reviewer from the WE3DS team
5. Ensure all CI checks pass before requesting review

> [!IMPORTANT]
> PRs that do not follow this process or fail CI will not be reviewed.

---

## 👁️ Code Review

- Expect a review within **24 hours**
- Address all review comments before the PR can be merged
- Non-blocking suggestions will be prefixed with `nit:`
- Be open to feedback — reviews are about improving the code, not the person

---

## 🧪 Tests

- Write tests for all new functionality
- Run tests locally before pushing:

```bash
php artisan test          # Laravel
dotnet test               # ASP.NET Core
npm run test              # Frontend
```

- Do not submit PRs that break existing tests

---

## 📖 Documentation

- Update relevant documentation when behavior changes
- New APIs must be documented before the PR is merged
- Complex business logic should include inline comments explaining *why*, not *what*

---

## 🔒 Security

- **Never** commit secrets, credentials, or API keys
- If you discover a security vulnerability, **do not open a public issue**
- Report it privately to: [info@we3ds.com](mailto:info@we3ds.com)
- See [SECURITY.md](./.github/SECURITY.md) for our full security policy

---

## 📬 Contact

For questions not covered here, reach out at [info@we3ds.com](mailto:info@we3ds.com).

---

*WE3DS Engineering*
