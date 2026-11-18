# 06. Launch, Observability & Customer Support Loop Playbook

## 1. Trigger & Scope
- **Load When:** Preparing a production release, configuring CI/CD, adding logging/metrics/alerts, verifying a live deployment, or triaging customer support tickets and production bugs.
- **Skip When:** Early local prototyping prior to production readiness.

## 2. Researched Best Practices (Core Standards)
1. **Automated Pre-Flight & Release Gates:** Every release must pass typechecking, linting, unit/integration tests, and build verification in CI before merge. Maintain a rollback path (or feature flag kill-switch) for every high-risk change.
2. **Structured RED + Business Telemetry:** Emit structured JSON logs with a correlation `requestId` and `tenantId`/`userId` (without PII). Track Rate, Errors, and Duration (RED metrics) on critical user flows (signup, core action, checkout) plus token/latency metrics on any LLM calls.
3. **Post-Deploy Canary Verification:** Never treat "CI green" as "production healthy." Inspect live production routes, console errors, and error rates immediately after deploy.
4. **The Support-to-Scar-Tissue Loop:** Every customer-reported bug or production incident follows a strict 4-step closure:
   1. Reproduce and diagnose root cause (`diagnosing-bugs`).
   2. Write a failing automated regression test (`tdd`) that proves the bug.
   3. Ship the minimal fix and verify in production.
   4. Append a 1-line preventive rule to the relevant playbook's **Scar-Tissue Log** (and update docs via `gstack-document-release`) so the agent never re-introduces that class of bug.

## 3. Hard Bans
- **NO** deploying to production with failing tests, skipped typechecks, or unverified destructive migrations.
- **NO** unstructured `console.log("here")` debugging left in production code or logging raw tokens/passwords/PII.
- **NO** closing a customer bug report with a code patch alone—every bug fix must include a regression test.

## 4. Antigravity Execution Loop (Skills & Subagents)
1. **Instrument:** Load `observability-and-instrumentation` and `ci-cd-and-automation` to wire structured telemetry, health checks, and CI quality gates.
2. **Ship & Canary:** Run `shipping-and-launch` / `gstack-ship` to prepare the release, followed by `gstack-land-and-deploy` and `gstack-canary` to verify live production health.
3. **Support & Triage:** When a bug is reported, invoke `diagnosing-bugs` + `tdd` to reproduce, test, and fix it, then run `/learn` (or `gstack-retro`) to codify the lesson into the playbook.

## 5. Definition of Done (Verification Gate)
- Deployment is live, canary check confirms zero console/5xx regressions on core routes, alerts are active, and any resolved support incident has a corresponding regression test and scar-tissue entry.

## 6. Scar-Tissue Log
- *(Append real production incident and support lessons here via `/learn`)*
