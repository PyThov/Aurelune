# Elements TD — Tower Roster

## Design Rules
- Every tower answers a distinct battlefield question
- Every tower has one clear weakness
- Element infusion modifies role, not just damage numbers
- No more than 4–5 towers should be active in the first playable prototype
- Selling during build phase refunds 100% of placement cost
- Towers cannot be moved after placement

---

## Stat Notation
- **DPS:** approximate damage per second at that level against an unarmored enemy
- **Buildup/hit:** status buildup applied per projectile or tick
- **Range:** radius in world units
- **Cost:** gem cost to place or upgrade

---

## 1. Arrow Tower

**Role:** Cheap, fast single-target physical damage. The backbone tower; spam-placeable and reliably effective at all stages.
**Weakness:** Low damage per shot; struggles against high-armor targets without Earth setup.
**Damage Type:** Physical

### Stats

| Level | Damage/shot | Attack Speed | Range | DPS  | Buildup/hit | Cost       |
|-------|-------------|--------------|-------|------|-------------|------------|
| 1     | 15          | 1.2/sec      | 12    | 18   | 5           | 80 gems    |
| 2     | 22          | 1.4/sec      | 12    | 31   | 5           | 65 gems    |
| 3A    | 40          | 1.0/sec      | 16    | 40   | 5           | 90 gems    |
| 3B    | 18          | 2.4/sec      | 12    | 43   | 5           | 90 gems    |

### Upgrade Branches (Level 3)

**3A — Marksman:**
- Greatly increased range and damage; reduced fire rate
- Gains 20% armor penetration
- Ideal for long-range single-target pressure

**3B — Rapid Shot:**
- Greatly increased fire rate; modest damage per shot
- Each hit applies a 5% slow for 1.5 seconds (stacks up to 25%)
- Ideal for lane saturation and status buildup support

### Elemental Infusion Effects

| Element | Infusion 1 Effect                                                      |
|---------|------------------------------------------------------------------------|
| Fire    | Shots apply Burning buildup (+50% buildup rate). Burning enemies take +15% damage from this tower. |
| Water   | Shots apply Soaked buildup. Soaked enemies hit by this tower are slowed an additional 10%. |
| Earth   | Shots apply Shattered buildup. Tower gains +15% armor penetration.     |
| Air     | Shots apply Gusted buildup. Every 5th shot pierces through one additional enemy. |

---

## 2. Cannon Tower

**Role:** Slow, high-damage area splash. The anti-swarm and cluster-clearing anchor.
**Weakness:** Slow fire rate and minimum range (0.5 units) means it cannot reliably target fast single units. Poor against flying units.
**Damage Type:** Physical (splash)

### Stats

| Level | Damage/shot | Attack Speed | Range | Splash Radius | DPS (single) | Buildup/hit | Cost    |
|-------|-------------|--------------|-------|---------------|--------------|-------------|---------|
| 1     | 65          | 0.5/sec      | 10    | 2.5           | 32           | 8           | 130 gems|
| 2     | 95          | 0.55/sec     | 10    | 3.0           | 52           | 8           | 100 gems|
| 3A    | 160         | 0.45/sec     | 12    | 4.0           | 72           | 8           | 120 gems|
| 3B    | 75          | 0.65/sec     | 10    | 2.5           | 49           | 8           | 120 gems|

### Upgrade Branches (Level 3)

**3A — Siege Cannon:**
- Greatly increased damage and range; larger splash radius; slightly slower
- Ideal for open-lane clustered waves

**3B — Cluster Bomb:**
- Fires a shell that splits into 3 cluster charges mid-air, each dealing splash damage in separate small areas
- Great for covering a wider area with irregular enemy spread

### Elemental Infusion Effects

