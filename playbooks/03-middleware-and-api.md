# 03. Middleware, API Contracts & Auth Boundaries Playbook

## 1. Trigger & Scope
- **Load When:** Designing or modifying REST/GraphQL/tRPC/Server Action endpoints, request middleware, authentication/authorization, webhooks, or third-party API integrations.
- **Skip When:** Pure UI styling or internal domain logic with no boundary changes.

## 2. Researched Best Practices (Core Standards)
1. **Contract-First Schema Validation at Every Ingress:** Validate and parse 100% of untrusted inputs (`body`, `query`, `params`, `headers`, webhook payloads) at the boundary using runtime schemas (e.g., Zod, TypeBox, OpenAPI) before passing typed data to domain services.
2. **Explicit Auth & Tenant Isolation in Middleware:** Enforce authentication and tenant/resource-level authorization (RBAC/ABAC) centrally in middleware or guard wrappers—never rely on the frontend hiding a button.
3. **Idempotency & Rate Limiting on Mutations:** All state-mutating and payment/webhook endpoints must enforce rate limiting and support idempotency keys (or deduplication IDs) so network retries never double-charge or duplicate records.
4. **Uniform, Non-Leaking Error Envelopes:** Return structured error responses (`{ error: { code, message, requestId } }`) with accurate HTTP status codes. Log full stack traces internally with `requestId`, but never leak stack traces or raw SQL errors to clients.

## 3. Hard Bans
- **NO** unvalidated `req.body` or `as SomeType` type assertions on external API/webhook payloads.
- **NO** business logic or raw multi-step database transactions inside route handlers/middleware (delegate to deep service modules).
- **NO** secrets, API keys, or PII logged in plaintext or exposed to client bundles.

## 4. Antigravity Execution Loop (Skills & Subagents)
1. **Design Contract:** Load `api-and-interface-design` and `source-driven-development` to define request/response schemas and error codes before writing handler code.
2. **Test Boundary First:** Load `tdd` to write integration tests covering happy path, 400 validation failure, 401/403 auth failure, and idempotency/retry behavior.
3. **Security Audit:** Run `security-auditor` (or `gstack-cso`) on auth, webhook signature verification, and tenant boundary changes.

## 5. Definition of Done (Verification Gate)
- Boundary schemas validate all inputs, unauthorized/malformed requests are rejected with tested status codes, and handler code delegates business rules cleanly to backend services.

## 6. Scar-Tissue Log
- *(Append real API/middleware lessons here via `/learn`)*
