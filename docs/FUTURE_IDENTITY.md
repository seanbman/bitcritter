# BitCritter Future Identity and Container Direction

## Status

This document records future architectural intent. None of these features are required for V1.

V1 is a local pixel-pet creator. Future versions may allow a critter to become a portable persistent entity whose appearance, state, memories, and history can move between compatible containers.

## Core Principle

**Appearance may be copied. Identity must be proven. History must be earned.**

Digital bytes can always be duplicated. BitCritter should therefore avoid pretending that sprite copying can be prevented absolutely.

The stronger goal is to make authentic identity and historical continuity verifiable.

## Conceptual Critter Model

```text
Critter
├── Body
│   ├── 32×32 frames
│   ├── palette
│   ├── animations
│   └── states
│
├── Identity
│   ├── public key
│   ├── identity hash
│   └── creation record
│
└── Life
    ├── memories
    ├── experiences
    ├── relationships
    ├── learned state
    └── authenticated history
```

V1 implements only the Body portion plus basic metadata.

## Identity Direction

A future critter may have its own cryptographic key pair.

Conceptually:

```text
identity id = hash(public key)
```

The public identity can travel with the critter. The corresponding signing authority must be protected appropriately and must not be exposed as ordinary editable metadata.

The identity should not be derived only from the current sprite bytes. Appearance can change while the critter remains the same entity.

## Signed History

Future life events may form an append-only hash-linked sequence.

```text
GENESIS
   │
   ▼
event 1
   │ hash(previous)
   ▼
event 2
   │ hash(previous)
   ▼
event 3
```

A conceptual event may contain:

```json
{
  "event": "entered_container",
  "subject": "critter:example-id",
  "timestamp": 0,
  "previous": "hash-of-prior-event",
  "payload": {},
  "signature": "signature-data"
}
```

The exact format and cryptographic scheme are deliberately not frozen yet.

The intended property is continuity: an observer should be able to verify whether a presented event belongs to the same authenticated chain.

## Copies Versus Authentic Continuity

Someone may copy:

- a sprite,
- a name,
- a palette,
- an exported representation.

That copied appearance should not automatically carry the original critter's authenticated identity and life history.

A replica may look identical while lacking the cryptographic continuity needed to prove it is the same historical entity.

## Memories

Future memories may be typed rather than stored as arbitrary undifferentiated text.

Possible categories:

```text
memory
├── observation
├── interaction
├── achievement
├── relationship
├── preference
└── internal reflection
```

Memories may include provenance indicating where they came from.

A subjective memory may be asserted only by the critter. A significant external event may also be witnessed or signed by a compatible container or another critter.

This allows future systems to distinguish between:

- self-reported memory,
- container-observed event,
- mutually witnessed interaction,
- strongly corroborated historical event.

## Containers

A container is any application or environment that satisfies the BitCritter compatibility interface.

Examples could include:

- a habitat app,
- a small game,
- a website,
- a desktop companion,
- a hardware device,
- another browser application.

The critter should not be defined by whichever container currently hosts it.

## Capability Negotiation

Different containers may support different features.

Example:

```text
Container A
✓ appearance
✓ states
✓ emotes
✗ memories
✗ relationships

Container B
✓ appearance
✓ states
✓ emotes
✓ memories
✓ relationships
✓ environment events
```

A simpler container should still be able to host a critter without understanding every future extension.

## Possible JavaScript Interface

A future container contract may resemble:

```ts
interface CritterContainer {
  capabilities(): string[];
  enter(critter: unknown): Promise<void>;
  leave(): Promise<unknown>;
  perceive(event: unknown): Promise<void>;
  act(action: unknown): Promise<void>;
  remember(memory: unknown): Promise<void>;
}
```

A critter-facing API may eventually expose concepts such as:

```text
identity
appearance
states
emotes
memories
history
relationships
```

The precise interface should be designed only after V1 usage makes the real needs clearer.

## Transfer Versus Export

Future work should distinguish these concepts.

### Export

Produces a copyable representation for backup, inspection, development, or compatible tooling.

### Transfer

Represents an authenticated handoff from one compatible container to another.

A transfer may eventually produce historical events such as:

```text
departed container A
        │
        ▼
 signed handoff
        │
        ▼
arrived container B
```

The goal is not to make bytes physically uncopyable. The goal is to make legitimate continuity distinguishable from ordinary copying.

## Format Extensibility

V1 serialized data should reserve conceptual room for future sections such as:

```text
identity
history
memories
relationships
extensions
```

V1 does not need to emit meaningful values for them.

Future compatible containers should ideally be able to ignore unsupported extensions rather than rejecting the entire critter.

## Security Caution

Do not implement cryptographic uniqueness by simply hashing the whole exported critter file. That would bind identity to mutable appearance and would not solve ownership of signing authority.

Any future cryptographic design must explicitly define:

- key generation,
- key storage,
- signing authority,
- recovery,
- transfer semantics,
- revocation or compromise handling,
- event verification,
- cloning behavior,
- backup behavior,
- privacy boundaries.

These require a dedicated protocol design phase and are intentionally outside V1.
