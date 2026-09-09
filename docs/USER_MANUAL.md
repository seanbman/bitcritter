# BitCritter V1 User Manual

BitCritter is a mobile-first 32×32 pixel-pet creator. You can draw a critter, give it a name, manage its colors, create animation frames for different states, preview those animations, save the critter locally, and export its data.

BitCritter is designed to feel like a small retro handheld. The app display sits inside a plastic-style chassis with a D-pad, circular menu button, and A/B buttons. Touch remains the primary way to draw and edit, but the chassis controls are functional and provide an alternate navigation path.

---

## 1. Starting BitCritter

When BitCritter opens, the **My Pets** screen shows your saved critters.

From here you can:

- Tap an existing critter to open it.
- Tap **New Pet** or the **+** button to create a critter.
- Use the D-pad to move focus between visible controls.
- Press **A** to activate the focused control.
- Press the circular **Menu** button to open the current screen menu.

BitCritter saves V1 data locally on the device. After the application has been installed or cached for offline use, the primary creation workflow should remain available without a network connection.

---

## 2. Creating a Critter

Choose **New Pet** from My Pets.

A new critter begins with:

- a name,
- a blank 32×32 transparent canvas,
- an initial palette,
- one state named **Idle**,
- and one frame in that state.

The critter name can be changed later.

A single-frame critter is valid. You do not need to create multiple states or animations unless you want them.

---

## 3. Chassis Controls

The controls below appear beneath the display and are part of the BitCritter interaction model.

### D-pad

The D-pad moves focus through interface controls. When the drawing canvas has keyboard-style focus, it may also move the pixel cursor one cell at a time.

- **Up / Down / Left / Right:** move focus or canvas cursor.

Direct touch remains the fastest way to draw on a phone.

### A button

The **A** button is the primary confirm/action button.

Typical uses:

- open a focused critter,
- select a tab,
- confirm a menu item,
- activate a focused button,
- apply the current drawing tool at the canvas cursor.

### B button

The **B** button is the secondary/back button.

Typical uses:

- dismiss an open menu,
- cancel a pending action,
- return to the previous screen when doing so will not discard unsaved work.

### Circular Menu button

The circular center button opens the current screen menu.

The menu changes depending on context. Typical items include:

- Save,
- Save / Export,
- Rename,
- Duplicate,
- Redo,
- Clear Frame,
- Delete,
- Settings,
- Return to My Pets.

Destructive actions must ask for confirmation.

### Ellipsis menu

Some screens also contain a **•••** button inside the display. This opens actions that belong specifically to the current critter, frame, state, or screen.

The circular chassis Menu button and the on-screen ellipsis may expose overlapping actions, but the ellipsis is more local to the item currently being edited.

---

## 4. My Pets

The **My Pets** screen is the critter library.

Each critter card shows:

- the critter sprite or Idle preview,
- the critter name,
- and enough visual information to distinguish it from other saved critters.

### My Pets controls

**Critter card**  
Opens that critter.

**+ / New Pet**  
Creates a new critter.

**Circular Menu**  
Opens library-level actions such as Settings or import options when available.

**D-pad + A**  
Provides an alternate way to select and open critters.

A critter can be renamed, duplicated, or deleted through its contextual menu. Duplicating a critter creates a separate editable design and does not alter the original.

---

## 5. Critter Editor

The main critter editor contains three tabs:

- **Draw**
- **Palette**
- **Frames**

The critter name appears at the top of the editor. The back arrow returns toward My Pets. The ellipsis opens critter-level actions.

---

## 6. Draw Tab

The Draw tab contains the 32×32 canvas, drawing tools, and the critter palette.

### 32×32 canvas

Every frame is exactly 32 pixels wide by 32 pixels high.

The canvas is enlarged on screen using crisp nearest-neighbour scaling so individual pixels remain visible.

You can draw by dragging a finger across the canvas. Normal page scrolling should not interfere while a drawing gesture is active inside the canvas.

Transparent pixels are represented by empty canvas cells. Erasing a pixel restores transparency.

### Palette strip

The palette strip appears beneath the canvas.

Tap a swatch to make it the active drawing color. The selected palette slot is used by the Pencil and Fill tools.

