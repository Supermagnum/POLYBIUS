# POLYBIUS — Reproduction Project Specifications
### *"Property of US Government / SRI International"*
#### Hackerspace/Makerspace Showpiece — Period Reproduction 1981-1982

---

## Overview

A period-authentic reproduction arcade cabinet inspired by the Polybius urban legend.
Designed as a conversation piece and functional game unit for hackerspace/makerspace environments.
Not intended as a forgery — a loving, technically accurate homage to the golden age of arcade hardware.

---

## Cabinet

- Standard **Midway/Atari upright** cabinet style, common 1981 form factor
- Slightly worn finish — chipped paint, faded marquee, authentic patina
- **Cabinet door: glass window panel** to expose internal hardware for viewing
- Worn joystick surround and button bezel
- Coin mechanism (functional or non-functional)
- Slightly faded/flickering fluorescent marquee backlight
- Period correct speaker grille cloth
- Subtle 60Hz hum from power supply — a feature, not a bug

---

## Display

- **Wells-Gardner or equivalent CRT raster scan monitor**
- Period correct curved glass face
- Authentic phosphor glow and visible scan lines
- Slight screen burn-in pattern (simulated or natural)
- No LCD substitutes — CRT only for authenticity

---

## PCB

- **Green PCB, no copper fills** — bare, utilitarian government look
- **100% THT (through-hole) components** — no SMD
- **Lead solder** — 60/40 tin-lead, period correct
- Components socketed where appropriate (EPROMs especially)
- **Edge finger connectors** for board interconnects
- **Molex connectors** for power and larger harnesses
- **JST connectors** for smaller signal harnesses
- **Flat ribbon cables** between boards
- **Test points** placed at natural locations:
  - CPU clock line
  - Reset line
  - Sound chip output before amplifier
  - Video sync signals (H-sync, V-sync)
  - Power rails (+5V, +12V, GND)
  - EPROM chip select lines
  - Audio amplifier input/output
- Silkscreen: **SRI International logo**
- Silkscreen: **"PROPERTY OF US GOVERNMENT"**
- Government-style serial number format (e.g. SRI-GOV-1981-XXXX)
- Slight oxidation on edge connectors — period authentic

---

## CPU

- **Zilog Z80** or **Motorola 6809**
- 6809 preferred for its clean architecture and West Coast developer familiarity
- Period correct clock speed (1-4 MHz)

---

## ROM

- **Intel 2732 EPROMs** (4KB each)
- Approximately **10 chips** for ~40KB total
- Chips in DIP-24 sockets — swappable, mysterious looking
- UV-erasable quartz windows visible on chips
- Hand-labeled chips with government-style markings

---

## RAM

- Period correct **4116 or 4164 DRAM** chips
- Or **6116 SRAM** for simpler design
- Fully socketed

---

## Sound

**Primary sound chip (choose one or combine):**
- **GI AY-3-8910** — period perfect, built-in noise generator, flexible
- **Yamaha YM2149** — AY-3-8910 compatible, excellent quality
- **TI SN76489** — dead-on period correct
- **Namco 54XX** — late 1982, acceptable within reproduction window

**Secondary/supplemental:**
- **HC-55516 (CVSD)** — for distorted, unsettling voice/speech elements
- Adds genuine psychological unease — period correct (Williams hardware)

**Audio output:**
- Period correct small speaker
- Slightly tinny cabinet acoustics
- Simple transistor or LM386 amplifier circuit
- Test point at amplifier input and output

**Sound palette (not strictly locked, period appropriate):**
- Square waves
- Sawtooth approximations
- Sine-like tones via DAC or filtered output
- White/pink noise
- Occasional distorted CVSD voice fragments

---

## Software

**Language: C — West Coast / K&R Dialect**

Period correct C quirks to preserve:
- **K&R function declarations** (not ANSI prototypes)
  ```c
  /* K&R style — not ANSI */
  int update_player(x, y, state)
  int x, y, state;
  {
      /* ... */
  }
  ```
- Implicit `int` return types where used in period code
- `register` keyword used liberally for hints to compiler
- Minimal or terse comments — West Coast Unix style
- No function prototypes — declaration order matters
- `char` used freely as small integer
- Manual memory layout awareness — knowing exactly where things live
- Bitwise tricks preferred over multiplication/division
- Terse variable names (Unix heritage): `p`, `q`, `cnt`, `flg`
- Occasional hand-coded assembly inserts for critical loops
- No standard library luxury — roll your own where needed

**Target size: ~40KB across EPROMs**

**Single player only**

---

## Game Design

**Influences:**
- **Cube Quest** (1983) — vector/polygon style 3D
- **Tempest** (1980) — tube shooter, edge-of-screen movement
- **Tron** (1982) — grid aesthetics, geometric environments

**Core Mechanic:**
- 11 levels of increasing psychological intensity
- Geometric tunnel/grid environments
- Enemy patterns become increasingly erratic and unpredictable

**The Polybius Twist — Control Inversion:**
- At unpredictable moments controls flip:
  - Up becomes Down
  - Left becomes Right
  - Fire may reverse or misdirect
- Player must adapt or fail
- Frequency of inversion increases with level progression
- Designed to disorient — faithful to the legend

**Visual Style:**
- **Psychedelic color palette shifts** between and during levels
- Color cycling inspired by:
  - **Moebius (Jean Giraud)** — geometric, clean, cosmic
  - **H.R. Giger** — biomechanical undertones, dark geometry
  - **Roger Dean** — flowing, surreal environmental shapes
- Strobing and pulse effects (consider photosensitivity disclaimer on cabinet)
- Grid warping effects
- Tunnel/vortex perspective shifts

**Audio Design:**
- Tangerine Dream / John Carpenter influenced atmosphere
- Dissonant tones during control inversion moments
- HC-55516 voice fragments — barely intelligible
- White noise bursts at key stress moments
- Sound deliberately designed to be slightly unsettling

---

## Aesthetic & Markings

**Cabinet exterior:**
- Minimal, stark side art — geometric, Moebius-influenced
- No cheerful arcade colors — dark, governmental
- Small, slightly cryptic marquee

**PCB markings:**
- SRI International logo (silkscreen)
- "PROPERTY OF US GOVERNMENT"
- "UNAUTHORIZED DUPLICATION PROHIBITED"
- Date code: 1981 or 1982
- Government contract number format

**Documentation (for display):**
- Laminated "technical manual" pages in period typewriter font
- Fictional government memo referencing the project
- Adds to the narrative for hackerspace visitors

---

## Power Supply

- Period correct **linear power supply** (no switching supply)
- +5V, +12V rails
- Contributes to authentic 60Hz hum
- Proper fusing, period correct

---

## Notes for Builders

- Period correct Panasonic capacitors throughout
- Source vintage NOS components where possible for authenticity
- New Nichicon/Panasonic acceptable where NOS unavailable
- EPROM burner required for programming 2732 chips
- Cabinet can be sourced from a donor 1981-era cabinet and repainted
- Glass door panel retrofitted to standard cabinet door opening
- This is a **novelty/showpiece** — not a forgery — enjoy the craft!

---

*"What you are about to experience may cause dizziness, altered perception, and an inexplicable urge to play again."*

---
**Project Type:** Hackerspace/Makerspace Showpiece
**Period:** 1981–1982 Reproduction
**Status:** Specification Document v1.0
