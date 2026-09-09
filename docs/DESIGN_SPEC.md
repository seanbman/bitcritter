# BitCritter V1 Design Specification

## Design Intent

BitCritter should feel like a tiny retro handheld that lives on a smartphone. The interface is intentionally restrained so the critter artwork remains the visual focus.

The chassis is part of the interaction model, not decorative framing.

## Color Rule

The application chrome is black and white.

Allowed color sources:

- critter artwork,
- palette swatches,
- critter previews that display that artwork.

Do not introduce arbitrary UI accent colors for:

- selected tabs,
- buttons,
- active tools,
- alerts,
- navigation,
- menus.

Use black/white inversion, line weight, fill, or spacing to communicate state.

## Chassis Layout

The chassis must fit within a portrait smartphone screen without requiring horizontal scrolling.

The fixed control arrangement is:

```text
┌──────────────────────────────┐
│                              │
│          APP DISPLAY         │
│                              │
├──────────────────────────────┤
│                              │
│  ┌─────┐      ○       ○  ○   │
│  │D-pad│     Menu      A  B   │
│  └─────┘                      │
│                              │
└──────────────────────────────┘
```

### Required controls

- D-pad on the lower left.
- Circular Menu button in the lower middle.
- A and B buttons on the lower right.

### Explicit exclusions

- No speaker grille.
- No smiley-face decoration.
- No extra physical-looking controls added without a product decision.

The control positions should remain stable between screens.

## Display

The display is a black-bordered rectangular screen inset into the plastic chassis.

The display area contains the actual BitCritter application UI.

It should:

- remain readable on small phones,
- use compact but legible typography,
- avoid horizontal page scrolling,
- keep primary touch targets large enough for a finger,
- preserve enough space for the 32×32 editor to remain useful.

The visual mockup language is retro and plastic, but the implementation should stay crisp rather than photorealistic.

## Typography

Use a pixel/bitmap-inspired display face only where it remains readable.

Recommended hierarchy:

- product title: pixel-style or blocky display face,
- screen titles and labels: high-contrast sans or readable bitmap-inspired face,
- dense metadata: simple monospace or sans-serif.

Legibility on a phone overrides retro styling.

## Main Screens

V1 includes these primary screen families:

1. My Pets
2. Draw
3. Palette
4. Frames
5. Preview
6. Save / Export

These should reuse the same chassis and display proportions.

## My Pets

The library uses a compact card grid.

Each card should show:

- critter sprite or Idle preview,
- critter name.

A New Pet card or + control should be visually obvious without introducing color.

## Draw Screen

The 32×32 canvas is the visual priority.

Recommended order:

1. critter name/header,
2. Draw / Palette / Frames tabs,
3. canvas,
4. drawing tools beside or beneath the canvas depending on width,
5. palette strip.

On narrow phones, tools may reflow as long as the logical grouping remains obvious.

### Tool state

The active tool should use black fill with a white icon or equivalent black/white inversion.

Inactive tools remain white/light with black icons and borders.

## Palette Screen

Palette rows should show:

- slot index,
- swatch,
- color value,
- edit action,
- safe delete action.

The swatch is allowed to use the actual palette color; surrounding controls remain monochrome.

## Frames Screen

The frame editor should emphasize quick animation creation.

Frame thumbnails must be large enough to distinguish pose changes.

Visible actions:

- state selector,
- preview/play,
- frame thumbnails,
- add frame,
- state list,
- add state.

Duplicate, delete, and reorder actions may live in contextual menus to avoid clutter.

## Preview Screen

The critter should appear significantly larger than its editor thumbnail and without the drawing grid.

Controls remain simple:

- state selector,
- previous,
- play/pause,
- next,
- FPS choices,
- loop toggle.

## Save / Export Screen

This screen is information-dense but should remain visually plain.

Group content into:

- name,
- save status,
- export actions,
- format information.

Avoid decorative cards unless they improve grouping or touch affordance.

## Responsive Rules

V1 is phone-first.

At small widths:

- no page-level horizontal scrolling,
- no clipped chassis controls,
- no control smaller than a reasonable finger target,
- the canvas may shrink visually but must remain crisp,
- labels may abbreviate only when meaning stays clear,
- tool groups may wrap or reposition.

The entire chassis does not need to mimic a fixed physical device ratio if doing so harms usability. The retro-device language should adapt to the available phone width.

## Touch Rules

All primary workflows must work by tap or drag.

Do not depend on hover.

Drawing gestures inside the canvas should not trigger page scrolling.

Any drag-only operation such as frame reordering must also provide a menu-based alternative.

## Motion

Animation belongs primarily to critter previews and state playback.

Avoid decorative interface motion that competes with the critter.

Respect reduced-motion preferences where applicable.

## Product Character

BitCritter should feel:

- small,
- tactile,
- playful,
- deliberate,
- constrained,
- collectible,
- more like a pocket object than a generic web dashboard.

The visual system should never overpower the critters users create.
