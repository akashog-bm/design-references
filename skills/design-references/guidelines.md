# Borrowed design guidelines

Rules paraphrased from three design skills we don't install: Hallmark (MIT), Taste Skill (MIT) and Transitions.dev (custom licence: use freely, don't redistribute the library). Load only the section that fits the surface, and apply it on top of impeccable. If a rule here conflicts with impeccable's craft floor, impeccable wins.

Sources are tagged [H] Hallmark, [T] Taste Skill, [TD] Transitions.dev.

---

## A. Console, dashboard and call-analytics screens

Skip the landing-page layout rules (one section per screen, 16px body minimum, word budgets) here.

**Density and structure**
- Body text 13/20, controls 36px. Never let a hit target drop below 44px. [TD modern.md, H flow.md]
- Keep the type scale tight: ratio 1.125–1.2. [H]
- Add a sidebar only past about 7 destinations; below that, use top nav or tabs. [H]
- Tables before cards when items share fields. [H]
- Filters, tabs and sort order live in the URL, so a view can be shared. [H]
- Animate state changes only. No decorative motion. [H]

**Every data region has four states** [H]
- Loading: a skeleton shaped like the content coming.
- Empty: say what belongs here, plus one action to fill it.
- Error: say what broke and what to do next.
- Full.

**Dashboards and charts** [H data-viz.md]
- One hero figure, one supporting chart, one table. No KPI walls, gauges, or trend arrows for things nobody measured.
- Pick the chart from the data:
  - one value → stat tile
  - 2–5 values → bars
  - a series over time → line
  - more than 7 categories → table
  - parts of a whole → stacked bar (not a pie or donut by default)
- Bars start at zero. One y-axis. One accent series, everything else muted. Labels in ink, not series colour. Tabular numbers.

**Surfaces** [H craft.md]
- Separate content in this order: whitespace, then a hairline, then a tinted well, then a card (border *or* shadow, not both).
- Never a card inside a card, and never white cards on a tinted page. Maximum two levels of nesting. [T cards.md]
- One shadow recipe across the product. A good layered default: `0 4px 42px rgba(0,0,0,.06), 0 2px 6px rgba(0,0,0,.05), 0 0 0 1px rgba(0,0,0,.06)`. [TD]

**Forms and feedback** [H interaction-and-states.md, microinteractions.md]
- A field's border never changes width between states. Focus is an instant outline (inset on inputs).
- Disabled: 0.55 opacity, not-allowed cursor, and the native `disabled` attribute.
- Reserve one line under each field for help text that swaps to the error, so the layout doesn't jump.
- Prefer undo over a confirm dialog for reversible actions.
- Use toasts only for failures and for effects the user can't see.
- Update optimistically and roll back on failure. Debounce search input.

---

## B. Landing and marketing pages

**Page shape** [H macrostructures.md, anatomy.md, layout.md]
- Pick one of Hallmark's 21 page shapes deliberately instead of the default SaaS stack. Most useful for us:
  - 04 Stat-led
  - 05 Workbench (product UI as the hero)
  - 06 Conversational FAQ
  - 14 Narrative workflow (good for a call flow)
  - 16 Feature stack
  - 19 Map/diagram

  The others are bento grid, long document, marquee hero, manifesto, photographic, quote-led, specimen, catalogue, letter, index-first, split studio, type specimen, portfolio grid, ecosystem index and component playground.
- Build sections from what the visitor came to do (sign up, compare, evaluate), not from a template list.

**Hero and motion** [T motion.md]
- Headline lines enter over 700ms each, 80ms apart. Then the lead and buttons fade up 12px, 520ms each, 60ms apart. About 1.1s in total, once per visit.
- Nothing fades or staggers in on scroll.
- Card loops run 2.5–4s, show one subject per cycle, change something every 1–2s with each change under 300ms, and hold the finished frame for the last 10–15%.
- Anything that moves for more than 5s gets a 32px pause control, 12px in from the bottom-right corner.
- Voice-AI hero reference: Taste's `ui/voice` card shows a call with an orb, word-by-word captions and a waveform on a ~2.75s loop. Use it for the idea, not the code.

**Performance limits** [T perf.md]
- Fail if: CLS > 0.25, LCP > 8s, any image > 700 KiB, more than 3 font families, or more than 4 WebGL canvases.

---

## C. Motion anywhere

**Token scale** [TD transitions-dev.md]
| Token | ms |
|---|---|
| stagger | 40 |
| micro | 80 |
| quick | 150 |
| fast | 250 |
| medium | 350 |
| slow | 400–500 |