Pixels reference palette slots rather than storing independent RGB colors. Editing one palette slot therefore updates every pixel that uses that slot throughout the critter.

### Pencil

The **Pencil** draws the active palette color.

- Tap a pixel to color one cell.
- Drag to draw continuously.
- With the canvas cursor focused, press **A** to draw the current pixel.

### Eraser

The **Eraser** changes pixels back to transparency.

- Tap or drag across pixels to erase them.

### Fill

The **Fill** tool replaces a connected region of matching pixels with the active palette color.

Fill affects only the connected region selected by the user, not every matching pixel in the frame.

### Eyedropper

The **Eyedropper** samples a visible pixel from the current frame and selects its palette slot as the active drawing color.

Sampling transparency does not create a new palette color.

### Mirror

The **Mirror** control mirrors the current frame horizontally.

This action changes the frame itself and can be undone.

### Undo

**Undo** reverses the most recent reversible edit to the current critter.

Typical reversible actions include drawing, erasing, filling, mirroring, and compatible frame edits.

### Redo

**Redo** restores the most recently undone edit.

Redo is available from the contextual menu when it is not shown as a dedicated on-screen control.

### Clear Frame

**Clear Frame** sets every pixel in the current frame to transparency.

It is available from the contextual menu and requires confirmation if the frame contains artwork.

---

## 7. Palette Tab

The Palette tab manages the indexed colors used by the critter.

Each row represents one palette slot and shows:

- slot number,
- color swatch,
- color value,
- edit control,
- delete control when deletion is safe.

### Edit a color

Tap the edit icon beside a palette slot to change that color.

Because frames store palette indices, changing a slot recolors every pixel using that slot across all frames and states.

### Add Color

Tap **Add Color** to append a new palette slot.

V1 should keep the palette deliberately small and usable on a phone. The implementation may enforce a documented maximum palette size.

### Delete a color

A palette color can be deleted only when doing so will not silently corrupt artwork.

If the color is currently used, BitCritter must either:

- refuse deletion until the color is unused, or
- require the user to explicitly replace those pixels with another slot.

V1 must never silently remap used colors to an arbitrary value.

### Transparency

Transparency is not treated as an ordinary visible color swatch. The Eraser writes transparent pixels directly.

---

## 8. Frames Tab

The Frames tab manages animation states and the frames inside them.

A **state** is a named action or condition such as:

- Idle
- Walk
- Sleep
- Happy
- Sad
- Eat
- Hurt
- Celebrate
- or a custom state

States are optional. A critter may contain only Idle.

### State selector

The state selector shows the currently active state.

Choose another state to edit or preview its frames.

### Frame thumbnails

Each frame appears as a small thumbnail.

Tap a thumbnail to select that frame for editing.

### Add Frame

Tap **+** beside the frame thumbnails to add a frame to the current state.

When possible, the user should be offered a fast path to create the new frame as a duplicate of the current frame because most pixel animation is created by changing only a few pixels between frames.

### Duplicate Frame

Duplicate creates a copy of the current frame immediately after it in the frame order.

This is the preferred workflow for creating blinking, breathing, walking, tail movement, and similar small animations.

### Delete Frame

Delete removes the selected frame after confirmation when necessary.

A state must retain at least one valid frame unless the state itself is being deleted.

### Reorder Frames

Frames can be reordered within a state.

Touch users may drag a frame thumbnail to a new position. A non-drag alternative must also exist through a frame context menu, such as **Move Left** and **Move Right**.

### Add State

Tap **Add State** to create a new named state.

The user may choose a suggested state name or provide a custom name.

### Rename State

Rename is available from the state context menu.

### Delete State

Delete removes a state and its contained frames after confirmation.

If deleting the final state would leave the critter without a usable frame, BitCritter must prevent the action or create a valid fallback Idle state.

### Play button

The Play button beside the selected state opens or starts animation preview for that state.

---

## 9. Preview Screen

Preview shows the critter animation without the drawing grid.

### State dropdown

Choose which state to preview.

### Previous Frame

Moves to the previous frame when playback is paused.

### Play / Pause

Starts or pauses animation playback.

