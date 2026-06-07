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

---

### West Coast Unix C Style — Background

West Coast C grew from **UC Berkeley's BSD Unix** culture, geographically and culturally close to SRI International in the San Francisco Bay Area. It contrasts with Bell Labs (East Coast/AT&T) C in attitude: terse, clever, slightly cavalier, and deeply Unix-influenced. Code was expected to be read by people who already knew what they were doing. Comments were considered a sign of weakness.

Key influences:
- **Bill Joy** (vi, csh, BSD) — terse, fast, ship it
- **Ken Arnold** (curses library) — clean but minimal
- **Unix philosophy** — do one thing, do it well, use pipes
- **SRI hacker culture** — adjacent to Stanford, ARPA funded, brilliant and secretive

---

### West Coast C Code Examples

**K&R Function Declarations — not ANSI prototypes:**
```c
/* update player position and state -- sn 1982 */
update_player(x, y, flg)
int x, y, flg;
{
    register int d;
    d = flg & 0x1 ? -1 : 1;   /* inversion active? */
    px += d * x;
    py += d * y;
}
```

**Implicit int, terse names, no ceremony:**
```c
/* no return type = implicit int, West Coast standard */
chk_bounds(x, y)
int x, y;
{
    return (x < 0 || x >= XMAX || y < 0 || y >= YMAX);
}
```

**Bitwise tricks instead of multiply/divide:**
```c
/* multiply by 8 -- never use * on this hardware */
#define TILE(x)   ((x) << 3)

/* fast modulo power of 2 */
#define WRAP(x,n) ((x) & ((n)-1))

/* check if level is odd -- controls inversion phase */
#define ODD(n)    ((n) & 1)
```

**Register keyword used liberally:**
```c
render_tunnel(lvl, frame)
int lvl, frame;
{
    register int i, j, d;
    register char *p;

    p = vram_base;
    d = inv_active ? -1 : 1;   /* direction flipped? */
    for (i = 0; i < ROWS; i++) {
        for (j = 0; j < COLS; j++) {
            *p++ = tunnel_lut[lvl][WRAP(i + frame, 16)];
        }
    }
}
```

**Terse, almost hostile comments:**
```c
/* invert ctl -- per spec */
inv_ctl(flg)
int flg;
{
    ctl_state ^= flg;   /* xor flip bits */
}

/* dont call this twice -- sn */
init_hw()
{
    *(char *)0xC000 = 0;   /* reset sound latch */
    *(char *)0xC001 = 0xFF; /* enable all channels */
}
```

**Inline assembly for critical loop (6809 example):**
```c
/* too slow in C -- asm for scanline fill */
fill_line(addr, val, cnt)
char *addr;
int val, cnt;
{
#asm
    LDX  addr
    LDA  val
    LDB  cnt
LOOP:
    STA  ,X+
    DECB
    BNE  LOOP
#endasm
}
```

**Pointer arithmetic showing off:**
```c
/* blast sprite to vram -- no memcpy on this target */
blt(dst, src, n)
char *dst, *src;
int n;
{
    while (n--)
        *dst++ = *src++;
}
```

**Global state, minimal structure:**
```c
/* globals -- West Coast didn't believe in hiding state */
int  px, py;        /* player pos */
int  plives;        /* lives remaining */
int  lvl;           /* current level */
int  score;
int  ctl_state;     /* bitmask: bit0=inv_x, bit1=inv_y */
int  inv_tmr;       /* inversion countdown */
char inv_active;    /* nonzero if controls flipped */
```

**The Polybius inversion logic — West Coast style:**
```c
/*
 * ctl -- read joystick, apply inversion if active
 * returns dx,dy via pointers -- sn/jb 1982
 */
ctl(dx, dy)
int *dx, *dy;
{
    register int raw, d;
    raw = *(char *)JOY_PORT;
    d   = inv_active ? -1 : 1;
    *dx = d * ((raw & JOY_R) ? 1 : (raw & JOY_L) ? -1 : 0);
    *dy = d * ((raw & JOY_D) ? 1 : (raw & JOY_U) ? -1 : 0);
}
```

---

**Additional West Coast style notes:**
- No function prototypes — declaration order matters, caller beware
- `char` used freely as small integer to save RAM
- Manual memory layout — developer knows exactly where every byte lives
- No standard library — roll your own `strlen`, `memset` etc.
- Magic numbers preferred over named constants in hot paths
- Occasional unexplained `/* ?? */` comment left in deliberately
- One or two intentionally cryptic variable names — authenticity detail

---

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

## The Secret — Hidden Modern Hardware if authentic working hardware is not possible to source

The glass door shows the beautiful period correct PCB to visitors.
What visitors *don't* see depends entirely on how the PCB is mounted. 

**The Approach:**
- Period correct green PCB mounted face-forward, fully visible through glass
- PCB can be **non-functional** — purely decorative display board
- Behind the PCB, hidden from view, the *actual* game hardware runs

**Hidden Modern Options:**

| Hidden Hardware | Notes |
|----------------|-------|
| **Raspberry Pi 4/5** | Runs MAME or custom emulator, HDMI to CRT via converter |
| **MiSTer FPGA** | Cycle accurate hardware emulation, audiophile quality |
| **Raspberry Pi Zero 2W** | Tiny, easily hidden behind even a small PCB |
| **Orange Pi / Odroid** | Alternative SBC options |
| **Arduino Mega** | If keeping it simple and partially authentic |

**The Sneaky Details:**
- PCB mounted on standoffs — enough gap behind for a Pi or FPGA board
- Modern board powered from same supply, wiring hidden behind PCB
- USB from modern board connects to original-looking joystick/button harness
- CRT driven via **GBS-8200 or similar** scan converter from HDMI
- Audio from modern board through period correct amplifier circuit on display PCB




**MiSTer FPGA Note:**
For the most authentic feel without full deception, MiSTer running a
6809/Z80 core is genuinely cycle-accurate — the hidden hardware is
*actually behaving* like 1981 hardware, just on modern silicon.

**Mounting Suggestion:**
- PCB on 25-30mm standoffs from rear panel
- Modern board velcro or screwed to rear panel behind PCB
- Cable management with period-looking braided sleeving on visible runs



---

*"What you are about to experience may cause dizziness, altered perception, and an inexplicable urge to play again."*

---
**Project Type:** Hackerspace/Makerspace Showpiece
**Period:** 1981–1982 Reproduction
**Status:** Specification Document v1.0
