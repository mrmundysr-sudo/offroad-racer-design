# Touch Off-Road — Visuals (NES Pixel Art Pass)

**Status:** Visuals-first design pass. No game code.
**Companion to:** [DESIGN.md](DESIGN.md) · [SCREEN-LIST.md](SCREEN-LIST.md)
**Working title:** **Touch Off-Road**

Purpose: lock a coded NES-style look (palette, sprites, tiles) and show what the **background + gameplay screen** should feel like before any implementation. ASCII frames are schematic, not final art. No ROMs in this repo — screenshots as reference only.

---

## 1. Pixel art style guide

### 1.1 Resolution and camera

- Target feel: **NES arcade** (chunky pixels, limited colors, readable at a glance).
- Working canvas (design intent): **256×240** logical pixels (classic NES), scaled integer-up on phone.
- Camera: **fixed single-screen isometric** (elevated bird’s-eye). Whole track visible. **No scrolling.**
- One race = one arena screen. Elevation is faked with **shading + heavy dither**, not 3D or parallax scroll.

### 1.2 Limited palette (NES feel)

Keep a small locked set. Bright car colors do the identity work; dirt stays earthy so trucks pop.

| Role | Colors (name → intent) |
| --- | --- |
| **Dirt light** | Warm tan / light brown |
| **Dirt mid** | Medium brown / clay orange |
| **Dirt dark / shadow** | Deep brown (dithered into mid for hills) |
| **Barrier** | Bright red + white (checkered chrome) |
| **Water** (Huevos mood) | Mid blue + dark blue edge |
| **Sky / wall** | Flat gray-blue or indoor gray strip (Blaster mood) |
| **UI text** | White / yellow highlight on dark bar |
| **Beetle / truck body** | Four bright custom primaries (exact hex TBD) — e.g. yellow, red, blue, white/silver *or* purple / pink variants |
| **Tire / outline** | Near-black |
| **Dust / nitro streak** | Light tan puff + short white/yellow speed streak |
| **Spin-out flash** | Brief white/yellow flash on hit truck |
| **Armor glint** (full nitro) | Short cyan/white rim flash |

Rules:

- Prefer **flat fills + 1–2 dither patterns** over smooth gradients.
- No soft anti-aliasing in source art — scale with nearest-neighbor.
- Silhouettes must read when shrunk; outline trucks in dark so colors don’t melt into dirt.

### 1.3 Sprite sheet approach — Baja Beetle + AI trucks

Shared chassis language: **chunky toy 4×4**, big tires, short wheelbase, readable roof. Player = **Baja Beetle** silhouette (bug-like rounder cabin); AI = stadium-truck / boxier cabin. Same scale so races stay fair to the eye.

**Sheet layout (design intent):**

```
+----------------------------------------------------------------+
|  ROW A — Baja Beetle (player), 8 facings (N NE E SE S SW W NW) |
|  [N][NE][E][SE][S][SW][W][NW]   body tint = player color slot   |
+----------------------------------------------------------------+
|  ROW B — AI truck, same 8 facings                               |
|  [N][NE][E][SE][S][SW][W][NW]   body tint = AI color slot     |
+----------------------------------------------------------------+
|  ROW C — FX overlays (shared)                                   |
|  [dust puff ×3] [nitro streak ×2] [spin swirl ×4] [armor glint] |
+----------------------------------------------------------------+
|  ROW D — Optional: mid-air / jump squash-stretch (1–2 frames)   |
+----------------------------------------------------------------+
```

**Tinting:** Draw body in a **neutral mid gray** (or single magenta key) and recolor at runtime per truck so one sheet serves all four colors. Tires, windows, and outlines stay fixed (not tinted).

**Animation budget (v1):**

- Idle / drive: facing frames only (no walk cycle needed).
- Jump: 1–2 airborne frames + dust on land.
- Spin-out: 3–4 swirl / rotate frames, few seconds, **no lap loss**.
- Shoot: short muzzle flash on shooter; hit flash on target.

Keep sprite size toy-like and large enough to read on a phone held at arm’s length (design target ~16×16 to ~24×24 logical px per truck, exact size TBD at art lock).

### 1.4 Tile-based rendering approach

Arenas are built from a **small tileset**, not one giant bitmap per track.

**Tile roles:**

| Tile family | Use |
| --- | --- |
| **Dirt flat** | Base floor (light / mid variants) |
| **Dirt dither slope** | Fake elevation / humps / whoops |
| **Checkered barrier** | Red-white edge pieces + corners |
| **Jump ramp / whoop** | Raised lip tiles |
| **Pit / shadow** | Darker inset |
| **Water** | Blue pool tiles + edge |
| **Decor** | Flag poles, flagger stand, tiny crowd strip, start/finish stripe |

