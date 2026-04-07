# Elements TD — Pre-Development Expansion Brief

## Purpose
This document expands the original concept notes into a more development-ready brief. It is intended to help scope an MVP, identify missing systems, reduce rework, and give design, engineering, art, and narrative a shared starting point.

---

## 1. High-Level Review of the Current Concept

### What is already strong
- **Clear fantasy:** a 3D fantasy action tower defense where the player fights alongside their towers.
- **Strong differentiator:** elemental combo interactions between towers create a memorable combat identity.
- **Campaign structure:** reclaiming regions/kingdoms gives a natural sense of macro progression.
- **Visual potential:** post-apocalyptic European fantasy mixed with visible status effects and magical stone architecture is distinctive.
- **Meta progression potential:** unlockable towers, elements, passives, and later heroes provide long-tail retention.

### Main design risks to resolve before production
1. **Scope is currently too large for an MVP.** Open world hub traversal, 25–50 hour campaign, multiple regions, action combat, tower placement, combos, XP systems, permanent unlocks, and narrative campaign together can balloon quickly.
2. **The player role is not fully defined.** The notes say the player has auto attacks and can place towers, but not how much direct combat matters relative to tower strategy.
3. **Economy rules are incomplete.** Gems, tower refunds, XP upgrades, orb drops, and permanent unlocks are mentioned, but their relationships are not yet defined.
4. **Moment-to-moment readability will be hard in first person.** Tower defense requires strong battlefield readability; first-person perspective can make lane awareness difficult.
5. **Elemental combos may create large balance and implementation complexity.** The status system is promising, but it needs rules for stacking, duration, priority, immunity, and performance.
6. **Narrative inspiration is emotionally strong but too close to existing IP in places.** The emotional structure can remain, but names, lore, and mechanics should be made fully original.

---

## 2. Recommended MVP Definition

The best path is to define a smaller "prove the fun" version first.

### Recommended MVP Pillars
1. **Action + rougelike + tower defense hybrid feels good.**
2. **Elemental tower infusion and combo reactions feel readable and satisfying.**
3. **Regional progression creates a sense of reclaiming territory.**
4. **A hub/camp between missions gives light world continuity without requiring a true open world.**
5. **Heavily story driven**

### Recommended MVP Scope
- **Perspective:** third person by default for readability; optional first-person aim mode can be explored later.
- **Playable content:** 1 region + 1 hub + 4–6 missions + 1 boss mission.
- **Tower roster:** 4 base towers + 4 elemental infusions + 1 special experimental tower.
- **Enemy roster:** 6 core enemy archetypes + 2 minibosses + 1 major boss.
- **Progression:** mission rewards, simple unlock tree, tower upgrades within missions, and a few permanent passives.
- **Narrative:** intro cinematic/text, region-specific objective, end-of-region confrontation.
- **No full open world for MVP.** Use a **walkable camp hub** with mission board/world map selection.
- **No modular tower designer in MVP.** Keep it as post-launch or sequel feature.
- **No multiple heroes in MVP.** One protagonist only.

### Post-MVP / Expansion Features
- Full 5-region campaign
- Additional heroes/playstyles
- Optional co-op
- Modular tower creator
- True open-world
- Deeper tech trees and faction-specific tower variants

---

## 3. Core Player Experience

### Player fantasy
The player is a battle commander on the ground: fighting directly, building fortified magical defenses, and engineering devastating elemental chain reactions to reclaim corrupted lands.

### Intended emotional loop
- Enter hostile territory
- Establish order through tower placement
- Survive escalating waves
- Trigger visually satisfying elemental combos
- Secure the area and restore part of the world
- Return to camp stronger, with new tools and narrative progress

### Core gameplay loop
1. Select next mission from camp
2. Load into combat map
3. Scout the lanes / chokepoints
4. Spend starting resources to place opening towers
5. Fight waves while earning gems and orb drops
6. Upgrade, reposition, or infuse towers as enemy composition changes
7. Defeat minibosses and boss
8. Earn mission rewards and permanent progression
9. Return to camp for unlocks, dialogue, and next mission choice

---

## 4. Player Combat Design

This needs to be locked down early.

### Recommendation
The player should be **support-DPS / utility**, not the main damage source. Towers should remain the primary path to victory.

