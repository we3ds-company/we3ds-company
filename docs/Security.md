# 🔒 WE3DS Security Standards

> Security is not a final step — it is integrated throughout every stage of development at WE3DS. This document defines the security standards every project must follow.

---

## 🚨 Critical Rule: No Secrets in Code

> [!CAUTION]
> Never commit secrets, credentials, API keys, or passwords to any repository — public or private.

**What must NEVER appear in code or git history:**

```bash
# ❌ NEVER commit these values
.env                     # Real environment files
API_KEY=sk-...
DB_PASSWORD=...
STRIPE_SECRET_KEY=...
AWS_SECRET_ACCESS_KEY=...
JWT_SECRET=...
SMTP_PASSWORD=...
```

**Correct approach:**

```bash
# ✅ Always use .env.example with placeholder values only
DB_PASSWORD=             # Leave empty or use placeholder
STRIPE_SECRET_KEY=       # Set in deployment environment
AWS_SECRET_ACCESS_KEY=   # Injected via CI/CD secrets
```

> [!TIP]
> If a secret is accidentally committed, treat it as compromised immediately — revoke and rotate it, even if the commit was "private".

---

## 🔑 Authentication

| Standard | Requirement |
|---|---|
| **Password hashing** | Use `bcrypt` or `argon2` — never MD5 or SHA1 |
| **Token storage** | JWTs stored in `httpOnly` cookies, not `localStorage` |
| **Token expiry** | Access tokens expire in short intervals (15–60 min) |
| **Refresh tokens** | Implement refresh token rotation |
| **Login attempts** | Rate limit and lock accounts after repeated failures |
| **MFA** | Offer multi-factor authentication for sensitive systems |
| **Session handling** | Invalidate sessions on logout and password change |

---

## 🛡️ Authorization

| Standard | Requirement |
|---|---|
| **Check before act** | Authorization verified before any data access or modification |
| **Ownership** | Users can only read/write their own resources |
| **Role-based access** | Permissions defined by roles, enforced at service layer |
| **Fail closed** | Deny by default — access must be explicitly granted |
| **No client-side control** | Never rely on frontend to enforce authorization |

---

## 🌐 API Security

- [ ] All API endpoints require authentication unless explicitly public
- [ ] Rate limiting applied on all endpoints (especially auth routes)
- [ ] API keys scoped to minimum required permissions
- [ ] Sensitive operations (delete, payment) require re-verification
- [ ] API versioning used — breaking changes in new versions only
- [ ] Error responses do not reveal stack traces or system internals

---

## 🗄️ Database Security

- [ ] All queries use parameterized statements — no string concatenation
- [ ] Database user has minimum required permissions (no root access)
- [ ] Database is not publicly accessible (firewall / VPC)
- [ ] Sensitive fields (passwords, PII) are encrypted at rest
- [ ] Database backups are encrypted and tested regularly

```php
// ❌ SQL Injection vulnerability
DB::select("SELECT * FROM users WHERE email = '$email'");

// ✅ Parameterized query
DB::select('SELECT * FROM users WHERE email = ?', [$email]);
```

---

## 🌍 CORS

- [ ] CORS is configured explicitly — not set to allow all origins (`*`) in production
- [ ] Only known, trusted domains are whitelisted
- [ ] Credentials (`withCredentials`) only allowed for necessary origins

---

## 🛡️ CSRF

- [ ] CSRF protection enabled on all state-changing routes (POST, PUT, DELETE, PATCH)
- [ ] SPA frontends use CSRF token headers correctly
- [ ] APIs using stateless JWT are exempt (CSRF tokens not needed for token-based auth)

---

## ⏱️ Rate Limiting

| Endpoint Type | Limit |
|---|---|
| **Login / Register** | 5 attempts per minute per IP |
| **Password reset** | 3 attempts per 15 minutes |
| **General API** | 60 requests per minute per user |
| **Public endpoints** | 30 requests per minute per IP |

---

## 📁 File Uploads

- [ ] Validate file type by MIME type, not just extension
- [ ] Enforce maximum file size limits
- [ ] Store uploaded files outside the web root (not publicly accessible by default)
- [ ] Rename files on upload — never use user-provided filenames
- [ ] Scan uploads for malware where applicable

---

## 💳 Payment Integrations

- [ ] Never store raw card data — use tokenization (Stripe, PayTabs, etc.)
- [ ] Webhook signatures verified before processing
- [ ] Payment secrets never logged
- [ ] All payment flows tested in sandbox before production

---

## ⚙️ Infrastructure & DevOps Security

| Area | Standard |
|---|---|
| **Environment variables** | Set via CI/CD secrets — never hardcoded |
| **GitHub Actions** | Use pinned action versions (`@sha` not `@latest`) |
| **Docker** | Run as non-root user inside containers |
| **Production config** | Debug mode disabled, detailed errors off |
| **Dependencies** | Dependabot enabled, vulnerabilities fixed promptly |
| **Secret scanning** | GitHub secret scanning enabled on all repos |

---

## 📋 Security Checklist (Pre-deployment)

- [ ] No secrets in code or environment files committed
- [ ] Authentication and authorization tested
- [ ] Rate limiting configured and tested
- [ ] CORS restricted to known origins
- [ ] Error responses do not leak system information
- [ ] All dependencies scanned for vulnerabilities
- [ ] File upload validation in place
- [ ] Payment webhook signatures verified
- [ ] Database access follows principle of least privilege
- [ ] Logging captures security events without logging sensitive data

---

## 🐛 Reporting Security Issues

If you discover a security vulnerability in a WE3DS project, **do not open a public GitHub issue**.

Contact us directly: **[info@we3ds.com](mailto:info@we3ds.com)**

Please include a description of the vulnerability, steps to reproduce, and potential impact.

---

*Last updated: 2024 · WE3DS Engineering*
