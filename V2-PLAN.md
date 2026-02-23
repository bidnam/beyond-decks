# Plan: Beyond Decks — Alternative Version (Horizontal Cinema)

## Context

The current `index.html` is a vertical scroll presentation — sections stacked vertically, one per viewport, arrow keys scroll down. It works, but the form factor feels like the same template repeated 29 times: centered text on dark/light backgrounds, scroll, repeat. It's a deck about going beyond decks — and it still feels like a deck.

This plan creates `index-v2.html` as an alternative version, leaving the current version intact.

## The Alternative: Horizontal Cinema with Act Breaks

### Core concept

**The presentation moves horizontally** — left to right — like a camera panning across a landscape. Each beat is a full-viewport "frame." Arrow right smoothly pans to the next frame. Arrow left pans back.

**Between acts, the screen goes black.** A brief blackout (like a theater scene change), then the act title fades in, then the first beat of the new act. This creates breathing room, resets attention, and gives the narrative dramatic structure.

**The horizontal motion IS the metaphor.** The thesis is about a journey — moving forward, extending, going beyond. The audience literally moves forward through the presentation. When we talk about "extending the journey" in Beat 14, the visual format has been demonstrating that all along.

### Why this feels fundamentally different

1. **Horizontal panning breaks the scroll paradigm** — it doesn't feel like a website, it feels like a film. The content moves past you rather than you scrolling through it.
2. **Act breaks with blackouts create silence** — the 29 beats become a 9-act story. The pause between acts lets the room breathe. It's theatrical, not templated.
3. **Each frame is a "shot"** — content isn't always centered. Some frames are left-aligned, some right-aligned, some use the full width. The variety comes from cinematographic framing, not CSS templates.
4. **The horizontal strip implies a timeline** — the audience subconsciously feels the length and position of the narrative. You're 1/3 through. You're approaching the end. The spatial awareness adds weight.
5. **Transitions BETWEEN beats have character** — not just "next slide." The pan itself is a design element. Some pans are fast (urgency), some are slow (gravity). Some beats zoom in from the previous one.

### Act structure (9 acts)

| Act | Name | Beats | Duration feel |
|-----|------|-------|---------------|
| I | The Hook | 0-1 | Quick, intriguing |
| II | The Tension | 2-5 | Building, tightening |
| III | The Bridge | 6 | Brief, pivotal |
| IV | The Shift | 8-10 | Evidence-driven |
| V | The Pressure | 11-12 | Urgent |
| VI | The Provocation | 13-17 | Expansive, exciting |
| VII | The Proof | 18-22 | Concrete, transformative |
| VIII | The Payoff | 23-25 | Emotional, callback |
| IX | The Invitation | 26-29 | Forward, closing |

### Navigation model

- **Arrow Right / Space / Arrow Down**: Pan to next beat (smooth GSAP tween, ~0.8s)
- **Arrow Left / Arrow Up**: Pan to previous beat
- **At act boundaries**: Right arrow triggers blackout → act title → first beat (total ~2.5s)
- **Beat 13 (diverge)**: Right arrow reveals one line at a time before moving on (same sub-navigation as current)
- **Home / End**: Jump to start / end

### Technical approach

```
┌──────────────────────────────────────────────────────────────────┐
│ .cinema-strip (display: flex, width: N * 100vw)                  │
│ ┌─────────┐┌─────────┐┌─────────┐┌─────────┐┌─────────┐        │
│ │ Beat 0  ││ Beat 1  ││ ACT II  ││ Beat 2  ││ Beat 3  │ ...    │
│ │ (frame) ││ (frame) ││ (title) ││ (frame) ││ (frame) │        │
│ └─────────┘└─────────┘└─────────┘└─────────┘└─────────┘        │
└──────────────────────────────────────────────────────────────────┘
```

- All frames sit in a horizontal flex container
- GSAP tweens the container's `x` position to "pan" between frames
- Act title cards are full frames within the strip (black background, act name)
- A blackout overlay fades in/out during act transitions for the theatrical effect
- Each frame is `100vw × 100vh`, positioned with `flex-shrink: 0`

### Frame design language

**Not every frame is centered.** The variety comes from how content is "shot":

| Composition | Used for | Example |
|-------------|----------|---------|
| **Center frame** | Key statements, paradox, payoff | Beat 5: "You can't be a true partner..." |
| **Left-weighted** | Narrative text with room to breathe | Beat 4: "We hand off the recipe..." |
| **Right-weighted** | Counter-arguments, questions | Beat 9: "But we're not developers" |
| **Top-heavy** | Labels + headings (visual below) | Beat 2: Journey line sits low |
| **Bottom-anchored** | Quiet, grounding moments | Beat 16: "This isn't a pivot" |
| **Split** | Before/after, comparisons | Beat 8: Shift comparison |
| **Full-bleed type** | Dramatic scale moments | Beat 29: Final statement fills the frame |

