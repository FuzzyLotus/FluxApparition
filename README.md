MoonChild
A boutique ambient DSP instrument for Electro-Smith Daisy Petal—where motion (chorus), space (reverb), and memory (freeze) behave as one evolving voice.

Overview
MoonChild is not a conventional multi-effect chain. It’s a single, composed instrument: a chorus and reverb that breathe together around a freeze system designed to hold rather than constantly destabilize. The result is an ambient platform that stays musical under the hands—lush when you lean in, steady when you stop, and intentional in how it grows over time.

MoonChild is a finished, artist-tested build. The core DSP is complete and the master is treated as a locked reference.

Core concept / design philosophy
MoonChild’s design is built around one rule:

Freeze is the stable anchor.
The frozen bed is captured as a musically stable “time anchor.” Motion and space evolve around it rather than repeatedly re-writing it. The pedal remains alive and expressive, but the memory stays intact: no accidental re-capture, no wobble, no pumping—just a stable bed with subtle evolution in the layers that follow.

Features
Chorus engine — motion / water
Lush, organic, stable chorus tuned for musical movement rather than obvious modulation.
Asymmetric voicing for width and depth without “chorus glare.”
No ticking, and stable behavior across performance dynamics.
Clean bypass behavior (no bleed when off).
Reverb engine — space / moon
Integrated as part of the same instrument as the chorus, not a separate “reverb block.”
Expressive bloom and ambient expansion that remains playable and controllable.
Plate ↔ hall character shaping via a dedicated switch, voiced for musical “space” rather than exaggerated special effects.
Naturally bonded to the chorus so motion and space feel cohesive.
Freeze system — memory / time anchor
Stable frozen bed intended to sit under live playing as a reliable foundation.
No accidental re-capture: freeze behavior is designed to preserve the captured material.
Graceful shutdown tail when disabling reverb while freeze is active—no abrupt collapse.
Extended fade-out behavior for musical exits.
Consistent freeze loudness tuned for performance reliability.
Freeze evolution (post-freeze)
Age-based evolution: the post-freeze layer becomes gradually more cloud-like over time.
Subtle responsiveness to new playing only in the post-freeze layer.
The core frozen capture remains stable and undisturbed.
No rhythmic pumping, no pitch wobble, no obvious ducking.
Chorus-to-freeze send (momentary)
FS1 hold enables a momentary chorus → freeze send.
Slightly enhanced for presence, intentionally subtle and musical.
Designed for performance gestures—not a latched “always feeding” state.
LED behavior
Hold states pulse slowly for clear, non-distracting feedback.
The reverb/freeze LED pulse subtly deepens with freeze age.
Expressive status indication without becoming a visual effect.
Control layout (final)
Knobs
K1 — Motion: chorus rate / motion speed of the instrument.
K2 — Mix: wet/dry blend.
K3 — Bloom: reverb decay / expansion.
K4 — Flow: modulation depth / movement intensity.
K5 — Tether: bonding/interaction between motion and space.
K6 — Aura: tonal contour of the instrument.
Switches
SW1 — Halo: chorus enhancement / additional articulation.
SW2 — Wide: stereo widening / orbiting space feel.
SW3 — Merge: interaction strength between chorus and reverb character.
SW4 — Orbit: reverb character (plate ↔ hall style shaping).
Footswitches
FS1 — Chorus / Send
Tap: chorus on/off
Hold: momentary chorus-to-freeze send (only while held)
FS2 — Reverb / Freeze
Tap: reverb on/off
Hold: freeze toggle
DSP architecture (high-level)
MoonChild is implemented in C++ using a libDaisy / DaisySP-style embedded DSP workflow with real-time audio processing on Daisy Petal.

At a high level:

A custom chorus provides stable motion with a voiced stereo image.
A custom reverb is tuned as a companion to the chorus, shaping bloom and space as one instrument.
A freeze subsystem captures and sustains a stable bed with safeguards against accidental re-capture.
A post-freeze evolution layer adds gradual, age-based diffusion and subtle performance responsiveness while preserving the integrity of the frozen anchor.
The architectural intent is musical: capture once, hold steady, evolve the surroundings.

Build status (locked master)
This repository represents a completed, validated master build:

The core DSP is complete.
The pedal has been artist-tested and the master is locked.
If you want to experiment (new algorithms, alternate voicings, different freeze behaviors), treat that work as:

a new branch, or
an explicitly named experimental variant,
not casual edits to the master.

Hardware / platform
Platform: Electro-Smith Daisy Petal (Daisy Seed ecosystem)
Language: C++
Domain: real-time embedded audio DSP
Workflow: Makefile-based build, DaisySP/libDaisy-style development
Usage / playing notes
MoonChild rewards intentional playing—both sparse and dense.

Establish the bed: engage reverb, then hold FS2 to freeze. The capture becomes your stable anchor.
Play over memory: the frozen bed stays stable while the instrument evolves around it—space breathes, motion moves, but the anchor remains.
Gesture with FS1: with chorus enabled, hold FS1 to momentarily feed chorus into the freeze path. Use it like a brush stroke, not a mode.
Exit gracefully: if you disable reverb while frozen, MoonChild performs a controlled shutdown tail rather than snapping the world off.
The goal is confidence: you should be able to build an ambient structure live, then trust it while you perform.

Repository guidance
MoonChild.cpp contains the primary firmware source.
terrarium.h defines the Terrarium hardware mapping used by the firmware.
The top-level Makefile describes the build configuration for Daisy Petal workflows.
PreProd/ is intentionally not part of the published build and is ignored by git.
If you are archiving a performance-validated version, tag releases from main and do experimental work elsewhere.

Optional future directions (as experimental branches)
MoonChild is complete as-is. Any future ideas—alternate voicings, additional modes, or variant evolution behaviors—belong in clearly named experimental branches to preserve the locked master.

License
See LICENSE (GPL-3.0).

Closing note
MoonChild is an instrument built from motion, space, and memory—designed to feel alive, but never unstable.