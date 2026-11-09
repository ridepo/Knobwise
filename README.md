# Knobwise

**Patch editor and macro knob standard for the original Novation Circuit.**

**▶ Open Knobwise: https://ridepo.github.io/Knobwise/**

On the original Circuit, every patch assigns the 8 macro knobs differently, so you never know what a knob will do until you turn it. Knobwise is a browser-based patch editor that also defines a **knob standard**: knob N always has the same function, in every patch, and clockwise always means “more”.

Knobwise is an independent project. It is not affiliated with, endorsed by or supported by Novation or Focusrite.

## Use it

Open [the editor](https://ridepo.github.io/Knobwise/) in **Chrome, Edge or Opera** (they support Web MIDI), connect the Circuit over **USB**, press **Connect MIDI** and allow MIDI and SysEx when the browser asks.

You can also download `index.html` and open it from your computer: it is a single file with no external dependencies and works offline.

Safari does not support Web MIDI. Firefox needs MIDI permission for the site.

## What it does

- Edits every synth parameter of Synth 1 and Synth 2 live (CC/NRPN), and shows changes made on the Circuit.
- Reads the current patch from the Circuit, sends a whole patch, and stores it in one of the 64 slots.
- Opens and exports `.syx` files: single patches and banks of 64.
- Backs up all 64 slots of the Circuit to a bank file, and sends a bank back.
- Modulation matrix with a plain-language description of each slot.
- Checks every patch against the knob standard, explains what is wrong, and converts patches automatically. Misplaced destinations are moved to their own knob, and the patch keeps sounding the same when loaded.
- Undo/redo, unsaved-changes warnings, on-screen and computer keyboard, sections you can show or hide.

## The knob standard

| Knob | Name | Clockwise |
|---|---|---|
| 1 | Tone | soft to harsh |
| 2 | Cutoff | centre = the saved sound; left closes, right opens |
| 3 | Resonance | more resonance |
| 4 | Env Mod | more filter envelope |
| 5 | Attack | percussive to soft |
| 6 | Length | short to long |
| 7 | Drive | clean to saturated |
| 8 | Motion | still to alive |

Left to right, the knobs follow the signal path: oscillators → filter → amplifier → distortion, with the modulator last. Knobs 2, 3, 4 and 6 form the TB-303 block for acid and techno.

The full rules, the destinations that belong to each knob and the hardware tests behind them are in [STANDARD.md](STANDARD.md).

## Technical notes

- MIDI channels: Synth 1 on channel 1, Synth 2 on channel 2.
- Parameter numbers, value lists and the 340-byte SysEx patch format come from Novation's *Circuit Programmer's Reference Guide*.
- The Circuit answers SysEx requests over USB only.
- How the Circuit applies macro depth (depth ±64 = full parameter range, linear between start and end, no effect below start) is not documented by Novation. It was verified on a Circuit with listening tests, recorded in [STANDARD.md](STANDARD.md).

## Versions

See [CHANGELOG.md](CHANGELOG.md).

## License

Knobwise is free software, released under the [GNU General Public License v3.0](LICENSE) or any later version.
You may use, study, share and modify it; if you distribute a modified version, you must release it under the same license.