| Element | Infusion 1 Effect                                                           |
|---------|-----------------------------------------------------------------------------|
| Fire    | Shots leave a small Lava Patch at impact (1.5 unit radius, 3 sec, 8 magic dmg/sec) |
| Water   | Shots release a water burst on impact, applying Soaked buildup (20 buildup) to all hit enemies |
| Earth   | Shots shatter the ground on impact; all hit enemies receive Shattered buildup (25 buildup) |
| Air     | Shots detonate in an air shockwave; all enemies in splash are knocked back 1.5 units |

---

## 3. Crossbow Tower

**Role:** Long-range armor-piercing physical damage. The specialist tower for picking off armored elites at the back of the lane.
**Weakness:** Low splash; inefficient against swarms. No status application without infusion.
**Damage Type:** Physical (armor piercing)

### Stats

| Level | Damage/shot | Attack Speed | Range | Armor Pierce | DPS  | Buildup/hit | Cost    |
|-------|-------------|--------------|-------|--------------|------|-------------|---------|
| 1     | 30          | 0.8/sec      | 18    | 20%          | 24   | 5           | 110 gems|
| 2     | 45          | 0.9/sec      | 20    | 30%          | 40   | 5           | 85 gems |
| 3A    | 40          | 1.2/sec      | 18    | 30%          | 48   | 5           | 110 gems|
| 3B    | 85          | 0.6/sec      | 22    | 50%          | 51   | 5           | 110 gems|

*Armor pierce is a flat % reduction to effective armor: a 30% pierce on a 50-armor target treats it as a 35-armor target.*

### Upgrade Branches (Level 3)

**3A — Bolt Storm:**
- Increased fire rate; each bolt pierces through 2 enemies in a line
- Ideal for lane control when enemies are bunched in a column

**3B — Siege Bolt:**
- Very high damage and armor penetration; reduced fire rate
- Each shot briefly staggers the target (0.3 sec interrupt)
- The go-to for armored minibosses and high-HP elite units

### Elemental Infusion Effects

| Element | Infusion 1 Effect                                                                |
|---------|----------------------------------------------------------------------------------|
| Fire    | Bolts apply Burning buildup. Burning targets take +20% damage from this tower.   |
| Water   | Bolts apply Soaked buildup. Soaked targets hit by this tower have armor reduced by an additional 5 flat. |
| Earth   | Bolts apply Shattered buildup at double rate (+100% buildup). Ideal for setting up Disintegrate combos. |
| Air     | Bolts apply Gusted buildup. Every 4th bolt fires a burst that hits all enemies in a 2-unit cone behind the target. |

---

## 4. Mage Spire

**Role:** Magic damage, high status application rate. The primary status-enabling and combo-setup tower. Low physical damage role; focused on debuffing and priming.
**Weakness:** Reduced effectiveness against high magic-resist targets; lower raw DPS than physical towers.
**Damage Type:** Magic

### Stats

| Level | Damage/shot | Attack Speed | Range | DPS  | Buildup/hit | Cost    |
|-------|-------------|--------------|-------|------|-------------|---------|
| 1     | 20          | 1.0/sec      | 13    | 20   | 25          | 120 gems|
| 2     | 30          | 1.1/sec      | 13    | 33   | 35          | 90 gems |
| 3A    | 25          | 1.4/sec      | 13    | 35   | 45          | 110 gems|
| 3B    | 55          | 0.8/sec      | 15    | 44   | 55          | 110 gems|

### Upgrade Branches (Level 3)

**3A — Conduit:**
- Slightly lower damage per hit; increased attack speed and buildup
- Every 6th shot chains to an adjacent enemy (2 chain targets)
- Best for dense lanes where status spread multiplies combo potential

**3B — Arcane Bastion:**
- High damage, lower attack speed; fires an AoE pulse (2 unit radius) instead of a single bolt
- Massive buildup application across clusters
- Best when you need AoE status coverage

### Elemental Infusion Effects

| Element | Infusion 1 Effect                                                                    |
|---------|--------------------------------------------------------------------------------------|
| Fire    | Shots apply Burning buildup. On status trigger, initial Burning tick deals 2× damage. |
| Water   | Shots apply Soaked buildup. Soaked enemies take +20% damage from all magic sources.   |
| Earth   | Shots apply Shattered buildup. Shattered enemies hit by this tower lose an additional 10 flat armor. |
| Air     | Shots apply Gusted buildup. Gusted enemies hit by this tower have a 20% chance to spread Gusted buildup (10 buildup) to the nearest enemy. |

