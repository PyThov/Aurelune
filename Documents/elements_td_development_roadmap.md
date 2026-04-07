# Elements TD --- Development Roadmap

## Overview

This roadmap converts the design documents into a structured development
plan. The goal is to move from concept → prototype → vertical slice →
full production while controlling scope and validating the core gameplay
systems early.

The most important systems to prove early are: - Elemental combo
combat - Tower defense strategy - Player support combat role -
Wave-based progression

------------------------------------------------------------------------

# Phase 1 --- Pre‑Production

Estimated time: 2--4 weeks

## Goals

-   Lock MVP scope
-   Finalize core systems
-   Choose engine and technical architecture
-   Define art direction and performance targets

## Tasks

-   Choose engine (Unity recommended)
-   Setup project repository
-   Create basic project architecture
-   Implement data‑driven system structure for:
    -   towers
    -   enemies
    -   status effects
    -   combo interactions
    -   wave definitions
-   Define performance target:
    -   1080p 60 FPS on mid‑range PC

## Design Tasks

-   Finalize tower roster for MVP
-   Finalize enemy archetypes
-   Finalize elemental combo rules
-   Define mission length (\~30 minutes)

## Deliverables

-   Finalized MVP feature list
-   Combat system specification
-   Basic architecture setup

------------------------------------------------------------------------

# Phase 2 --- Core Prototype

Estimated time: 4--8 weeks

## Goals

Build the **first playable combat loop**.

## Systems to Implement

-   Basic combat map
-   Enemy pathing
-   Wave spawning system
-   Player character movement and attacks
-   Basic tower placement system
-   Tower upgrading
-   Gem economy

## Prototype Content

-   1 map
-   10 waves
-   3 enemy types
-   2 towers
-   2 elements (Fire + Water)

## Combo System

Implement first two combos:

Fire + Fire → Explosion\
Fire + Water → Steam Burst

## Success Criteria

-   Towers feel satisfying
-   Element combos are readable
-   Player combat assists but does not dominate
-   Performance stable

------------------------------------------------------------------------

# Phase 3 --- Vertical Slice

Estimated time: 8--12 weeks

## Goals

Create a polished slice representing the final game.

## Content

-   1 region
-   4--6 missions
-   1 hub camp
-   4 tower types
-   4 elemental infusions
-   6 enemy types
-   2 minibosses
-   1 boss

## Systems

-   Upgrade tree
-   Mission rewards
-   Element orb drops
-   Combo matrix expanded

## Art

-   First stylized environment kit
-   Tower models
-   Enemy models
-   Elemental VFX

## Success Criteria

-   Complete region playable
-   Core progression loop proven
-   Combos visually clear
-   Performance meets targets

------------------------------------------------------------------------

# Phase 4 --- Production

Estimated time: 6--12 months

## Goals

Build the full campaign.

## Regions

-   Fire Kingdom
-   Water Kingdom
-   Earth Kingdom
-   Air Kingdom
-   Capital Region

## Content Targets

-   5 regions
-   20--30 total missions
-   8--10 tower types
-   12--15 enemy types
-   multiple bosses

## Systems

-   Research tree
-   Passive upgrades
-   Expanded combos
-   Region mechanics

## Story

-   Narrative progression
-   Camp dialogue
-   Region lore

------------------------------------------------------------------------

# Phase 5 --- Polish & Beta

Estimated time: 2--4 months

## Goals

Improve quality and stability.

## Tasks

-   Performance optimization
-   UI polish
-   Audio implementation
-   Bug fixing
-   Balance tuning
-   Accessibility settings

## Testing

-   Closed playtests
-   Balance iteration
-   Performance testing

------------------------------------------------------------------------

# Phase 6 --- Launch & Post‑Launch

## Launch Goals

-   Stable performance
-   Full campaign playable
-   Balanced tower roster

## Post Launch Content

-   Endless mode
-   Rogue-lite mode
-   Additional heroes
-   Modular tower system
-   Co-op support
-   Mod support

------------------------------------------------------------------------

# Estimated Total Timeline

Solo Developer Estimate

Pre‑Production: 1 month\
Prototype: 2 months\
Vertical Slice: 3 months\
Production: 6--12 months\
Polish: 2--4 months

Total Estimated Development: \~12--20 months

------------------------------------------------------------------------

# Key Risk Areas

## Scope Creep

The game contains many systems: - action combat - tower defense -
combos - campaign progression

Stick to MVP before expanding.

## Performance

Tower defense + VFX heavy combos can cause performance spikes.

Maintain: - particle limits - enemy count limits - efficient pathfinding

## Balance

Element combos must remain readable and predictable.

------------------------------------------------------------------------

# Recommended Next Documents

To accelerate development create:

-   combat_system_spec.md
-   tower_roster.md
-   enemy_roster.md
-   campaign_outline.md
-   UI_wireframes.md
