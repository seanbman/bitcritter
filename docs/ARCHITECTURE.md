# BitCritter Architecture

## Goal

BitCritter should be a self-contained browser application that can:

- run at its own endpoint,
- be installed as a PWA,
- keep working offline after installation/caching,
- persist user data locally,
- export critter data in a JavaScript-friendly format,
- and be hosted by Rails or another server without depending on that server for the core workflow.

## Recommended V1 Stack

- **TypeScript** for application logic and typed data structures
- **Vite** for development and production builds
- **HTML Canvas** for the 32×32 editor surface
- **Pointer Events** for touch, stylus, and mouse input
- **IndexedDB** for persistent local critter data
- **Plain CSS** for the application and chassis UI
- **Web App Manifest** for installability
- **Service Worker** for offline application-shell caching

A large front-end framework is not required for V1. Introduce one only if real implementation pressure justifies it.

## Deployment Model

BitCritter is built as a portable static/browser bundle.

```text
BitCritter source
      │
      ▼
    Vite
      │
      ▼
    dist/
    ├── index.html
    ├── assets/
    │   ├── bitcritter.js
    │   └── bitcritter.css
    ├── manifest.webmanifest
    └── sw.js
```

The same build can be served by:

```text
Static host
Rails endpoint
Another application server
Local development server
Compatible embedded host
```

A Rails host could expose the app at `/bitcritter/`, but Rails is infrastructure around the app, not the app's execution model.

## Runtime Layers

```text
┌─────────────────────────────┐
│        BitCritter UI        │
│ chassis / screens / menus   │
└──────────────┬──────────────┘
               │
┌──────────────▼──────────────┐
│       Application Core      │
│ critters / states / frames  │
│ tools / undo / preview      │
└──────────────┬──────────────┘
               │
      ┌────────┴────────┐
      │                 │
┌─────▼─────┐     ┌─────▼─────┐
│ Renderer  │     │ Pet Store │
│  Canvas   │     │ IndexedDB │
└─────┬─────┘     └─────┬─────┘
      │                 │
      └────────┬────────┘
               │
┌──────────────▼──────────────┐
│ Serializer / Import-Export  │
└─────────────────────────────┘
```

## Data Model

The authoritative frame representation is an indexed grid.

```ts
interface CritterFrame {
  id: string;
  pixels: number[]; // exactly 1024 palette indices
}

interface CritterState {
  id: string;
  name: string;
  frameIds: string[];
  fps: number;
  loop: boolean;
}

interface Critter {
  id: string;
  formatVersion: number;
  name: string;
  createdAt: string;
  modifiedAt: string;
  palette: string[];
  frames: Record<string, CritterFrame>;
  states: CritterState[];
}
```

The exact production schema may differ, but these constraints are authoritative:

- every frame is 32×32,
- every pixel stores a palette index or documented transparent value,
- palette editing can recolor all referencing pixels,
- state frame order is explicit,
- format versioning exists from V1 onward.

## Canvas Rendering

The visible editor should not contain 1,024 interactive DOM nodes.

Use Canvas as the drawing surface. Maintain the logical model separately from the rendered pixels.

Typical approach:

```ts
const LOGICAL_SIZE = 32;
```

Render with image smoothing disabled and use CSS pixelated scaling so the enlarged grid remains crisp.

Pointer coordinates are translated from the visible canvas rectangle into integer logical x/y coordinates between 0 and 31.

## Input Model

Touch is primary.

Use Pointer Events so one implementation supports:

- touch,
- stylus,
- mouse.

The chassis controls feed the same application commands as touch controls rather than implementing separate behavior.

Example command layer:

```text
select
back
menu
focus-up
focus-down
focus-left
focus-right
draw
undo
redo
play
pause
```

This keeps A/B/D-pad behavior consistent with touch UI actions.

## Undo / Redo

Undo and redo should operate on model changes, not screenshots of the canvas.

V1 can use a bounded history stack per open critter or editing session. History must cover at least:

- pixel edits,
- fill,
- erasing,
- mirror,
- clear frame,
- safe frame operations where practical.

History must be bounded to avoid unbounded mobile memory growth.

## Persistence

Use IndexedDB for persistent user data.

Recommended stores:

```text
bitcritter
├── critters
├── settings
└── metadata / migrations
```

Do not use the service-worker cache as the source of truth for user-created critters.

Persist a schema version and define migrations when the local data model changes.

## Offline / PWA Model

The service worker caches only versioned application assets required to launch the app.

```text
Service Worker Cache
├── HTML shell
├── JavaScript
├── CSS
├── icons
└── built-in static assets

IndexedDB
└── user critters and settings
```

Core editing must not make network requests.

An update flow should:

1. download a new application version,
2. activate safely,
3. preserve IndexedDB,
4. migrate user data only through explicit versioned migrations.

## App Manifest

The PWA should define its own start URL and scope so it installs as BitCritter rather than as a parent collection of apps.

Example deployment intent:

```json
{
  "name": "BitCritter",
  "short_name": "BitCritter",
  "start_url": "/bitcritter/",
  "scope": "/bitcritter/",
  "display": "standalone"
}
```

The final paths may vary by host.

## Portable JavaScript Application Contract

The browser implementation should expose a small mountable application boundary rather than coupling all behavior to one HTML page.

A reasonable direction is:

```ts
interface BitCritterApp {
  mount(root: HTMLElement): void;
  start(): Promise<void>;
  exportData(): Promise<Blob>;
  importData(blob: Blob): Promise<void>;
  destroy(): void;
}
```

The exact API is not frozen in V1, but the build must remain portable enough to be hosted at different endpoints or mounted by another compatible shell.

## Critter Export Versus Application Export

These are separate concepts.

### Application export

The complete BitCritter browser bundle:

```text
HTML + JavaScript + CSS + manifest + service worker + assets
```

### Critter export

User-created data:

```text
name + palette + states + frames + playback settings + metadata
```

Do not mix the two formats.

## Future Extensibility

Reserve room in serialized critter data for future extensions, but do not require V1 to understand them.

Possible later namespaces include:

```text
identity
history
memories
relationships
extensions
```

Unknown future extension blocks should eventually be ignorable or preservable by compatible containers where feasible.

## Backend Boundary

A future backend may provide:

- account sync,
- backups,
- signed identity services,
- transfer coordination,
- shared or social features.

No backend may become necessary for the documented V1 success path without an intentional product-spec revision.
