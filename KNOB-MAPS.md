# Knob maps

On the original Novation Circuit every patch can assign the 8 macro knobs differently, so you never know what a knob will do until you turn it.
A **knob map** solves this: it gives each knob a fixed function, so whatever patch is loaded, knob N always does the same thing.

Knobwise offers two maps. Choose one in the editor (**Macros → Knob map**) and use it for the whole **bank**, the 64 synth patches stored on the Circuit: the Circuit cannot show which map a patch follows, so mixing maps in one bank brings the original problem back.

## Signal Path

Knobwise's own map, made for acid and techno and usable for any sound.
Left to right, the knobs follow the signal path: **oscillators → filter → amplifier → distortion**. The last knob is the modulator, which acts on everything.

| Knob | Name | Stage | Clockwise | Home of these destinations |
|---|---|---|---|---|
| 1 | **Tone** | oscillators | soft to harsh | Osc 1/2: interpolate, PW/index, v-sync, density, density detune, semitones, cents, level; ring mod; noise |
| 2 | **Cutoff** | filter | brighter (opens the filter) | Filter frequency, filter tracking |
| 3 | **Resonance** | filter | more resonance | Filter resonance |
| 4 | **Env Mod** | filter | more filter envelope | Env 2 → frequency |
| 5 | **Attack** | amplifier | percussive to soft | Env 1 attack, Env 2 attack |
| 6 | **Length** | amplifier | short to long | Env 1 decay, sustain, release; Env 2 decay, sustain, release |
| 7 | **Drive** | distortion | clean to saturated | Distortion, filter drive |
| 8 | **Motion** | modulators | still to alive | matrix slot 1–20 depth; LFO 1/2 rate, rate sync, slew; Env 3; chorus/phaser level, rate, feedback, depth, delay; portamento |

Knobs 2, 3, 4 and 6 are the TB-303 block: cutoff, resonance, envelope amount and decay. Resonance and filter envelope amount are on separate knobs, so they can be balanced against each other.

## Tracks

The same eight functions as the macro knobs of the Circuit Tracks, for people who move between the two machines. Which destinations sit behind each function is Knobwise's choice.

| Knob | Name | Clockwise | Home of these destinations |
|---|---|---|---|
| 1 | **Oscillator** | changes the oscillator sound | Osc 1/2: interpolate, density, semitones, cents, level; ring mod; noise |
| 2 | **Osc Mod** | more pulse width / index, sync, detune | Osc 1/2: PW/index, v-sync, density detune |
| 3 | **Amp Env** | slower and softer | Env 1 attack, decay, sustain, release |
| 4 | **Filter Env** | more filter envelope | Env 2 → frequency; Env 2 attack, decay, sustain, release |
| 5 | **Filter Freq** | brighter (opens the filter) | Filter frequency, filter tracking |
| 6 | **Resonance** | more resonance | Filter resonance, filter drive |
| 7 | **Modulation** | more movement | matrix slot 1–20 depth; LFO 1/2 rate, rate sync, slew; Env 3; portamento |
| 8 | **FX** | more effect | Distortion; chorus/phaser level, rate, feedback, depth, delay |

## Rules shared by all maps

1. **Every macro destination has exactly one home knob** in each map. Knob N only uses destinations whose home is knob N.
2. The only exception is **Post FX level**: it has no home, because a knob must never change the patch volume.
3. Clockwise always gives **“more”** of the function. For matrix depths and Env 2 → frequency, the knob increases the amount in the direction the patch already uses.
4. **The stored position is free**: the patch designer chooses where each knob starts. A knob stored in the middle can go both ways; a knob stored fully right has no room left for “more”.
5. A freshly loaded patch sounds exactly as designed, whatever the stored positions.
6. All 8 knobs have at least one destination with a non-zero depth that has an audible effect (the parameter must not already be at its limit).
7. Every patch has its own name (not “Initial Patch”) and a category.

## In the editor

- **Knob map** (in the Macros section) selects the map; the editor remembers the choice.
- Each macro card shows the knob's function in the selected map and a status: ✓ follows the map, ! warning, ✕ error, with the reason. A misplaced destination says which knob it belongs to.
- The destination menu lists that knob's destinations first.
- When a patch looks more like the other map, the editor says so and offers to switch.
- **Complete to map**:
  - moves misplaced destinations to their home knob, keeping start, end and depth;
  - removes Post FX level from the knobs;
  - fills empty knobs with the map's default assignments.

  Stored positions are left as they are. Only a knob that was empty gets a suggested starting position: 64 for the filter knob, so it can close and open the filter, and 0 for the others.

  The patch keeps sounding the same when loaded: the editor recalculates the base value of each affected parameter, taking all its macro slots into account. Only if the base value would leave its range does it also adjust the start or end of a moved slot. In the rare cases where the sound cannot be kept exactly (for example a knob stored fully right with the parameter already at its limit), it says so. If the home knob already has 4 destinations, the misplaced one stays where it is and is reported.

  Converting a patch from one map to the other works the same way: select the target map and press **Complete to map**.
- **Rewrite all knobs** replaces all 8 knobs with the map's default assignments.
- In a bank, **Check map** shows the state of all 64 patches and which map each one looks like; **Complete the whole bank to this map** converts them.

### Default assignments written for empty knobs

| Knob | Signal Path | Tracks |
|---|---|---|
| 1 | per audible oscillator: interpolate (wavetable), PW/index (if used), otherwise v-sync | per audible oscillator: interpolate (wavetable), otherwise density |
| 2 | Filter frequency +50, position 64 | per audible oscillator: PW/index (if used), otherwise v-sync |
| 3 | Filter resonance +50 | Env 1 attack +40, Env 1 release +40 |
| 4 | Env 2 → frequency ±40 | Env 2 → frequency ±32, Env 2 decay +32 |
| 5 | Env 1 attack +40, Env 2 attack +40 | Filter frequency +50, position 64 |
| 6 | Env 1 decay, Env 1 release, Env 2 decay, each +40 | Filter resonance +50 |
| 7 | Distortion +50 | as Signal Path knob 8 |
| 8 | depth of the first two active matrix slots ±30; if there are none, a free slot becomes LFO 1 ± → filter frequency at depth 0 (the sound does not change) and the knob raises its depth | Distortion +50, Chorus level +50 |

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
