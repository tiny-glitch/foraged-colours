# Foraged Colours

A dice-roll colour palette generator. Tap roll, get earthy, hard-to-name colours — the kind you'd find on a forest floor or a weathered stone wall. Each swatch gets a name like "Cellar Sage" or "Tallow Ochre" because naming is half the experience.

**[Live Demo](https://foraged-colours.netlify.app)**

## Features

* Roll dice to generate palettes from curated, nature-inspired hue pools
* Two pigment modes per roll — concentrated (deep, dark) and raw (chalky mid-tones)
* 10% wildcard chance for a vivid "bright find" that pops against the earthy base
* Combinatorial swatch names (adjective × noun per hue family)
* Single-screen layout — header, palette, and roller fit in one viewport on any device
* Roll history lives in its own scroll zone below

## Tech

React, JavaScript, single-file HTML bundle. No build step, no dependencies beyond React. Deployed on Netlify.

## Interesting problems solved

**Nature isn't random.** Full HSL randomness produces "digital" looking colours. Natural pigments cluster in specific hue families. The fix was five curated hue pools (warm earths, olive/moss, oxidized teal, storm/indigo, dusty mauve/plum) with harmony constraints — majority of swatches near a dominant hue, lightness spread ≥15 apart, and near-duplicate prevention. Random within constraints beats truly random.

**Perceptual lightness lies.** At equal HSL lightness, cool hues look noticeably brighter than warm ones — a 50% olive reads as "vivid moss" while a 50% sienna reads as "earthy umber." We iterated this twice: first capping only indigos/mauves, then realizing the correction should apply from hue 100 onward (greens through the whole cool side). Warms below 100 keep the full range.

**Depth needs two registers.** Early palettes were all the same "muted mid-tone" energy. Adding concentrated pigment (deep, dark) alongside raw pigment (chalky, silty) solved it — like a real dye sample card with full-strength pulls next to diluted ones.

**The wildcard paradox.** We kept tightening rules to prevent digital-looking colours, then kept finding bold ones we liked. The 10% wildcard is a deliberate escape hatch — it reframes vivid colours from "the system failed" to "you found something rare," like a bright mushroom cap on the forest floor.

**100dvh, not 100vh.** The whole UI needed to fit one viewport on any device. `100vh` is broken on mobile (ignores browser chrome), so we used `100dvh` throughout and layered `clamp()` on font sizes, palette height, and padding, with breakpoints at `max-height: 640px` and `480px` for short screens.

## Deployment

Hosted on Netlify.
