# BitCritter

BitCritter is a mobile-first 32×32 pixel-pet creator. Users draw a critter on a smartphone, manage its palette, create animation frames for different states, preview those animations, save the critter locally, and export its data.

The V1 application is intentionally small, tactile, and offline-first. The interface is black and white; the only color in the application should come from critter artwork and its palette.

## V1 Goals

- Create, name, save, rename, duplicate, and delete critters.
- Draw on a fixed 32×32 pixel grid with touch input.
- Use pencil, eraser, fill, eyedropper, mirror, undo, and contextual edit actions.
- Manage indexed palettes so palette edits recolor all pixels that reference a slot.
- Create, duplicate, delete, reorder, and preview animation frames.
- Organize frames into states such as Idle, Walk, Sleep, Happy, Sad, and custom states.
- Persist all core work locally and operate without a network after installation.
- Install to a phone home screen as a PWA.
- Build as a portable JavaScript package that can be hosted at its own endpoint or embedded by another compatible host.

## Proposed V1 Stack

- TypeScript
- Vite
- HTML Canvas for the 32×32 editor
- Pointer Events for touch, stylus, and mouse input
- IndexedDB for local persistence
- Plain CSS for the chassis and application UI
- Web App Manifest + Service Worker for PWA installation and offline use

A Rails application or any other server may host the compiled BitCritter bundle at an endpoint such as `/bitcritter/`, but Rails is not required for BitCritter's core workflow.

## Documentation

All project manuals and specifications are Markdown files under [`docs/`](docs/README.md).

Start with:

- [`docs/USER_MANUAL.md`](docs/USER_MANUAL.md) — V1 user manual and control reference
- [`docs/V1_SPEC.md`](docs/V1_SPEC.md) — V1 product scope and behavior
- [`docs/USER_STORIES.md`](docs/USER_STORIES.md) — V1 backlog
- [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) — browser/PWA architecture and host model
- [`docs/DESIGN_SPEC.md`](docs/DESIGN_SPEC.md) — visual and interaction rules
- [`docs/FUTURE_IDENTITY.md`](docs/FUTURE_IDENTITY.md) — future portable identity, history, and container direction

## Product Principles

1. The interface is an instrument, not the artwork.
2. 32×32 is a deliberate constraint.
3. Animation should be fast to create by duplicating and adjusting frames.
4. A one-frame critter is still a complete critter.
5. Complexity is optional and layered on top of a simple core format.
6. Appearance may be copied. Identity must be proven. History must be earned.
7. Critters should outlive containers.

## Repository

Canonical repository: `seanbman/bitcritter`
