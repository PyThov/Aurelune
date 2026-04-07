# Elements TD — UI/UX Wireframes

## Purpose
This document describes the layout, behavior, and design intent of every major UI screen and HUD element. Because this is a text-based wireframe document, layouts are described with ASCII diagrams and structured descriptions. These should be treated as design specifications, not final visuals.

**Art style reminder:** Elegant fantasy militaristic framing. Minimal clutter during combat. Strong iconography. Readable at 1080p from a normal viewing distance.

---

## 1. In-Combat HUD

The combat HUD must never obscure critical battlefield information. All persistent elements are anchored to screen edges.

```
+------------------------------------------------------------------+
|  [WAVE 3 / 10]   [OBJ HP: ████████░░ 280/350]   [⏸ BUILD PHASE]|
+------------------------------------------------------------------+
|                                                                  |
|                                                                  |
|              [ COMBAT VIEWPORT ]                                 |
|                   (gameplay area)                                |
|                                                                  |
|                                                                  |
+------------------------------------------------------------------+
| [GEM ICON] 240   [ORB: 🔥 x1  💧 x0]     [PLAYER HP: ██████ 90/150] |
+------------------------------------------------------------------+
|  [Q] Empower Zone  [E] Hunter's Mark  [R] Arcane Surge  [DASH■] |
|  [COOLDOWN BARS UNDER EACH ABILITY ICON]                         |
+------------------------------------------------------------------+
```

### Top Bar (persistent)
- **Wave counter:** "WAVE 3 / 10" — large, readable; pulse animation on wave start
- **Objective HP bar:** Wide horizontal bar with numeric display; turns red below 30%; flashes on damage
- **Phase indicator:** Shows "BUILD PHASE" (paused) or "WAVE IN PROGRESS" with a subtle animated indicator

### Bottom Bar (persistent)
- **Gem count:** Icon + number; briefly animates on gem gain
- **Orb inventory:** Shows stacked icons by element (up to 4 visible; scroll or +N indicator beyond that)
- **Player HP:** Bar + number; no regen indicator (HP only changes at wave ends or on hit)

