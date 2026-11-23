# Design reference sheet

Last checked: 23 Nov 2026. Counts and pricing come from each site on that date and will drift.

## Task → start here

| Task | Look first | Then |
|---|---|---|
| Visual direction for a landing or marketing page | Saaspo (SaaS), Land-book (broad) | awesome-design-md for a brand spec to anchor on |
| Pricing, hero or OG-image section | Saaspo filters (Pricing pages, Hero sections, OG Images) | Land-book Sections |
| Dashboard or console UI | Atlassian llms.txt (tokens, components), aidesign.guide (pick a base system) | shadcnregistry search |
| AI agent or voice-agent UI | Thinking Orbs, `@agentfaces`, `@affectui`, `@ai-elements`, `@agents-ui` (LiveKit) | ElevenLabs DESIGN.md, Saaspo "AI SaaS websites" |
| Match a known brand's look | awesome-design-md | aidesign.guide |
| A specific component | `npx shadcn@latest search @sr -q "<query>"` | uploadcn (uploads), itshover / `@animateicons` (icons) |
| Micro-interactions on buttons and icons | Amicro, itshover | Transitions.dev, GSAP library BTN-* |
| Page transitions, scroll effects, text reveals | motionprompts, GSAP library | Transitions.dev |
| UI state transitions (toast, tabs, dropdown, streaming text) | Transitions.dev | Amicro |
| Loading or skeleton states | boneyard (real layouts), Skullet | ascii-reveal (decorative/branded) |
| File upload | uploadcn | — |
| Layout, state and motion rules for any build | `guidelines.md` (section by surface) | Source files listed at its end |

## 1. Inspiration galleries (what good looks like)

Use these for direction and page structure. Browse in the in-app browser; neither has a usable API for us.

**Saaspo** — https://saaspo.com
Curated SaaS landing pages. Filters: Landing pages, Pricing pages, Hero sections, AI SaaS websites, OG Images, Dark mode. Each entry is tagged by industry (AI, Automation, Infrastructure, Security…) and build tool (Next.js, Framer, Webflow). Free to browse; Pro tier for extras. Its MCP is marked "Soon" in the nav and isn't live yet, so browse it in the in-app browser. Their FAQ asks people not to copy designs exactly.

**Land-book** — https://land-book.com
Hand-picked website gallery, updated daily. Tabs: Websites, Sections, Mobile, Motion, OG Images, Headlines. Page-type filters: Landing, Portfolio, Blog, Ecommerce, About, Career, Sign Up, Pricing, Case Study, Product page. Wider than Saaspo (portfolios, agencies, ecommerce). Blocks plain fetches (403), so use the browser.

## 2. Brand specs and design systems (what to anchor on)

**awesome-design-md** (VoltAgent) — https://github.com/VoltAgent/awesome-design-md
84 DESIGN.md files pulled from real brand sites, each with `preview.html` and `preview-dark.html`. Categories: AI & LLM (Claude, ElevenLabs, Mistral, Runway, xAI…), Dev tools (Cursor, Vercel, Raycast, Linear-style), Backend/DevOps (Supabase, PostHog, Sentry), Productivity (Linear, Notion, Resend), Design tools (Figma, Framer), Fintech (Stripe, Wise, Revolut, Mercury), Ecommerce (Airbnb, Shopify, Nike), Media (Apple, Spotify), Automotive, Retro web. MIT.
Fetch one spec: `https://getdesign.md/<brand>/design-md`. Use by dropping the DESIGN.md into the project root as the style brief.

**AI Design Guide, design systems directory** — https://www.aidesign.guide/design-systems
185 design systems and component libraries, updated weekly. Filters for AI-ready systems: 40 with llms.txt, 34 with MCP, 24 with Skills. Includes shadcn/ui, Radix, MUI, Ant, Chakra, HeroUI, Mantine, Carbon, Primer, Spectrum, Atlassian, Astryx (Meta), Tremor, GOV.UK. Use it to pick a base system that agents can read.

