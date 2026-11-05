# Touch Off-Road — Screen List

**Status:** Visuals-first mockups. No code.
**Companion to:** [DESIGN.md](DESIGN.md)
**Working title:** **Touch Off-Road**

Purpose of this file: show what each screen looks like and is for before any implementation. ASCII frames are schematic, not final art.

**Controls reminder (default layout, all screens that accept play input):**
- Invisible **A** zone — lower-right corner (consistent Touch-family default)
- Invisible **B** zone — below A in the same corner stack (A above B)
- **Swipe** area — center / lower playfield for steering / hop-style motion
- Zones are **invisible in play**; shown here as dashed labels only for the mockup
- Independent multi-touch (one finger must not block another)

Open mapping (from DESIGN.md): exact A / B → steer / nitro / shoot still TBD.

---

## 1. Title screen

**Purpose:** Attract / entry. Name the game, invite a start, establish the NES arena look before racing.

**Looks like:**
- Full-screen dirt-arena backdrop (browns / oranges, dithered hills, red-and-white checkered barrier strip)
- One or more Baja Beetle silhouettes parked or idling (bright custom colors)
- **TOUCH OFF-ROAD** as the big title lockup (chunky NES lettering, high contrast)
- Short cue under the title: e.g. `PRESS A TO START` / `SWIPE OR TAP A`
- Optional tiny Mundy Morning Studios credit at the bottom
- Default invisible A / B / swipe zones present (same corners as in-game) so muscle memory starts here

```
+------------------------------------------+
|                                          |
|           TOUCH OFF-ROAD                 |
|                                          |
|        [ Baja Beetle silhouette ]        |
|     checkered barrier · dirt dither      |
|                                          |
|           PRESS A TO START               |
|                                          |
|  ····· swipe area ·····                  |
|                                          |
|                     : A (invis) :        |
|                     : B (invis) :        |
|  Mundy Morning Studios                   |
+------------------------------------------+
```

---

## 2. Gameplay screen

**Purpose:** The race. Solo-first slice: **one track**, **AI trucks**, player **Baja Beetle**, **spin-out** special, **nitro** economy. Whole arena visible — no scrolling.

**Looks like:**
- Fixed single-screen **isometric** dirt arena (Blaster / Sidewinder / Huevos Grande mood)
- Red-and-white **checkered barriers**; humps / whoops / optional water read via shading + dither
- Player Beetle + AI trucks as chunky toy 4×4s; **color** is identity
- Compact HUD: **timer**, per-truck **LAP**, per-truck **NITRO** (counts color-matched to trucks)
- On hit: target **spins out a few seconds** (no lap loss); shot costs a nitro; full tank = brief bulletproof
- Playfield stays clean — **no permanent on-screen buttons**
- Mockup labels only: invisible **A** / **B** (lower-right) + **swipe** area over the arena

```
+------------------------------------------+
| TIMER 00:36     LAP  NITRO               |
|                 Y 1   10                 |
|                 R 1   25                 |
|                 B 1   10                 |
|                 W 1   10                 |
|                                          |
|   #### checkered ####                    |
|  /   dirt arena · AI trucks · Beetle  \  |
| |  humps / whoops / (optional water)   | |
|  \     ····· swipe area ·····         /  |
|   ##################                    |
|                                          |
|                     : A (invis) :        |
|                     : B (invis) :        |
+------------------------------------------+
  Spin-out flash / dust puff when a truck is hit.
  Nitro boost = short speed streak; full tank = armor glint.
```

---

## 3. Pause screen

**Purpose:** Soft interrupt. Let the player breathe, resume, or quit without losing the race state.

**Looks like:**
- Dimmed / frozen arena underneath (still readable: track + trucks + HUD ghosts)
- Center panel: **PAUSED**
- Simple choices: **RESUME** · **RESTART** · **QUIT** (selection via A / B or tap; exact bind TBD)
- Optional one-liner tip: e.g. full nitro = bulletproof
- Same default invisible A / B / swipe footprint (swipe may be idle while paused)

```
+------------------------------------------+
|  (dimmed arena + HUD underneath)         |
|                                          |
|           +------------------+           |
|           |     PAUSED       |           |
|           |  RESUME          |           |
|           |  RESTART         |           |
|           |  QUIT            |           |
|           +------------------+           |
|                                          |
|                     : A (invis) :        |
|                     : B (invis) :        |
+------------------------------------------+
```

---

## 4. Game-over / results screen

**Purpose:** End the race cleanly. Show place, lap, and enough feedback to retry or return to title.

**Looks like:**
- Arena backdrop still visible (or a static finish frame)
- Banner: **FINISH** / **RESULTS**
- Ordered standings for player Beetle + AI trucks (color swatch + name/place + final LAP)
- Spotlight on the player line (win / place callout)
- Actions: **RACE AGAIN** · **TITLE** (A / B or tap)
- Invisible zones remain in the default corners for consistent exit / retry

```
+------------------------------------------+
|              RESULTS                     |
|                                          |
|   1.  [Y] Baja Beetle (YOU)   LAP 3      |
|   2.  [R] AI Truck            LAP 3      |
|   3.  [B] AI Truck            LAP 2      |
|   4.  [W] AI Truck            LAP 2      |
|                                          |
|        RACE AGAIN     TITLE              |
|                                          |
|                     : A (invis) :        |
|                     : B (invis) :        |
+------------------------------------------+
```

---

## Screen flow (v1 solo slice)

```
Title  →  Gameplay (one track + AI)  →  Results
              ↕
            Pause
```

Multiplayer screens are **out of v1** (see Solo-First Roadmap in DESIGN.md).

---

*Mundy Morning Studios · Visuals-first · No game code in this repo*
