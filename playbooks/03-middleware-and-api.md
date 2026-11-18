# 03. Middleware, API Contracts & Auth Boundaries Playbook

*Synthesized from Dual-Agent Consensus: **Craft Experts** (Stripe API Design, OWASP API Security Top 10, RFC 9457 Problem Details, Post-CVE-2025-29927 Defense-in-Depth) + **AI-Native Practitioners** (Wrapper-First Route Factories, Contract-First OpenAPI/Zod/TypeBox, Session-Derived BOLA Scoping).*

---

## 1. Trigger & Scope
- **Load When:** Designing or modifying REST/GraphQL/tRPC/Server Action endpoints, edge/framework middleware, authentication/authorization, webhooks, or third-party API integrations.
- **Skip When:** Pure UI styling or internal domain logic with no boundary changes.

## 2. Dual-Agent Consensus Standards (Craft + Practitioner)
1. **Wrapper-First Route Factories & Defense-in-Depth Auth (Never Middleware-Only):** Never rely on edge/Next.js middleware alone as the sole security perimeter (preventing CVE-2025-29927-style header bypasses). Strip untrusted internal headers (`x-middleware-*`, spoofed `x-forwarded-*`) at ingress, and register all endpoints through typed route factories (`createProtectedRoute(schema, handler)`) that re-verify session, role (**BFLA**), and resource ownership (**BOLA**) inside the handler/data boundary.
2. **Strict Allowlist Schema Validation at Every Ingress:** Define schemas in `/contract/openapi.yaml` or colocated Zod (`.strict()`) / TypeBox (`additionalProperties: false`) schemas before writing handler code. Parse `body`, `query`, `params`, and headers at the boundary and pass only validated DTOs to services.
3. **Session-Derived Tenant Scoping (Zero Trust on Request IDs):** Derive `userId`, `tenantId`, and `role` strictly from the verified server session—never from client request bodies or query strings. Every single-record read, update, or delete must include `tenantId`/`userId` in the query predicate (`where: { id, tenantId: session.tenantId }`).
4. **Three-State Idempotency Keys & Multi-Tier Rate Limiting:** Require `Idempotency-Key` headers on state-mutating `POST`/`PATCH` routes, scoped to `(tenant_id, user_id, route, key)` with three states (`in_flight` atomic lock returning `409`/`425`, `completed` 24h response replay, and canonical request payload hash check). Apply burst-capped rate limits (IP + user/tenant) returning `429` with `Retry-After`.
5. **RFC 9457 Problem Details & Raw-Byte Webhook Verification:** Emit uniform `application/problem+json` error envelopes (`type`, `title`, `status`, `detail`, `instance`, plus `X-Request-Id`) with zero stack-trace or SQL leakage. For webhooks, consume raw request bytes before JSON parsing, verify HMAC-SHA256 signatures via `crypto.timingSafeEqual`, enforce replay timestamp tolerances, and deduplicate `event_id` atomically.
6. **Agent & MCP Tool Boundaries (OWASP Agentic / MCP Top 10):** Treat external MCP tool manifests, retrieved text, and runtime tool responses as untrusted data (context isolation). Pin hashed/signed tool schemas against runtime changes, route agent tool calls through deterministic API policy middleware with least-privilege read/write/execute capability grants (never system-prompt-only checks), and block unapproved cross-tool escalation.

## 3. Hard Bans
- **NO** raw framework route handlers bypassing the authenticated/validated route factory, and no `if (!secret) return true` dev fallbacks.
- **NO** bare `findUnique({ where: { id: req.params.id } })` queries on user/tenant resources without session ownership predicates (IDOR/BOLA).
- **NO** passing unvalidated `req.body` or `.passthrough()` schemas into ORM `create`/`update` calls (Mass Assignment).
- **NO** JSON body parsing prior to webhook HMAC verification or using `===` instead of `timingSafeEqual` on signatures.
- **NO** passing unvalidated MCP/tool outputs as trusted system instructions or issuing broad wildcard tokens to external MCP servers.
- **NO** modifying `middleware/`, `webhooks/`, or `contract/` auth rules without explicit human review.

## 4. Antigravity Execution Loop (Skills & Subagents)
1. **Contract First:** Load `api-and-interface-design` and `source-driven-development` to define strict input/output schemas and RFC 9457 error types.
2. **Negative Boundary Test Matrix First (`tdd`):** Write integration tests covering: (a) `401` unauthenticated, (b) `403`/`404` cross-tenant IDOR/BOLA probe, (c) `400`/`422` malformed or unknown field injection, (d) `409`/`400` duplicate or mismatched `Idempotency-Key`, and (e) `401` invalid webhook HMAC.
3. **Security Audit:** Run `security-auditor` (`gstack-cso`) on all auth, webhook, and tenant-scoping diffs.

## 5. Definition of Done (Verification Gate)
- Endpoint is registered via the typed route factory, enforces `.strict()` input/output schemas, scopes all queries by `session.tenantId`, emits RFC 9457 errors with `X-Request-Id`, and passes the 5-case Negative Boundary Test Matrix.

## 6. Scar-Tissue Log
- *(Append real API, auth, and webhook lessons here via `/learn`)*
