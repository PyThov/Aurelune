# Elements TD — Enemy Roster

## Design Rules
- Each enemy archetype answers a specific strategic threat
- Enemy types are introduced one or two at a time per mission so players can learn them
- Resistances create meaningful tower choices; no enemy should be trivially countered by one tower type
- HP values are for Standard difficulty; see combat_system_spec.md for difficulty multipliers
- Wave-scaling applies an HP multiplier of `1.0 + (wave_number - 1) × 0.12` per wave

---

## Stat Notation
- **HP:** Health points at base (wave 1, standard difficulty)
- **Speed:** Movement speed in units/second along the path
- **Armor:** Flat armor stat (reduces physical damage)
- **Magic Resist:** Flat magic resist stat (reduces magic damage)
- **Gems:** Gem reward on kill
- **Tags:** System tags that influence tower interactions and game rules

---

## Standard Enemies

### 1. Raider
**Role:** Baseline melee unit. The reference enemy. All numbers are balanced around the Raider.
**Threat:** Reliable damage to the objective if towers don't keep up. Fast enough that delayed placement is punished.

| Stat         | Value        |
|--------------|--------------|
| HP           | 150          |
| Speed        | 3.0 units/sec|
| Armor        | 5            |
| Magic Resist | 0            |
| Gems on Kill | 8            |
| Tags         | Light        |

**Behavior:**
- Targets objective; switches to player within 7-unit aggro range
- No special abilities
- Cannot damage towers

---

### 2. Skitterling
**Role:** Fast, fragile swarm unit. Forces players to spread towers or use splash; a single focused tower can be overwhelmed by quantity.
**Threat:** Speed and numbers. Individually weak but punishes gaps in tower coverage.

| Stat         | Value        |
|--------------|--------------|
| HP           | 60           |
| Speed        | 5.0 units/sec|
| Armor        | 0            |
| Magic Resist | 0            |
| Gems on Kill | 5            |
| Tags         | Light, Swarm |

**Behavior:**
- Always spawns in groups of 4–8
- Targets objective exclusively; does not aggro on player
- Cannot damage towers
- Immune to Mud Trap slowdown (skitter through it at 80% of normal speed instead of 40%)

---

### 3. Brute
**Role:** Slow, high-health frontline absorber. The tower damage sponge that buys time for other enemies.
**Threat:** Pure durability. Ties up tower fire while other units slip through.

| Stat         | Value        |
|--------------|--------------|
| HP           | 500          |
| Speed        | 1.5 units/sec|
| Armor        | 30           |
| Magic Resist | 0            |
| Gems on Kill | 12           |
| Tags         | Armored      |

**Behavior:**
- Targets objective; aggro range 5 units (less responsive than lighter units)
- When below 30% HP, gains a 15% movement speed burst for 3 seconds
- Cannot damage towers
- Susceptible to Earth setups (Shattered + Disintegrate combo recommended)

---

### 4. Bulwark
**Role:** High-armor frontline. Directly punishes physical-only tower loadouts.
**Threat:** Hard counter to Arrow, Cannon, and Crossbow towers if the player hasn't invested in Earth infusions or magic damage.

| Stat         | Value        |
|--------------|--------------|
| HP           | 400          |
| Speed        | 1.8 units/sec|
| Armor        | 60           |
| Magic Resist | 0            |
| Gems on Kill | 10           |
| Tags         | Armored      |

**Behavior:**
- Targets objective; no aggro on player
- Cannot damage towers
- Carries a shield that blocks the first status effect application (shield has no HP; it simply negates one successful status trigger, then breaks)

---

### 5. Wraith
**Role:** High magic resist. Directly punishes magic-heavy tower loadouts.
**Threat:** Hard counter to Mage Spire and Arc Ray if the player hasn't invested in Air infusions or physical damage.

| Stat         | Value        |
|--------------|--------------|
| HP           | 250          |
| Speed        | 2.5 units/sec|
| Armor        | 0            |
| Magic Resist | 50           |
| Gems on Kill | 10           |
| Tags         | Arcane       |

**Behavior:**
- Targets objective; aggro range 7 units
- Every 10 seconds, performs a phase step (teleports 3 units forward along the path)
- Cannot damage towers
- Air infusions and Gusted combos are particularly effective (Disintegrate shreds magic resist)

---

### 6. Siegeborn
**Role:** Elite support/carrier unit. Does not deal high damage itself but creates a danger zone around it.
**Threat:** Its aura buffs nearby enemies and it is one of the few unit types that can damage towers.

| Stat         | Value        |
|--------------|--------------|
| HP           | 320          |
| Speed        | 2.0 units/sec|
| Armor        | 10           |
| Magic Resist | 10           |
| Gems on Kill | 30           |
| Tags         | Elite        |

**Behavior:**
- Targets objective; aggro range 10 units (actively seeks player if nearby)
- **Aura:** Nearby enemies within 4 units gain +20% move speed and +15% HP regeneration per second
- **Tower sabotage:** When within melee range of a tower, attacks it for 25 physical damage per second; player must spend gems to repair
- Priority target: always route player attacks toward Siegeborn first

---

## Miniboss Enemies

### 7. Miniboss A — The Ashen Stalker
**Role:** Fast assassin boss. Tests the player's ability to deal damage quickly and use mobility.
**Threat:** Speed, aggression, and directly targeting the player.

| Stat         | Value        |
|--------------|--------------|
| HP           | 1,500        |
| Speed        | 4.0 units/sec|
| Armor        | 15           |
| Magic Resist | 10           |
| Gems on Kill | 80           |
| Tags         | Elite, Boss  |

