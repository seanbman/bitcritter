# AGENTS.md

This repository contains **BitCritter**, a mobile-first, offline-first 32×32 pixel-pet creator.

## Authoritative Project Rules

1. The product name is **BitCritter**. Do not introduce alternate product names.
2. Do not use the word `Studio` in product-facing copy, documentation, UI labels, metadata, or code-generated titles.
3. V1 is a small browser application first. Do not require a backend for drawing, editing, animation, persistence, preview, or export.
4. The app must remain buildable as a portable JavaScript bundle and installable as a PWA.
5. Core functionality must continue to work offline after the application has been installed or cached.
6. The authoritative drawing format is a fixed 32×32 grid of palette indices, not 1,024 DOM elements and not raw per-pixel RGB values.
7. Use Canvas for the editor rendering layer and nearest-neighbour/pixelated scaling.
8. Use IndexedDB for persistent local V1 data unless the architecture document is intentionally revised.
9. Prefer TypeScript, Vite, browser APIs, and plain CSS. Do not add a large UI framework without a demonstrated need.
10. Keep the V1 implementation deliberately constrained. Do not silently promote future identity, memory, relationship, or cryptographic concepts into V1.

## Visual Contract

The V1 visual design is intentionally strict:

- Black-and-white application chrome.
- Color is reserved for critter artwork and palette swatches.
- Retro plastic handheld chassis surrounding the app display.
- Smartphone-sized portrait layout.
- D-pad on the lower left.
- Circular menu button in the lower middle.
- A and B buttons on the lower right.
- No speaker grille.
- No smiley-face decoration or mascot icon on the chassis.
- Selected UI states should use black/white inversion rather than arbitrary accent colors.

Do not casually reposition, add, or remove chassis controls. The chassis is part of the product interaction model, not decorative artwork.

## Interaction Contract

Touch is the primary input, but the chassis controls must also be functional:

- **D-pad:** move focus or a pixel cursor where applicable.
- **A:** activate/confirm the current focus; on the canvas, apply the current drawing tool.
- **B:** cancel, dismiss, or go back one level when safe.
- **Circular menu button:** open the current screen's main/context menu.
- **Ellipsis menu inside the display:** open item/screen-specific secondary actions.

Every visible control must have a documented behavior. Do not leave decorative buttons that appear interactive but do nothing.

## Documentation Discipline

All manuals and project documentation live in `docs/` as Markdown.

When changing behavior, data format, navigation, controls, persistence, offline behavior, or export behavior, update the corresponding Markdown documentation in the same change.

Primary references:

- `docs/USER_MANUAL.md`
- `docs/V1_SPEC.md`
- `docs/USER_STORIES.md`
- `docs/ARCHITECTURE.md`
- `docs/DESIGN_SPEC.md`
- `docs/FUTURE_IDENTITY.md`

If implementation and documentation disagree, stop and resolve the discrepancy rather than guessing which behavior is intended.

## V1 Scope Boundary

V1 includes creation, editing, palettes, frames, states, animation preview, local persistence, PWA/offline support, and portable data export.

Future concepts include cryptographic pet identity, signed history, memories, relationships, transfer between containers, and provenance. These may influence extensibility but must not complicate the V1 user experience.

## Development Principle

Build the smallest coherent implementation that satisfies the documented user stories. V1 exists to generate real usage feedback that will shape V1.1.
