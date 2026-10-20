# CloudDev Homepage — Design & Developer Notes

## Files
- **`CloudDev Homepage v3.dc.html`** — final design (open directly in a browser)
- `CloudDev Homepage.dc.html`, `CloudDev Homepage v2.dc.html` — earlier iterations
- `Homepage Options.dc.html` — three explored directions (1a terminal dark, 1b clean corporate, 1c split grid); v3 is built from 1b
- `uploads/logo-1784754404877.png` — CloudDev logo (2000×1922 PNG, transparent)
- `support.js` — component runtime; required for the `.dc.html` files to render as-is. For production, port the markup/styles to your stack of choice.

## Brand & palette (derived from the logo)
| Token | Hex | Use |
|---|---|---|
| Navy (logo "Cloud") | `#2456a6` | Primary CTA gradient start |
| Cyan (logo "Dev") | `#35a8dc` | Primary CTA gradient end, link hover |
| Link blue | `#1f5fb0` | Default link color |
| Accent cyan | `#2d8fbd` | Mono eyebrow line, bullets |
| Teal | `#23808a` | PiTest / open-source accent |
| Ink | `#14263f` | Headings, body on light |
| Muted | `#3d5470` | Secondary text |
| Dark panel | `#0e2138` | Code demo background |
| Section tint | `#f2f7fb` | Mutation-testing band |
| Border | `#dde8f1` / `#e6edf4` | Card and section borders |
| Mutant orange | `#e07a3f` / `#f0a86e` | Mutated character / mutant code |
| Killed green | `#23a06a` / `#6ee08a` | Corrected character / KILLED status |

## Typography
- **IBM Plex Sans** (400–700) — headings and body
- **IBM Plex Mono** (400–700) — eyebrow line, badges, code demo
- Loaded from Google Fonts. Scale: h1 46px, h2 28px, h3 24px, body 15–18px.

## Layout
- Max content width 1000–1160px, centered; 32px side padding
- Sections: nav → centered hero → mutation-testing band (tinted, 2-col grid) → product cards (2-col grid) → footer
- Logo stands alone in the nav (contains the wordmark — do not repeat "CloudDev" as text)

## Copy (agreed with client)
- Eyebrow: `// makers of PiTest & ArcMutate`
- H1: "We break your software to make it better & safer."
- Sub: "CloudDev software is trusted by over 100,000 corporations around the world, in every major industry that uses software. Cars run safely, online banking is more secure and healthcare software works better. ArcMutate slashes your development costs and speeds up your release."
- Footer: © 2026 Cloud Development Group Limited

## Additions (July 2026)
- **Responsive/mobile**: fluid clamp() type & padding; grids use repeat(auto-fit, minmax()) so sections collapse to one column; nav, CTAs and footer wrap
- **Logo strip** under hero: grayscale marquee of real customer logos ("Trusted by engineering teams at" — Booking.com, Cisco, Samsung, Delta, Cummins, U.S. Bank, Sysco, Neo4j, Wiz, Labcorp, Optum, J.B. Hunt, Otto.de, Flutter, Sompo, Folkhälsomyndigheten, Harvest, Interbank, Inter, InfinBank, MService, Banote, Polixis, Bivantis, OnlinePsy). Assets in `uploads/logos/`, ported from the arcmutate-main site. Infinite scroll (60s), pauses on hover, collapses to a static centered wrap under `prefers-reduced-motion`. Logos are grayscale @ 62% opacity, full-color on hover. Replaced the earlier "WORKS WITH & TRUSTED BY" integration wordmarks (GitHub/GitLab/etc.) — those were integrations, not customer endorsements
- **Quick start** section: Maven/Gradle tabs + copy-to-clipboard (pitest-maven 1.17.2 — confirm current version before launch)
- **Meta**: page title, description, OG tags, favicon (logo PNG)
- **Start free trial** button on ArcMutate card (logo gradient #2456a6 → #35a8dc, same as hero CTA)

## Interactions & animation
1. **Headline glitch** (concept: a live mutation test on the copy). A random letter mutates to a wrong character (orange, 650ms), then is corrected (green flash, 700ms). Runs **exactly twice** on load (~2.2s in, then once more after a 3.5–6s gap) and then **settles on the true headline permanently** — no perpetual motion, for accessibility. Controlled by `MAX_GLITCHES` in the component logic; still fully toggleable via the `titleGlitch` prop. The mutation-testing section references it ("You just saw it happen to our headline").
2. **Code demo loop** in the mutation-testing panel: original → mutant → "$ running tests…" → "✔ KILLED", advancing every 1.6s, looping (4 steps).
3. **Blinking cursor** after the eyebrow line (`@keyframes blink`, 1.1s step-end).
4. **Hover lifts**: CTAs and product cards translate up 2–4px with a soft shadow.

## Links
- ArcMutate: https://www.arcmutate.com (trial: https://subscribe.arcmutate.com/trial)
- PiTest: https://pitest.org
- Docs: https://docs.arcmutate.com · Blog: https://blog.arcmutate.com/ · LinkedIn: https://www.linkedin.com/in/trudinger/

## Implementation notes for developers
- All styling is inline (no stylesheet) except fonts, link colors, body reset, and the blink keyframes — trivially portable to any framework
- The glitch + demo animations are ~60 lines of plain JS (see the logic class in v3); port as a React hook or vanilla interval
- Product positioning: ArcMutate leads (commercial), PiTest presented as the open-source foundation
- Removed from the old site per client: the M&A / data-analysis positioning, entirely
