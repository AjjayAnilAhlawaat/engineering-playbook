# 05. Positioning, Marketing, Pricing & Selling (GTM) Playbook

*Synthesized from Dual-Agent Consensus: **Craft Experts** (April Dunford's *Obviously Awesome* & *Sales Pitch*, Madhavan Ramanujam's *Monetizing Innovation*, Elena Verna's PLG / Product-Led Sales) + **AI-Native Practitioners** (Stack-Specific Hero Copy, Interactive Demos, Fast-Ack Idempotent Billing & Entitlement Pipelines).*

---

## 1. Trigger & Scope
- **Load When:** Defining product positioning, writing landing page or launch copy, structuring pricing tiers, wiring Stripe/Paddle/Lemon Squeezy checkout & webhooks, or designing PLG onboarding and sales discovery flows.
- **Skip When:** Pure internal engineering refactors with no customer, pricing, or onboarding surface.

## 2. Dual-Agent Consensus Standards (Craft + Practitioner)
1. **Competitive-Alternatives-First Positioning (`POSITIONING.md` — April Dunford):** Never pick a market category or write taglines first. Lock down in order:
   1. *Competitive Alternatives:* What users do today if you didn't exist (spreadsheets, WhatsApp, manual scripts, doing nothing).
   2. *Unique Attributes:* Specific mechanics your product has that those alternatives lack.
   3. *Value Themes (1–4):* Concrete, measurable customer outcomes (*"so what?"*).
   4. *Best-Fit ICP:* The exact buyer segment that feels the pain most acutely and converts fastest.
   5. *Market Category:* The frame of reference that makes your differentiated value obvious within 3 seconds.
2. **Above-the-Fold Mechanism + Interactive Proof (Zero AI Slop):** Use the formula `[What you do] + [for whom/stack] + [without the status-quo pain]`. Embed a live interactive sandbox, real workflow artifact, or unedited 10-second product clip in the hero so visitors experience the core loop unauthenticated in 3 clicks before a 1-click OAuth prompt.
3. **WTP-Validated Value-Metric Packaging (*Monetizing Innovation*):** Price on the **value metric** that scales with customer success (pods, active seats, runs, orders)—never cost-plus guesswork. Offer 3 transparent tiers (**Free/Starter** with core value unlocked, **Pro/Growth** as the 70% default sweet spot, **Team/Enterprise** gating governance/SSO/SLAs) audited against *Feature Shocks*, *Minivations*, and *Hidden Gems*.
4. **Zero-Form Onboarding & PQA-Triggered Sales (Elena Verna):** Strip upfront credit card walls and multi-step intake surveys; ship pre-populated template/sample data so new users never land on an empty screen and reach **Time-to-First-Value (TTFV) in `< 3 minutes`** (and `< 3 hours` for full integration). Trigger founder/sales outreach from **Product-Qualified Account (PQA)** usage signals using Dunford's **8-Step Decision-Story Pitch** (Market Insight -> Alternatives -> Perfect World -> Solution Intro at Step 4 -> Differentiated Value -> Proof -> Objections -> Low-Risk CTA).
5. **Fast-Ack, Idempotent Billing & Entitlement Reconciliation:** Verify webhook HMAC signatures on raw bytes (`< 500ms` `200 OK` ack), deduplicate `event.id` in a `processed_webhooks` table with `last_event_timestamp` ordering guards, gate access on `payment_status === 'paid'` (handling async SEPA/ACH), poll with synchronous API fallback on `success_url` redirect to prevent the *"paid user sees Free Tier"* race condition, and run a daily entitlement reconciliation cron.

## 3. Hard Bans
- **NO** AI-slop marketing copy (*"In today's fast-paced world"*, *"Empower/Supercharge/Revolutionize"*, interchangeable headlines, tricolon fluff, or fake *"Alex M., Founder"* testimonials). Enforce `no-ai-slop` on 100% of copy.
- **NO** opening a sales pitch or landing page with company history or generic feature lists before framing status-quo alternatives.
- **NO** multi-field signup questionnaires before delivering first product value.
- **NO** unlocking paid entitlements from client-side `?success=true` query params, out-of-order webhook overwrites, or unverified `checkout.session.completed` events where `payment_status !== 'paid'`.

## 4. Antigravity Execution Loop (Skills & Subagents)
1. **Lock Positioning & Pricing:** Run `interview-me` + `no-ai-slop` (plus active `domains/<category>.md`) to write `POSITIONING.md` (Dunford's 5 steps + Ramanujam value-metric tiers + 8-step pitch).
2. **Build Conversion & Checkout Surface:** Use `gstack-design-shotgun`, `frontend-ui-engineering`, and `gstack-design-motion` to build the evidence-led landing page, interactive hero preview, and idempotent billing webhook pipeline.
3. **Live Funnel & TTFV Audit:** Run `gstack-devex-review` and `/browser` to time the live signup-to-first-value flow (`< 3 min` target) and run the 6-test billing webhook replay/race matrix.

## 5. Definition of Done (Verification Gate)
- `POSITIONING.md` is approved, landing copy passes the 3-second clarity test and `no-ai-slop` audit, live onboarding hits first value in `< 3 minutes` with zero empty-state dead ends, and billing webhooks pass HMAC, replay, out-of-order, and redirect-race integration tests.

## 6. Scar-Tissue Log
- *(Append real positioning, conversion, pricing, and billing lessons here via `/learn`)*
