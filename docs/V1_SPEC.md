# BitCritter V1 Specification

## Purpose

V1 exists to validate the core experience of creating and animating a tiny pixel pet on a smartphone. It should be small enough to build quickly, pleasant enough to use repeatedly, and technically clean enough to become the base for V1.1.

## Core Experience

The user can:

1. create a critter,
2. name it,
3. draw it on a 32×32 canvas,
4. edit its palette,
5. create frames,
6. organize frames into states,
7. preview animations,
8. save locally,
9. reopen and edit later,
10. export critter data,
11. install BitCritter to a phone home screen,
12. keep using core features offline after installation/caching.

## V1 Functional Scope

### Critter Library

- Create a critter.
- Open a saved critter.
- Rename a critter.
- Duplicate a critter.
- Delete a critter with confirmation.
- Display a recognizable preview and name for each critter.

### 32×32 Editor

- Fixed 32×32 logical resolution.
- Touch drawing with Pointer Events.
- Pencil.
- Eraser.
- Flood fill.
- Eyedropper.
- Horizontal mirror.
- Undo.
- Redo through context action if not visible as a dedicated button.
- Clear frame through context action.
- Crisp enlarged rendering with no smoothing.

### Palette

- Indexed palette shared by the critter.
- Add a color.
- Edit a color.
- Select the active color.
- Delete unused colors safely.
- Never silently remap a used color.
- Transparency is separate from the visible palette and is written by the Eraser.

### Frames

- Add frame.
- Duplicate frame.
- Delete frame.
- Select frame.
- Reorder frame.
- Show frame thumbnails.
- Provide a non-drag reorder path.

### States

- Default Idle state.
- Add custom state.
- Rename state.
- Delete state safely.
- Assign an ordered frame sequence to each state.
- Loop setting per state.
- Playback speed per state.

Suggested names may include Idle, Walk, Sleep, Happy, Sad, Eat, Hurt, and Celebrate, but only Idle is required by the data model.

### Preview

- Preview selected state.
- Play/pause.
- Previous/next frame while paused.
- FPS control.
- Loop toggle.

### Persistence

- Persistent local storage with IndexedDB.
- Saved critters survive app restarts.
- No account required.
- No network required for core editing once assets are cached.
- Data schema is versioned.

### Export

V1 should support structured critter export containing at minimum:

- format version,
- name,
- created timestamp,
- modified timestamp,
- palette,
- states,
- state playback settings,
- ordered frames,
- each frame's 32×32 palette-index grid.

A JavaScript-friendly JSON representation should be available.

Visual sprite export may be offered as individual PNG frames or a documented sprite sheet.

## Chassis Interaction

The visual handheld chassis is functional.

- D-pad: focus navigation; canvas cursor movement when applicable.
- A: confirm/activate; draw at focused pixel when canvas cursor is active.
- B: cancel/back/dismiss.
- Circular Menu: open current screen menu.
- On-screen ellipsis: item- or screen-specific secondary actions.

Touch remains the primary interaction method.

## Visual Scope

- Portrait smartphone layout.
- Retro molded-plastic chassis aesthetic.
- Black-and-white application chrome.
- Color only in critter artwork and palette swatches.
- D-pad lower left.
- Circular menu button lower middle.
- A/B lower right.
- No speaker grille.
- No smiley-face decoration.
- No arbitrary accent color for selected UI; use black/white inversion.

## Technical Scope

Recommended V1 implementation:

- TypeScript
- Vite
- Canvas
- Pointer Events
- IndexedDB
- plain CSS
- Web App Manifest
- Service Worker

The app must be buildable as a self-contained JavaScript/browser bundle. A server such as Rails may host the compiled output but must not be required for the primary workflow.

## Offline Requirement

After initial installation or successful cache population, users must be able to perform the core creation workflow offline.

The service worker should cache the application shell and versioned static assets. Runtime data belongs in IndexedDB, not in the service-worker cache.

Updates must not destroy or invalidate user critter data.

## Out of Scope for V1

- accounts,
- required cloud storage,
- collaboration,
- cryptographic critter identity,
- signed history,
- memories,
- relationships,
- cross-container transfer,
- container provenance,
- remote synchronization,
- marketplace/social features,
- complex drawing tools,
- layers,
- arbitrary canvas sizes,
- brushes,
- gradients,
- text tools.

## V1 Acceptance Principle

A first-time user should be able to open BitCritter, create a named critter, draw it, duplicate a frame, make a two-frame Idle animation, preview it, close the app, reopen it offline, and find the critter intact without creating an account.

That is the core V1 success path.