---

## 5. Arc Ray

**Role:** Continuous beam attack. Sustained status buildup over time. Excels at keeping high-HP targets primed continuously. Requires good placement to maximize uptime.
**Weakness:** Targets one enemy at a time. Does not reacquire until current target leaves range or dies. Poor against fast swarms.
**Damage Type:** Magic (beam, ~8 ticks/sec)

### Stats

| Level | Damage/tick | Ticks/sec | Range | DPS  | Buildup/tick | Cost    |
|-------|-------------|-----------|-------|------|--------------|---------|
| 1     | 8           | 8         | 14    | 64   | 15           | 160 gems|
| 2     | 12          | 8         | 14    | 96   | 20           | 120 gems|
| 3A    | 20          | 8         | 16    | 160  | 30           | 140 gems|
| 3B    | 8           | 8         | 14    | 64   | 20           | 140 gems|

### Upgrade Branches (Level 3)

**3A — Focused Lens:**
- High single-target damage; increased range
- After 3 seconds of continuous fire on the same target, the beam deals bonus magic damage equal to 10% of the target's max HP per second (armor-ignoring portion)
- Best for melting bosses and minibosses

**3B — Sweep Ray:**
- Beam rotates in a 60-degree arc, hitting all enemies in the sweep path
- Lower damage per target but excellent for applying buildup across a cluster
- Best for high-density lanes

### Elemental Infusion Effects

| Element | Infusion 1 Effect                                                                       |
|---------|-----------------------------------------------------------------------------------------|
| Fire    | Beam applies Burning buildup continuously. After 2 sec of continuous fire, the target begins Burning regardless of threshold. |
| Water   | Beam applies Soaked buildup continuously. Beam also reduces target move speed by 20% while firing. |
| Earth   | Beam applies Shattered buildup continuously. After 3 sec on the same target, it applies Shattered instantly regardless of remaining threshold. |
| Air     | Beam applies Gusted buildup continuously. After 1.5 sec, the beam begins displacing the target slightly backward (0.5 units/sec). |

---

## 6. Seed Core (Special Tower)

**Role:** Aura support tower. Has no base functionality; only activates after receiving an elemental infusion. Powerful area buff with the right element. Intentionally weak without investment.
**Weakness:** Zero DPS and no buildup without infusion. Expensive for what it does early. Must be positioned centrally to benefit multiple towers.
**Damage Type:** None (aura)

### Stats (Base — Uninfused)

| Level | Effect (uninfused) | Aura Range | Cost    |
|-------|-------------------|------------|---------|
| 1     | None              | 8 units    | 70 gems |
| 2     | None              | 10 units   | 55 gems |
| 3     | None              | 12 units   | 70 gems |

*Upgrading base levels only expands the aura; effects come from infusion.*

### Elemental Infusion Effects

| Element | Infusion 1 Aura Effect                                                                          |
|---------|-------------------------------------------------------------------------------------------------|
| Fire    | All towers in aura deal +20% fire/magic damage and apply +25% Burning buildup per hit           |
| Water   | All towers in aura gain +15% attack speed; Soaked enemies inside the aura receive +20% buildup from all sources |
| Earth   | All towers in aura deal +15% physical damage and gain +10 flat armor penetration                |
| Air     | All towers in aura gain +1 projectile (extra shot per attack); Gusted enemies inside aura take +15% magic damage |

*Advanced infusion (second orb) effects are post-MVP and will be defined in an expansion document.*

---

## MVP Prototype Tower Set
For the first playable, use only:
1. Arrow Tower (levels 1–2 only)
2. Mage Spire (levels 1–2 only)
3. Fire and Water infusions only
4. No Seed Core yet (introduce in vertical slice)

