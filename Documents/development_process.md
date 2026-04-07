# Elements TD — Development Process

## How to Use This Document

This document translates the roadmap phases into an ordered, step-by-step build sequence for a solo developer. Each step has a clear definition of done. Do not move to the next step until the current one works reliably — a shaky foundation compounds quickly in a game with this many interdependent systems.

The order is deliberate: systems that everything else depends on come first, content comes last.

---

## Guiding Principle: Data-Driven From Day One

Before writing any gameplay code, establish that towers, enemies, statuses, combos, and waves are defined in **ScriptableObjects** (or equivalent data assets), not hardcoded. This is the single most important architectural decision in the project.

Every time you think "I'll just hardcode this for now and refactor later" — don't. Refactoring data out of hardcode in a combo-heavy system is expensive. Build the data layer once, correctly, and every future piece of content is just filling in fields.

---

## Phase 1 — Foundation (Do This Before Any Gameplay)

These steps have no visible gameplay result. That is fine. Skipping them will cost far more time than they take.

### Step 1 — Project Architecture Setup
Create the folder structure and core ScriptableObject definitions for all data types.

**Folders to create:**
```
Assets/
  Core/           ← game loop managers, scene bootstrapping
  Towers/         ← tower data, tower behavior scripts
  Enemies/        ← enemy data, enemy behavior scripts
  Elements/       ← element definitions, status effect data
  Combos/         ← combo definitions
  Waves/          ← wave data, spawner scripts
  Player/         ← player controller, abilities
  Gameplay/       ← economy, objective, mission state
  UI/             ← all HUD and menu scripts
  Editor/         ← custom inspector tools
  _Project/       ← scenes, settings, shared prefabs
```

**ScriptableObjects to define (data only, no logic yet):**
- `TowerData` — name, cost, damage, attack speed, range, buildup per hit, damage type, upgrade costs, upgrade branches
- `EnemyData` — name, HP, speed, armor, magic resist, gem reward, tags, aggro range
- `ElementData` — element name, color, status name, buildup per hit modifier
- `StatusEffectData` — status name, element, duration per tier, effect type
- `ComboData` — primer status, trigger element, combo name, effect type, damage multiplier
- `WaveData` — list of enemy spawn instructions (enemy type, count, spawn delay, lane)
- `MissionData` — ordered list of WaveData, map scene reference, reward values

**Done when:** All ScriptableObjects exist as empty definitions. You can create instances of each in the editor and fill in fields.

---

### Step 2 — Create One Filled Data Set
Populate the minimum data assets needed for the prototype:

- 2 enemies: Skitterling, Raider (from enemy_roster.md)
- 2 towers: Arrow Tower, Mage Spire (stats from tower_roster.md, Level 1 only)
- 2 elements: Fire, Water
- 2 statuses: Burning, Soaked
- 2 combos: Explosion, Steam Burst
- 10 waves for Mission E1 (from campaign_outline.md)

**Done when:** All prototype data assets exist and are filled with real values from the design documents. No placeholder zeros.

---

## Phase 2 — Core Prototype (Prove the Fun)

Build the minimum playable loop. At the end of this phase, you should be able to play a full 10-wave mission, place towers, trigger one combo, and win or lose.

### Step 3 — Basic Map and Enemy Pathing
- Create a simple test scene: a flat plane with a defined path (can be a NavMesh or a waypoint array)
- Create a basic enemy prefab that moves along the path from spawn point to objective
- Enemy reaches the end of the path and deals damage to a placeholder "objective" object
- Enemy has HP and can be killed by a placeholder (e.g., clicking it)

**Done when:** An enemy spawns, walks a path, reaches the objective, and deals damage. You can kill it manually.

---

### Step 4 — Wave Spawning System
- Create a WaveSpawner that reads a WaveData asset
- Spawns enemies in sequence according to wave definitions (count, delay between spawns)
- Advances through the wave list when all enemies in a wave are dead
- Broadcasts events: `OnWaveStart`, `OnWaveComplete`, `OnAllWavesComplete`

**Done when:** All 10 waves from Mission E1 spawn correctly in sequence. You can kill them manually and waves advance.

---

### Step 5 — Objective and Failure State
- Create an Objective object with an HP value
- Enemies that reach the objective deal damage to it
- When objective HP reaches 0: trigger mission fail state (log to console for now; UI comes later)
- When all waves are cleared: trigger mission complete state

**Done when:** You can lose a mission by letting enemies through, and win by killing all enemies across all waves.

---

### Step 6 — Gem Economy
- Create a GemManager (singleton) that tracks the current gem total
- Enemies drop their gem reward on death (from EnemyData)
- Wave completion awards the wave completion bonus (+15 gems)
- GemManager exposes `TrySpend(int cost)` — returns false and does nothing if insufficient gems

