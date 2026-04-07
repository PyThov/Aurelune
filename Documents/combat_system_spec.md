# Elements TD — Combat System Specification

## Purpose
This document defines all numerical rules, formulas, and system behaviors for combat. It is the authoritative reference for implementing status effects, combo reactions, player stats, and damage calculations.

---

## 1. Damage Types

### Physical Damage
- Dealt by Arrow Tower, Cannon Tower, Crossbow Tower
- Reduced by enemy **Armor**
- Formula: `effective_damage = max(1, raw_damage × (1 - armor / (armor + 100)))`

### Magic Damage
- Dealt by Mage Spire, Arc Ray, and most elemental effects
- Reduced by enemy **Magic Resist**
- Formula: `effective_damage = max(1, raw_damage × (1 - magic_resist / (magic_resist + 100)))`

### True Damage
- Bypasses both Armor and Magic Resist
- Used by a small number of combo effects (noted explicitly)

### Armor / Magic Resist Reference Table

| Stat Value | Damage Reduction |
|------------|-----------------|
| 0          | 0%              |
| 10         | 9%              |
| 20         | 17%             |
| 30         | 23%             |
| 50         | 33%             |
| 75         | 43%             |
| 100        | 50%             |

---

## 2. Status Effect System

### Buildup Model
Towers do not instantly apply status effects. Instead, each hit applies **buildup points** toward a **status threshold**. When the threshold is reached, the status is applied and buildup resets.

This model allows towers to contribute to status without instantly locking enemies into CC, and enables meaningful race-to-status tower combinations.

### Buildup Per Hit (Base Values, before infusion)

| Tower         | Buildup / Hit | Notes                          |
|---------------|---------------|--------------------------------|
| Arrow Tower   | 5             | Physical, low status role      |
| Cannon Tower  | 8             | Applied to each enemy in AoE   |
| Crossbow Tower| 5             | Physical, armor-focus role     |
| Mage Spire    | 25            | Primary status application tower|
| Arc Ray       | 15 / tick     | Continuous, ~8 ticks/sec       |
| Seed Core     | 0 (base)      | Aura-only; gains buildup on infusion |

**Infused towers** apply **+50% buildup** per hit (rounded up).

### Status Thresholds by Enemy Tier

| Enemy Tier   | Buildup Threshold | Status Duration | Hard CC Cap    |
|--------------|-------------------|-----------------|----------------|
| Standard     | 100               | Full duration   | Full duration  |
| Elite        | 200               | Full duration   | 2.5 sec max    |
| Miniboss     | 400               | 50% duration    | 2.0 sec max    |
| Boss         | 800               | 25% duration    | 1.0 sec max    |

### Status Effects

#### Burning (Fire)
- Source: Fire-infused tower hits
- Effect: Deals damage over time
- Damage: `8 × tower_level` magic damage per second
- Duration: 6 seconds (standard)
- Stack behavior: Refreshes duration, does not stack damage

#### Soaked (Water)
- Source: Water-infused tower hits
- Effect: 30% movement speed reduction; increases buildup received from all sources by 25%
- Duration: 5 seconds (standard)
- Stack behavior: Refreshes duration

#### Shattered (Earth)
- Source: Earth-infused tower hits
- Effect: Reduces enemy Armor by 40% for the duration
- Duration: 6 seconds (standard)
- Stack behavior: Refreshes duration; does not stack the reduction

#### Gusted (Air)
- Source: Air-infused tower hits
- Effect: Reduces enemy Magic Resist by 40% for the duration; affected enemy has 10% chance per hit to be briefly displaced (0.5 sec knockback)
- Duration: 5 seconds (standard)
- Stack behavior: Refreshes duration

### Status Immunity
- Enemies cannot hold more than one base status at a time
- When a second status is applied to an already-primed enemy, a **combo triggers** instead of overwriting
- After a combo resolves, the enemy enters a **1.5 second status immunity window** before buildup can resume
- Bosses have a **3 second immunity window** after any combo

---

## 3. Combo System