### Next Frame

Moves to the next frame when playback is paused.

### FPS selector

The FPS selector controls playback speed.

The V1 mockup uses simple choices such as:

- 1 FPS
- 2 FPS
- 4 FPS
- 8 FPS

The exact supported values may be expanded later, but V1 should keep the control simple.

### Loop toggle

When **Loop** is enabled, the state repeats continuously.

When disabled, playback stops after the final frame.

---

## 10. Saving

BitCritter saves V1 critters locally using persistent browser storage.

The interface should show whether the current work has been saved.

Core editing must not require an account or network connection.

### Automatic and explicit saving

The implementation may autosave safe edits, but an explicit **Save** action must remain available from the menu so the user can deliberately commit the current state before leaving or exporting.

### Reopening a critter

Saved critters appear in My Pets after the app is reopened.

---

## 11. Save / Export

The Save / Export screen contains the critter name, save status, export actions, and format information.

### Pet Name

The name field displays the current critter name. Use the edit control to rename it.

### Save

Saves the latest local critter data.

### Export Critter Data

Exports the structured critter representation for backup or compatible tools.

V1 exported data should contain at minimum:

- format version,
- critter name,
- created and modified timestamps,
- palette,
- states,
- frame order,
- frame pixel grids,
- state playback settings.

### Export for JavaScript

Exports data in a JavaScript-friendly representation such as JSON so another application can load the sprite, palette, states, and animation data.

This is critter-data export. It is separate from the BitCritter application's own portable JavaScript build.

### Export Sprites

Exports visual sprite output for use outside BitCritter. The implementation may provide individual frame images or a documented sprite-sheet format.

### Pet Info

Displays format and file information such as:

- format version,
- created date,
- modified date,
- frame count,
- state count.

---

## 12. Menus and Context Actions

BitCritter uses menus to keep the visible interface small.

### Critter menu

Typical actions:

- Save
- Save / Export
- Rename Critter
- Duplicate Critter
- Delete Critter
- Return to My Pets

### Draw context menu

Typical actions:

- Redo
- Clear Frame
- Duplicate Frame
- Frame actions

### Frame context menu

Typical actions:

- Duplicate Frame
- Delete Frame
- Move Left
- Move Right

### State context menu

Typical actions:

- Rename State
- Duplicate State when implemented
- Delete State
- Playback settings

Menus should hide or disable actions that are invalid in the current context.

---

## 13. Installing BitCritter on a Phone

BitCritter is intended to be installable as a Progressive Web App.

When the browser and operating system support installation, the user can add BitCritter to the device home screen and launch it in a standalone app-like window.

After the required application shell and assets have been cached, the following core V1 tasks should work offline:

- open saved critters,
- create a critter,
- draw and erase,
- edit palettes,
- manage frames and states,
- preview animations,
- save locally,
- export local critter data where the browser allows local file generation.

A server may provide updates or future sync features, but it must not be required for these primary V1 tasks.

---

## 14. V1 Data Model in Plain Language

A BitCritter critter consists of:

```text
Critter
├── name
├── format version
├── created / modified metadata
├── palette
└── states
    ├── Idle
    │   ├── frame 1: 32×32 palette indices
    │   ├── frame 2: 32×32 palette indices
    │   └── playback settings
    └── custom states...
```

Pixels store references to palette slots. They do not independently store arbitrary color values.

This is why changing one palette color can recolor the same indexed color throughout every animation frame.

---

## 15. What V1 Does Not Yet Do

The following ideas are intentionally future work:

- cryptographically unique critter identity,
- signed creation records,
- authenticated life history,
- memories,
- relationships with other critters,
- witnessed or corroborated events,
- secure transfer between compatible containers,
- server accounts or cloud synchronization as a requirement.

The V1 data format should remain extensible enough to add these concepts later without making them part of the current editing experience.

---

## 16. BitCritter Design Rule

The application UI is black and white. Color belongs to the critter.

The retro chassis is part of the interaction language: D-pad left, circular menu button in the middle, A/B buttons right. The chassis contains no speaker grille and no smiley-face decoration.

The result should feel like a small creative handheld that happens to live on a phone.