**Done when:** Gems increase as enemies die. You can verify counts in the inspector.

---

### Step 7 — Tower Placement System
- Create buildable zones in the scene (trigger volumes or designated grid cells)
- Player can open a tower selection panel and choose a tower type
- Clicking a valid zone places the tower prefab and deducts gem cost
- Show range preview circle on the ground while placing
- Invalid placements (occupied zone, insufficient gems) are blocked

**Done when:** You can place an Arrow Tower and a Mage Spire in the scene by spending gems. Range circles appear correctly. Placement is blocked when broke.

---

### Step 8 — Tower Attacking
- Tower finds the nearest enemy within range each attack cycle
- Tower fires a projectile (simple sphere/capsule) toward the target
- Projectile hits the enemy and deals damage (from TowerData)
- Enemy dies when HP reaches 0; drops gems

**Done when:** A placed Arrow Tower kills enemies walking past it. Gem count increases. Enemies die.

---

### Step 9 — Build Phase / Wave Phase Toggle
- Game state machine with two states: `BuildPhase` and `WavePhase`
- In BuildPhase: time is paused; placement UI is available; "Start Wave" button is visible
- In WavePhase: time runs; placement UI is hidden; tower management panel is read-only
- Transition from WavePhase back to BuildPhase when all enemies in the current wave are dead

**Done when:** The game correctly pauses between waves. You can place towers, then start the wave, then it returns to build phase when clear.

---

### Step 10 — Player Character
- Third-person character controller: WASD movement, mouse look
- Primary attack (Arcane Bolt): fires a projectile dealing magic damage
- Dash: short directional dash with cooldown
- Player has HP; taking damage from enemies reduces it
- On death: mission restarts

**Done when:** The player can move, aim, and shoot enemies. Taking enough hits restarts the mission.

---

### Step 11 — Status Buildup System
- Each enemy instance tracks a buildup counter per element
- When a tower (or player) with an element assigned hits the enemy, buildup increases by the tower's buildup-per-hit value
- When buildup reaches the threshold (100 for standard enemies), apply the status effect
- Active status is stored on the enemy; buildup resets; immunity timer starts after expiry

**Done when:** A Fire-infused Mage Spire (set manually in inspector for now) builds up Burning on an enemy after 4 hits. The Burning status visually indicates (color tint is fine for prototype).

---

### Step 12 — First Element Infusion
- Tower infusion: assign an element to a tower via the tower management panel during build phase
- Infused tower applies buildup of its element on each hit
- Infusion costs an orb (hardcode one orb available for testing)

**Done when:** You can infuse a Mage Spire with Fire during build phase. It then applies Burning buildup on enemies. Burning applies after threshold.

---

### Step 13 — First Two Combos
Implement Explosion and Steam Burst using the ComboData assets.

- On each hit that would apply a status: check if the enemy already has a different active status
- If yes: look up the matching ComboData (primer + trigger element)
- Execute the combo effect (Explosion: AoE true damage; Steam Burst: AoE magic damage + root)
- Clear the existing status; start immunity timer

**Done when:** A Fire-infused tower applies Burning; a Water-infused tower hits the Burning enemy and triggers Steam Burst (root + damage pulse visible). An Arrow Tower and a Mage Spire together trigger Explosion when both Fire-infused and one hits a Burning target.

---

### Step 14 — Tower Upgrading and Selling
- Tower management panel (click on placed tower): shows current stats, upgrade button, sell button
- Upgrade button: deducts gem cost, swaps to upgraded prefab/updates stats from TowerData Level 2
- Sell button (build phase only): refunds 100% of gems spent on that tower

**Done when:** You can upgrade an Arrow Tower to Level 2, see its stats increase, and sell it for a full refund during build phase.

---

### Step 15 — Basic HUD
Wire up the UI to the live game state:
- Wave counter (current / total)
- Objective HP bar
- Gem count
- Player HP bar
- Build phase / wave phase indicator
- Start Wave button

**Done when:** All HUD elements update in real time during play. The game is now fully playable end-to-end.

---

### Step 16 — Prototype Review

**Before continuing, evaluate the prototype against the success criteria from the design brief:**
- [ ] Placing and upgrading towers feels intuitive
- [ ] Player combat is helpful but not dominant
- [ ] Elemental combos are readable and satisfying
- [ ] Enemy composition creates meaningful build decisions
- [ ] One full mission already suggests replay value

If the answer to all five is yes: proceed to Phase 3.
If the answer to any is no: identify and fix the problem before adding more content. Do not paper over a broken loop with more features.

---

## Phase 3 — Vertical Slice (Prove the Region)

Expand the prototype into a complete first region: Emberveil. All 5 missions, the hub camp, basic progression.

