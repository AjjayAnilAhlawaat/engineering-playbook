# The End-to-End Playbook Framework

Every playbook in `playbooks/` follows an identical 6-part structure so both humans and AI agents can scan, execute, and update it without ambiguity or context bloat.

## Why This Framework Exists

1. **Zero Context Tax (Progressive Disclosure):** Root `AGENTS.md` stays under 25 lines. An agent fixing a PostgreSQL migration loads only `04-backend-and-data.md` and never wastes tokens on CSS or pricing rules.
2. **Research-Backed Defaults:** Each playbook distills proven industry frameworks (Matt Pocock's `skills`, Garry Tan's `gstack`, John Ousterhout's *A Philosophy of Software Design*, April Dunford's *Obviously Awesome*, and Google SRE / OpenTelemetry standards) into concrete checklists.
3. **Full Lifecycle Coverage:** Covers the entire arc from raw idea validation to writing code, packaging/selling the product, and supporting live customers.

---

## The 6-Part Module Template

Every playbook in `playbooks/01-*.md` through `06-*.md` is structured with these six sections:

### 1. Trigger & Scope
- **Load When:** Exact task types or file patterns that require reading the playbook.
- **Skip When:** Tasks that must bypass the playbook to keep small edits fast.

### 2. Researched Best Practices (Core Standards)
- 4 to 6 concrete, non-negotiable standards backed by primary engineering/product sources.
- Written as imperative rules with measurable thresholds (not vague advice).

### 3. Hard Bans (Anti-Slop & Anti-Fragility Guardrails)
- Explicit patterns the agent is forbidden from generating (e.g., building features before writing a spec, unvalidated `req.body`, `transition: all`, or generic AI marketing fluff).

### 4. Antigravity Execution Loop (Skills, Subagents & MCPs)
- The exact sequence of built-in subagents (`research`, `browser`, `code-reviewer`, `security-auditor`, `test-engineer`), skills, and MCP tools to invoke at that phase.

### 5. Definition of Done (Verification Gate)
- The concrete artifact or runtime proof required before moving to the next phase (e.g., approved spec file, live localhost browser screenshot, passing contract test, verified Stripe webhook, canary check).

### 6. Scar-Tissue Log (Continuous Learning)
- When a mistake happens in production or during review, append a 1-line rule here (or run `/learn`) so the agent never repeats that failure mode across any future project.