**Atlassian Design System** — https://atlassian.design/llms.txt
Tokens, primitives, components, styling standard, WCAG 2.1 AA guidance. Good reference for dense, enterprise dashboard UI. Fetch only the part needed:
- Tokens: https://atlassian.design/llms-tokens.txt
- Components: https://atlassian.design/llms-components.txt
- Primitives (Box, Stack, Inline, Grid…): https://atlassian.design/llms-primitives.txt
- Accessibility: https://atlassian.design/llms-a11y.txt
- Styling: https://atlassian.design/llms-styling.txt
- Content/voice: https://atlassian.design/llms-content.txt
- Everything: https://atlassian.design/llms-full.txt
- Public MCP: https://mcp.atlassian.com/v1/ads/public/mcp

## 3. Component sources

**shadcnregistry (`@sr`)** — https://shadcnregistry.com
Index of 498 shadcn registries, searchable from the CLI. Setup in `components.json`:
```json
{ "registries": { "@sr": "https://shadcnregistry.com/r/{name}.json" } }
```
Search: `npx shadcn@latest search @sr -q "<query>"`
Registries worth knowing:
- AI/agent UI: `@ai-elements` (conversations, messages), `@assistant-ui` (chat primitives), `@affectui` (tool calls, thinking states, approvals), `@agents-ui` (LiveKit voice agents), `@agentfaces` (animated agent faces with voice lip sync)
- Motion-heavy: `@animate-ui` (789 items), `@aceternity` (landing-page effects), `@atelier` (WebGL, shaders, page transitions), `@aicanvas` (components with reproduction prompts, has MCP)
- Icons and loaders: `@animateicons` (1,500 animated Lucide-style icons), `@atomloader` (591 CSS loaders)
- Systems: `@astryx` (Meta, 1,022 items), `@ai2` (OKLCH tokens, 414 items)
- Styled: `@8bitcn` (retro), `@afterglow` (terminal UI), `@0nlytype` (type-only)

**uploadcn** — https://uploadcn.dev
Upload components for shadcn plus an upload engine (queues, retries, resumable multipart, S3/R2 presigned URLs). Blocks include Liquid Dropzone, Upload Dock, Progress Ring, Upload Table, Chat Attachments, CSV Import, Document Ingest, Identity Verification, Avatar. The registry ships 59 installable blocks (plus UI, hooks and files, 67 items); the 92 on the examples page are demos of those blocks. MIT. llms.txt at https://uploadcn.dev/llms.txt.
Install: `npx shadcn@latest add @uploadcn/file-upload`

**Thinking Orbs** — https://www.thinkingorbs.com
Animated status orbs for AI: idle, reasoning, working, searching, compacting, retrying, waiting, computer use. Variants (Spiral, Gyro, Twins, Fuse, Surge…), shapes and halftone render. React, vanilla JS, SwiftUI, Jetpack Compose. 3.8 KB, no dependencies, MIT. Strong fit for voice-agent console states.
Install: `npm i @yogesharc/thinking-orbs` → `<Orb state="reasoning" />`. Playground at /playground, llms.txt at /llms.txt.

**itshover** — https://itshover.com
263 animated React icons built with Motion, editable source, works with Next.js and shadcn. Browse at /icons. Apache-2.0.
Install one icon: `npx shadcn@latest add https://itshover.com/r/<icon-name>.json` (needs `motion`).

**Amicro** — https://amicro.dev
160+ copy-paste React micro-interaction components: morphing buttons, card spreads, 3D carousels, loaders, mono charts, text animations. Free, open source, Vercel OSS-backed.

## 4. Loading and skeleton states

**boneyard** — https://boneyard.vercel.app
Generates skeletons from the real rendered DOM, so they match the layout exactly. React, Preact, React Native, Svelte, Vue, Angular. ~7.5 KB.
`npm install boneyard-js` → `npx boneyard-js build` → `<Skeleton name="blog-card" loading={isLoading}>`. MIT (github.com/0xGF/boneyard).