### Step 17 — Remaining Prototype Enemies
Add Brute and the two minibosses using existing enemy systems:
- Brute: high HP/armor, speed burst on low HP
- Miniboss A (Ashen Stalker): player-aggro priority, dash at HP thresholds
- Miniboss B (Ironbound): tower damage on contact, Fortify stance

**Done when:** All 5 enemy types appear in waves and behave per enemy_roster.md.

---

### Step 18 — Remaining Towers
Add Cannon Tower and Crossbow Tower with their Level 1 and 2 stats. Seed Core is post-vertical-slice.

---

### Step 19 — All 4 Elements and Full Combo Matrix
Extend the status and combo system to support Earth and Air. Implement the remaining 8 combo effects using ComboData assets.

**Done when:** All 10 combos are triggerable and produce their defined effects.

---

### Step 20 — Orb Drop System
- Miniboss kill drops 1 guaranteed orb (random element)
- Elite kills have 15% chance to drop an orb shard
- 3 shards of any type combine into 1 orb
- Player collects by walking over the orb world object
- Orb inventory shown in HUD

---

### Step 21 — Tower Infusion via Orb Inventory
Replace the hardcoded test infusion with the real flow:
- Player clicks tower → management panel → INFUSE → select from owned orbs → confirm
- Orb consumed; tower gains element

---

### Step 22 — Level 3 Tower Branches
Add Level 3A and 3B upgrade paths for Arrow Tower and Mage Spire. Implement branch selection UI (confirm screen with two choices).

---

### Step 23 — All 5 Emberveil Maps
Build the 5 mission maps per campaign_outline.md:
- E1: single lane, intro
- E2: split lane, forge vents
- E3: portal siege mechanic
- E4: escort (Siege Engine) mechanic
- E5: boss arena with geysers

Each map needs: spawn points, waypoints/NavMesh, tower placement zones, elevated spots, objective placement, and any unique mechanic scripts.

---

### Step 24 — The Cinderbound Boss
Implement the 3-phase boss encounter per enemy_roster.md:
- Phase transitions at 60% and 30% HP
- Spawning adds
- Lava Pool generation
- Damage reduction shield in Phase 3
- Death explosion

---

