# Domain Category 01: Education, EdTech & AI Tutoring Overlay

*Synthesized from Dual-Agent Consensus: **Craft Experts** (Desmos / Eli Luberoff, Math Academy / Justin Skycak, Brilliant, Khan Academy / Khanmigo, Duolingo Learning Engineering, Causal studio principles) + **EdTech Practitioners** (KaTeX streaming, OpenCV + Mathpix + SymPy AST grading, COPPA/FERPA multi-role RBAC).*

Load this domain overlay alongside the active lifecycle playbook (`playbooks/01..06`) whenever building an education, tutoring, or learning application (such as `loveformaths`).

---

## Phase 01: Brainstorming & Pedagogical Spec
- **Consensus Standards:**
  - **Split-Stakeholder Value Prop:** Explicitly separate the **Buyer** (parent/school seeking measurable grade/mastery outcomes), the **User** (student needing low-intimidation, high-agency entry), and the **Operator** (tutor/teacher needing fast prep and post-session evidence review).
  - **Pedagogy as Systems Engineering (Math Academy / Desmos):** Design around worked examples, micro-scaffolding, and "low floor, high ceiling" tasks. Decide upfront whether software is used *live in class* or in a *Prep-then-Capture rhythm* (pre-session prep + post-session handwritten evidence review).
- **Hard Bans:**
  - **NO** passive walls of text/video without active retrieval or physical workbook action.
  - **NO** single-persona specs that conflate parent buyer motivations with student UX.

## Phase 02: Frontend & Tactile Classroom UI/UX
- **Consensus Standards:**
  - **Intrinsic Object Shapes Over SaaS Dashboards:** Model UI objects after real learning artifacts—wide ruled briefing sheets, compact pending pupil slips, and natural-aspect handwritten workbook prints (`love_for_maths_design_and_motion_specification.md`).
  - **Stream-Safe Math & Direct Manipulation (KaTeX + 60fps):** Render mathematical notation with **KaTeX** (`tabular-nums` for scores/timestamps) using a stream-buffer parser that holds unclosed `$$`/`\(` delimiters so partial LaTeX never flashes raw code.
  - **Effort-Calibrated Progress:** Tie progress indicators to verified mastery and cognitive work—never time-on-page.
- **Hard Bans:**
  - **NO** superficial gamification slop (confetti bursts, noisy badges, cartoon streaks) during problem solving.
  - **NO** 3-column symmetrical placeholder student grids or synthetic `"Student 1"` / `"No snap yet"` copy.

## Phase 03: Middleware, Student Privacy (COPPA/FERPA) & Role APIs
- **Consensus Standards:**
  - **Four-Role RBAC + `ParentChild` Consent Bridge:** Enforce strict server-side boundaries across `Student`, `Tutor/Teacher`, `Parent/Guardian`, and `TenantAdmin`. Validate parent reads against a verified `ParentChild` bridge table (blocking IDOR on `studentId`).
  - **Zero-Retention Minor Privacy (COPPA 2026 / FERPA / GDPR-K):** Strip third-party ad/behavioral trackers on student routes. Enforce a published written deletion schedule prohibiting indefinite storage of minor records, treat voiceprints/faceprints as protected biometric PI (FTC COPPA Rule § 312.10), require written zero-training/security assurances from OCR/LLM vendors, and obtain separate verifiable parental consent for any non-operational third-party disclosures.
  - **Direct Presigned Evidence Uploads:** Upload handwritten homework photos via short-lived presigned storage URLs partitioned by `/tenant_id/pod_id/student_id/` and process OCR asynchronously on background queues.
- **Hard Bans:**
  - **NO** synchronous OCR/vision grading inside the HTTP request thread (causes mobile upload timeouts).
  - **NO** sending unredacted student PII or unconsented minor records to consumer LLM endpoints.

## Phase 04: Backend, Mastery Graph & Symbolic Verification
- **Consensus Standards:**
  - **Three-Stage Handwritten Math Pipeline (OpenCV -> OCR -> Symbolic AST + Tutor Override):** Deskew/binarize photo uploads, extract structured LaTeX + bounding boxes via Math OCR/Vision, and verify algebraic equivalence deterministically via `SymPy`/`mathjs` AST—always exposing a **1-click Tutor Override** for misread handwriting.
  - **Directed Prerequisite Knowledge Graph & Implicit Spaced Repetition:** Model concepts as dependency-linked nodes. Credit underlying prerequisite nodes when a student demonstrates mastery on an advanced problem to prevent review-queue fatigue.
  - **Multi-Layer Socratic Guardrails:** Prevent AI tutors from leaking final answers using prompt constraints + a mid-stream AST/regex verifier that aborts answer leaks and substitutes a Socratic step hint.
- **Hard Bans:**
  - **NO** raw LLM vision-only math grading without symbolic verification or tutor override.
  - **NO** stateless chat loops that let students badger the LLM into giving away the final answer.

## Phase 05: Positioning, Parent/Tutor GTM & Pricing
- **Consensus Standards:**
  - **Dual-Track Onboarding (TTFL < 48h):** Route parents to billing/goal setup and students straight to a low-stress diagnostic or first pod worksheet. Anchor subscription pricing against hourly human tutoring rates.
  - **Parent Proof-of-Value Digests:** Send automated post-session/weekly digests to the paying parent showing annotated handwritten work and concrete misconceptions resolved.
- **Hard Bans:**
  - **NO** forcing paying parents to complete student placement quizzes during checkout.
  - **NO** paywalling core tutor preparation tools needed for organic pod/classroom adoption.

## Phase 06: Classroom-Safe Launch, Ops & Anti-Churn Loop
- **Consensus Standards:**
  - **School/Tutoring Hours Release Freeze:** Never run breaking deployments or heavy DB migrations during peak tutoring/classroom hours.
  - **Default Anonymization on Shared Views:** Provide 1-click pupil name anonymization when tutors project or share work samples.
  - **Academic Calendar Pause Deflection:** Offer 1-click term-break/summer pause and tutor-swap flows inside the cancel funnel to beat seasonal EdTech churn.
- **Hard Bans:**
  - **NO** year-round B2B hard-cancel-only flows that ignore school holidays and exam cycles.
