# design-references

A Claude Code skill for design and prototype work. Before building or improving a design, it suggests 2–4 matching references, waits for you to pick, then applies layout, state and motion guidelines suited to the surface.

## Quick install (one prompt)

Paste this into Claude Code or Codex (ChatGPT's coding agent):

```
Install the design-references skill from https://github.com/akashogext/design-references for me.

1. Find out which agent you are and pick the skills folder:
   - Claude Code: ~/.claude/skills/design-references
   - Codex: ~/.codex/skills/design-references
2. If that folder already exists, show me what's in it and ask before replacing it.
3. Clone the repo to a temporary folder and copy only skills/design-references/ (SKILL.md, references.md, guidelines.md) into the skills folder. Don't run any scripts or install any packages.
4. Check that all three files are there and that SKILL.md starts with "name: design-references".
5. Ask me whether to add the routing lines from the README's "Optional" step to my global instructions file (~/.claude/CLAUDE.md or ~/.codex/AGENTS.md). Add them only if I say yes.
6. Delete the temporary folder, then tell me to start a new session.
```

This works in coding agents that can write files on your computer. The ChatGPT and Claude web chats can't install it this way.

## What's inside

- `references.md`: 18 design sources sorted by purpose (inspiration galleries, brand DESIGN.md specs, shadcn registries, component libraries, loading states, motion libraries), with a task lookup table and the links to fetch.
- `guidelines.md`: rules for console and dashboard screens, landing pages, motion, and copy and mock data, paraphrased from Hallmark, Taste Skill and Transitions.dev. None of those are installed.
- `SKILL.md`: when the skill runs and the steps it follows.

## Manual install

With the skills CLI:

```
npx skills add akashogext/design-references
```

Or by hand:

```
git clone https://github.com/akashogext/design-references
cp -r design-references/skills/design-references ~/.claude/skills/
```

Start a new Claude Code session afterwards. The skill runs on its own for design requests.

Optional: add this to the "Skill routing" section of your `~/.claude/CLAUDE.md` so it triggers more reliably:

```
## design-references
- Use before any design or prototype work, or any request to improve an existing design: UI, mockups, landing pages, dashboards, console screens, motion, loading states, uploads, icons, AI or voice indicators, etc.
- Shortlist matching references and get my pick before using any.
```

## Sources

Rules in `guidelines.md` are paraphrased from:
- [Hallmark](https://github.com/Nutlope/hallmark) (MIT)
- [Taste Skill](https://github.com/Leonxlnx/taste-skill) (MIT)
- [Transitions.dev](https://github.com/Jakubantalik/transitions.dev) (its own licence)

No files from these projects are copied here. Each source in `references.md` keeps its own licence.

Links and counts were last checked on 23 Nov 2026.