### Trigger Conditions
A combo fires when:
1. An enemy has an active status effect (is "primed")
2. A tower dealing a **different element** hits that enemy

The combo consumes the existing status and fires its reaction effect.

### Combo Matrix

| Primer (Status) | Trigger Element | Combo Name    | Primary Verb       |
|-----------------|-----------------|---------------|--------------------|
| Burning         | Fire            | Explosion     | Burst              |
| Burning         | Water           | Steam Burst   | Heavy control      |
| Burning         | Earth           | Lava Pool     | Area denial        |
| Burning         | Air             | Wildfire      | Mass spread        |
| Soaked          | Fire            | Steam Burst   | Heavy control      |
| Soaked          | Water           | Tidal Wave    | Lane control       |
| Soaked          | Earth           | Mud Trap      | Choke control      |
| Soaked          | Air             | Wind Chill    | Progressive disable|
| Shattered       | Fire            | Lava Pool     | Area denial        |
| Shattered       | Water           | Mud Trap      | Choke control      |
| Shattered       | Earth           | Disintegrate  | Anti-tank shred    |
| Shattered       | Air             | Sandstorm     | Attrition zone     |
| Gusted          | Fire            | Wildfire      | Mass spread        |
| Gusted          | Water           | Wind Chill    | Progressive disable|
| Gusted          | Earth           | Sandstorm     | Attrition zone     |
| Gusted          | Air             | Cyclone       | Displacement       |

### Combo Power Formula
All combo effects are scaled by a **combo_power** value:

```
combo_power = triggering_tower_base_damage × level_multiplier
```

**Level Multipliers:**

| Tower Level | Multiplier |
|-------------|-----------|
| 1           | 1.0       |
| 2           | 1.3       |
| 3           | 1.7       |

### Combo Effect Definitions

#### Explosion
- Type: Burst / True Damage
- Effect: Instant AoE detonation centered on target
- Damage: `combo_power × 4.0` true damage to all enemies within 3.5 units
- Notes: Most reliable burst finisher; no persistent effect

#### Steam Burst
- Type: Heavy Control + Magic Damage
- Effect: Primed target and nearby enemies (2.5 unit radius) are rooted for 3 sec and take magic damage
- Damage: `combo_power × 2.0` magic damage
- Root duration vs tiers: Standard 3 sec / Elite 2 sec / Miniboss 1 sec / Boss 0.5 sec

#### Lava Pool
- Type: Area Denial / Magic Damage over Time
- Effect: Creates a persistent lava zone (3.0 unit radius) at impact location
- Damage: `combo_power × 0.6` magic damage per second
- Duration: 8 seconds
- Notes: Applies Burning buildup to enemies standing inside (10 buildup/sec); limit of 4 simultaneous active Lava Pools per map for performance

#### Wildfire
- Type: Mass Status Spread
- Effect: Spreads the Burning status to up to 4 nearby enemies (within 4.0 units of target), then deals bonus fire damage to all affected
- Damage: `combo_power × 1.5` magic damage to original target; `combo_power × 0.8` to each spread target
- Notes: Does not require spread targets to be primed; applies Burning instantly to spread targets (skips buildup threshold)

#### Tidal Wave
- Type: Lane Control / Physical + Magic Damage
- Effect: Pushes all enemies in a 4.0 unit forward cone back 6 units along the path; deals damage
- Damage: `combo_power × 1.5` magic damage to affected enemies
- Pushback cap: Cannot push enemies past their spawn point; cannot push bosses more than 2 units
- Notes: May expose enemies to additional tower fire during pushback

#### Mud Trap
- Type: Choke-Point Control / Slow Zone
- Effect: Creates a mud zone (3.5 unit radius) that slows enemies by 60% while inside and for 1 second after leaving
- Damage: `combo_power × 0.3` physical damage per second (tick rate: 1/sec)
- Duration: 6 seconds
- Notes: Applies Shattered buildup slowly (5 buildup/sec) to enemies inside