### Suggested player combat kit for MVP
- **Primary attack:** ranged magical bolt or weapon shot with modest DPS
- **Secondary attack:** charged shot / piercing attack / small AoE blast
- **Utility ability 1:** temporary empower zone that buffs nearby towers
- **Utility ability 2:** enemy mark that amplifies elemental status application
- **Mobility:** dodge or short dash
- **Ultimate-style cooldown:** short-duration battlefield effect, such as slowing all enemies in a radius or overcharging infused towers

### Design rule
If a skilled player can regularly clear maps while underbuilding towers, the action side is probably overtuned. The player's combat should help stabilize weak points, finish dangerous targets, and increase combo reliability.

---

## 5. Camera and Readability

### Recommended direction
- **Default camera:** over-the-shoulder third person
- **Optional mode:** first-person aiming for player attacks only, if implemented later
- **Build mode:** pull camera back slightly, slow time or pause in solo mode if desired

### Why
Tower defense lives or dies on situational awareness. A pure first-person presentation may look immersive but can obscure lane management, tower ranges, and combo outcomes.

### Readability requirements
- Strong lane telegraphing
- Clear enemy silhouettes by archetype
- Distinct colors/shapes for elemental states
- Obvious ground decals for persistent combo zones
- Tower range preview while placing/upgrading
- Floating icons or outlines for armor/magic-resist enemy traits

---

## 6. Combat Map Structure

### Recommended map format for MVP
Each mission map should have:
- 1–3 enemy lanes
- Clear buildable areas
- One core defense objective (gate, crystal, convoy point, camp beacon, etc.)
- A few elevated or premium tower spots
- Small traversal space for the player to rotate quickly between fronts

### Mission types
- **Standard defense:** defend a central objective from waves
- **Split-lane defense:** manage two or three fronts
- **Escort fortification:** defend a moving caravan or siege engine between holdout points
- **Portal siege:** destroy/collapse a demon portal after surviving waves
- **Boss holdout:** survive until a boss becomes vulnerable, then finish the encounter

---

## 7. Campaign and World Structure

### Recommended campaign structure
Instead of a true open world, structure the game as:
- **Home island camp hub**
- **5 world regions total** (4 elemental kingdoms + capital)
- Each region contains:
  - intro setup
  - 4–6 combat maps
  - 1 climax mission
  - region-specific enemies/mechanics

### Suggested region themes
- **Kingdom of Embers** — volcanic ruins, forges, fire cult corruption
- **Kingdom of Tides** — flooded canals, drowned keeps, marshland choke points
- **Kingdom of Stone** — collapsed fortresses, mining roads, armored enemies
- **Kingdom of Gales** — high cliffs, wind bridges, speed/displacement mechanics
- **Capital / Crownlands** — mixed biomes, elite enemies, narrative climax

### Hub activities for MVP
- Mission selection table / war map
- Tower unlock station / forge
- Passive upgrade shrine
- NPC dialogue and lore
- Training yard for testing towers and combos

---

## 8. Economy and Progression Rules

The economy needs explicit rules before prototyping.

### In-mission economy
**Primary currency:** Gems
- Earned from enemy kills, wave completion, minibosses, and optional objectives
- Used for placing towers, upgrading towers, and possibly rerolling orbs if desired

### Element orb rules
Recommended version:
- One random orb after every miniboss
- Small chance for elite enemies to drop bonus orb shards
- Three shards combine into one orb
- Orbs can infuse a compatible tower with one element
- A second orb of the same or different element enables advanced evolution/combos

### Tower selling
- Can be sold during build phases for full refund
- Cannot be sold during combat phase

### Permanent progression
Use three tracks:
1. **Campaign unlocks** — new towers, regions, mechanics
2. **Research tree** — passive bonuses and tower branches
3. **Player mastery** — cosmetic or account-level milestones, challenge rewards

### Recommendation for MVP progression
Keep it simple:
- Region clears award research points
- Research points unlock new towers or passive bonuses
- Mission stars/objectives unlock side upgrades or cosmetics

---

## 9. Tower System

### Recommended base tower roster for MVP
1. **Arrow Tower**
   - Cheap, fast, reliable physical single-target damage
2. **Cannon Tower**
   - Slow splash damage, ideal into swarms and clusters
3. **Crossbow Tower**
   - Long range, armor-piercing physical damage
4. **Mage Spire**
   - Magic damage, high status application rate
5. **Arc Ray** (optional MVP inclusion)
   - Continuous beam, strong for sustained status buildup
