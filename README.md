# 🧬 Cellular Automaton Simulators

> **Two standalone HTML simulators exploring emergent complexity from simple rules.**
> Save as `.html` → double-click → runs instantly in any browser. No installation. No internet. No dependencies.

---

## 📁 Files

| File | Size | Description |
|------|------|-------------|
| `conways_game_of_life.html` | ~70 KB | Conway's Game of Life — full-featured simulator |
| `langtons_ant.html` | ~90 KB | Langton's Ant — multi-ant, multi-rule simulator |
| `langtons_ant_simple.html` | ~34 KB | Langton's Ant — lightweight send-anywhere version |

**Why a single `.html` file?**

- ✅ No installation, no Node.js, no Python, no server
- ✅ Works offline on any device (phone, tablet, laptop, air-gapped machine)
- ✅ Share by email or USB stick — the whole app is one file
- ✅ Open-source and self-contained — inspect everything in one place
- ✅ Runs identically in Chrome, Firefox, Safari, Edge

---

## 🌱 Conway's Game of Life

### What is it?

Conway's Game of Life is a **zero-player cellular automaton** invented by mathematician John Horton Conway in 1970. An infinite grid of cells, each either alive or dead, evolves generation by generation according to four simple rules:

```
┌─────────────────────────────────────────────────────┐
│              THE FOUR RULES                         │
│                                                     │
│  Count the 8 surrounding neighbours of each cell:  │
│                                                     │
│   □ □ □                                             │
│   □ ■ □   ← the cell being checked                 │
│   □ □ □                                             │
│                                                     │
│  1. Lonely   : alive + 0–1 neighbours → dies        │
│  2. Survival : alive + 2–3 neighbours → lives       │
│  3. Crowded  : alive + 4+ neighbours  → dies        │
│  4. Born     : dead  + 3 neighbours   → comes alive │
└─────────────────────────────────────────────────────┘
```

From these four rules — applied simultaneously to every cell — astonishing complexity emerges: spaceships, factories, computers, and self-replicating machines.

---

### 🖥️ Interface Layout

```
┌──────────────────┬──────────────────────────────────────────┐
│   CONTROL PANEL  │                                          │
│  ┌────────────┐  │                                          │
│  │  Playback  │  │                                          │
│  │  Speed     │  │         C A N V A S                      │
│  │  Stats     │  │                                          │
│  │  View      │  │    (infinite scrollable white grid)      │
│  │  Draw      │  │                                          │
│  │  Rules     │  │                                          │
│  │  Patterns  │  │                                          │
│  │  Advanced  │  │                                          │
│  │  Export    │  │                                          │
│  └────────────┘  │                                          │
├──────────────────┴──────────────────────────────────────────┤
│  TIMELINE ◄──────────────●──────────────────────► GEN 4821 │
└─────────────────────────────────────────────────────────────┘
```

---

### ⚙️ Features

#### Playback Controls
| Button | Action |
|--------|--------|
| ▶ / ⏸ | Play / Pause |
| ⏭ Step | Advance exactly one generation |
| 🗑 Clear | Wipe the grid and reset rule to Conway |
| ↩ Undo | Restore previous grid state |

#### Speed Control
Nine speed levels from ultra-slow to ultra-fast:

```
0.01×  →  ~0.6 gen/sec   (slow motion — watch each cell change)
0.1×   →  ~6   gen/sec   (slow, good for oscillators)
0.5×   →  ~30  gen/sec   (half speed)
1×     →  ~60  gen/sec   (default — comfortable to watch)
10×    →  600  gen/sec   (fast — good for methuselahs)
100×   →  6K   gen/sec   (very fast — breeders, guns)
1K×    →  60K  gen/sec   (skip ahead quickly)
10K×   →  600K gen/sec   (maximum — instant evolution)
```

> The fractional speeds (0.01×, 0.1×, 0.5×) use a **frame accumulator** — no sleep/delay, so the UI never freezes.

#### View Controls
- **🔍 Auto-Follow** — camera smoothly tracks the centroid of all live cells. Essential for watching gliders and breeders travel.
- **📍 Go to Cells** — instantly jump the camera to wherever life currently is
- **⊕ Origin** — return to coordinate (0, 0)
- **⊞ Fit** — zoom out to show all live cells at once
- **Scroll wheel** — zoom in/out centered on mouse cursor
- **Drag** — pan the infinite grid (works during playback too)
- **Pinch** — zoom on touch devices