### Transition types

Not all pans are equal. The transition speed/style varies by narrative moment:

- **Standard pan** (0.8s, expo.inOut): Most beat-to-beat transitions
- **Slow pan** (1.2s, power2.inOut): Entering payoff beats (23-25), building gravity
- **Quick cut** (0.3s, power3.out): Within evidence section (stats), urgency
- **Blackout** (fade 0.4s → hold 0.6s → fade in 0.4s → pan): Act transitions

### What carries over from v1

- Same base64 inlined fonts (Instrument Serif + Inter)
- Same GSAP 3.14 CDN links (ScrollTrigger, ScrollToPlugin, SplitText, DrawSVGPlugin)
- Same narrative content for all 29 beats
- Same color palette (--black, --cream, --accent indigo, --accent-warm)
- SplitText reveals on key statements (hero, paradox, final)
- DrawSVG animations (journey line, bridge diagram, value curve, diverge lines)
- Counter animations for evidence stats
- Morph animations for proof beats (19-22)
- Interactive diverge sub-navigation (Beat 13)

### What's new in v2

- **Horizontal layout** — flex strip instead of vertical sections
- **Act title cards** — 9 black frames with act names inserted between acts
- **Blackout overlay** — fades in/out for act transitions
- **Variable transition speeds** — different easing per narrative moment
- **Cinematographic framing** — layout utility classes for left/right/top/bottom positioning
- **No scroll** — pure keyboard/click navigation, no scrollbar, `overflow: hidden` on body
- **Frame counter** — subtle "12 / 38" in bottom-left (optional, can hide)

## Implementation order

### Step 1: Scaffold the horizontal cinema
- Create `index-v2.html`
- Copy font declarations from `index.html` (base64 fonts)
- Set up the cinema-strip container with `overflow: hidden` on body
- Create the GSAP pan function: `panTo(frameIndex)` with variable duration
- Wire up keyboard navigation (arrow keys, space, home/end)
- Test with 3 placeholder frames

### Step 2: Build act title cards
- Insert act title frames at act boundaries (9 total)
- Style: pure black, act name in small caps, fades in/out
- Build the blackout transition: overlay div that fades in → wait → fades out
- Wire into navigation: detect act boundaries, trigger blackout before pan

### Step 3: Port all 29 beats
- Create each beat as a horizontal frame
- Apply composition classes (center, left-weighted, right-weighted, etc.)
- Port the visual elements: SVGs, morph cards, spectrum grid, tool links
- Maintain all content exactly as in v1

### Step 4: Port animations
- SplitText reveals (hero, quote, paradox, final statement)
- DrawSVG animations (journey, bridge, value curve, diverge, extend)
- Counter animations (evidence stats)
- Morph animations (proof beats 19-22)
- General reveals (fade-up on labels, body text, headings)
- Adapt ScrollTrigger usage → many will become "on frame enter" triggers instead

### Step 5: Transition polish
- Assign transition types to each beat boundary (standard, slow, quick, blackout)
- Test full presentation flow with keyboard
- Refine timing: act transitions should feel theatrical, not sluggish
- Add subtle nav indicator (frame counter or progress dots)

### Step 6: Verify
- Full run-through of all 29 beats + 9 act titles using arrow keys
- All SplitText reveals render correctly
- All DrawSVG paths draw smoothly
- Both interactive moments work (Beat 13 diverge, Beats 19-22 morph)
- Act transitions feel dramatic (blackout → title → content)
- No content overflow at 1920×1080 and the user's ~1440px viewport
- No orphaned words on key statements
- Horizontal pan feels cinematic, not mechanical
- Variable transition speeds match narrative energy
- The whole thing feels like a FILM, not a deck

## Files

- `index-v2.html` — The alternative version (new file)
- `index.html` — Current version (untouched)

## Key Gotchas from v1 (avoid repeating)

- SplitText `mask` + `background-clip: text` = invisible text. Use simple `color` instead of gradient-clip on SplitText targets.
- SplitText mask containers clip descenders if `line-height` < 1.1 for large serif text.
- `clamp()` font sizes need careful max values — huge text pushes content off-screen at large viewports.
- Use `&nbsp;` between last 2-3 words to prevent orphans; use explicit `<br>` for intentional line breaks.
