# 🔒 Security Policy

## Supported Versions

| Version | Supported |
|---|---|
| Latest release | ✅ Yes |
| Previous release | ⚠️ Critical fixes only |
| Older versions | ❌ No |

---

## 🐛 Reporting a Vulnerability

**Do not open a public GitHub issue for security vulnerabilities.**

If you discover a security vulnerability in any WE3DS project, please report it privately so we can address it before public disclosure.

### How to Report

**Email:** [info@we3ds.com](mailto:info@we3ds.com)

**Subject line:** `[SECURITY] Brief description of the vulnerability`

**Please include in your report:**

- A clear description of the vulnerability
- The affected project and version
- Step-by-step instructions to reproduce the issue
- Potential impact and severity assessment
- Any proof-of-concept code or screenshots (if applicable)

---

## ⏱️ Response Timeline

| Stage | Timeline |
|---|---|
| **Acknowledgement** | Within 48 hours of report |
| **Initial assessment** | Within 5 business days |
| **Fix or mitigation** | Depends on severity (critical: ASAP, high: within 14 days) |
| **Public disclosure** | Coordinated with the reporter |

---

## 🏆 Recognition

We appreciate responsible disclosure. If you report a valid, previously unknown vulnerability, we will:

- Credit you in the security advisory (unless you prefer to remain anonymous)
- Work with you on coordinated disclosure timing

---

## 🔐 Our Security Practices

For a full description of our internal security standards, see [Security.md](../Security.md).

Key principles:
- Secrets and credentials are never stored in source code
- All authentication uses industry-standard hashing (bcrypt / argon2)
- Dependencies are monitored continuously via Dependabot
- All repositories have GitHub secret scanning enabled

---

*WE3DS — [we3ds.com](https://we3ds.com) · [info@we3ds.com](mailto:info@we3ds.com)*
