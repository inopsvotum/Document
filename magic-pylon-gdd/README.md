# Pylon Guard — Game Design Document

## Overview

**Genre:** Top-down action roguelite (mobile)
**Platform:** iOS / Android
**Session Length:** 8–15 min
**Core Fantasy:** You are the last guardian — channel devastating abilities to hold back the horde and keep your pylon alive.

---

## Core Loop

1. **Pick a hero & loadout** (4 ability slots).
2. **Defend the pylon** across escalating waves.
3. **Earn crystals & XP** → unlock maps, enemies, abilities, buffs, map upgrades.
4. **Repeat** with harder modifiers for higher scores.

---

## Controls

| Input | Action |
|---|---|
| Left virtual joystick | Move hero |
| Ability buttons (×4) | Tap to quick-cast; hold + drag to aim |
| Aim mode | **Time slows to 30 %** while dragging an ability — release to fire |

> **No basic attack.** All damage comes from abilities. Resource management *is* the combat.

---

## Heroes

| Hero | HP | Speed | Passive | Signature Ability |
|---|---|---|---|---|
| **Ember** | 100 | Medium | Burns nearby enemies (2 dps) | *Meteor* — AoE slam, 8 s CD |
| **Frost** | 120 | Slow | Slows enemies in aura by 20 % | *Blizzard* — zone slow + damage, 10 s CD |
| **Volt** | 80 | Fast | Dodge-roll grants shield (15 HP) | *Chain Lightning* — bounces ×5, 6 s CD |
| **Terra** | 140 | Slow | +10 % pylon armor | *Stone Wall* — blocks path 5 s, 12 s CD |

Each hero equips **4 abilities** from a shared pool (30+ unlockable). Abilities have cooldowns; no mana.

---

## Enemies

| Type | Examples | Behaviour |
|---|---|---|
| **Swarm** | Slimes, Bats, Beetles | Beeline to pylon; low HP, high count |
| **Elite** | Shielded Brute, Phase Stalker | Targets hero; special mechanics (shield, teleport) |
| **Boss** | Bone Colossus, Storm Wyrm | Spawns every 5 waves; multi-phase, telegraphed attacks |
| **Siege** | Catapult Golem | Ignores hero; lobs ranged AoE at pylon |

---

## Wave System

Waves escalate every ~25 s. Enemy power scales with:

### Formula 1 — Wave Difficulty

```
W_diff = BASE_DIFF × (1 + 0.12 × wave)^1.3
```

`W_diff` drives enemy count, HP multiplier, and elite spawn chance. Boss waves (5, 10, 15 …) add a flat +50 % budget.

---

## Damage

### Formula 2 — Ability Damage

```
DMG = base_dmg × (1 + buff_pct / 100) × streak_mult
```

- `base_dmg` — ability's listed damage.
- `buff_pct` — sum of all active damage buffs.
- `streak_mult` — `1 + 0.02 × min(hit_streak, 50)` (max ×2.0). Streak resets on 3 s without a hit.

---

## Scoring

### Formula 3 — Run Score

```
Score = (kills × streak_best × 10) + (clear_wave × 500) + (pylon_hp_pct × 2000) - (time_s × 2)
```

Leaderboards rank by Score. Star thresholds (★–★★★) gate progression unlocks.

---

## Progression (Meta)

| Layer | Unlock Method |
|---|---|
| **Maps** (5 biomes) | Star milestones |
| **Enemies** | Appear as maps unlock |
| **Abilities** (30+) | Crystals earned per run |
| **Buffs** (passive tree) | XP levels — e.g. +5 % AoE radius, −1 s CD |
| **Map Upgrades** | Crystals — pylon turrets, traps, heal zones |

Buffs and upgrades are **persistent** across runs (roguelite, not roguelike).

---

## Session Flow

```
Menu → Hero Select → Loadout → Wave 1…N → Defeat / Victory → Score Screen → Rewards → Menu
```

- **Victory** = survive the final boss wave of the chosen map.
- **Defeat** = pylon destroyed. Partial rewards granted.

---

## Monetization (F2P)

- **Battle Pass** (cosmetics + crystal boosters).
- **Cosmetic skins** per hero.
- **No pay-to-win** — all abilities and buffs earnable through play.

---

## Art & Audio

- Stylised 2D pixel art, vibrant palette.
- Dynamic soundtrack intensifies with wave count.
- Haptic feedback on ability hits.

---

*Target scope: 4 heroes, 5 maps, 30 abilities, 12 enemy types at launch.*