- Default ease `cubic-bezier(0.22,1,0.36,1)`. For elements travelling across the screen, use `cubic-bezier(.65,0,.35,1)`. [T]
- Pick the token by what the element does, not by the nearest number.
- Scales on open: modal .96, dropdown .97, tooltip .98. Blur 2–8px at most.

**Open and close**
- Overlays close faster than they open: dropdown and modal open in 250ms, close in 150ms. Exits run at about 60% of the entrance time.
- Tabs, accordions, icon swaps and page slides take the same time both ways.
- Never bounce a close, and never delay a close or a hover-out. Bounce is off by default. The one allowed case is a badge pop.
- Stagger 40ms per item, keeping the whole sequence under 300ms. A tooltip waits 80ms before showing. Avoid moving anything more than about 40px.

**Micro-interactions**
- Hover in 150ms, out 120ms, press 90ms. [T]
- Press scale by size [TD modern.md]:
  - 99% for controls 200px and wider
  - 97% for buttons
  - 95% for icon buttons up to 64px
- Hover lifts stay small: card 2px, arrow 3px, photo zoom 1.02–1.03. [T]

**Agent and live-data motion** [TD recipes 14, 28, 34–36]
- Agent "thinking" status line: hold each state 2s, swap in 150ms with a 50ms gap, 8px travel and 2px blur. Size the box to the longest label so it never resizes.
- Live numbers: change over 455ms with a 0.14em shift.
- Switching a chart's period: swap the label text in 200ms.
- Donut morph: 400ms, 3px gaps, 2px corner radius.
- Skeleton: one 1000ms pulse, then a 400ms cross-fade to content with a 2px blur.

**Self-check before handing over** [TD rules.mjs]
- Nothing runs longer than 1000ms.
- No more than 2–3 distinct durations in use.
- No `transition: all`.
- Every modal, toast and dropdown has both an enter and an exit.
- A `prefers-reduced-motion` guard is in place.

---

## D. Copy, mock data and prototypes

- **Honest prototypes** [H craft.md]
  - Sample data uses example.com and round "Example" values that can't be mistaken for real claims.
  - A form with no backend says nothing was sent. It never shows a success state.
  - A fact we don't have goes in a visible dashed placeholder, not invented text.
- **Swap test** [H]: if a headline would work on a competitor's page, rewrite it around something only BlueMachines has. No buzzword lists and no stock second CTA.
- **Indic mock data** [T copy-tells.md]: "Priya Sharma/Nair/Shah"-style names are the overused default. Use a varied, believable mix across regions.
- **Indic text** [H responsive.md, fonts.md]
  - Leave 30–40% extra room for strings that run longer in Hindi, Tamil, Malayalam and other Indic languages.
  - Before choosing a font, confirm it covers the scripts on screen (Devanagari, Malayalam, Tamil…).
- **No invented brand values** [H brand-truth.md]: take brand colours from the client's real CSS or brand files, never from memory.

---

## Where the sources disagree

| Topic | Our rule |
|---|---|
| Body size and density | Console: 13/20 type, 36px controls [TD]. Landing: 16px body minimum [T]. |
| Press scale | By control size, as in section C. |
| Bounce | Off, except a badge pop. |
| Card edges | Console: hairlines and borders, following the surface ladder. Landing: border or shadow, one recipe. |
| Accordions | Fine in console screens and FAQs. |

## Source files (fetch only when a rule needs more detail)

Hallmark, pinned to commit 04977e15: `https://raw.githubusercontent.com/Nutlope/hallmark/04977e15f3dfd6ee4b74c887dac3eb52665d6c92/skills/hallmark/references/<file>`
- flow.md (the App screens section)
- data-viz.md
- interaction-and-states.md
- microinteractions.md
- craft.md
- brand-truth.md
- layout.md
- anatomy.md
- macrostructures.md
- macrostructures/<NN-name>.md

Taste Skill: `https://raw.githubusercontent.com/Leonxlnx/taste-skill/main/skills/taste-skill/<path>`
- references/motion.md
- references/cards.md
- references/perf.md
- references/copy-tells.md
- assets/ui/voice/meta.json

Transitions.dev: `https://raw.githubusercontent.com/Jakubantalik/transitions.dev/main/<path>`
- assets/community/skills/transitions-dev.md
- assets/community/design-systems/modern.md
- skills/transitions-polish/_refine-rules.md
- skills/transitions-dev/ recipes:
  - 14-skeleton-reveal.md
  - 28-thinking-states.md
  - 34-text-swap-soft.md
  - 35-donut-chart.md
  - 36-number-subtle-change.md

Read these for reference only. Don't copy Transitions.dev recipe files into a project or a packaged skill.