#### Wind Chill
- Type: Progressive Disable / Magic Damage
- Effect: Applies a stacking slow to target on each hit from any tower while Gusted is active
- Slow per stack: 15%; Maximum stacks: 5 (75% max slow)
- Stacks are consumed when the enemy exits Wind Chill state
- Damage: `combo_power × 1.0` magic damage on trigger
- Duration of stacking window: 5 seconds

#### Disintegrate
- Type: Anti-Tank Shred / Magic Damage
- Effect: Instantly strips 50% of the target's current Armor and Magic Resist for 5 seconds; deals burst damage
- Damage: `combo_power × 2.5` magic damage
- Notes: Reduction is applied before the damage; extremely effective against armored elites; boss version: 25% strip, 3 seconds

#### Sandstorm
- Type: Attrition Zone / Mixed Damage
- Effect: Creates a swirling storm zone (4.0 unit radius) that continuously applies Gusted buildup and deals damage
- Damage: `combo_power × 0.4` magic damage per second
- Gusted buildup rate inside zone: 15 buildup/sec
- Duration: 10 seconds
- Notes: Limit of 3 simultaneous active Sandstorms per map for performance

#### Cyclone
- Type: Premium Displacement / True Damage
- Effect: Launches the target into the air (hard CC); on landing, deals AoE true damage and briefly stuns nearby enemies
- Damage: `combo_power × 5.0` true damage to primary target; `combo_power × 2.0` true damage to nearby (2.5 unit radius)
- Air duration: Standard 2 sec / Elite 1.5 sec / Miniboss 0.75 sec (no air, just knockback) / Boss 0 sec (immune to air, still takes damage)
- Cooldown: A given enemy can only be Cycloned once every 8 seconds
- Notes: Highest damage ceiling of all combos; tightly gated by rarity of Air+Gusted setup

### Performance Rules for Persistent Zones
| Zone Type   | Max Simultaneous |
|-------------|-----------------|
| Lava Pool   | 4               |
| Mud Trap    | 5               |
| Sandstorm   | 3               |
| Total Zones | 8               |

When the cap is reached, the oldest zone of that type is removed.

---

## 4. Player Combat

### Player Stats (Base Values)

| Stat                    | Value            |
|-------------------------|------------------|
| Max HP                  | 150              |
| HP Regen                | 0 (none in combat)|
| Movement Speed          | 5.5 units/sec    |
| Dash Distance           | 4.0 units        |
| Dash Cooldown           | 1.2 seconds      |
| Dash I-frames           | 0.4 seconds      |

### Player Abilities

