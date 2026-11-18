# 01. Brainstorming, Problem Validation & Executable Spec Playbook

*Synthesized from Dual-Agent Consensus: **Craft Experts** (Ryan Singer / Shape Up, Marty Cagan / SVPG, Teresa Torres, YC, Linear Method) + **AI-Native Practitioners** (`mattpocock/skills` `/grill-me`, Garry Tan's `gstack` `/office-hours` & `/plan-ceo-review`, GitHub Spec Kit).*

---

## 1. Trigger & Scope
- **Load When:** Starting a new product, proposing a feature, challenging product direction, or turning a rough idea into an approved spec and vertical-slice backlog.
- **Skip When:** Executing an already-approved spec or fixing an isolated bug.

## 2. Dual-Agent Consensus Standards (Craft + Practitioner)
1. **Six Forcing Questions & Hair-on-Fire Demand (YC + `gstack`):** Never accept waitlists, surveys, or polite compliments as validation. Before designing solutions, interrogate:
   - *Demand Reality & Status Quo:* What hacky workaround (spreadsheets, WhatsApp, manual scripts) do users rely on today, and what does it cost them in hours or money?
   - *Desperate Specificity & Narrowest Wedge:* Name the exact user role and the smallest slice shippable in days/weeks that solves the core pain 10x better.
2. **Adversarial Design-Tree Interviewing (`mattpocock/skills` + Teresa Torres):** Map open decisions as a dependency tree. Walk the frontier one question at a time with a recommended default (`-> recommended answer`), while dispatching read-only subagents to gather codebase/domain facts so the human only answers *product decisions*, never lookup trivia.
3. **Fix Appetite, Vary Scope (Shape Up + Linear Method):** Set a fixed time/effort appetite (e.g., 1–2 week batch) and strip scope to fit the budget. De-risk Marty Cagan's **Four Big Risks** (*Value, Usability, Feasibility, Viability*) before writing production code.
4. **Reuse Ladder & Premise Sign-Off (`gstack` + Spec Kit):** Audit existing repo primitives (`Reuse Ladder`: existing helper -> stdlib -> platform API -> installed package) before proposing new architecture. Present explicit `PREMISES` (agree/disagree) and 2–3 `APPROACH A/B/C` options with Effort/Risk/Reuse trade-offs.
5. **1-Page Bounded Spec -> Tracer-Bullet Vertical Slices:** Compile settled decisions into a 1-page spec with explicit **Rabbit Holes** and **No-Gos (Out of Scope)**, then slice into end-to-end vertical tracer bullets (UI + API + DB per slice).

## 3. Hard Bans
- **NO** invoking implementation tools, scaffolding projects, or writing application code before the spec is approved (**Hard Output Gate**).
- **NO** sycophantic hedging (*"That's an interesting approach"*, *"There are many ways to think about this"*); take a concrete position backed by evidence.
- **NO** silent assumption filling (guessing auth, billing, or storage choices without listing an explicit `ASSUMPTIONS I'M MAKING` block).
- **NO** non-binary "vibe-check" acceptance criteria (*"fast dashboard"*, *"robust errors"*) instead of measurable assertions (`LCP < 2.0s`, `400 Bad Request` with RFC 9457 body).
- **NO** horizontal task breakdowns (all DB tables first, all UI last).

## 4. Antigravity Execution Loop (Skills & Subagents)
1. **Grounding & Reuse Check:** Dispatch `research` subagent to inspect existing repo primitives, `GLOSSARY.md`, and relevant domain overlay (`domains/<category>.md`).
2. **Frontier Interview & Premise Challenge:** Run `grilling` or `interview-me` + `idea-refine` to resolve the decision tree and sign off on premises.
3. **Scope & Architecture Lock:** Run `gstack-plan-ceo-review` (pick `SCOPE EXPANSION`, `SELECTIVE EXPANSION`, `HOLD SCOPE`, or `SCOPE REDUCTION`) followed by `gstack-plan-eng-review`.
4. **Emit Spec & Vertical Slices:** Run `gstack-spec` and `planning-and-task-breakdown` to write `.scratch/<feature>/SPEC.md` and stop turn for human sign-off.

## 5. Definition of Done (Verification Gate)
- Approved 1-page `SPEC.md` containing: **Problem & Workaround Evidence**, **Appetite**, **Premises & Chosen Approach**, **Data/State Model**, **Rabbit Holes**, **No-Gos (Out of Scope)**, **Kill/Pivot Metric**, and **Ordered Vertical Tracer Slices**.

## 6. Scar-Tissue Log
- *(Append real planning and product-validation lessons here via `/learn`)*
