# 02. Frontend & UI/UX Engineering Playbook

*Synthesized from Dual-Agent Consensus: **Craft Experts** (Emil Kowalski, Rauno Freiberg, Paco Coursey, Linear / Vercel Geist / Stripe / Causal Design Systems, WCAG 2.2 AA) + **AI-Native Practitioners** (`DESIGN.md` contract stack, `gstack` `/design-shotgun` & `/design-review`, Playwright & Chrome DevTools MCP).*

---

## 1. Trigger & Scope
- **Load When:** Creating or modifying frontend screens, UI components, layouts, design tokens, CSS, or motion choreography.
- **Skip When:** Backend-only changes, test-only updates, copy tweaks, or single-token CSS fixes.

## 2. Dual-Agent Consensus Standards (Craft + Practitioner)
1. **Three-Tier Semantic Tokens & Stepped Surface Ladders:** Structure tokens in `DESIGN.md` as `Primitives -> Semantic -> Component` (zero raw hex codes inside components). Build hierarchy using stepped surface luminance and `1px` hairline borders rather than heavy drop-shadow stacks. Restrict chromatic emphasis to one primary interactive accent per view.
2. **Engineered Typography & `tabular-nums` Discipline:** Apply negative tracking (`-0.02em` to `-0.04em`) and tight line-height (`1.0–1.17`) on display headings, `text-wrap: balance` on titles, and mandatory `font-variant-numeric: tabular-nums` on every counter, price, timestamp, grade, and table column so live updates never jitter horizontally.
3. **Divergent Variant Boards Before Boilerplate (`/design-shotgun` & `generative_ui`):** For open-ended screens or layout redesigns, generate 2–3 distinct visual variants on a comparison board before writing production stateful components.
4. **Interruptible Spring / `ease-out` Motion with Strict Latency Budgets:** Animate strictly `transform` and `opacity` using retargetable springs or aggressive deceleration (`cubic-bezier(0.23, 1, 0.32, 1)`). Enforce latency caps: `:active` press (`scale(0.97)`) `<= 160ms`, tooltips/popovers `<= 200ms` (anchored to trigger `transform-origin`, scaling from `0.94`, never `0`), drawers/modals `<= 300ms`. Always honor `prefers-reduced-motion` in both CSS and JS.
5. **WCAG 2.2 AA & Programmatic Live Browser QA:** Bake `:focus-visible` rings (`>= 3:1` contrast), `>= 24x24px` hit targets (SC 2.5.8), `scroll-margin-top` for sticky headers (SC 2.4.11), and explicit empty/loading/error states into primitives. Verify rendered output via `/browser` + Chrome DevTools MCP using computed-style assertions and capped screenshots (`<= 1` per viewport).

## 3. Hard Bans
- **NO** unapproved system blue (`#007AFF`/`#0071E3`), purple/indigo AI gradients, glowing glassmorphism cards, or `border-left: 3px solid` callout boxes.
- **NO** symmetrical 3-column icon-in-circle feature grids or nested card-in-card wrappers.
- **NO** more than one filled primary CTA per screen state, and no vague labels (`"Get Started"`, `"Submit"`).
- **NO** synthetic placeholder copy (`"Student 1"`, `"Item 1"`, `"Lorem ipsum"`, fake `"10k+ users"` badges).
- **NO** `transition: all`, `ease-in` on UI entrances, `scale(0)` popover origins, or routine staggered list animations on frequent tab switches.

## 4. Antigravity Execution Loop (Skills, Subagents & MCPs)
1. **Reference & Spec:** Read the project's `DESIGN.md` (or run `gstack-design-consultation` to create one) plus the active domain overlay (`domains/<category>.md`), and load `frontend-ui-engineering`. Call **Mobbin** or **Figma** MCP only when explicitly requested.
2. **Explore & Build:**
   - Open-ended screen/layout: Preview 2–3 variants via `generative_ui` or `gstack-design-shotgun`.
   - Defined spec: Implement directly in thin slices (`incremental-implementation`).
3. **Verify Live (Capped Token Loop):** Run `/browser` (`browser` subagent) + **Chrome DevTools** MCP + `gstack-design-review` on `localhost` (`375px`, `768px`, `1440px`), checking computed styles, keyboard focus, `prefers-reduced-motion`, and zero console errors. Commit atomic `style(design):` fixes if issues are found.

## 5. Definition of Done (Verification Gate)
- Zero raw hex values in components, `tabular-nums` on all dynamic numbers, all 5 UI states implemented (empty, loading, error, hover, focus-visible), WCAG 2.2 AA target/contrast checks pass, and live browser check shows zero console/layout regressions.

## 6. Scar-Tissue Log
- *(Append real UI/UX lessons here via `/learn`)*