#### Primary Attack — Arcane Bolt
- Type: Magic damage, single target, ranged projectile
- Damage: 18 magic damage per hit
- Fire Rate: 2.0 shots/sec
- Range: 20 units
- Buildup applied: 12 buildup per hit (applies buildup of the player's equipped element if any; default: none)

#### Secondary Attack — Charged Shot
- Type: Magic damage, piercing AoE in a line
- Damage: 55 magic damage
- Charge Time: 1.2 seconds (hold)
- Range: 25 units, width: 1.5 units
- Cooldown (after release): 2.5 seconds
- Buildup applied: 40 buildup per enemy hit

#### Utility 1 — Empower Zone
- Effect: Creates a 6-unit radius aura around the player for 6 seconds; all towers inside deal +25% damage and apply +30% buildup
- Cooldown: 22 seconds

#### Utility 2 — Hunter's Mark
- Effect: Marks a single target for 8 seconds; marked enemy receives +50% buildup from all sources and +15% damage from all towers
- Cooldown: 18 seconds
- Notes: Highly effective for triggering combos on elites or priming bosses

#### Mobility — Dash
- Covered in stats above; no damage component

#### Ultimate — Arcane Surge
- Effect: For 4 seconds, all towers within 10 units of the player gain +50% attack speed and +50% buildup rate; player gains brief invulnerability (1 sec)
- Cooldown: 60 seconds
- Notes: Intended to be used to force a combo chain on a tough target or survive a dangerous moment

### Player HP Sources
- HP is restored only by:
  - Completing a wave (restores 20 HP)
  - Specific research passives (post-MVP)
- If the player reaches 0 HP: mission restarts from the beginning

---

## 5. Economy Rules

### Gems (In-Mission Currency)

| Source                        | Gem Reward         |
|-------------------------------|--------------------|
| Standard enemy kill           | 5–12 gems (by tier)|
| Elite enemy kill              | 25–40 gems         |
| Miniboss kill                 | 80 gems            |
| Wave completion bonus         | 15 gems            |
| Optional objective completed  | 30–50 gems         |

**Enemy gem values by type:**

| Enemy Type  | Gems on Kill |
|-------------|-------------|
| Skitterling | 5           |
| Raider      | 8           |
| Wraith      | 10          |
| Bulwark     | 10          |
| Brute       | 12          |
| Siegeborn   | 30          |
| Miniboss A  | 80          |
| Miniboss B  | 80          |

### Tower Selling
- During **build phase** (paused): sell for **100% gem refund**
- During **combat phase**: cannot sell

### Tower Repair
- If a tower is damaged by an enemy, it continues to function at reduced efficiency (damage reduced proportional to missing HP)
- Repair cost: `missing_tower_hp × 0.4` gems (rounded up)
- Towers cannot be permanently destroyed

### Element Orbs

| Source                   | Drop                                    |
|--------------------------|-----------------------------------------|
| Miniboss kill            | 1 guaranteed orb (random element)       |
| Elite enemy kill         | 15% chance to drop 1 orb shard         |
| 3 orb shards (any combo) | Combine into 1 orb (random element)    |

- Orb element is randomized; research upgrades allow limited rerolls or element targeting (post-MVP)
- Orbs can infuse any tower with one element
- A second orb on the same tower enables advanced evolution behaviors (defined per tower in tower_roster.md)
- Orbs are consumed on use

---

## 6. Wave System

- Waves are **manually started** by default
- An option to enable **auto-start** (with a configurable countdown timer) is available in settings
- **Build phase** when a wave ends: time is **paused** for tower management
- Recommended build phase layout: enter → assess → buy/sell/upgrade → start wave

### Wave Scaling
Each wave increases enemy count and introduces new archetypes. Specific wave compositions are defined per mission in campaign_outline.md.

General scaling rules:
- Enemy HP scales by `1.0 + (wave_number - 1) × 0.12` per wave
- Enemy count scales by approximately 2–3 additional units per wave beyond wave 3
- New enemy types are always introduced on a lighter wave to allow the player to learn them

---

## 7. Difficulty Modifiers

### Base Difficulty Tiers

| Setting     | Enemy HP | Enemy Speed | Gem Rewards | Player HP | Build Phase |
|-------------|----------|-------------|-------------|-----------|-------------|
| Story       | ×0.75    | ×0.9        | ×1.0        | 225       | Paused      |
| Standard    | ×1.0     | ×1.0        | ×1.0        | 150       | Paused      |
| Heartbroken | ×1.4     | ×1.1        | ×0.85       | 100       | Paused      |

### Mission Modifiers (Optional)
Modifiers are optional per-mission challenges that award bonus rewards on completion.

Examples:
- **No Retreat** — Cannot sell any towers once placed; +20 bonus gems reward
- **Rush Hour** — Waves auto-start with no pause; +15 bonus gems reward
- **Ironhide** — All enemies have +50% armor; +orb shard reward
- **Warded** — All enemies have +50% magic resist; +orb shard reward

---

## 8. Enemy Aggro Rules

- Enemies **priority target the objective** at all times
- If the **player moves within aggro range** of an enemy, that enemy switches to targeting the player until:
  - The player exits aggro range for 3 continuous seconds, or
  - The enemy is forced by pathing to resume objective routing
- **Aggro range:** 7 units (standard), 10 units (Siegeborn), 5 units (Brute/miniboss — less reactive)
- Only certain enemies (defined in enemy_roster.md) can damage towers
- Towers have no aggro; enemies do not route toward them unless they block the pathing lane

