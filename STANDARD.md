# The Knobwise standard

Macro knob standard for patches of the original Novation Circuit.

Goal: whatever patch is loaded, you know what each of the 8 macro knobs does.
The layout comes from techno and acid, but it works for any kind of sound.

## The 8 knobs

Left to right, the knobs follow the signal path:
**oscillators → filter → amplifier → distortion**.
The last knob is the modulator, which acts on everything.

| Knob | Name | Stage | Clockwise | Home of these destinations |
|---|---|---|---|---|
| 1 | **Tone** | oscillators | soft to harsh | Osc 1/2: interpolate, PW/index, v-sync, density, density detune, semitones, cents, level; ring mod; noise |
| 2 | **Cutoff** | filter | centre = the saved sound; left closes, right opens | Filter frequency, filter tracking |
| 3 | **Resonance** | filter | more resonance | Filter resonance |
| 4 | **Env Mod** | filter | more filter envelope | Env 2 → frequency |
| 5 | **Attack** | amplifier | percussive to soft | Env 1 attack, Env 2 attack |
| 6 | **Length** | amplifier | short to long | Env 1 decay, sustain, release; Env 2 decay, sustain, release |
| 7 | **Drive** | distortion | clean to saturated | Distortion, filter drive |
| 8 | **Motion** | modulators | still to alive | matrix slot 1–20 depth; LFO 1/2 rate, rate sync, slew; Env 3; chorus/phaser level, rate, feedback, depth, delay; portamento |

For techno and acid, knobs 2, 3, 4 and 6 are the TB-303 block: cutoff, resonance, envelope amount and decay.

## Rules

1. **Every macro destination has exactly one home knob** (table above). Knob N only uses destinations whose home is knob N.
2. The only exception is **Post FX level**: it has no home, because a knob must never change the patch volume.
3. Clockwise always gives **“more”** of the function. For matrix depths and Env 2 → frequency, the knob increases the amount in the direction the patch already uses.
4. **Stored position = 0** (fully left) for every knob except **2 “Cutoff”**, stored at **64** (centre).
5. A freshly loaded patch sounds exactly as designed: base parameter values take the stored position into account.
6. Resonance and filter envelope amount stay on two separate knobs, so they can be balanced against each other.
7. All 8 knobs have at least one destination with a non-zero depth that has an audible effect (the parameter must not already be at its limit).
8. Every patch has its own name (not “Initial Patch”) and a category.

## In the editor

- Each macro card shows the knob's function and a status: ✓ follows the standard, ! warning, ✕ error, with the reason. A misplaced destination says which knob it belongs to.
- The destination menu lists that knob's destinations first.
- **Complete to standard**:
  - moves misplaced destinations to their home knob, keeping start, end and depth;
  - removes Post FX level from the knobs;
  - fills empty knobs with the standard assignments;
  - sets stored positions to the standard.

  The patch keeps sounding the same when loaded. If the home knob already has 4 destinations, the misplaced one stays where it is and is reported.
- **Rewrite all knobs** replaces all 8 knobs with the standard assignments.
- In a bank, **Check standard** shows the state of all 64 patches; **Complete the whole bank** converts them.

### Standard assignments written for empty knobs

| Knob | Slots created |
|---|---|
| 1 | for each audible oscillator: interpolate if the waveform is a wavetable, PW/index if the waveform uses it, otherwise v-sync |
| 2 | Filter frequency +50, position 64, base frequency lowered to keep the sound |
| 3 | Filter resonance +50 |
| 4 | Env 2 → frequency ±40, in the direction already set |
| 5 | Env 1 attack +40, Env 2 attack +40 |
| 6 | Env 1 decay +40, Env 1 release +40, Env 2 decay +40 |
| 7 | Distortion +50 |
| 8 | depth of the first two active matrix slots ±30. If there are none, a free slot becomes LFO 1 ± → filter frequency at depth 0 (the sound does not change) and the knob raises its depth |

## Verified on the hardware

To keep the sound identical when a knob's stored position is not 0, the editor uses this model:
**depth ±64 = the parameter's full range**, linear between start and end, no effect below start.
Novation's guide does not document it, so it was checked on a Circuit with listening tests.
Synth 1 used macro 2 → Filter frequency; Synth 2 had no macro. Each pair sounded the same:

| Synth 1 slot | Synth 1 frequency | Synth 1 position | Synth 2 frequency |
|---|---|---|---|
| start 0, end 127, depth +32 | 0 | 127 | 64 |
| start 0, end 127, depth +32 | 0 | 64 | 32 |
| start 64, end 127, depth +32 | 40 | 127 | 104 |
| start 64, end 127, depth +32 | 40 | 96 | 72 |
| start 64, end 127, depth +32 | 40 | 50 | 40 |
| start 0, end 127, depth −32 | 104 | 127 | 40 |
| start 0, end 127, depth −32 | 104 | 64 | 72 |
| start 0, end 127, depth −32 | 104 | 0 | 104 |

A second destination was checked the same way: macro 3 → Filter resonance, start 0, end 127, depth +32, both synths at frequency 60.

| Synth 1 resonance | Synth 1 position | Synth 2 resonance |
|---|---|---|
| 0 | 127 | 64 |
| 0 | 64 | 32 |

This confirms the scale (depth ±32 = half the range, in both directions), that the effect is linear with the knob position between start and end, that the knob has no effect below start, and that the same rule holds for a second destination.

Not tested one by one: the other destinations. They go through the same macro mechanism, and the two tested destinations behave identically, so the editor applies the same rule to all of them.