6. **Bombard Foundry / Magebomb Factory** (better as post-MVP unless scoped tightly)
7. **The Egg / Seed Core**
   - Special aura tower that only activates after infusion

### Recommended tower design rules
- Every tower should answer a distinct battlefield question.
- Every tower should have one clear weakness.
- Element infusion should modify role, not just recolor damage.
- No more than 4–5 towers in the first playable prototype.

### Upgrade structure per tower
Each tower should have:
- **Level 1:** base functionality
- **Level 2:** stat enhancement or minor role specialization
- **Level 3:** major branch choice (example: single-target vs splash)
- **Infusion slot 1**
- **Infusion slot 2 / advanced evolution** (post MVP)

---

## 10. Element System and Status Rules

This is the heart of the game and should be formalized in a systems spec.

### Core elemental identities
- **Fire:** damage over time, area pressure, detonation payoff
- **Water:** slows, control, path manipulation
- **Earth:** armor break, grounding, durable area denial
- **Air:** magic resistance shred, displacement, chaining spread

### Base status effects
- **Burning** — damage over time
- **Soaked** — slow / conductive / combo-ready
- **Shattered** — armor reduction
- **Gusted** — magic resist reduction / volatile airflow state

### Rule Definitions
1. Enemies can only hold one status effect a time, but the addition of another element (from a second tower) causes a combo (see below)
2. Each tower hit applies one stack, with a cap on number of stacks (TBD for balancing later)
3. Bosses can be hard CC'd but it takes significantly more hits / stacks and does not last as long
4. Combos consume all statuses and replace with new effects as described by combo
6. Combo damage is based on a formula of source tower damage, tower level, and enemy health, depending on the combo type
7. Different enemies have different resistances. Some are high in armor, some are high in magic resist.
   - Armor reduces damage taken from a tower's physical damage.
   - Magic resist reduces damage taken from a tower's magic damage.
8. If in co-op mode, XP is shared among party for everything. (Everyone is same level)

### Recommended status framework
Use a clean rule set:
- Base infused hits apply **buildup** toward a status threshold
- Double-infused towers apply status faster and may also spread a primed state
- A combo triggers when a primed enemy is hit by a second element
- Combo consumes the primed state unless otherwise specified

This will be easier to balance than instantly applying all statuses at full strength.

---

## 11. Recommended Combo Matrix Guidance

Your combo matrix is already promising. The main thing needed is consistency.

### Design principles for combos
- Each combo should have **one primary verb**:
  - burst
  - slow
  - zone control
  - displacement
  - debuff
- Each combo should be recognizable at a glance
- Persistent ground effects should be limited for performance and readability
- Knockback/displacement effects must be capped to avoid pathing exploits

### Suggested role framing for current combos
- **Explosion** — burst finisher
- **Steam Burst** — heavy control / setup
- **Lava Pool** — area denial
- **Wildfire** — mass priming / spread
- **Tidal Wave** — lane control / setback
- **Mud Trap** — choke-point control
- **Wind Chill** — progressive disable
- **Disintegrate** — anti-tank shred
- **Sandstorm** — attrition zone
- **Cyclone** — premium displacement / execution tool

### Important balance note
Cyclone, Tidal Wave, freeze, and stun effects are the most likely to break encounters. These should be gated by cooldowns, elite resistance, or boss control reduction.

---

## 12. Enemy Design

### Recommended core enemy roster for MVP
1. **Raider** — baseline melee unit
2. **Skitterling** — fast, weak swarm unit
3. **Brute** — slow, high-health frontline
4. **Bulwark** — high armor, weak to magic/earth setup
5. **Wraith** — high magic resist, weak to physical/air setup
6. **Siegeborn** — elite carrier/support enemy that buffs nearby enemies or targets objectives
7. **Miniboss type A** — fast assassin boss
8. **Miniboss type B** — slow siege boss
9. **Region boss** — unique mechanic encounter

### Enemy system tags to support gameplay clarity
Each enemy can have one or more tags:
- Light
- Armored
- Arcane
- Flying (post-MVP unless pathing is ready)
- Elite
- Boss
- Swarm

### Enemy abilities worth considering
- Shield bubble
- Heal aura
- Summoner unit
- Burrow / leap past first tower line (post-mvp)
- Anti-tower saboteur (post-mvp)
- Temporary status cleanse

