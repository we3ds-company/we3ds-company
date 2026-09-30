# ✅ WE3DS Code Quality Standards

> This document defines what "good code" means at WE3DS. These standards apply to all code written, reviewed, and shipped across every project.

---

## 🏗️ Architecture

Every project must follow a clear, layered architecture. Code must not mix concerns.

| Layer | Responsibility |
|---|---|
| **Controllers** | Receive requests, delegate to services, return responses — no business logic |
| **Services** | Core business logic and orchestration |
| **Repositories** | Data access layer — all DB queries live here |
| **Models** | Represent data structures — no business logic |
| **Form Requests** | Input validation and authorization |
| **API Resources** | Shape and format API responses |

> [!TIP]
> If a method is longer than 30 lines, it likely does too much. Break it apart.

---

## 🔍 Code Review Checklist

### Architecture & Structure

- [ ] Business logic lives in Services, not Controllers
- [ ] Database queries are in Repositories, not Services or Controllers
- [ ] Models do not contain business logic
- [ ] Form Requests handle validation — not inline in controllers
- [ ] API Resources format responses — raw models are not returned directly

---

### 🔒 Authentication & Authorization

- [ ] Every route requiring authentication is protected by middleware
- [ ] Authorization is checked before data is accessed or modified
- [ ] Users can only access and modify their own data
- [ ] Role-based access is implemented correctly and consistently

---

### ⚡ Database & Performance

- [ ] No N+1 queries — use eager loading (`with()`, `Include()`)
- [ ] Queries are paginated — no unbounded result sets
- [ ] Indexes exist on columns used in `WHERE`, `ORDER BY`, `JOIN`
- [ ] Heavy operations use queues / background jobs
- [ ] Frequently read data uses caching where appropriate

```php
// ❌ N+1 Problem
$orders = Order::all();
foreach ($orders as $order) {
    echo $order->user->name; // Fires a query per order
}

// ✅ Correct — Eager Loading
$orders = Order::with('user')->get();
```

---

### 🛡️ Security

- [ ] No secrets or credentials in code or version control
- [ ] User input is validated before use
- [ ] SQL queries use parameterized statements — no raw string interpolation
- [ ] API endpoints are rate limited
- [ ] File uploads validate type, size, and are stored outside the web root
- [ ] CORS is configured correctly for the environment
- [ ] CSRF protection is enabled on all state-changing routes

---

### 🚨 Error Handling & Logging

- [ ] All exceptions are caught and handled appropriately
- [ ] Error responses are clear and do not expose internal system details
- [ ] Failures are logged with enough context to debug
- [ ] Log levels are used correctly: `debug`, `info`, `warning`, `error`

```php
// ✅ Correct error handling
try {
    $result = $this->paymentService->charge($amount);
} catch (PaymentFailedException $e) {
    Log::error('Payment failed', ['order_id' => $orderId, 'error' => $e->getMessage()]);
    throw new HttpException(402, 'Payment could not be processed.');
}
```

---

### 🧪 Testing

- [ ] Unit tests cover all service methods and business logic
- [ ] Feature tests cover all API endpoints (happy path + edge cases)
- [ ] Every bug fix includes a regression test
- [ ] Test names are descriptive: `it_calculates_discount_correctly()`
- [ ] Tests do not depend on each other or on external services

---

### 📦 Queues & Background Jobs

- [ ] Long-running operations (emails, reports, imports) are queued
- [ ] Failed jobs are retried with backoff
- [ ] Job failures are logged and monitored
- [ ] Jobs are idempotent — safe to run multiple times

---

### 🗃️ Caching

- [ ] Cache keys are namespaced and descriptive
- [ ] Cache TTLs are appropriate for the data freshness requirements
- [ ] Cache is invalidated when underlying data changes
- [ ] Caching is never used to mask performance problems

---

## 📏 General Code Standards

| Standard | Requirement |
|---|---|
| **Method length** | Max ~30 lines — extract if longer |
| **Class responsibility** | Single Responsibility Principle |
| **Naming** | Clear, descriptive, no abbreviations |
| **Comments** | Explain *why*, not *what* |
| **Dead code** | No commented-out code or unused variables |
| **Dependencies** | Injected, not instantiated inside methods |
| **Magic numbers** | Use named constants, not inline literals |

---

*Last updated: 2024 · WE3DS Engineering*
