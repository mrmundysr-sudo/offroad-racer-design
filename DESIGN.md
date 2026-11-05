# Offroad Racer — Design Sketch

**Status:** Early design sketch. Visuals-first. No code yet.
**Audience:** Matt (not a coder) + future implementers.
**Platforms (later):** Android and iOS.
**Working name:** Offroad Racer (title TBD).

This doc replaces the paused **Touch Frogert** plan as the next game focus. It is a design sketch, not a tech plan.

---

## 1. Visual reference

Inspired by three Super Off Road–style screenshots (NES look). Use those shots as **visual reference only** — do **not** put ROM files in this repo (copyrighted). Screenshots as reference are fine.

### Camera and layout

- **Fixed single-screen isometric** (elevated bird’s-eye) view
- **Whole track visible** at once
- **No scrolling**, no chase-cam
- Arena racing: one screen = one race

### Vehicles

- Chunky, **toy-like 4×4** sprites with **big tires**
- Stadium-truck / off-road toy feel
- Car **color** is the main identity cue (readable at a glance)

### Track chrome

- Dirt arena floors
- **Red-and-white checkered barriers** as the signature track chrome
- Humps, whoops, jumps, pits; elevation read through **shading and heavy dithering**, not 3D models

### Palette (NES feel)

- Dirt: earth **browns / oranges**
- Cars: **bright primaries** (and custom colors — see concept)
- Hills / shadows: **heavy dithering**
- Keep shapes big and readable

### HUD

- **Timer**
- Per-truck **LAP** count
- Per-truck **NITRO** count
- Counts **color-matched** to each truck
- Compact: LAP + NITRO stay readable without crowding the arena

### Reference tracks (from the screenshots)

| Track | Feel | Dirt | Hazards / props | Example car colors |
| --- | --- | --- | --- | --- |
| **Blaster** | Indoor arena | Reddish-brown | Humps / whoops, mid-air jump, crowd strip | Yellow, red, blue, silver |
| **Sidewinder** | Outdoor dirt | Browner | Jumps / pits, flagger stand, flag poles | Red, blue, white, yellow |
| **Huevos Grande** | Clay bowl | Burnt-orange | Blue **water** hazards | Purple, white, pink, yellow |

### Visual takeaways (lock these)

1. Single-screen **arena racing**, not chase-cam.
2. Elevation via **shading / dither**, not perspective scroll.
3. **Car colors** as the main identity.
4. Compact **LAP + NITRO** HUD, color-matched to trucks.
5. **Checkered barriers** as signature chrome.

---

## 2. Concept

- Genre: **off-road racer**
- Look: **NES-style** (chunky sprites, limited palette, readable silhouettes)
- **Custom-colored cars**
- Player cars: **Baja Beetle** style, in **four colors** (exact set TBD; screenshots show both classic RGB+silver and more custom sets like purple / pink)

Tone: toy-like, arcade, loud colors, short races you can read from across the room.

---

## 3. Specials (combat + nitro)

Players can **shoot** each other. Combat and nitro share the same resource so every shot is a tradeoff.

| Rule | Behavior |
| --- | --- |
| **Shoot** | Players fire at each other |
| **Hit** | Target **spins out for a few seconds** |
| **Lap on hit** | **No lap loss** from being shot |
| **Shot cost** | Each shot costs a **nitro charge** |
| **Full nitro tank** | Briefly **bulletproof** |
| **Player choice** | **Speed vs firepower** — burn nitro to boost, or spend it to shoot, or hold a full tank for armor |

Design intent: racing stays primary; shooting is a readable interrupt, not a death match. Spin-outs punish positioning without throwing the race into chaos.

---

## 4. Context (why this doc exists)

- This game sketch **replaces the paused Frogert plan** as current game focus.
- Separate project note — **Touch TV Guide**: email already sent to EPGTalk (`support@epgtalk.com`) asking for written OK for a free store app with rewarded ads / one-time purchase / Touch-family subscription.
  - **PERC Data** ~$40/yr is typically an **end-user** membership, not a free redistributable feed for the whole app.
  - **Gracenote** ~$5K/mo class — **out** for a small indie app.
- **This repo:** design notes only. **No ROMs.** Screenshots as visual reference are OK.

---

## 5. How to use this doc

Matt is **not a coder**. Keep future work **visuals-first**:

- Sketch tracks and car colors before systems.
- Lock the single-screen isometric look early.
- No implementation, engines, or folder layouts in this doc yet.
- When code starts later, it should follow this sketch — not the other way around.

### Open questions (for later)

- Final game title and four Baja Beetle colors
- How many tracks in v1; whether Blaster / Sidewinder / Huevos Grande are names we keep or only mood boards
- Exact spin-out duration and nitro economy numbers
- How A / B map to steer / nitro / shoot for this racer

## 6. Solo-First Roadmap

- **First playable slice = one track with AI trucks and the spin-out special working** — that is the minimum complete game.
- **Multiplayer mode is deferred** to a later pass — not part of v1.
- **After the first slice works, iterate visuals** (icons, layouts, animations) **without changing core logic**, per Matt's usual workflow.
- **Matt is not a coder** — visuals-first, **no code until explicitly asked**.

---

## 7. Controls

Touch-family standard. Invisible zones keep the playfield clean — no permanent on-screen buttons.

- **Shared foundation** — The invisible A/B zones + swipe scheme is a **shared foundation** across the **Touch family of apps** and the **emulator apps**, already **tested and proven** there (including independent multi-touch). **Future games in the family inherit this same control system.**
- **Default A / B zones** — Same default layout across **all Touch family games**, parked in **consistent screen corners** so muscle memory carries from one title to the next.
- **Customization** — Players can **resize and reposition** the invisible zones, ideally by **dragging them live in-game**.
- **Per-game saved profiles** — Each game stores its **own** button layout so players do not re-tune when switching titles (e.g. big zones for Frogert-style, tight corners for Pac-Man-style).
- **Independent multi-touch** — Zones are **independent**. More than one input must register at once without one affecting the other (e.g. swipe-hop + action together, or two directions for diagonal). **One finger must not block or cancel another.**

---

*Mundy Morning Studios · Design sketch · No code in this repo yet*
