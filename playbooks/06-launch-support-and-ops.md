# 06. Launch, Observability & Customer Support Loop Playbook

*Synthesized from Dual-Agent Consensus: **Craft Experts** (Charity Majors / Honeycomb Wide-Event Observability, Google SRE RED/USE & Multi-Window Burn-Rate Alerting, Progressive Delivery) + **AI-Native Practitioners** (`gstack-ship`, `gstack-land-and-deploy`, `gstack-canary`, EvalOps Golden Datasets, "Rule of 3" Scar-Tissue Promotion Ladder).*

---

## 1. Trigger & Scope
- **Load When:** Preparing a production release, configuring CI/CD, adding logging/metrics/alerts, verifying a live deployment, running LLM evals, or triaging customer support tickets and production incidents.
- **Skip When:** Early local exploration prior to staging/production integration.

## 2. Dual-Agent Consensus Standards (Craft + Practitioner)
1. **Observability-Driven Development via Wide Structured Events (Honeycomb + OpenTelemetry):** Emit one wide, structured JSON/OTel event per service hop containing high-cardinality context (`trace_id`, `request_id`, `tenant_id`, `user_id`, active feature flags, DB duration, error code, and LLM model/token/latency metadata) with automated PII/secret redaction. Surface a copyable `request_id` in user-facing error UI so support tickets link directly to traces.
2. **SLO Error Budgets & Multi-Window Burn-Rate Alerts (Google SRE):** Track service **RED** (Rate, Errors, p50/p95/p99 Duration) and infrastructure **USE** (Utilization, Saturation, Errors) metrics anchored to explicit 30-day SLOs. Page humans only on multi-window error-budget burn rates (e.g., `14.4x` fast burn over 1h/5m) with a linked remediation runbook—never on brief 1-minute spikes or non-user-impacting CPU fluctuations.
3. **Evidence-Bound Release & Exact-SHA Progressive Canary (`gstack-ship` + `gstack-canary`):** Merge `origin/<base>` before testing, enforce non-zero test execution (`tests_ran > 0`) and golden LLM eval gates (`evals/golden_dataset.jsonl` when prompts/agent code change), and verify live deployment by matching exact `MERGE_SHA`. Supplement static CI golden datasets with stratified production trace sampling (5–10% live traffic + 100% of thumbs-down and tool-exception traces) and distributional drift alerts so sanitized production failures continuously feed the CI golden set. Run a 10-minute post-deploy canary loop diffing console errors, p95 load time (`< 2x` baseline), 404s, and screenshots against the pre-deploy baseline, backed by runtime feature-flag kill switches.
4. **Test-First Support Triage (`diagnosing-bugs` + EvalOps):** Never patch production bugs from guesswork. First commit an isolated reproduction test (or failing LLM trace in `golden_dataset.jsonl`) that fails on `HEAD` and passes after the fix (`regression_proof`). During SEV-1/2 incidents, restore service first via feature-flag kill switch or `git revert` before root-causing.
5. **The "Rule of 3" Scar-Tissue Promotion Ladder (`gstack-learn` + `gstack-retro`):** Prevent `AGENTS.md` from rotting into a 1,000-line wall of warnings:
   - *1st occurrence:* Fix root cause in the shared module + commit a regression test and log to `learnings.jsonl`.
   - *2nd occurrence:* Tighten the relevant phase/domain playbook checklist (`playbooks/*.md` or `domains/*.md`).
   - *3rd occurrence (or high-severity invariant):* Convert the rule into a **deterministic mechanical check** (ESLint/AST rule, pre-commit hook, schema constraint, or CI test) so the mistake becomes impossible to merge.

## 3. Hard Bans
- **NO** unstructured `console.log`/`print` debugging in production or logging raw tokens, API keys, or PII.
- **NO** inferring deploy success from PR merge or HTTP 200 without verifying the live `MERGE_SHA` and baseline-diffed canary check.
- **NO** paging on-call engineers without an SLO burn-rate condition and a linked runbook.
- **NO** closing a customer bug or LLM failure without an automated regression test or golden eval case.
- **NO** bloating root `AGENTS.md` with one-off incident prose when a mechanical lint/test check or scoped playbook entry belongs instead.

## 4. Antigravity Execution Loop (Skills & Subagents)
1. **Instrument & Gate:** Load `observability-and-instrumentation` and `ci-cd-and-automation` to wire wide OTel events, `request_id` error surfaces, and CI gates.
2. **Ship & Verify Live:** Run `shipping-and-launch` / `gstack-ship` -> `gstack-land-and-deploy` -> `gstack-canary` (plus active `domains/<category>.md` ops rules).
3. **Support Incident Closure:** Run `diagnosing-bugs` + `tdd` to reproduce and fix customer issues, then run `/learn` and `gstack-retro` to promote recurring patterns up the Rule-of-3 ladder.

## 5. Definition of Done (Verification Gate)
- Exact `MERGE_SHA` is live, 10-minute `gstack-canary` pass shows zero new console/5xx/latency regressions against baseline, wide OTel events with `request_id` are verified, and every resolved support issue has a committed regression test + scar-tissue classification.

## 6. Scar-Tissue Log
- *(Append real launch, observability, and support lessons here via `/learn`)*
