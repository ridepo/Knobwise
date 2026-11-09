# Changelog

## 0.2.0 — 2026-11-09
- Knob standard: the stored knob position is now free. The standard fixes only each knob's function and direction; the patch designer chooses where each knob starts.
- The checker no longer warns about stored positions, and “Complete to standard” no longer changes them. A knob that was empty still gets a suggested starting position (64 for Cutoff, 0 for the others).
- “Complete to standard” keeps the loaded sound in more cases: base values are recalculated per parameter with all its macro slots together, and start/end are fitted precisely when needed. Any case where the sound cannot be kept exactly is reported.
- Fixed: when a home knob was full, a moved destination could be written past the knob's 4 slots.

## 0.1.3 — 2026-11-09
- Project named **Knobwise**.
- Footer states that the project is not affiliated with Novation or Focusrite.

## 0.1.2 — 2026-11-09
- Modulation matrix: one slot per row, column headers, and the “In words” description of each slot.

## 0.1.1 — 2026-11-09
- Modulation matrix back to the compact layout with a small depth knob per slot.

## 0.1.0 — 2026-11-08
First version.
- Full synth patch editing for Synth 1 and Synth 2 over Web MIDI (CC/NRPN live, SysEx patch read, send and store).
- `.syx` import and export, bank backup and bank send.
- Macro knob standard with checking and automatic conversion; misplaced destinations are moved to their home knob.
- Undo/redo, unsaved-changes protection, visible sections, on-screen keyboard.
- English interface.