### Ability Tray (bottom bar, right side)
- 4 slots: Q / E / R / Dash
- Each shows ability icon + keybind label
- Cooldown shown as a circular sweep indicator over the icon
- Active effects (Empower Zone, Hunter's Mark) show a glowing border + remaining duration tick

### Combat Phase vs. Build Phase Distinction
- During build phase: HUD dims combat elements; tower placement UI slides in from the left
- During active waves: tower UI is hidden entirely; HUD returns to full combat state
- Subtle vignette color shift: warm amber during build phase; neutral/cool during waves

---

## 2. Tower Placement UI

Triggered when the player enters build phase (or manually opens it via keybind during build phase).

```
+-----------------------------+
|  PLACE TOWER                |
|-----------------------------|
|  [↑] [↓] to scroll         |
|                             |
|  [1] Arrow Tower      80 💎 |
|  [2] Cannon Tower    130 💎 |
|  [3] Crossbow Tower  110 💎 |
|  [4] Mage Spire      120 💎 |
|  [5] Arc Ray         160 💎 |
|  [6] Seed Core        70 💎 |
|                             |
|  [Grey = locked]            |
+-----------------------------+
```

- Panel slides in from the left side during build phase
- Tower list shows name, cost, and a small icon
- Locked towers are greyed out with a lock icon (no tooltip in prototype; tooltip added in polish)
- Hovering/selecting a tower shows its **range preview** as a ground decal circle around the cursor
- **Placement decal:** Valid placement = green circle; invalid (blocked/overlapping) = red
- After placement: tower appears immediately; gem count deducts; player can continue placing

### Tower Selection Shorthand
Players can also click an existing placed tower to bring up the tower management panel.

---

## 3. Tower Management Panel

Opened by clicking a placed tower. Appears as a small panel anchored near the tower (offset to not block the tower).

```
+-----------------------------+
|  ARROW TOWER  Lv.1          |
|  ————————————————————————  |
|  DMG: 15   SPD: 1.2/s       |
|  Range: 12  Buildup: 5      |
|  ————————————————————————  |
|  [UPGRADE → Lv.2]  65 💎   |
|  [INFUSE 🔥]        — (no orb)|
|  [SELL]            80 💎   |
|  ————————————————————————  |
|  Status: No infusion        |
+-----------------------------+
```

- Stats shown at current level
- Upgrade button greyed out if gem cost can't be met; shows cost in red
- At Level 2, upgrade button shows branching choice (3A or 3B) with brief text label
- Infuse button: available if player has an orb in inventory; shows element icon and "USE ORB" confirmation step
- Sell button: only available during build phase; shows exact gem refund; always 100% of total gems spent on that tower
- During active wave: upgrade, infuse, and sell are all hidden; the tower management panel shows stats only (read-only)

### Level 3 Branch Selection UI
When upgrading a Level 2 tower, a split panel appears:

```
+------------------------------+
|  UPGRADE ARROW TOWER         |
|  Choose upgrade path:        |
|  ——————————————————————————  |
|  [3A] MARKSMAN         90 💎 |
|  Long range, armor pierce    |
|                              |
|  [3B] RAPID SHOT       90 💎 |
|  High speed, slowing hits    |
+------------------------------+
```

- Both options shown side by side or stacked
- Brief two-line description per path
- Player taps/clicks their choice; a confirmation prompt appears ("Confirm? This cannot be changed.")

---

## 4. Wave UI and Wave Start

### Wave Countdown (during build phase)
When the player is ready to start the next wave:

```
+------------------------------------------+
|  Wave 4 incoming                         |
|  Enemies: [Brute x2] [Raider x6]        |
|  [▶ START WAVE]  or  Auto in: --         |
+------------------------------------------+
```

- Small panel at top-center of the screen
- Shows enemy type icons for the upcoming wave (no specific counts in early waves; icons only)
- START WAVE is a clearly visible button; clicking it ends build phase and begins the wave
- If auto-start is enabled, shows a countdown timer instead

### Wave Start Announcement
- Brief fullscreen overlay text: "WAVE 4" fades in and out in 1 second
- Accompanied by a distinct audio cue (miniboss waves have a different, more intense cue)

### Wave Complete Notification
- Brief text at the top: "WAVE COMPLETE — +15 💎" 
- If it's the final wave, shows "ALL WAVES CLEARED" before transitioning to mission end

---

## 5. Status Effect HUD

Enemy status is communicated primarily through in-world VFX, not on-screen bars. However, for clarity:

### Enemy Status Icons
- Floating icon above affected enemy's head showing the active status (small, readable from mid-distance)
- Icons: flame (Burning), droplet (Soaked), crack (Shattered), swirl (Gusted)
- Icon pulses as status is close to expiring (last 1.5 seconds)

### Combo Announcement
When a combo triggers, a brief in-world floating text appears at the combo location:

```
    💥 EXPLOSION!
```

- Text style matches the combo's element color
- Display duration: 0.8 seconds
- No full-screen interruption; purely diegetic/world-space

### Player Status (if affected by enemy debuff — post-MVP)
- Status icon appears next to player HP bar
- Duration shown as a small timer beneath the icon

---

## 6. Element Orb UI

### Orb Pickup Notification
When an orb drops:
- A world-space orb object appears at the enemy's death location
- Player must walk over it to collect (auto-pickup within 1.5 units)
- On collection: brief popup at bottom of screen: "🔥 Fire Orb obtained"

### Orb Shard Tracking
- Shard count shown as small stacked icons in the bottom bar (e.g., "🔥 [■■□] 2/3 shards")
- On third shard: brief animation and sound — "Fire Orb assembled!"

### Orb Use (via tower management panel)
- Player selects a tower → clicks INFUSE → element selection popup appears
- Shows available orbs; player selects element
- Confirmation step: "Infuse with Fire? This tower will now apply Burning buildup."
- Orb is consumed on confirm

---

## 7. Mission End Screen

Shown after the final wave is completed (all enemies defeated, objective survived).

```
+--------------------------------------------------+
|           MISSION COMPLETE                       |
|          The Ashen Road                          |
|  ——————————————————————————————————————————————  |
|  ★ ★ ★  (3 stars — optional objectives met)     |
|  ——————————————————————————————————————————————  |
|  Gems earned this mission: 340                   |
|  Research Points: +80                            |
|                                                  |
|  [CONTINUE TO CAMP]                              |
+--------------------------------------------------+
```

- Star rating: 1 star = mission completed; 2 stars = completed with objective HP above 50%; 3 stars = completed with HP above 75% + optional objective met
- Stats shown: gems earned, research points rewarded, optional: combos triggered, towers placed
- Continue button returns player to the hub camp

### Mission Fail Screen
```
+--------------------------------------------------+
|           MISSION FAILED                         |
|  Objective destroyed.                            |
|  ——————————————————————————————————————————————  |
|  [RETRY]         [RETURN TO CAMP]                |
+--------------------------------------------------+
```

- No shaming tone; simple and direct
- RETRY immediately restarts from wave 1 (all progress within the mission is lost)

---

## 8. Hub Camp Navigation

The hub camp is a 3D walkable space. UI is triggered by walking near interactable locations.

### Interaction Prompt
When the player is near an interactable object (War Map, Forge, etc.):

```
    [ F ] War Map
```

- Context prompt appears in world-space above the object
- Pressing F opens the relevant screen

### War Map Screen

```
+------------------------------------------------------------+
|  THE WAR MAP                                               |
|  ——————————————————————————————————————————————————————   |
|  [EMBERVEIL]  ████ CLEARED                                 |
|  [THALVERE]   ░░░░ LOCKED (Clear Emberveil first)          |
|  [GREYMANTLE] ░░░░ LOCKED                                  |
|  [AELCREST]   ░░░░ LOCKED                                  |
|  [SOLHARROW]  ░░░░ LOCKED                                  |
|  ——————————————————————————————————————————————————————   |
|  Selected Region: EMBERVEIL                                |
|  Mission 3: Ember Gates       ★★☆  [REPLAY]               |
|  Mission 4: Siege of Ironworks ☆☆☆  [START]               |
|  Mission 5: The Hollow Furnace ░░░  [LOCKED]               |
|  ——————————————————————————————————————————————————————   |
|                                           [CLOSE]          |
+------------------------------------------------------------+
```

- Region list on the left; mission list on the right
- Star ratings visible for completed missions
- Locked missions show a lock icon and unlock condition
- Clicking START launches the mission

### Forge / Research Screen (simplified MVP version)

```
+------------------------------------------------------------+
|  THE FORGE                                                 |
|  Research Points: 180                                      |
|  ——————————————————————————————————————————————————————   |
|  [UNLOCK] Cannon Tower         Cost: 100 RP               |
|  [UNLOCK] Arrow Tower Lv.2     Cost: 80 RP  ← AVAILABLE   |
|  [LOCKED] Mage Spire Lv.2      Requires: Clear Emberveil  |
|  [PASSIVE] +10% Wave Gem Bonus Cost: 60 RP  ← AVAILABLE   |
|  ——————————————————————————————————————————————————————   |
|                                           [CLOSE]          |
+------------------------------------------------------------+
```

- Linear list for MVP; visual tree for full game
- Available unlocks highlighted; locked ones greyed with unlock condition shown
- Purchase confirmation step before spending RP

---

## 9. Codex / Combo Encyclopedia

Accessible from the camp (bookshelf object or menu option).

```
+------------------------------------------------------------+
|  CODEX                                                     |
|  ——————————————————————————————————————————————————————   |
|  [ELEMENTS]  [COMBOS]  [ENEMIES]  [TOWERS]  [LORE]        |
|  ——————————————————————————————————————————————————————   |
|  COMBOS > EXPLOSION                                        |
|                                                            |
|  Burning + Fire trigger                                    |
|  "A detonation of compressed fire energy."                 |
|                                                            |
|  Damage: High (true damage)    AoE: 3.5 units              |
|  Best against: Clustered enemies                           |
|  First triggered: Mission 2, Wave 4                        |
+------------------------------------------------------------+
```

- Entries are **discovered** — new combos, enemies, and lore entries appear as the player encounters them
- Combo entries appear after the player triggers that combo for the first time
- Enemy entries appear after the player first defeats that enemy type
- Lore entries are found as collectibles in missions

---

## 10. Accessibility and Settings Notes

The following should be addressed before launch:

| Setting                         | Default | Notes                                  |
|---------------------------------|---------|----------------------------------------|
| Colorblind mode                 | Off     | Remaps element colors; required        |
| Subtitles                       | On      | For all voiced/text narrative moments  |
| HUD scale                       | 100%    | UI elements should scale cleanly       |
| Auto-start waves                | Off     | Can be toggled to on with timer        |
| Camera sensitivity              | Medium  | Slider; separate X/Y axes             |
| Status effect icon size         | Medium  | Small / Medium / Large options         |
| Combo announcement display time | 0.8 sec | User adjustable 0.5–2.0 sec           |

---

## 11. Onboarding / Tutorial Notes

The game does not use a traditional tutorial screen. Instead:

- Mission E1 (The Ashen Road) is the tutorial mission
- Context prompts appear the first time each system is used:
  - First time in build phase: tooltip highlights the tower placement panel
  - First tower placed: tooltip explains range preview
  - First wave started: tooltip indicates the wave counter
  - First status applied: tooltip briefly explains the element icon floating above the enemy
  - First combo triggered: combo announcement is slightly larger and held for 1.5 sec instead of 0.8 sec; codex entry unlocked notification appears
- All tooltips are dismissible and do not repeat after first encounter
- No unskippable tutorial pauses; the game never locks the player into a forced sequence