---

## 13. Objectives, Failure States, and Difficulty

### Primary objective
Defend a key structure, convoy, or camp seal from enemy waves.

### Failure state
Mission fails if:
- objective health reaches zero, or
- all required hold points are lost, or
- optional special mission rules are broken

### Recommended difficulty model
Three layers:
1. **Base difficulty selection** — Story (easiest) / Standard / Heartbroken (hardest)
2. **Mission modifiers** — optional mutators for rewards
3. **Endgame challenge mode** — post-campaign scalable defense mode

### Difficulty considerations
Because this is an action + strategy hybrid, difficulty can come from:
- higher enemy count
- smarter wave composition
- harsher economy
- less build phase time
- stronger elites
Avoid only inflating health values, which can make combat feel muddy.

---

## 14. Save Structure and Long-Term Modes

### Save/profile data should track
- Campaign progress
- Region completion
- Unlocked towers
- Researched passives
- Best mission ratings
- Combo encyclopedia / codex entries
- Lore collectibles discovered
- Accessibility settings

### Good post-launch mode ideas
- Endless defense
- Daily challenge with fixed seed
- Rogue-lite expedition mode using temporary blessings/curses
- Score attack / leaderboard mode

---

## 15. Narrative Development Notes

### Core story structure
Keep the emotional shape, but make it fully original:
- A devoted ruler/commander becomes consumed by the war effort
- Their partner, left isolated under impossible pressure, becomes vulnerable to corruption
- The capital falls from within, not only from brute invasion
- The player now fights both for restoration of the realm and redemption of the relationship

### Important narrative caution
Because the inspiration is personal and emotionally charged, make sure the final story gives the possessed/corrupted queen real agency, humanity, and complexity. She should not feel like a passive object to be recovered.

### Themes throughout story
- neglect through duty
- grief weaponized by evil
- rebuilding trust and civilization together
- cleansing corruption without erasing memory
- restoration instead of revenge

### Suggested original naming direction
These are placeholders only, but enough to unblock worldbuilding:
- **World / continent:** Aurelune, Elyndor, Solharrow
- **4 Kingdops:** Frostspire, Crownrest, Halcyr, Norvaine
- **Player character:** Caelan, Lucen, 
- **Queen / spouse:** Elany
- **Archmage:** Oryn, Maeric
- **Main demon:** , (Malveris / Vorath) *The Hollow Regent*
- **Magic-absorbing stone:** Alumite, Veilstone

### Region narrative hooks
- Fire kingdom: old industrial furnaces reignited by hellfire
- Water kingdom: floodgates opened during the fall
- Earth kingdom: mines and bastions turned into demon foundries
- Air kingdom: signal towers and sky bridges broken by corruption
- Capital: center of betrayal, loss, and final restoration

---

## 16. Art Direction Notes

### Visual direction
The notes point toward a painterly, high-contrast fantasy world with ruined elegance and magical devastation.

### Art pillars
- Noble stone architecture scarred by corruption
- Distinct elemental VFX readable from mid-distance
- Corruption should feel invasive and intelligent, not generic demonic sludge
- Camps should feel hopeful, warm, and alive in contrast to fallen kingdoms

### Asset priorities for prototype
- 1 biome kit
- 4 tower models
- 6 enemy silhouettes
- 4 elemental VFX packages
- 1 hub camp kit
- 1 objective structure
- placeholder UI for statuses and wave flow

### UI style notes
- Elegant fantasy militaristic framing
- Minimal clutter during combat
- Strong iconography for statuses, elements, resistances, and combos

---

## 17. Audio Direction Notes

### Audio priorities
- Tower attacks must be readable by sound
- Every combo should have a unique signature impact sound
- Miniboss spawn should be unmistakable
- Hub music should contrast with warzone tension

### Music direction
- melancholic orchestral fantasy
- regional instrumentation differences
- hopeful motifs in camp
- corrupted variations of noble themes in fallen regions

---

## 18. Technical and Production Considerations

### Engine-level concerns to decide early
- Engine choice
- Target platforms
- Performance target (recommended: stable 60 FPS on target PC spec)

