# 01. Brainstorming, Validation & Executable Spec Playbook

## 1. Trigger & Scope
- **Load When:** Starting a new product, proposing a new feature, rethinking product scope, or turning a rough idea into an actionable spec/ticket.
- **Skip When:** Implementing an already-approved spec or fixing an isolated bug.

## 2. Researched Best Practices (Core Standards)
1. **Interrogate Premises Before Writing Code:** Never jump from a 1-sentence prompt to writing application code. Clarify *who* the target user is, *what painful status-quo workflow* this replaces, and *why* existing alternatives fail.
2. **Define the Narrowest High-Value Wedge:** Identify the 10-star version of the product, then strip scope down to the single core workflow ("the one action") that delivers undeniable value in under 5 minutes.
3. **Lock Edge Cases & Failure Modes Upstream:** Document empty states, permission boundaries, offline/error states, and performance budgets in the spec when changes cost 10 lines of markdown instead of 2,000 lines of refactored code.
4. **Tracer-Bullet Vertical Slices:** Break approved specs into vertical, end-to-end testable slices (UI + API + DB for one thin path) rather than horizontal layers (all DB tables first, all UI last).

## 3. Hard Bans
- **NO** generating production feature code before an explicit spec or plan is agreed upon for multi-file features.
- **NO** silently inventing product requirements when the user's intent has major ambiguities—ask one sharp question at a time.
- **NO** horizontal "big bang" task breakdowns that cannot be verified incrementally.

## 4. Antigravity Execution Loop (Skills & Subagents)
1. **Clarify Intent:** Run `interview-me` or `grilling` (one question at a time) until requirements, target persona, and non-goals are 95% clear.
2. **Diverge & Converge:** Use `idea-refine` and `gstack-plan-ceo-review` to challenge assumptions and pick the scope mode (`SCOPE EXPANSION`, `SELECTIVE EXPANSION`, `HOLD SCOPE`, or `SCOPE REDUCTION`).
3. **Architecture & DX Lock:** Run `gstack-plan-eng-review` (and `gstack-plan-design-review` for UI features) to lock data flows, state machines, and edge cases.
4. **Emit Executable Spec & Slices:** Use `gstack-spec` and `planning-and-task-breakdown` to write the spec under `.scratch/<feature>/` (or `docs/specs/`) and break it into incremental vertical slices.

## 5. Definition of Done (Verification Gate)
- A written spec file exists containing: Problem Statement, Target Persona, Non-Goals, Data/State Model, Edge Cases, and Ordered Vertical Slices with verification criteria.

## 6. Scar-Tissue Log
- *(Append real planning/spec lessons here via `/learn`)*
