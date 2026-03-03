Flux Apparition

An experimental C++ reverb firmware for the Daisy Seed on the PedalPCB Terrarium. It escapes standard algorithms by using a degrading external feedback loop with lo-fi decimation, SVF filtering, and ghostly pitch-smearing to create haunting, atmospheric washes.
Hardware Controls

Knobs

    Mix (Knob 1): Wet/Dry balance.

    Decay (Knob 2): Feedback amount fed into the degrading loop.

    Dwell (Knob 3): Input drive and saturation into the tank. Higher settings slow down the internal modulation rate.

    Tone (Knob 4): SVF lowpass filter cutoff inside the feedback loop.

    Mod (Knob 5): Reverb modulation depth.

    Atmosphere (Knob 6): Mix of the ghostly pitch-shifter (octave up + detune) inside the loop.

Switches

    Mode (SW 1): UP = Vintage routing. DOWN = Haunted (routes wet output back into the Pre-Delay for chaotic swells).

    Pre-Delay (SW 2): UP = Short slapback attack. DOWN = Envelope swell (pseudo-reverse bowing).

    Mod Character (SW 3): UP = Smooth sine modulation. DOWN = Warped (Sample & Hold style broken tape flutter).

    Lo-Fi (SW 4): UP = Clean reflections. DOWN = Aged (engages loop decimation and bitcrushing).

Footswitches

    Bypass (FS 1): DSP bypass. Allows existing reverb trails to decay naturally when disengaged.

    Apparition (FS 2): Momentary infinite freeze. Forces the feedback loop to maximum and slowly sweeps the Tone filter downward, degrading the frozen pad the longer it is held.

Building and Flashing

    Clone the repository and initialize submodules:
    Bash

    git clone https://github.com/FuzzyLotus/Flux-Apparition.git
    cd Flux-Apparition
    git submodule update --init --recursive

    Build the underlying Daisy libraries (only required once):
    Bash

    cd libDaisy && make
    cd ../DaisySP && make
    cd ..

    Compile the firmware and flash it to the Daisy Seed (ensure the Seed is in bootloader mode):
    Bash

    make
    make program-dfu
