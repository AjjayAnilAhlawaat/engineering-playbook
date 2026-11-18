# 02. Frontend & UI/UX Engineering Playbook

## 1. Trigger & Scope
- **Load When:** Creating or modifying frontend screens, UI components, layouts, design tokens, CSS, or motion/animations.
- **Skip When:** Backend-only changes, test-only updates, copy tweaks, or single-token CSS fixes.

## 2. Researched Best Practices (Core Standards)
1. **Design Tokens & Intrinsic Shapes First:** Every project must maintain a markdown design spec (`DESIGN.md` or `*_design_and_motion_specification.md`) defining surface/ink hex tokens, typography hierarchy, spacing scales, and intrinsic object proportions.
2. **Visual Exploration Before Component Boilerplate:** For new screens or open-ended layouts, generate 2–3 lightweight visual options using inline HTML/CSS or a comparison board before writing stateful framework code.
3. **WCAG AA & Keyboard Completeness by Default:** Every interactive element requires visible focus rings, full keyboard navigation, semantic ARIA roles, and explicit loading, empty, error, and populated states.
4. **Composited Motion Only:** Animate strictly `transform` and `opacity` using spring physics (or cubic-bezier tokens) and always honor `prefers-reduced-motion`.
5. **Live Browser Verification Over Source Guessing:** Always inspect the rendered DOM, computed styles, responsive viewports, and console logs on `localhost` before marking UI work complete.

## 3. Hard Bans
- **NO** unapproved system default blue (`#007AFF` / `#0071E3`), generic 3-column symmetrical placeholder card grids, dot-indicator status pills, or sparkle icons.
- **NO** more than one filled primary CTA per screen state.
- **NO** synthetic placeholder copy (`"Student 1"`, `"Item 1"`, `"Lorem ipsum"`).
- **NO** `transition: all` in CSS.

## 4. Antigravity Execution Loop (Skills, Subagents & MCPs)
1. **Reference & Spec:** Read the project's `DESIGN.md` (or run `gstack-design-consultation` if none exists) and load `frontend-ui-engineering`. Call **Mobbin** or **Figma** MCP only when explicitly requested.
2. **Explore & Build:**
   - Open-ended screen/layout: Preview 2–3 options via `generative_ui` or `gstack-design-shotgun`.
   - Defined spec: Implement directly in thin slices (`incremental-implementation`).
3. **Verify Live:** Run the `browser` subagent (`/browser`), **Chrome DevTools** MCP, and `gstack-design-review` against `localhost` to verify layout, responsive breakpoints, and zero console errors. (If blocked by missing local backend/auth, report the blocker once and verify via component tests.)

## 5. Definition of Done (Verification Gate)
- Component passes typecheck/tests, adheres to all `DESIGN.md` hard bans, and has been verified on a live rendered viewport (`localhost`) with zero console errors.

## 6. Scar-Tissue Log
- *(Append real UI/UX lessons here via `/learn`)*
