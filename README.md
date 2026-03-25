# Moonchild
### Chorus, Reverb & Freeze for the Electrosmith Daisy Seed / PedalPCB Terrarium

Moonchild is a hi-fi multi-effect pedal implemented in C++ for the [Daisy Seed](https://electro-smith.com/products/daisy-seed) microcontroller running on the [PedalPCB Terrarium](https://www.pedalpcb.com/product/terrarium/) guitar pedal platform.

It combines a transparent modulated chorus, a plate/hall reverb with continuous character morphing, and a freeze function that captures your reverb tail as a living, evolving pad you can play over.

*by Folklore Electronics*

---

## Features

- **Chorus** — three decorrelated delay lines with triangle LFO modulation and slow drift oscillator
- **Reverb** — four-tap FDN with input diffusion, plate/hall character morphing, and stereo late field
- **Freeze** — captures the reverb tail into three parallel voices that evolve over time
- **Tilt EQ** — full-range tone control that shifts spectral balance without killing content
- **Chorus Enhancement** — shimmer voice chain adds octave-up harmonic layer to the chorus (SW1)
- **Orbit / Widen** — stereo field expansion with bloom (SW2)
- **Bond / Interaction** — cross-couples the chorus and reverb engines with feedback (SW3)
- **Character** — continuous plate-to-hall reverb morphing (SW4)

---

## Controls

| Control | Label | Function |
|---|---|---|
| Knob 1 | FLOW | Chorus LFO rate (0.1 – 3 Hz) |
| Knob 2 | VEIL | Dry/wet crossfade |
| Knob 3 | FADE | Reverb decay time |
| Knob 4 | SWAY | Chorus modulation depth (0.2 – 5 ms) |
| Knob 5 | BIND | Chorus/reverb balance (left = chorus, right = reverb) |
| Knob 6 | HAZE | Tilt EQ (left = warm, noon = flat, right = bright) |
| SW1 | AURA | Chorus enhancement on/off |
| SW2 | ORBT | Orbit / stereo widening on/off |
| SW3 | LINK | Bond / chorus-reverb interaction on/off |
| SW4 | HALL | Reverb character (plate to hall) on/off |
| FS1 | CHR | Tap: chorus on/off. Hold: momentary chorus-to-freeze send |
| FS2 | REV | Tap: reverb on/off. Hold: freeze toggle |

### LEDs

| LED | Off | Solid | Pulsing |
|---|---|---|---|
| LED1 | Chorus off | Chorus on | FS1 held (sending to freeze) |
| LED2 | Reverb off | Reverb on | Freeze active |

LED pulse range is 50–100% brightness to avoid flicker.

---

## Hardware Requirements

- [Electrosmith Daisy Seed](https://electro-smith.com/products/daisy-seed)
- [PedalPCB Terrarium](https://www.pedalpcb.com/product/terrarium/) (or compatible Daisy Seed pedalboard)
- ARM DFU-capable USB connection for flashing

---

## Flashing (No Computer Skills Required)

You don't need to install anything or know how to code. Just download the `.bin` file from the [Releases page](https://github.com/FuzzyLotus/Moonchild/releases) and follow these steps:

### Step 1 — Put your Daisy Seed into bootloader mode
1. Locate the two small buttons on the Daisy Seed: **BOOT** and **RESET**
2. Hold down **BOOT**
3. While holding BOOT, tap **RESET**
4. Release **BOOT**
5. The Daisy Seed is now ready to receive firmware

### Step 2 — Flash using the web programmer
1. Go to **[flash.daisy.audio](https://flash.daisy.audio)**
2. Click the **File Upload** tab
3. Click **BROWSE...** and select the `moonchild.bin` file you downloaded
4. Click the **FLASH** button (this may prompt you to select your Daisy Seed from a browser popup)
5. Wait for it to finish, and your pedal is ready!

> The web programmer works in Chrome or Edge. It will not work in Firefox or Safari.

### 🪟 Windows Users: Web Flasher Not Working?
If your Windows PC doesn't recognize the Daisy Seed in the browser flasher, you likely need to replace the default USB driver with WinUSB.
1. Put your Daisy Seed in BOOT mode (Hold **BOOT**, tap **RESET**, release **BOOT**).
2. Download and run [Zadig](https://zadig.akeo.ie/).
3. Go to **Options** > **List All Devices**.
4. Select **DFU in FS Mode** (or **STM32 BOOTLOADER**) from the main dropdown menu.
5. Ensure the target driver with the green arrow points to **WinUSB**.
6. Click **Replace Driver**.
7. Refresh the web flasher page and try connecting again.

---

## How It Works

### Chorus Engine

Three delay lines with offset triangle LFO modulation create a rich ensemble effect. A 12kHz anti-alias filter blended 55/45 with the raw input keeps the chorus transparent. A single gentle saturation stage (linear below 0.8) runs in parallel with the clean signal at 72/28 for dynamics preservation.

### Reverb Engine

Four-tap feedback delay network with four input diffusion allpasses. Delay tap positions crossfade between plate (bright, tight) and hall (dark, wide) based on SW4 state and K3 decay setting. The late reflection field includes stereo cross-feed, halo blending, and slow drift modulation for spatial movement.

### Freeze

Hold FS2 to capture the current reverb tail into three parallel freeze voices with staggered loop lengths (97ms, 149ms, 199ms). The frozen pad evolves over time through texture drift, tonal evolution, and live-play reactivity. Hold FS1 while frozen to blend live chorus into the frozen bed.

Turning off reverb while frozen triggers a graceful shutdown tail that decays naturally instead of cutting abruptly.

### Signal Path

The dry signal is never filtered on the bypass path. An 80Hz HPF only applies to the effect engine inputs. A 120Hz bass recovery filter blends lost low end back into the wet bus. Matched stereo HPFs on the reverb output prevent phase mismatch on mono sum. The tilt EQ replaces a traditional resonant lowpass for full-range usability across the entire knob sweep.

---

## Building from Source

### 1. Clone the DaisyCloudSeed repository and its submodules

```bash
git clone https://github.com/GuitarML/DaisyCloudSeed
cd DaisyCloudSeed
git submodule update --init --recursive
```

### 2. Build the required libraries

```bash
make -C libdaisy
make -C DaisySP
```

### 3. Clone Moonchild into the petal folder

```bash
cd petal
git clone https://github.com/FuzzyLotus/Moonchild
cd Moonchild
```

### 4. Build and flash

```bash
make
make program-dfu
```

> Connect your Daisy Seed via USB and put it into DFU mode (hold BOOT, tap RESET, release BOOT) before running `make program-dfu`.

---

## Toolchain

You need the ARM GCC embedded toolchain. On most Linux systems:

```bash
# Fedora/RHEL
sudo dnf install arm-none-eabi-gcc arm-none-eabi-newlib

# Ubuntu/Debian
sudo apt install gcc-arm-none-eabi
```

Or download directly from [ARM's website](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads).

---

## Project Structure

```
Moonchild/
├── MoonChild.cpp        # Main DSP source
├── terrarium.h          # Terrarium hardware abstraction (included locally)
├── Makefile
└── README.md
```

`terrarium.h` is included directly in this repo so you don't need to rely on the Terrarium submodule separately.

---

## Switch Wiring Note

SW2 (ORBT) and SW3 (LINK) are physically swapped in software to match the intended panel layout. SW2 reads from `Terrarium::SWITCH_3` and SW3 reads from `Terrarium::SWITCH_2`. If you're wiring your own enclosure, label them according to the panel layout above, not the PCB silkscreen.

---

## Contributing

Pull requests are welcome! If you build on this project, please share your work openly under the same license.

- Fork the repo
- Create a branch: `git checkout -b my-feature`
- Commit your changes: `git commit -m "Add my feature"`
- Push and open a Pull Request

Please test on real hardware before submitting.

---

## License

GNU General Public License v3.0 — see [LICENSE](LICENSE) for details.

You are free to use, modify, and share this project. You may **not** use it in closed-source or commercial products. Any derivatives must also be released under GPL-3.0.

---

## Credits

Built on the [GuitarML DaisyCloudSeed](https://github.com/GuitarML/DaisyCloudSeed) build environment, which bundles [libDaisy](https://github.com/electro-smith/libDaisy) and [DaisySP](https://github.com/electro-smith/DaisySP).

`terrarium.h` is copyright [PedalPCB](http://www.pedalpcb.com), included with original copyright notice intact.

*Moonchild by Folklore Electronics*
