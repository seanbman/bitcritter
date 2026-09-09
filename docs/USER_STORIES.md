# BitCritter V1 User Stories

## Epic 1 — Critter Creation

- As a user, I can create a new critter so that I can begin designing a character.
- As a user, I can give my critter a name.
- As a user, I can start from a blank 32×32 canvas.
- As a user, I can save my critter and continue editing it later.
- As a user, I can rename my critter.
- As a user, I can duplicate a critter without changing the original.
- As a user, I can delete a critter I no longer want.

## Epic 2 — Drawing

- As a user, I can draw individual pixels on a 32×32 grid using touch input.
- As a user, I can erase pixels back to transparency.
- As a user, I can select a color from the critter palette.
- As a user, I can flood-fill a connected region.
- As a user, I can sample a color already present on the canvas.
- As a user, I can undo recent edits.
- As a user, I can redo edits I have undone.
- As a user, I can clear the current frame.
- As a user, I can mirror the current frame horizontally.
- As a user, I can draw without the page scrolling during the drawing gesture.

## Epic 3 — Palette

- As a user, I can add colors to my critter palette.
- As a user, I can edit an existing palette color.
- As a user, I can select the active drawing color.
- As a user, I can remove an unused palette color.
- As a user, I am protected from silently corrupting artwork when removing a used color.
- As a user, I can change one palette slot and see every pixel using that slot update automatically.
- As a user, I can use transparency without treating it as an ordinary visible color.

## Epic 4 — Frames

- As a user, I can create multiple frames for a critter state.
- As a user, I can duplicate the current frame to create small animation changes quickly.
- As a user, I can delete a frame.
- As a user, I can reorder frames within a state.
- As a user, I can reorder frames without being forced to drag.
- As a user, I can select a frame to edit.
- As a user, I can see frame thumbnails while editing.

## Epic 5 — States

- As a user, I can organize animation frames into named states.
- As a user, I begin with a valid Idle state.
- As a user, I can create states such as Walk, Sleep, Happy, Sad, Eat, Hurt, Celebrate, or my own custom state.
- As a user, I can rename a state.
- As a user, I can delete a state without leaving the critter in an invalid condition.
- As a user, I can control frame order within a state.
- As a user, I can choose whether a state loops.
- As a user, I can control a state's playback speed.

## Epic 6 — Animation Preview

- As a user, I can preview the selected state as an animation.
- As a user, I can start and pause playback.
- As a user, I can move to the previous or next frame while paused.
- As a user, I can change preview FPS.
- As a user, I can enable or disable looping.

## Epic 7 — Critter Library

- As a user, I can see all critters saved on the device.
- As a user, I can open an existing critter from the library.
- As a user, I can identify each critter by name and sprite preview.
- As a user, I can see an Idle preview when one is available.

## Epic 8 — Saving and Persistence

- As a user, my saved work survives closing and reopening the app.
- As a user, I can see whether my current work has been saved.
- As a user, I can keep multiple independent critters.
- As a user, I do not need an account to use the core app.
- As a user, I can keep using core creation features offline after BitCritter has been installed or cached.

## Epic 9 — Export

- As a user, I can export structured critter data for backup or compatible tools.
- As a user, I can export a JavaScript-friendly representation of my critter data.
- As a user, I can export visual sprite output.
- As a developer, I can determine the critter data format version.
- As a developer, I can access each frame as a 32×32 grid of palette indices.
- As a developer, I can access states and their ordered animation frames programmatically.

## Epic 10 — Mobile Installation

- As a user, I can add BitCritter to my phone home screen when my browser supports PWA installation.
- As a user, I can launch the installed app in a standalone app-like window.
- As a user, I can reopen saved critters while offline.
- As a user, app updates do not destroy my locally saved critters.

## Epic 11 — Chassis Controls

- As a user, I can navigate focus using the D-pad.
- As a user, I can activate the focused control with A.
- As a user, I can cancel, dismiss, or go back with B where appropriate.
- As a user, I can open the current screen menu with the circular Menu button.
- As a user, I can access item-specific secondary actions through the on-screen ellipsis menu.
- As a user, I can complete all primary workflows by touch without depending on hover.

## Epic 12 — Visual Design

- As a user, I see a black-and-white interface so that critter artwork remains the focus.
- As a user, I see color only in critter artwork and palette swatches.
- As a user, selected tools are communicated through black/white contrast rather than arbitrary accent colors.
- As a user, I can comfortably use the app in portrait orientation on a smartphone.
- As a user, the retro chassis controls remain consistent between screens.