#### ✏️ Drawing Tools
| Tool | Shortcut | Description |
|------|----------|-------------|
| ✏️ Draw | `D` | Click or drag to paint live cells |
| 🧹 Erase | `E` | Click or drag to kill cells |
| ✋ Pan | `P` | Drag to scroll without drawing |
| Right-click | — | Always erases, regardless of tool |

- **Brush size 1–20** — circular brush for painting large areas quickly
- **Add Random Cells** — sprinkle noise at adjustable density into the current view
- **Invert** — flip all cells in view (alive ↔ dead)

#### ⚙️ Rule Editor (B/S Notation)

Every rule in Life-like cellular automata is written as **B**orn/**S**urvive:

```
Conway's Life = B3/S23

B3   = a dead cell with exactly 3 live neighbours is Born
S23  = a live cell with 2 or 3 live neighbours Survives

Toggle the numbered buttons (0–8) to define your own rules:

  BORN if neighbours =  [ 0 ][ 1 ][ 2 ][■3][ 4 ][ 5 ][ 6 ][ 7 ][ 8 ]
SURVIVE if neighbours =  [ 0 ][ 1 ][■2][■3][ 4 ][ 5 ][ 6 ][ 7 ][ 8 ]
                                    ↑
                               pink = selected
```

**Built-in named rules:**

| Rule | Name | What it does |
|------|------|--------------|
| B3/S23 | Conway's Life | The classic |
| B36/S23 | HighLife | Like Conway + self-replicators |
| B3/S12345 | Maze | Grows dense mazes, cells rarely die |
| B3678/S34678 | Day & Night | Symmetric — alive/dead regions mirror each other |
| B368/S245 | Morley (Move) | Gliders in all 8 directions |
| B2/S | Seeds | Nothing survives, births explode |
| B1357/S1357 | Replicator | Every pattern self-replicates |
| B34/S34 | 34 Life | Large growing blobs |

- **↺ Reset to Conway** — one click restores B3/S23
- **↩ Undo Rule** — reverses the last rule change

#### 📚 Pattern Library (24 Patterns)

Patterns are grouped by category and **automatically set the correct rule** when loaded:

```
Still Lifes     → Block, Beehive, Loaf, Boat
Oscillators     → Blinker (p2), Toad (p2), Beacon (p2),
                  Pulsar (p3), Pentadecathlon (p15)
Spaceships      → Glider, LWSS, MWSS, HWSS
Guns            → Gosper Glider Gun, Simkin Glider Gun
Methuselahs     → R-pentomino (1103 gen), Diehard (130 gen),
                  Acorn (5206 gen)
Other Rules     → HighLife Replicator, Maze Growth,
                  Seeds Explosion, Day & Night
Random Fill     → 20% / 40% / 60% density
```

> Patterns for other rules (HighLife, Seeds, etc.) show an **orange badge** with the rule name so you know before clicking.

#### 🏗️ Advanced Patterns (19 Historical Structures)

A dedicated section for large, complex engineered patterns with expandable historical notes:

```
Guns & Factories
  🔫 Gosper Glider Gun     — Period 30, the original gun (1970)
  🔫 Simkin Glider Gun     — Period 120, more compact
  🚌 P60 Glider Shuttle    — Queen-bee shuttle oscillator
  🔫 Bi-Gun (Period 8)     — Two guns annihilating each other
  ✈️ Glider Airport        — Puffer that manufactures guns
  🌱 Breeder 1 (MSM)       — First quadratic growth (T²) pattern
  
Infinite Growth
  ⚙️ Switch Engine         — 6 cells → infinite chaotic trail
  🧱 Block-Laying Engine   — Diagonal trail of 2×2 blocks
  ♾️ 10-Cell Infinite      — Minimum known infinite growth
  🔥 Wickstretcher         — Diagonal burning line
  📡 Sawtooth 177          — Oscillating population
  🏴󠁧󠁢󠁳󠁣󠁴󠁥󠁿 Caber Tosser        — Variable-period gun

Logic / Computing
  🍽️ Eater + Glider        — Signal absorption gate
  ➤  Glider Duplicator    — Fanout (1 stream → 2 streams)
  ⏱️ Period-60 Oscillator  — Clock signal from shuttles
  🔀 AND Gate Concept      — Boolean logic demonstration
  🤖 Universal Constructor — Multi-gun construction demo

Methuselahs
  🥧 Pi Calculator Seed    — 7 cells, runs 173 gen
  📈 Max                   — 9 cells, runs 51,616 generations!
```

Each card has:
- **▶ Load & Reset** — loads pattern + applies its rule + sets recommended speed
- **🎯 Auto Setup** — same + enables Auto-Follow so the camera tracks it
- **📖 History & details** — the real historical story, expandable

#### ⏱️ Timeline Scrubber

```
GEN  4821  ◄────────────────●────────────────────►  / 9500   History: 243
           drag to replay any of the last 500 generations
```

Stores up to 500 generations in memory. Drag the handle to jump back to any saved state — useful for finding the exact moment a pattern transitions.

#### 📤 Export
- **📸 PNG** — screenshot of the current canvas
- **💾 RLE** — export in standard Life format (importable by any Life app)
- **📂 Import RLE** — load any `.rle` file from the web or Life archives

---

### ⌨️ Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `Space` | Play / Pause |
| `.` (period) | Step one generation |
| `D` | Switch to Draw tool |
| `E` | Switch to Erase tool |
| `P` | Switch to Pan tool |
| `C` | Jump camera to cells |
| `F` | Toggle Auto-Follow |
| `G` | Toggle grid lines |

---

## 🐜 Langton's Ant

### What is it?

Langton's Ant is a **two-dimensional Turing machine** invented by Chris Langton in 1986. An ant sits on an infinite grid and follows two rules:

```
┌──────────────────────────────────────────────────┐
│           CLASSIC RULES (LR)                     │
│                                                  │
│  On a WHITE cell:                                │
│    1. Turn LEFT 90°                              │
│    2. Flip cell to BLACK                         │
│    3. Move forward one step                      │
│                                                  │
│  On a BLACK cell:                                │
│    1. Turn RIGHT 90°                             │
│    2. Flip cell to WHITE                         │
│    3. Move forward one step                      │
│                                                  │
│  After ~10,000 steps the ant always builds       │
│  an infinite "highway" — no matter the start.   │
└──────────────────────────────────────────────────┘
```

Extended rules use any combination of four turn types across any number of cell states:

```
L = Turn Left  90°      R = Turn Right 90°
U = U-turn    180°      S = Straight (no turn)

Examples:
  LR       → Classic (2 states: white/black)
  LLRR     → Symmetric diamond growth
  LRRRLLRR → 8-state highway (famous pattern)
  LRSL     → Graceful spiral drift
```

---

### 🖥️ Interface Layout

```
┌─────────────────┬──────────────────────────────────────────┐
│  CONTROL PANEL  │                                          │
│  ┌───────────┐  │                                          │
│  │ Playback  │  │                                          │
│  │ Speed     │  │         C A N V A S                      │
│  │ View      │  │                                          │
│  │ Rule      │  │   (white background, black trail)        │
│  │ Builder   │  │                                          │
│  │ Pattern   │  │                                          │
│  │ Library   │  │                                          │
│  │ Gun       │  │                                          │
│  │ Setups    │  │                                          │
│  └───────────┘  │                                          │
├─────────────────┴──────────────────────────────────────────┤
│  STEP  12,847  ◄─────────●──────────────────►  / 50,000   │
└────────────────────────────────────────────────────────────┘
```

---

### ⚙️ Features

#### Speed Control (9 levels)
```
0.01×  →  ~0.6  steps/sec  (watch every single move)
0.1×   →  ~6    steps/sec
0.5×   →  ~30   steps/sec
1×     →  ~60   steps/sec  (default)
10×    →  600   steps/sec
100×   →  6K    steps/sec
1K×    →  60K   steps/sec
10K×   →  600K  steps/sec
100K×  →  6M    steps/sec  (maximum)
```

#### 🔧 Visual Rule Builder

Click buttons to cycle each state's turn direction:

```
State:   S0    S1    S2    S3
Turn:   [↰L]  [↱R]  [↱R]  [↰L]  → Rule: LRRL

  + State   − State   🎲 Random
  
  Rule: LRRL
  [▶ Apply & Reset]   [Apply (keep step)]
```

- Up to **16 states** per rule
- **🎲 Random** generates a random 2–8 state rule to explore
- **Apply (keep step)** changes the rule without losing your current progress

#### 📚 Pattern Library (32 Rules)

Categorised by the kind of pattern produced:

```
Highway     → LR, LLRL, RRLL, RLLR, RRRL (fast), LRRRLLRR, LRRL
Symmetric   → LLRR (diamond), RLLRRLLR, RRLL, LLRRLL
Spiral      → LRRRRLLLRRR (Archimedes), RLLLLRRRLLLR, LRSL
Square/Box  → LRRRRRLLR, RRLRR, RLLLR, RLLRRLLR
Triangle    → RRLLLRLLLRRR, LLRLRRLLL, RLRRLLLLL
Chaotic     → RLR, RLL, RRLLLRRL, RLRL
Exotic      → LRUL (U-turn drift), LRRUULL, LRSSRL, UULL
```

Each entry shows: recommended step count, visual category dot, one-line description.

#### 🔫 Ant Gun & Multi-Ant Setups (12 Configurations)

Pre-configured multi-ant arrangements loaded with one click:

```
💥 Highway Collider    — 2 LR ants head-on (25K steps)
🪞 Mirror Pair         — 2 LLRR ants mirrored (bilateral crystal)
✳️ Four Corners        — 4 ants facing inward (4-fold interference)
🌀 Rotational Quad     — 4 LRRRLLRR ants at 90° (pinwheel)
🛤️ Highway Crossroads  — 2 fast RRRL ants at right angles
🌸 Spiral Ballet       — 3 Archimedean spiral ants at 120°
📦 Bouncing Box Gun    — 4 LRRRRRLLR ants at corners
⚡ Chaos Engine        — 6 ants with mixed rules (max entropy)
☯️ Twin Spirals        — 2 spiral ants facing opposite (yin-yang)
△  Triangle Factory    — 3 triangle ants in a triangle
⭐ Symmetric Star      — 8 LLRR ants in octagon (mandala)
🌌 Galaxy              — 6 ants in hexagon (galaxy arms)
```

Each setup: clears existing ants, loads the configuration, sets recommended speed, centers view.

#### ⏱️ Timeline & Checkpoint System

```
STEP  12,847  ◄──●──────────────────────────►  / 50,000   CPs: 12
               ↑                              ↑
           drag to any                  green marks =
           history point               saved checkpoints
```

- Checkpoint saved every **1,000 steps** automatically
- Drag timeline → nearest checkpoint restored → steps replayed to target
- Supports 1,000,000+ steps without memory issues

#### 📊 Statistics Panel
Real-time display:
- Global step count
- Simulation speed
- Number of ants
- Colored cell count
- Current zoom level
- Simulation runtime
- Checkpoint count
- Memory usage estimate
- Per-ant: name, position (x, y), direction, step count, rule

#### 📤 Export
- **PNG 1×** — current view at screen resolution
- **PNG 4K** — 2× resolution (suitable for printing)
- **PNG 8K** — 4× resolution (high-detail export)
- **Export JSON** — full state (grid + ants + step count) saved to file
- **Import JSON** — restore any previously saved session
- **⏺ Record** — capture canvas as WebM video (30 or 60 fps)

---

## 🧠 The Big Idea: Emergent Complexity

Both simulators illustrate the same profound principle:

```
  Simple rules  +  Repetition  =  Unexpected complexity
```

| | Conway's Life | Langton's Ant |
|--|---|---|
| **Rule** | 4 rules on a grid | 2–16 turn rules |
| **States** | 2 (alive/dead) | 2–16 cell colours |
| **Agents** | None (synchronous) | 1 or more ants |
| **Behaviour** | Spaceships, guns, computers | Highways, spirals, chaos |
| **Computing power** | Turing complete | Turing complete |
| **Infinite growth** | Breeders, switch engines | Multi-state rules |

<details>
<summary><b>Why does this matter?</b></summary>

These simulations are not toys — they are windows into fundamental questions in mathematics and computer science:

- **Conway proved** Life is Turing complete: any computation a modern computer can perform, Life can perform too — using gliders as bits, guns as clock signals, and eaters as logic gates.

- **Langton's Ant** demonstrates that deterministic, local rules can produce globally unpredictable behaviour — a hallmark of **computational irreducibility** (you cannot predict step 1,000,000 without running all 1,000,000 steps).

- **The highway theorem** (Langton's Ant): it was proved that *every* 2-state ant rule eventually produces an infinite highway, but the proof gives no bound on *when* — some ants take billions of steps. This remains an active research area for multi-state rules.

- Both systems demonstrate **emergence**: the whole is more complex than the sum of its parts. Four rules → universal computation. Two turn rules → infinite ordered structure.

</details>

---

## 🚀 Quick Start

### Conway's Game of Life

1. Open `conways_game_of_life.html` in Chrome/Firefox
2. Press **▶** — the Gosper Glider Gun fires gliders immediately
3. Enable **🔍 Auto-Follow** to keep gliders on screen
4. Explore the Pattern Library → try **Acorn** at 100× speed
5. Try the Advanced Patterns → **Breeder 1** shows quadratic population growth

### Langton's Ant

1. Open `langtons_ant.html` in Chrome/Firefox
2. Press **▶** — the classic LR ant starts building
3. Wait ~10,000 steps — the highway appears (try 1K× speed)
4. Try the Ant Gun Setups → **Galaxy** for a visual spectacle
5. Use the Rule Builder to invent your own rule

### Langton's Ant (Simple version)

1. Open `langtons_ant_simple.html` — works on phones too
2. Pinch to zoom, drag to pan
3. Tap **☰** to open the panel on mobile

---

## 🔬 Suggested Experiments

### Conway's Life
```
1. Load Gosper Gun → watch at 1× → see glider stream
2. Load Gosper Gun → draw an Eater near the stream → stream stops
3. Load R-pentomino → run at 1K× for 1103 gen → count survivors
4. Switch to HighLife rule → load Random 40% → find replicators
5. Set rule to Seeds (B2/S) → draw a cross → watch it explode
6. Load Breeder 1 → run at 100× → watch population grow as T²
```

### Langton's Ant
```
1. LR rule → run 10K steps → spot the highway
2. LLRR rule → run 10K steps → symmetric diamond
3. LRRRLLRR rule → run 50K steps → 8-state highway
4. Add 3 ants with different rules → watch them interact
5. Load Rotational Quad → run 80K steps at 1K× → pinwheel
6. Try LRSL → run 8K steps → graceful spiral
```

---

## 📋 System Requirements

| | Minimum | Recommended |
|--|---------|-------------|
| Browser | Chrome 90+, Firefox 88+, Safari 14+ | Chrome latest |
| RAM | 512 MB | 2 GB (for large patterns) |
| Screen | Any | 1440p+ for detail |
| Internet | Not required | Not required |

> The simulators use **sparse storage** (JavaScript `Map`/`Set`) — only live/visited cells consume memory. A grid with 1 million live cells uses ~80 MB, not the gigabytes a naive array approach would require.

---

## 🏛️ Credits & History

- **Conway's Game of Life** — John Horton Conway (1970), popularised by Martin Gardner in *Scientific American*
- **Gosper Glider Gun** — Bill Gosper (1970), won Conway's $50 prize for proving infinite growth possible
- **Breeder 1** — Bill Gosper (1971), first quadratic-growth pattern
- **Langton's Ant** — Christopher Langton (1986), *Studying Artificial Life with Cellular Automata*
- **Switch Engine** — Charles Corderman (1971)
- **Acorn** — David Bell
- **Simkin Glider Gun** — Michael Simkin (2015)
- **Pattern data** sourced from [LifeWiki](https://conwaylife.com/wiki/) and [Paul's Page of Conway Life Miscellany](https://www.radicaleye.com/lifepage/)

---

*These simulators were built as interactive explorations of emergent complexity — the idea that the most sophisticated structures in nature, computation, and perhaps life itself arise not from complex blueprints, but from simple rules applied repeatedly.*
