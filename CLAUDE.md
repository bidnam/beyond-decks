# Beyond Decks

An interactive web presentation arguing that consulting firms should extend their thinking beyond static decks into lightweight, durable tools. The presentation itself is a "beyond decks" artifact — it practices what it preaches.

## File Structure

- `NARRATIVE-PLAN.md` — Source of truth for the thesis, narrative beats, evidence, and tone
- `index.html` — The interactive presentation (single-file, uses GSAP + ScrollTrigger)
- `_OLD-BEYOND-DECKS-NARRATIVE-PLAN-FINAL.md` — Archived earlier version of the plan

## The Thesis

Consultants sell transformation (a journey) but deliver decks (a moment). Building is now nearly free. Our thinking can take more forms. The partners who extend what's possible become impossible to replace.

## Key Decisions

- **Provocation, not a business plan** — This opens the aperture. Don't overaddress operational concerns (maintenance, billing, scope).
- **No ceiling on what can be built** — The spectrum shows where to start, not where it stops.
- **Signal/feedback point in Beat 15** — Tools give you feedback loops that decks can't.
- **Beat 16 renamed** — From "Not Enterprise Software" to "It Fits How We Already Work."
- **Self-referential proof** — The presentation itself is the strongest proof point.

## Design Principles

- **Let the words do the work** — The narrative is strong; visuals amplify, not compete.
- **Strip away visual gimmicks** — No custom cursor, floating shapes, noise textures, velocity effects.
- **Simplified color palette** — One or two accent colors, not five.
- **Full-screen moments** — Give the best lines space and silence.
- **Break dense sections** — Evidence and spectrum sections become individual beats, not walls of text.
- **Typographic visuals over diagrams** — Replace SVG wireframe diagrams with simpler typographic treatments.
- **Lean into self-reference** — This IS a beyond-decks artifact.

## Tone

- Confident about the moment, humble about individual outcomes
- Practical, not visionary — this is happening now
- Inclusive, not threatening — extending capability
- Urgent, not panicked — opportunity, not crisis

## Tech Stack

- Single HTML file, no build system
- GSAP 3.14 + ScrollTrigger + ScrollToPlugin + SplitText + DrawSVGPlugin for animations
- Fonts inlined as base64 woff2 (Instrument Serif regular + italic, Inter variable 300-700) — no CDN dependency
- 29 beats as individual `<section>` elements with keyboard arrow navigation