**Skullet** — https://skullet.lochie.me
Renders sample data invisibly, measures it and draws a matching skeleton. Demos: gallery, comment thread, stats dashboard, settings list. `npm i skullet`. Early version (v0.0.3). MIT (github.com/lochie/skullet).

**ascii-reveal** — https://github.com/quanhoangindex/ascii-reveal
ASCII placeholder that decodes into real content. Presets: decode, dither, terminal, blueprint. Optional mascots. ~15 KB, no dependencies, MIT. Good for a branded or dev-tool feel, less so for plain business UI.
`npm i ascii-reveal`

## 5. Motion and animation

**Transitions.dev** — https://transitions.dev
43+ UI transitions built for AI agents: card resize, number pop-in, toast, tooltip, tabs sliding, dropdown morph, streaming text, thinking states, skeleton reveal. Also a skill, an MCP, and a CLI that scores motion 0–100 and proposes fixes:
`npx transitions-agent`
Some items are Pro only. Custom licence: free to use and modify in personal and commercial projects, tooling is MIT, but you can't redistribute the library as a competing product.

**motionprompts** — https://motionprompts.dev/llms.txt
259 web animation components (GSAP, Three.js/WebGL, vanilla JS), each with a build prompt. 30 free; the rest are paid and return 402 without a login. Fetch:
- Motion token sets (ease, duration, stagger): https://motionprompts.dev/api/v1/motion-systems.json
- Composition rules: https://motionprompts.dev/api/v1/composition-rules.json
- Component index: https://motionprompts.dev/api/v1/components.json
- Free prompts, e.g. https://motionprompts.dev/prompts/sticky-cards.md, /overlay-menu.md, /block-reveal-page-transition.md, /text-reveal-animation.md, /page-transitions-view-transition-api.md
MCP: github.com/VanguardiaAI/motionprompts-mcp.

**GSAP Prompt Library** — https://gsap.brxprod.com/llms.txt
346 GSAP effects, each a markdown file with prompt, code and HTML. Sections: Entrances, Scroll & Sections, Text, Buttons, Boxes & Cards, Media & Galleries, SVG, Cursor, Nav, Header & Menus, Interface, Forms & Inputs, Numbers & Data. Read the index first:
- https://gsap.brxprod.com/effects-index.json
- One effect: `https://gsap.brxprod.com/effects/<id>.md` (e.g. ent-02 Blur In, scr-06 scroll-scrubbed timeline, t-07 scramble decode, btn-29, box-23)
- Everything: https://gsap.brxprod.com/llms-full.txt
Needs a `gsap-cloaking` head script; respects reduced motion. No licence stated, but the site tells you to copy an effect's prompt or code into your own project, and GSAP plus all its plugins are free. Site sidebar shows 322 effects; llms.txt says 346.

## 6. Guideline sources (not installed)

We use these as rulebooks, not as installed skills. Their rules are paraphrased in `guidelines.md` by surface. Don't run their scripts or CLIs.

**Hallmark** — https://usehallmark.com (github.com/Nutlope/hallmark, MIT)
Best for console and dashboard rules (four data states, chart choice, surface ladder, fields) and for landing-page structure (21 page shapes). → `guidelines.md` sections A, B, D.

**Taste Skill** — https://tasteskill.dev (github.com/Leonxlnx/taste-skill, MIT)
Best for landing-page motion timings, card nesting, performance limits, copy tells, and a voice-call hero card reference. Its layout rules are wrong for console screens. → sections B, C, D.

**Transitions.dev skills** — github.com/Jakubantalik/transitions.dev (custom licence)
Best for the motion token scale, open/close asymmetry, dense app UI values, and agent-status and live-data motion. Paraphrase only; don't copy recipe files. → sections A, C.

## Verification notes

All entries re-checked 23 Nov 2026. Licences confirmed from each GitHub repo or LICENSE file. Saaspo's MCP isn't live yet. The GSAP library states no licence, but it invites copying into projects.