```
Recommended target machine
   GPU: RTX 4060 / RTX 5060 / RX 7600-class or better
   CPU: 6-core modern CPU
   Examples: Ryzen 5 5600 / 7600, Intel i5-12400F / newer equivalent
   RAM: 16 GB
   Storage: SSD required
Then define adjacent tiers:
   Minimum playable
      1080p, 45–60 FPS, low/medium settings
   Recommended
      1080p, locked 60 FPS, medium/high settings
   Stretch
      1440p, 60 FPS with upscaling allowed

Representative worst-case gameplay target
   1 player character on screen
   30–50 active enemies
   8–12 active towers
   multiple elemental VFX/status effects active
   projectiles, hit reactions, death effects, and UI all visible
   still averages 60 FPS at 1080p

Game thread / simulation: 5–6 ms
Render thread: 3–4 ms
GPU: 8–10 ms
Keep extra headroom for spikes
```
- Save system approach
- AI pathing solution
- VFX budget for combo-heavy battles
- Data-driven tower/enemy/status configuration pipeline

### Strong recommendation
Build the combat systems as **data-driven** from the start:
- towers
- status effects
- combo definitions
- wave compositions
- enemy resistances
- region modifiers

This will dramatically reduce iteration cost.

### Prototype milestone order
1. Basic lane + wave spawning
2. One player combat kit
3. Two towers
4. Gem economy
5. One elemental infusion
6. One combo reaction
7. Basic upgrade flow
8. One miniboss
9. Hub return + unlock
10. Expand content after fun is proven

---

## 19. System definitions

### Design questions
- What is the exact mission length target?
   - About 30 minutes
- Are waves manually started or automatic?
   - Waves are default manually started, but can be toggled to be automatic
- Can the player move towers after placement?
   - No, but they can be sold during build phases for a full refund
- Is there a cap on infused towers per mission?
   - No, it's balanced through dropping of elemental orbs
- Can all towers accept all elements?
   - Yes
- Do enemies target towers, the player, or only the objective?
   - Enemies priority target the objective, unless the player is within an *aggro* range of the enemy
   - Only certain enemies can damage towers
   - When a tower is damaged, the player must spend gems to repair it, but it can't be permanently destroyed
- Can the player die, and if so what happens?
   - Yes, the level must be restarted
- Are build phases real-time, slowed time, or paused?
   - Paused
- How much RNG is acceptable in orb drops?
   - 100% RNG during waves, but research trees allow obtaining orbs more directly as player progresses campaign

### Production questions
- Solo project
- Desired art fidelity for first playable?
   - Stylized low-to-mid fidelity 3D, low poly or similar to Orcs Must Die, or Risk of Rain 2
- Need for controller support at launch?
   - No
- Is online/co-op in long-term vision?
   - Yes, but game should be focused on single player story driven
- Is mod support desirable later?
   - Post MVP potentially

---

## 20. Recommended First Prototype Spec

If the goal is to start building quickly, this is the first playable I would target.

### First playable content
- 1 combat map
- 1 objective to defend
- 10 waves
- 3 enemy types
- 2 towers
- 2 elements (Fire and Water)
- 2 combo outcomes (Explosion and Steam Burst)
- 1 miniboss on wave 5 and wave 10
- basic gem economy
- tower placement, upgrading, and selling
- simple third-person player attack

### Success criteria
The prototype is successful if:
- placing and upgrading towers feels intuitive
- player combat is helpful but not dominant
- elemental combos are readable and satisfying
- enemy composition creates meaningful build decisions
- one full mission already suggests replay value

---

## 21. Recommended Next Documents to Create

After this brief, the most useful follow-up docs would be:
1. **MVP feature list** with must-have / nice-to-have / cut
2. **Combat systems spec** for statuses, combo rules, and formulas
3. **Tower roster sheet** with stats and upgrade branches
4. **Enemy roster sheet** with resistances and role tags
5. **Campaign/region outline** with mission counts and unique mechanics
6. **Narrative bible** with renamed characters, places, factions, and lore
7. **UI/UX wireframes** for HUD, tower placement, upgrade menus, and map flow
8. **Production roadmap** by milestone

---

## 22. Final Recommendation

The concept is compelling and has real identity. The **elemental combo system** and **on-the-ground battle commander fantasy** are the strongest hooks. The most important move now is not adding more ideas, but **choosing what to prove first**.

If development starts with a tightly scoped vertical slice focused on:
- one region,
- one hub,
- a handful of towers,
- a handful of enemies,
- and a polished elemental combo loop,

then the broader campaign fantasy can grow from a stable foundation instead of collapsing under early scope.