**Map flow:**

1. Author a grid (e.g. 16×15 tiles for a 256×240 feel) per track.
2. Paint dirt + elevation dither first.
3. Lay checkered barrier loop as the signature chrome.
4. Drop hazard tiles (water, pits, ramps).
5. Place start line + optional props (flags, crowd).
6. Spawn Beetle + AI on the line; HUD drawn in a UI layer above tiles/sprites.

Tracks stay **mood-board compatible** with Blaster / Sidewinder / Huevos Grande (see DESIGN.md) without copying ROM art.

---

## 2. Background + gameplay screen mockups

Default invisible controls (mockup labels only — **invisible in real play**):

- **A** — lower-right corner
- **B** — below A (A above B)
- **Swipe** — center / lower playfield
- Independent multi-touch (Touch-family shared foundation)

Exact A/B → nitro / shoot / other still TBD (DESIGN.md open questions).

### 2.1 Background / arena mood (what the world looks like)

**Shared:**

- Whole dirt bowl fills the screen inside a **red-and-white checkered** ring.
- Dirt = browns / oranges with **heavy dither** on hills so humps read without 3D.
- No chase-cam; sky or wall is a thin strip at the top (indoor gray for Blaster mood, open for Sidewinder / Huevos).

**Mood variants (v1 picks one first):**

| Mood | Sky / walls | Dirt | Extra scenery |
| --- | --- | --- | --- |
| **Blaster-like** | Indoor gray wall + tiny crowd pixels | Reddish-brown | Bunting over jumps |
| **Sidewinder-like** | Open / simple sky strip | Browner dirt | Flag poles + flagger stand by start |
| **Huevos-like** | Open | Burnt-orange clay | Blue water pools |

ASCII “painted” background (Huevos-leaning example):

```
+--------------------------------------------------+
| :: pale sky strip ::                             |
| ################################################ |
| # R/W checkered barrier                        # |
| #   .... burnt-orange clay ....    [~~~~]      # |
| #  .. dithered hump ..   whoops    water       # |
| #     ....... dirt bowl ........   [~~~~]      # |
| #  start||finish   flag?                       # |
| # ............................................ # |
| ################################################ |
+--------------------------------------------------+
  # = checkered edge · . = dirt · ~ = water · dither = elevation
```

### 2.2 Gameplay screen (full mockup)

**Purpose:** Solo-first race — one track, player Baja Beetle, AI trucks, spin-out + nitro readable in one glance.

**Layers (back → front):**

1. Sky / wall strip
2. Tile arena (dirt, dither hills, water, barriers, props)
3. Truck sprites (AI + Beetle) + FX (dust, nitro, spin, armor)
4. Compact HUD (timer, LAP, NITRO — color-matched)
5. Invisible control zones (not drawn in play; shown dashed here)

```
+--------------------------------------------------+
| TIMER 00:36          LAP   NITRO                 |
|                      [Y] 1   10                  |
|                      [R] 1   25                  |
|                      [B] 1   10                  |
|                      [W] 1   10                  |
|--------------------------------------------------|
| #RWRW checkered###############################  |
| #                                            #  |
| #   [R truck]      dither hump               #  |
| #         ....... dirt .......   [~~water~~] #  |
| #   [B truck]              [Y BEETLE you]    #  |
| #        whoops / jump             [W truck] #  |
| #                                            #  |
| #      ········ swipe area ········          #  |
| #                                            #  |
| ##############################################  |
|                              : A (invis) :      |
|                              : B (invis) :      |
+--------------------------------------------------+

  [Y] player Baja Beetle (rounder cabin, bright color)
  [R][B][W] AI trucks (boxier, color = identity)
  Hit → spin swirl a few seconds (no lap loss)
  Shot costs nitro · full nitro = brief armor glint
  Playfield stays clean — no permanent on-screen buttons
```

**Readable beats on this screen:**

- Car **color** tells who is who before you read the HUD.
- Checkered ring = instant “this is Touch Off-Road.”
- Spin-out = obvious swirl / dust, not a confusing teleport.
- Nitro choice is visible in the color-matched NITRO column (speed vs shoot vs hold for armor).

---

## 3. How this feeds the next pass

- Lock **four Beetle/truck colors** and exact palette hexes next (still TBD).
- Pick **one** first track mood for the solo slice (recommend Sidewinder-like or Blaster-like).
- Art order: tileset → Beetle sheet → AI sheet → FX → HUD font.
- Still **no code** until Matt explicitly asks — iterate these visuals first.

---

*Mundy Morning Studios · Visuals-first · No game code in this repo*