### Step 25 — Hub Camp (Basic)
- Create a small walkable 3D hub scene
- Interactable objects: War Map, Forge, Training Yard (placeholder)
- War Map: mission select screen showing Emberveil missions with star ratings
- Forge: research point display and unlock list (read-only for now if RP system isn't ready)
- Scene transition: mission complete → returns to camp; camp → mission select → load mission

---

### Step 26 — Research Points and Forge
- Missions award research points on completion (per campaign_outline.md)
- Forge screen: spend RP to unlock towers, unlock tower levels, or buy passives
- Unlocked towers become available in the placement panel in future missions

---

### Step 27 — Save System
Define and implement save data for:
- Campaign progress (which missions are complete, star ratings)
- Unlocked towers and research
- Player settings (difficulty, auto-wave toggle)

Use Unity's built-in `PlayerPrefs` for MVP or a simple JSON file. Do not over-engineer this — the save structure from combat_system_spec.md covers what needs to be tracked.

---

### Step 28 — Mission End Screen and Difficulty Selection
- Mission complete screen: star rating, rewards summary, continue button
- Mission fail screen: retry / return to camp
- Difficulty selection screen before mission start: Story / Standard / Heartbroken
- Apply difficulty stat multipliers per combat_system_spec.md

---

### Step 29 — Vertical Slice Review

**Evaluate:**
- [ ] Complete Emberveil region is playable start to finish
- [ ] Progression loop (gems → upgrades → orbs → combos → mission rewards → research → unlocks) works end to end
- [ ] All 10 combos are visually distinct and readable
- [ ] Performance holds at 60 FPS with a full wave active (30–50 enemies + 8–12 towers + VFX)
- [ ] The boss encounter feels like a climax

If yes on all: begin Phase 4.

---

## Phase 4 — Full Production (Build the Campaign)

### Step 30 — Remaining 4 Regions
For each region (Thalvere, Greymantle, Aelcrest, Solharrow):
1. Build all mission maps
2. Add region-unique mechanic (flood tides, rubble, wind corridors, corruption spread)
3. Add region-specific enemies and elite variants
4. Write and implement NPC dialogue for that region
5. Add regional boss

Recommended order: Thalvere → Greymantle → Aelcrest → Solharrow. Solharrow is last because it depends on all prior systems being stable and the narrative being fully shaped.

---

### Step 31 — Remaining Towers
Add Arc Ray and Seed Core with full infusion behaviors. Add Level 3 branches for Cannon Tower, Crossbow Tower, Arc Ray, and Seed Core.

---

### Step 32 — Full Enemy Roster
Add Bulwark, Wraith, Siegeborn, and all regional elite variants and bosses.

---

### Step 33 — Narrative Implementation
- Camp NPC dialogue trees for Oryn (and Saris, Lenne, Daveth, Vael as regions are cleared)
- Mission opening and closing narrative scenes (text-based or simple cutscene)
- Elany encounter scenes in Solharrow missions
- Final confrontation and ending sequence

---

### Step 34 — Codex / Combo Encyclopedia
- Auto-unlock entries when player first encounters an enemy, triggers a combo, or finds a lore collectible
- Lore collectibles: place 2–3 per region map

---

### Step 35 — Player Ability Full Implementation
Add the remaining player abilities not yet implemented:
- Utility 1: Empower Zone
- Utility 2: Hunter's Mark
- Ultimate: Arcane Surge

---

### Step 36 — Difficulty Modifiers and Mission Modifiers
- Implement optional per-mission modifiers (No Retreat, Rush Hour, Ironhide, Warded)
- Modifier selection screen before mission start (optional checkbox UI)

---

## Phase 5 — Polish and Beta

### Step 37 — Art Pass
Replace placeholder geometry with final stylized assets:
- Environment kit for each region biome
- Tower models (1 per tower type)
- Enemy models and rigs (1 per type)
- Objective structure model
- Hub camp kit

**Priority order:** Enemies first (most screen time during combat), then towers, then environment.

---

### Step 38 — VFX
- Elemental projectile VFX per element (fire bolt, water orb, earth shard, air slash)
- Status effect VFX on enemies (flame loop, water drip, cracked stone, wind swirl)
- Combo detonation VFX for each of the 10 combos
- Tower range decal (clean circle)
- Orb pickup and collect VFX

**Performance rule:** All combo VFX must be benchmarked against the worst-case scenario (combat_system_spec.md: 8–12 towers, 30–50 enemies, multiple active zones). Profile before shipping any VFX.

---

### Step 39 — Audio
Implement in this order:
1. Tower attack sounds (one distinct sound per tower type)
2. Enemy death sounds (per archetype)
3. Combo trigger sounds (one distinct sound per combo)
4. Miniboss spawn sting
5. Player ability sounds
6. UI sounds (gem collect, orb collect, wave start, mission complete)
7. Ambient loop per region biome
8. Combat music loop per region
9. Hub camp music
10. Boss encounter music

---

### Step 40 — UI Polish
- Final font and icon set applied to all screens
- HUD element polish (animations, transitions)
- Status icon animations (pulse on expiry, combo announcement display timing)
- Codex visual polish
- Accessibility options implemented (colorblind mode, subtitle toggle, HUD scale)

---

### Step 41 — Balance Pass
Run each mission on all three difficulty settings. Tune:
- Enemy HP scaling per wave
- Gem reward rates
- Orb drop frequency
- Combo damage values
- Tower DPS curves
- Boss phase thresholds

Use the design doc values as a starting point, not a final answer. Feel is the arbiter.

---

### Step 42 — Performance Optimization
Profile and optimize:
- Enemy pathfinding (NavMesh query cost at peak enemy count)
- Particle system budgets per combo zone type
- Zone count caps (verify Lava Pool ×4, Sandstorm ×3 caps hold in worst case)
- Draw call reduction (GPU instancing for towers and enemies)
- Target: stable 60 FPS at 1080p in the worst-case scenario from the spec

---

### Step 43 — Closed Playtesting
Get 3–5 external players to play the full campaign. Watch silently. Do not explain anything.

Track:
- Where do players get confused without being told?
- Which missions feel too long or too short?
- Which combos do players never discover?
- Which towers get ignored?
- Where does the frame rate drop?

Iterate based on findings before launch.

---

## Post-Launch Backlog (Do Not Touch Until After Release)

| Feature              | Notes                                                   |
|----------------------|---------------------------------------------------------|
| Endless Defense mode | Separate scene, wave scaling formula, leaderboard       |
| Daily Challenge      | Seeded RNG per day, fixed modifiers, score tracking     |
| Rogue-lite Expedition| Chain of missions with blessings/curses, permadeath     |
| Co-op support        | Major scope addition; requires networking layer          |
| Additional heroes    | New player character with different kit                 |
| Modular tower creator| Post-launch feature; separate design document needed    |
| Mod support          | Requires data pipeline to be exposed; plan carefully    |

---

## Quick Reference: What to Build First

If you want to start today:

1. Create the ScriptableObject definitions (Step 1)
2. Fill in the prototype data assets (Step 2)
3. Build enemy pathing on a test map (Step 3)
4. Get a wave spawning (Step 4)

Everything else follows from there. The fastest path to knowing if this game is fun is getting a placed tower killing an enemy by wave 3 of a test mission — that is the proof-of-concept moment. Everything before it is infrastructure. Everything after it is content.

