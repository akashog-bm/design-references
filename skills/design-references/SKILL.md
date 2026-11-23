---
name: design-references
description: Design reference sheet and borrowed layout, state and motion guidelines. Use before any design or prototype work, or any request to improve an existing design: UI, mockups, landing pages, dashboards, console screens, motion, loading states, uploads, icons, AI or voice indicators, etc. Shortlist matching references and get the user's pick before using any.
---

# Design references

Read `references.md` in this folder. It holds every source, sorted by purpose, with what each one gives, how to pull from it, and the deep links to fetch. `guidelines.md` holds paraphrased rules from Hallmark, Taste Skill and Transitions.dev, sorted by surface. These skills are never installed.

## Workflow

1. **Classify the task.** Work out the surface (landing page, dashboard, agent console, component, motion, loading state, upload) and the stage (finding a direction, structuring a page, building a component, polishing motion).
2. **Match.** Use the "Task → start here" table in `references.md`. Pick 2–4 references that fit. Prefer ones with a machine-readable entry point (llms.txt, JSON index, DESIGN.md, shadcn registry) since you can fetch them directly.
3. **Look before proposing.** Fetch only the relevant deep link (one llms.txt section, one DESIGN.md, one registry search) to confirm it has something useful for this task. Don't load whole libraries.
4. **Stop and ask.** Present the shortlist to the user:
   - name and link
   - what to borrow (a layout, a motion pattern, a token set, a specific component)
   - what it costs (new dependency, paid tier, licence unknown)

   Then wait for their pick. This is a hard gate.
5. **Apply the guidelines.** Read only the matching section of `guidelines.md`: A for console, dashboard or analytics screens, B for landing pages, C for any motion, D for copy, mock data and prototypes. Apply them on top of impeccable; impeccable's craft floor wins any conflict.
6. **Build** only with the references the user approved, through the usual design skill (impeccable, ce-prototype, etc.).

## Hard rules

- No installs before the user picks: no `npm i`, `npx shadcn add`, `npx skills add`, no edits to `components.json`.
- Never install Hallmark, Taste Skill or Transitions.dev or run their scripts. Use `guidelines.md`, and fetch their raw source files only when a rule needs more detail.
- Never fetch paid content (motionprompts paid prompts, Transitions.dev Pro, Saaspo Pro).
- Galleries are for direction, not copying. Take patterns (layout rhythm, hierarchy, type pairing, motion timing). Never reproduce a site's design one-to-one.
- If nothing in the sheet fits, say so and move on. Don't force a reference.
- If a link is dead or the content has changed, tell the user and suggest updating `references.md`.