**Behavior:**
- Actively prioritizes the player over the objective when the player is within 15 units
- At 70% and 40% HP, dashes forward 6 units (passes through tower range momentarily)
- Cannot be slowed below 60% of base speed (Mud Trap and Wind Chill are capped)
- Deals 40 physical damage per hit to the player; hit rate 1.2/sec
- Cannot damage towers directly

**Status interactions:**
- Status threshold: 400 (elite tier)
- Hard CC cap: 2.0 seconds

---

### 8. Miniboss B — The Ironbound
**Role:** Slow siege boss. Tests the player's DPS output and resource investment.
**Threat:** Extreme HP and armor; can damage towers and ignores most CC.

| Stat         | Value        |
|--------------|--------------|
| HP           | 3,000        |
| Speed        | 1.0 units/sec|
| Armor        | 80           |
| Magic Resist | 20           |
| Gems on Kill | 80           |
| Tags         | Armored, Elite, Boss |

**Behavior:**
- Always targets the objective; does not aggro on player
- Attacks any tower within 3 units for 60 physical damage per second
- Every 20 seconds, performs a Fortify stance for 3 seconds: 50% damage reduction and immune to displacement effects
- Cannot be pushed back by Tidal Wave or Cyclone (hard CC immunity)

**Status interactions:**
- Status threshold: 400 (elite tier)
- No displacement effects during Fortify

---

## Regional Bosses

### 9. Emberveil Region Boss — The Cinderbound

**Lore hook:** A forge-lord whose body was consumed by hellfire, now bound in cracked volcanic stone and demonic flame. Commands fire elementals and can reshape the battlefield with lava.

| Stat         | Value        |
|--------------|--------------|
| HP           | 6,000        |
| Speed        | 1.2 units/sec|
| Armor        | 40           |
| Magic Resist | 30           |
| Gems on Kill | 200          |
| Tags         | Boss, Elite  |

**Phase 1 (100%–60% HP):**
- Walks toward objective; periodically spawns 2 Skitterlings every 12 seconds
- Attacks towers within 4 units for 80 physical damage/sec

**Phase 2 (60%–30% HP — Enraged):**
- Speed increases to 1.8 units/sec
- Every 18 seconds, creates 2 Lava Pool zones at random positions in the combat area (using game's own Lava Pool mechanics; does not count toward zone cap)
- Spawns 1 Raider every 20 seconds instead of Skitterlings

**Phase 3 (30%–0% HP — Inferno Mode):**
- Becomes immune to Burning status (already on fire)
- Gains a 20% damage reduction aura for 8 seconds that must be broken by dealing 1,000 damage to cancel
- On death: creates a large Lava Pool (5 unit radius, 6 seconds) centered on itself — the player must escape the area

**Status interactions:**
- Burning immunity in Phase 3
- Status threshold: 800 (boss tier)
- Hard CC cap: 1.0 second

---

## Enemy System Tags Reference

| Tag      | Behavior Notes                                                                 |
|----------|--------------------------------------------------------------------------------|
| Light    | No physical resistance; susceptible to standard attacks                        |
| Armored  | High armor; strongly recommended to use Earth setups or armor-piercing towers  |
| Arcane   | High magic resist; strongly recommended to use Air setups or physical towers   |
| Swarm    | Always spawns in groups; partial CC immunity (Mud Trap reduced effectiveness)  |
| Elite    | Higher status threshold (200 standard, higher for bosses)                      |
| Boss     | Status threshold 800; hard CC capped; unique phase behaviors                   |
| Flying   | Post-MVP; bypasses ground-level tower attack angles; requires special towers   |

---

## Enemy Ability Reference (Current and Post-MVP)

### Currently In Scope
| Ability            | Enemy          | Behavior                                              |
|--------------------|----------------|-------------------------------------------------------|
| Speed Burst        | Brute          | +15% speed below 30% HP for 3 seconds                |
| Phase Step         | Wraith         | Teleports 3 units forward every 10 seconds            |
| Shield Bubble      | Bulwark        | Blocks first status trigger; then breaks              |
| Aura Buff          | Siegeborn      | +20% speed and +15% HP regen to nearby enemies       |
| Tower Sabotage     | Siegeborn, Ironbound | Damages towers on contact                       |
| Dash               | Ashen Stalker  | Forward lunge at 70% and 40% HP                      |
| Fortify            | Ironbound      | 50% damage reduction + CC immunity for 3 sec         |
| Summon Adds        | Cinderbound    | Spawns waves of Skitterlings and Raiders              |
| Lava Field         | Cinderbound    | Creates environmental Lava Pools                     |

### Post-MVP (Do Not Implement Yet)
| Ability          | Notes                                                          |
|------------------|----------------------------------------------------------------|
| Burrow / Leap    | Bypasses the first tower line; enters the lane mid-path       |
| Anti-Tower Saboteur | Dedicated unit that actively routes to and destroys towers |
| Status Cleanse   | Removes all status effects from self and nearby allies        |
| Heal Aura        | Restores HP to nearby enemies; requires player to focus it    |
| Summoner Unit    | Continuously spawns weaker enemies until killed               |

---

## MVP Prototype Enemy Set
For the first playable, use only:
1. Skitterling
2. Raider
3. Brute (introduce on wave 5)
4. Miniboss A (wave 5 boss encounter)
5. Miniboss B (wave 10 final boss)

