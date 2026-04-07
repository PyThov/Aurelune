# Elements TD — Roadmap Visualization

Below are two visualizations of the roadmap: a phase flow diagram and a milestone timeline.

## 1) Roadmap Phase Flow

```mermaid
flowchart TD
    A[Phase 1<br/>Pre-Production] --> B[Phase 2<br/>Core Prototype]
    B --> C[Phase 3<br/>Vertical Slice]
    C --> D[Phase 4<br/>Full Production]
    D --> E[Phase 5<br/>Polish & Beta]
    E --> F[Phase 6<br/>Launch & Post-Launch]

    A1[Lock MVP scope] --> A
    A2[Choose engine / architecture] --> A
    A3[Define performance target] --> A
    A4[Finalize core systems] --> A

    B1[1 combat map] --> B
    B2[Wave spawning] --> B
    B3[2 towers] --> B
    B4[2 elements] --> B
    B5[First combo reactions] --> B

    C1[1 region] --> C
    C2[4 to 6 missions] --> C
    C3[Hub camp] --> C
    C4[4 towers / 6 enemies] --> C
    C5[Boss + progression loop] --> C

    D1[5 total regions] --> D
    D2[20 to 30 missions] --> D
    D3[Expanded towers / enemies] --> D
    D4[Research tree] --> D
    D5[Story + region mechanics] --> D

    E1[Optimization] --> E
    E2[Balance tuning] --> E
    E3[UI polish] --> E
    E4[Bug fixing] --> E
    E5[Playtesting] --> E

    F1[Release build] --> F
    F2[Endless mode] --> F
    F3[Roguelite mode] --> F
    F4[Co-op later] --> F
    F5[Mod support later] --> F
```

## 2) Milestone Timeline

```mermaid
gantt
    title Elements TD Development Roadmap
    dateFormat  YYYY-MM-DD
    axisFormat  %b %Y

    section Phase 1 - Pre-Production
    MVP scope / systems lock          :a1, 2026-03-16, 21d
    Tech setup / architecture         :a2, after a1, 7d

    section Phase 2 - Core Prototype
    First playable combat loop        :b1, after a2, 45d
    Towers / elements / first combos  :b2, after a2, 45d

    section Phase 3 - Vertical Slice
    1 region + hub + progression      :c1, after b1, 75d
    Boss / VFX / mission polish       :c2, after b1, 75d

    section Phase 4 - Full Production
    Remaining regions / content       :d1, after c1, 240d
    Narrative / progression expansion :d2, after c1, 240d

    section Phase 5 - Polish & Beta
    Optimization / balance / testing  :e1, after d1, 90d

    section Phase 6 - Launch & Post-Launch
    Launch prep                       :f1, after e1, 21d
    Post-launch features              :f2, after f1, 120d
```

## 3) Simplified Dependency View

```mermaid
flowchart LR
    S1[Core Combat Feel] --> S2[Elemental Combo Readability]
    S1 --> S3[Tower Placement & Economy]
    S2 --> S4[Vertical Slice]
    S3 --> S4
    S4 --> S5[Full Campaign Production]
    S5 --> S6[Polish / Optimization]
    S6 --> S7[Launch]
    S7 --> S8[Post-Launch Features]
```

## Notes
- The most important milestone is the **Core Prototype**. If the game is not fun there, later content will not save it.
- The **Vertical Slice** should prove the game can carry a full campaign.
- **Post-launch features** like co-op, modular towers, and mod support should stay out of MVP unless development moves unusually fast.
