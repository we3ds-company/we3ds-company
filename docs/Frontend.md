# 🎨 WE3DS Frontend Engineering Standards

> This document defines the frontend development standards followed across all WE3DS projects. These apply to React, Next.js, Angular, and any other frontend framework in use.

---

## 🏗️ Component Architecture

| Rule | Detail |
|---|---|
| **Single Responsibility** | Each component does one thing only |
| **Presentational vs. Container** | Separate UI components from logic/data-fetching components |
| **Reusability** | Extract shared UI into a component library or shared directory |
| **File co-location** | Component, styles, and tests live in the same folder |
| **No God components** | Break large components into smaller, focused ones |

**Recommended structure:**

```
src/
├── components/          # Shared, reusable UI components
│   └── Button/
│       ├── Button.tsx
│       ├── Button.test.tsx
│       └── index.ts
├── features/            # Feature-specific modules
│   └── auth/
│       ├── components/
│       ├── hooks/
│       └── api.ts
├── hooks/               # Shared custom hooks
├── lib/                 # Utilities and helpers
├── types/               # Global TypeScript types
└── pages/ (or app/)     # Route-level pages
```

---

## 🔷 TypeScript

- [ ] TypeScript is **required** on all frontend projects — no `any` without justification
- [ ] All props, function arguments, and return types are explicitly typed
- [ ] API response types are defined and match the backend contract
- [ ] `unknown` is used instead of `any` where type is truly unknown
- [ ] Shared types live in `types/` or are co-located with their feature

```ts
// ❌ Avoid — untyped props
const ProductCard = ({ product }) => { ... }

// ✅ Correct — explicit types
interface ProductCardProps {
  product: Product;
  onAddToCart: (id: number) => void;
}
const ProductCard = ({ product, onAddToCart }: ProductCardProps) => { ... }
```

---

## 🗂️ State Management

| Scope | Approach |
|---|---|
| **Local UI state** | `useState` / `useReducer` |
| **Server data** | React Query / SWR (fetch, cache, sync) |
| **Global app state** | Zustand / Redux Toolkit (only when truly needed) |
| **Form state** | React Hook Form |
| **URL state** | `useSearchParams` / router state |

> [!TIP]
> Before reaching for global state, ask: "Can this be server state managed by React Query?" Most data can be.

---

## 🌐 API Layer

- All API calls go through a **dedicated API module** — never scattered across components
- Use typed response models from the backend contract
- Centralize base URL, headers, and authentication token injection
- Handle errors globally with consistent error types

```ts
// ✅ Centralized API client example
// lib/api.ts
const api = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_URL,
  headers: { 'Content-Type': 'application/json' },
});

api.interceptors.request.use((config) => {
  const token = getToken();
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});
```

---

## 🎨 UI Consistency

- [ ] Design system / component library is established and used consistently
- [ ] No inline styles — use CSS classes, CSS modules, or utility classes
- [ ] Spacing, typography, and color follow a defined design token system
- [ ] No hardcoded hex values — use CSS variables or theme tokens
- [ ] Dark mode / theming support considered from the start

---

## ⚠️ Error Handling

- [ ] API errors are caught and display user-friendly messages
- [ ] Error boundaries used to catch unexpected render errors
- [ ] Form validation errors are displayed inline, next to the field
- [ ] Network errors give users an option to retry
- [ ] 404 and 500 pages are implemented and branded

---

## ⏳ Loading States

Every async operation must have a loading state:

| State | UI Treatment |
|---|---|
| **Loading** | Skeleton, spinner, or shimmer |
| **Empty** | Friendly empty state with call-to-action |
| **Error** | Descriptive error with retry option |
| **Success** | Data rendered cleanly |

---

## ⚡ Performance

| Area | Standard |
|---|---|
| **Code splitting** | Lazy-load routes and large components |
| **Images** | Use `next/image` or equivalent optimized image component |
| **Fonts** | Self-host or use `next/font` — avoid layout shift |
| **Bundle size** | Audit with `next-bundle-analyzer` or similar |
| **Re-renders** | Use `React.memo`, `useMemo`, `useCallback` judiciously |
| **Virtualization** | Use virtual lists for large datasets |

**Core Web Vitals targets:**

| Metric | Target |
|---|---|
| LCP (Largest Contentful Paint) | < 2.5s |
| FID / INP (Interaction) | < 200ms |
| CLS (Cumulative Layout Shift) | < 0.1 |

---

## 🔍 SEO

- [ ] Every page has a unique `<title>` and `<meta name="description">`
- [ ] Proper heading hierarchy: one `<h1>` per page, followed by `<h2>`, `<h3>`
- [ ] Semantic HTML elements used (`<main>`, `<nav>`, `<article>`, `<section>`)
- [ ] Images have descriptive `alt` attributes
- [ ] Open Graph tags set for shareable pages
- [ ] `robots.txt` and `sitemap.xml` configured
- [ ] Canonical URLs set where applicable

---

## ♿ Accessibility (a11y)

- [ ] All interactive elements are keyboard navigable
- [ ] Focus management handled correctly in modals and dialogs
- [ ] Color contrast meets WCAG AA (4.5:1 for normal text)
- [ ] Screen reader labels on all icons and icon-only buttons
- [ ] ARIA attributes used correctly — only when native HTML is not sufficient
- [ ] Forms use `<label>` elements linked to inputs
- [ ] Error messages are announced to screen readers

---

## 📱 Responsive Behavior

- [ ] Designed mobile-first (smallest breakpoint first)
- [ ] Breakpoints consistent with design system
- [ ] Tested on real devices, not only browser resize
- [ ] Touch targets are at least 44×44px
- [ ] No horizontal scroll on any viewport

---

## 🧪 Frontend Testing

| Level | Tool | Coverage |
|---|---|---|
| **Unit tests** | Jest / Vitest | Hooks, utilities, pure functions |
| **Component tests** | React Testing Library | Component behavior from user's perspective |
| **E2E tests** | Playwright / Cypress | Critical user flows |

**Testing principles:**
- Test behavior, not implementation details
- Query by role, label, or text — not by CSS class or test ID
- Avoid snapshot tests for UI that changes frequently

---

*Last updated: 2024 · WE3DS Engineering*
