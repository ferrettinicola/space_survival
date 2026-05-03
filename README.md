# 🚀 SPACE RACE

> **Survive the cosmos.** An HTML5 arcade space shooter — no install, no dependencies.

---

## How to Play

Open `space_survival.html` in any modern browser. That's it.

### Controls

| Input | Action |
|---|---|
| `↑ ↓ ← →` / `W A S D` | Move the ship |
| `SPACE` | Boost — burst of speed |
| `Click` / `F` | Fire |

---

## The World

A toroidal star field **20,000 × 20,000 pixels** — fly off one edge and you re-enter from the opposite side. The world is filled with planets, galaxies, pulsars, supernovas, constellations (based on real RA/Dec coordinates), asteroid belts and black holes — all procedurally distributed with uniform spacing every game.

### Health
You start with **20 HP**. Large meteors kill instantly (−20 HP), small fragments deal −5 HP, alien lasers deal −5 HP. Collect the green drop from Scout aliens to recover +10 HP.

---

## The 4 Ships

Each ship has unique stats and a **special ability**, unlocked by collecting the colored star dropped by Dreadnoughts.

| Ship | Style | Special Ability |
|---|---|---|
| 🔵 **VIPER** | Balanced, standard fire | Twin Shot — dual bullets at ±0.18 rad |
| 🟠 **SCORPION** | Fast, heavy slow projectiles | Heavy Burst |
| 🟣 **PHANTOM** | Slow, rapid piercing fire | Invisibility 8s — meteors pass through |
| 🟡 **TITAN** | Powerful, splitting beam | Supernova — 400px shockwave every 2.5s |

---

## Meteors

- **🪨 Normal** — baseline obstacle, +3 pts
- **🔴 Red** — 2.5× faster, +5 pts
- **💎 Crystal** — shatters into 3 fast fragments on hit, +7 pts each

---

## Aliens

Four types with distinct behaviors, each dropping a different power-up:

| Alien | Drop | Effect |
|---|---|---|
| 👾 **Scout** (green) | ❤️ Health | +10 HP |
| 💢 **Chaotic** (red) | ⚡ Rapid Fire | 5× fire rate + speed +60% for 30s |
| 🟣 **Bomber** (purple) | 🛡 Shield | Full invincibility for 30s |
| 🟡 **Dreadnought** (gold, 5 HP) | ⭐ Star Power + 🔥 Ship Ability | Rarest and most powerful |

### ⭐ Star Power (45 seconds)
The golden star makes you nearly unstoppable: speed +120%, full invincibility, auto-shield 220px that destroys nearby meteors, homing missiles that lock onto 2 targets simultaneously.

### 🔥 Ship Ability (12 seconds)
A second smaller star drops with Star Power, activating your ship's unique special ability.

---

## 🌀 The Void (Second World)

Fly into a **black hole** to be pulled into an alternate dimension:

- **Spectacular vortex** entry animation
- Time runs **1.875×** faster — everything is more intense
- **4 types of dark meteors**: obsidian, plasma, ghost, shard
- **6 enemy turrets** that auto-aim and fire (−2 HP; +5 HP if destroyed)
- Boost and ammo are **unlimited**
- **Survive 45 seconds** → cinematic exit animation → return to the main world
- Countdown shown **bottom-left** of the screen

---

## Scoring

| Event | Points |
|---|---|
| Each second survived | +1 |
| Normal meteor | +3 |
| Red meteor | +5 |
| Crystal meteor (+ each fragment) | +7 |
| Void meteor | +10 |
| Void turret destroyed | +15 |
| Alien (Scout / Chaotic / Bomber) | +20 |
| Dreadnought | +50 |

---

## Leaderboard

Local leaderboard, top 20 scores. Each name appears **at most once** — only the highest score is kept. Works fully offline.

---

## World Objects

Procedurally generated each game with even grid-based distribution:

- **Planets** with rings and orbiting moons
- **Colored galaxies**
- **Nebulae** and cosmic dust clouds
- **Pulsars** and **Supernovas** — pull nearby meteors into orbit
- **Decorative asteroid belts**
- **6 Constellations** from real astronomical data: Ursa Major, Orion, Cassiopeia, Leo, Scorpius, Cygnus
- **14 Black holes** with animated accretion disk, relativistic jets and gravitational lensing

---

## Languages

🌐 English / Italian — toggle in the top-right corner on menu screens.

---

## Files

```
space_survival.html      ← complete game, single file
SPACE_RACE_context.md    ← detailed developer context document
README.md                ← this file
```

---

*Built with HTML5 Canvas, CSS3 and vanilla JavaScript. Zero external dependencies.*
