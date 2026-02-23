# 🗺️ MAP DESIGN GUIDE — Brainrot Rush

> **Navigation**: [README](README.md) | [Quick Start](QUICK_START.md) | [Device Setup](DEVICE_SETUP_GUIDE.md) | [Balancing](BALANCING_GUIDE.md) | [Game Flow](GAME_FLOW.md) | **Map Design** | [Project Summary](PROJECT_SUMMARY.md) | [Improvements](IMPROVEMENTS.md)

How to build and lay out your UEFN island so every game system works correctly. This covers zone dimensions, device placement strategy, terrain design, and the full build order.

---

## 📐 Overall Map Layout

The map is built around a **central hub** with **radiating zones**. Think of it as a wheel: the deposit zone is the hub, upgrade shops are the inner ring, and collection zones are the outer rim.

**Recommended total playable area**: 100 m × 100 m (roughly the size of a Fortnite POI)

```
                        N
                        │
            ┌───────────┼───────────┐
            │     OUTER COLLECTION  │
            │        ZONE (rim)     │
            │  ┌────────────────┐   │
            │  │  INNER RING    │   │
            │  │  (Upgrades +   │   │
            │  │   Power-ups)   │   │
            │  │  ┌──────────┐  │   │
            │  │  │  CENTER  │  │   │
       W────┤  │  │ DEPOSIT  │  │   ├────E
            │  │  │   HUB    │  │   │
            │  │  └──────────┘  │   │
            │  │                │   │
            │  └────────────────┘   │
            │                       │
            │     OUTER COLLECTION  │
            │        ZONE (rim)     │
            └───────────┼───────────┘
                        │
                        S
```

### Zone Breakdown

| Zone | Radius from Center | Purpose |
|------|--------------------|---------|
| **Deposit Hub** | 0–10 m | Deposit zone, vault VFX, landmark beacon |
| **Inner Ring** | 10–25 m | Upgrade shops, prestige area, leaderboards |
| **Mid Ring** | 25–40 m | Common spawners (dense), power-up spawners |
| **Outer Rim** | 40–50 m | Rare/legendary/boss spawners, danger zones |

---

## 🏗️ Build Order (Step by Step)

### Phase 1: Terrain & Boundaries (15 min)

1. **Flatten the center area** — 20 m × 20 m flat platform for the deposit hub
2. **Create elevation changes** going outward:
   - Inner ring: slightly elevated platforms (1–2 m) for upgrade shops
   - Mid ring: ground level, open running space
   - Outer rim: varied terrain — ramps, platforms, alleys for risk/reward
3. **Add walls/boundaries** at the 50 m perimeter — players should not be able to leave
4. **Add 2–4 entry/exit routes** from outer rim back to center (no dead ends)

> **Tip**: Use the terrain sculpting tool for organic ground, or prefab platforms for a clean city look.

### Phase 2: Deposit Hub (10 min)

The **absolute center** of your map. This is where players return constantly.

1. Place the **Trigger Device** (`DepositZone`) — set radius to **10 m**
2. Place `DepositLandmarkVFX` directly above it — a tall glowing beam/column visible from anywhere
3. Place `DepositVFX` at the trigger center — plays on deposit
4. Place `DepositVaultVFX[0]` (wooden crate), `[1]` (steel safe), `[2]` (golden fortress) **stacked at the same spot** — code enables/disables the right one based on team total
5. Add **neon lights, particle rings, or glowing floor tiles** around the zone
6. Place a **Billboard**: "💰 DEPOSIT HERE 💰"

```
         ┌─────────────────────────┐
         │    DEPOSIT HUB (10m)    │
         │                         │
         │     [Billboard Sign]    │
         │          ↓              │
         │   ╔═══════════════╗     │
         │   ║  Vault Props  ║     │
         │   ║ (Crate/Safe/  ║     │
         │   ║  Fortress)    ║     │
         │   ╚═══════════════╝     │
         │       ▲                 │
         │  [DepositVFX]           │
         │  [DepositLandmarkVFX]   │
         │  (Tall glowing beam)    │
         │                         │
         │  ── Trigger Zone ──     │
         │    (10m radius)         │
         └─────────────────────────┘
```

**Design goals**:
- Visible from EVERYWHERE on the map (the landmark beam is the anchor)
- Easy to enter from all directions (no narrow doors)
- Feels satisfying — neon glow, particles, coin VFX on deposit

### Phase 3: Upgrade Shops (15 min)

Place these in the **inner ring** (10–25 m from center), forming a U-shape or semicircle around the deposit hub.

#### Speed Shop
1. **5 Button Devices** in a row (left → right = Tier 1 → 5)
2. Billboard above each button showing cost + tier name:
   ```
   "SPEED UP $500 🚀"  |  "ZOOM $1.2k 💨"  |  "SONIC $3k ⚡"  |  "FLASH $8k 🔥"  |  "LIGHTSPEED $20k 🌟"
   ```
3. Color ramp the buttons: Green → Yellow → Orange → Red → Purple/Rainbow
4. Add a **neon sign** above the row: "🚀 SPEED ZONE 🚀"
5. Floor color: **blue/cyan**

#### Multiplier Shop
1. **5 Button Devices** in a second row (same layout)
2. Billboards:
   ```
   "STONKS $1k 📈"  |  "MONEY PRINTER $2.5k 💰"  |  "WHALE $6k 🐋"  |  "CRYPTO KING $15k 👑"  |  "BILLIONAIRE $40k 💎"
   ```
3. Neon sign: "📈 MULTIPLIER HUB 📈"
4. Floor color: **green**

#### Prestige Altar
1. Place **1 PrestigeButton** on an elevated pedestal (stairs leading up)
2. Place `TrophyVFX[0]`, `[1]`, `[2]` (bronze/silver/gold) on display shelves nearby
3. Billboard: "⭐ PRESTIGE — RESET FOR +50% ($100k) ⭐"
4. Floor color: **gold**
5. Make it feel like an **achievement** to reach — slightly separate from other shops

```
    SPEED SHOP (blue floor)          MULT SHOP (green floor)
    ┌─[Btn1]─[Btn2]─[Btn3]─[Btn4]─[Btn5]─┐  ┌─[Btn1]─[Btn2]─[Btn3]─[Btn4]─[Btn5]─┐
    │  $500  $1.2k  $3k    $8k    $20k    │  │  $1k   $2.5k  $6k    $15k   $40k    │
    │        🚀 SPEED ZONE 🚀             │  │        📈 MULTIPLIER HUB 📈          │
    └──────────────────────────────────────┘  └──────────────────────────────────────┘
                              ↑
                         DEPOSIT HUB
                              ↓
                   ┌────────────────────┐
                   │  PRESTIGE ALTAR    │
                   │  (elevated pedestal)│
                   │  [PrestigeButton]   │
                   │  [TrophyVFX ×3]    │
                   │  ⭐ $100k RESET ⭐  │
                   └────────────────────┘
```

#### Leaderboards
- Place `IndividualLeaderboard` and `TeamLeaderboard` **near the upgrade shops** — players check rankings between purchases
- They should face outward so multiple players can read them

### Phase 4: Common Spawners (15 min)

These are the **bread and butter** — where players spend 80% of their time running.

1. Place **10–20 Item Spawner Devices** across the **mid ring** (25–40 m from center)
2. **Distribute evenly** — no clusters, no dead spots
3. Each spawner should be **2–4 m apart minimum** (players run between them)
4. Place them along natural running paths (loops, figure-8s, corridors)
5. Assign each spawner: phone prop, "Item Picked Up Event" = Enabled

**Placement strategy — the "Running Loop"**:

```
     ●───────●───────●
    /                   \
   ●                     ●
   │    (INNER RING)     │
   ●     DEPOSIT +       ●
   │     UPGRADES        │
   ●                     ●
    \                   /
     ●───────●───────●
   
   ● = Common Spawner
   ─ = Natural running path
```

Create 1–2 clear **loop routes** so players can run in a circuit collecting items without backtracking. This is the core gameplay flow — it must feel smooth.

> **Tip**: Place spawners on both sides of corridors / walkways so players zig-zag while running.

### Phase 5: Rare & Legendary Spawners (10 min)

These go in the **outer rim** — players must venture further from the safe deposit hub.

#### Rare Spawners (3–5)
- Place in **semi-hidden alcoves, side rooms, or elevated platforms**
- Not directly on the main running loop — players must detour
- Still reachable within 5–10 seconds from the loop
- Place 1 `LegendaryBeaconVFX` at each legendary spawner location

#### Legendary Spawners (1–2)
- Place in the **most remote or contested spots** on the map
- Elevated platforms, end of dead-end corridors, or island centers
- Maximum distance from deposit zone creates risk (death penalty + inventory loss)
- Place 1 `LegendaryBeaconVFX` at each — the golden beam signals when active

#### Boss Spawners (3–4)
- Place in **dramatic hidden locations**: rooftop, underground chamber, bridge platform
- Should require players to navigate obstacles or climb
- Co-locate 1 `BossBeaconVFX` (red beam) at each spawner — visible when boss spawns
- Boss beacon height: make the beam taller than legendary beacons (different color = red vs gold)

```
       [Boss3]
         ★  (rooftop)
         │
    ◆────┤────◆        ◆ = Rare (alcove)
    │         │         ★ = Boss (dramatic)
    │  Common │         ♦ = Legendary (remote)
    │  Loop   │
    │         │
    ◆────┤────◆
         │
       [Boss1]          ♦ Legendary
         ★              (far corner,
    (underground)        max risk)
```

### Phase 6: Power-Up Spawners (10 min)

Place these in the **mid ring** — easy to spot, tempting to grab during collection runs.

#### Shield Spawners (2–3)
- Place in **open areas** along the running loop
- Visible and easy to grab — the shield is a defensive tool players should want
- Space them 40–60 m apart around the loop

#### Magnet Spawners (2–3)
- Place **near dense common spawner clusters** — the magnet auto-collects nearby items
- Best near areas with 3–4 common spawners within 10 m
- Players will learn to activate magnet near these clusters

#### Double Spawners (2–3)
- Place in **risky/contested areas** — the double is high-value (2× next deposit)
- Near boss spawners, in the outer rim, or near danger zones
- Risk = reward: grabbing the double means you're far from deposit

### Phase 7: Danger Zones (5 min)

`DangerZones` are `damage_volume_device` areas that activate during viral events for added chaos.

1. Place **2–4 Damage Volume devices** in the mid-to-outer ring
2. Make them **large but avoidable** (10–15 m radius)
3. They should block parts of the running loop during events — forcing alternate routes
4. Place at **chokepoints** or intersections for maximum impact
5. Add a **red glow / lava floor texture** to signal danger (even when inactive, the floor hints "this gets dangerous")

```
    Normal: Safe to walk through
    During Viral Event: DAMAGE ACTIVE — find another route!
```

### Phase 8: Auto-Collect Zones (5 min)

`AutoCollectZones` activate only for players who've maxed their multiplier tier — a QoL reward.

1. Place **1–4 Trigger Devices** near popular common spawner areas
2. Radius: 5–8 m (smaller than deposit zone)
3. They passively collect items for max-tier players walking through
4. Place near the densest common spawner clusters

### Phase 9: Hidden Devices (10 min)

#### Movement Modulators (16)
- Place all 16 `SpeedModulators` in a **grid underground** or in a hidden sky platform
- They must be **completely invisible** to players
- Any open area works — behind a wall, under the terrain, in the void

#### SFX Devices (8)
- Place all SFX devices **near the center hub** (sound doesn't need to be positional for most UEFN setups)
- Group them together in a hidden area for easy management

#### Accolade Devices (6)
- Place all 6 `PersistenceAccolades` in a **hidden room** or underground
- They only trigger via code — players never interact with them directly

#### Other Hidden Devices
- `HUD Message Device` — place anywhere (it overlays globally)
- `Announcement Device` — place anywhere
- `Cinematic Sequence Devices` (Tutorial + Spectacle) — place with camera paths set in the sequencer

### Phase 10: Spawn Points & Team Setup (5 min)

1. Place **16 Player Spawn Pads** in the inner ring (near the upgrade shops)
2. Players should spawn **facing the deposit zone** — first thing they see is the landmark beam
3. Face them outward toward the collection loop — clear direction: "go grab items"
4. Add a **Team Settings Device** if using teams (2–4 teams, auto-assign, friendly fire off)

```
     Spawn Pads (inner ring, facing outward)
     
           S  S  S  S
          S            S
         S   DEPOSIT    S
         S    HUB       S
          S            S
           S  S  S  S
```

---

## 🎨 Visual Design & Theming

### Color Palette
| Zone | Primary Color | Accent | Floor Material |
|------|--------------|--------|----------------|
| Deposit Hub | **Cyan / White** | Gold particles | Glowing tiles |
| Speed Shop | **Blue** | Cyan neon | Blue-tinted floor |
| Mult Shop | **Green** | Lime neon | Green-tinted floor |
| Prestige Altar | **Gold** | Star particles | Gold/marble floor |
| Collection Loop | **Purple / Pink** | Neon strips | Dark concrete |
| Danger Zones | **Red** | Lava glow | Red-tinted floor |
| Boss Locations | **Dark Red / Orange** | Fire particles | Scorched earth |
| Power-Up Areas | **Rainbow / White** | Sparkle | Neutral floor |

### Lighting
- **Time of day**: Night or Dusk (neon colors pop best in dark)
- **Deposit hub**: Bright white/cyan — the safe zone, well-lit
- **Collection loop**: Medium lighting — can see clearly but feels like the "wild"
- **Outer rim**: Dimmer — tension, risk, drama
- **Boss locations**: Dramatic spotlight only when boss is active

### Neon Signs & Billboards (20+ recommended)
Place at every decision point:

| Location | Sign Text |
|----------|-----------|
| At deposit zone | "💰 DEPOSIT HERE 💰" |
| Speed shop entrance | "🚀 SPEED ZONE 🚀" |
| Mult shop entrance | "📈 MULTIPLIER HUB 📈" |
| Prestige altar | "⭐ PRESTIGE $100k ⭐" |
| Above each button | Cost + tier name (see Phase 3) |
| At loop entrances | "📱 COLLECT PHONES ➡️" |
| Near rare spawners | "💎 RARE ZONE — HIGH VALUE" |
| Near boss spawners | "🏆 BOSS ARENA — $10k" |
| Near danger zones | "⚠️ DANGER ZONE ⚠️" |
| Near power-up spots | "🛡️ SHIELD" / "🧲 MAGNET" / "×2 DOUBLE" |
| At spawn points | "🧠 BRAINROT RUSH — GET RICH! 🧠" |

### Props & Decoration
- **Urban/city theme**: benches, trash cans, graffiti walls, phone props as decoration
- **Social media imagery**: TikTok-style logos, hashtag symbols, heart/fire emojis
- **Meme signs** (tasteful): "No cap fr fr", "This game bussin", "STONKS 📈"
- **Scattered phone props** as decoration (different from spawnable ones — just set dressing)
- **Neon strips** along walls, floors, stairways
- **Particle effects** at major zones (sparkles at rare spawners, fire at danger zones)

---

## 📏 Dimension Reference

| Element | Size | Notes |
|---------|------|-------|
| Total map | 100 × 100 m | Fenced/walled perimeter |
| Deposit trigger radius | 10 m | Large, easy to enter |
| Inner ring width | 15 m (10–25 m) | Upgrade shops + spawn pads |
| Mid ring width | 15 m (25–40 m) | Common spawners + power-ups |
| Outer rim width | 10 m (40–50 m) | Rares, bosses, legendaries |
| Common spawner spacing | 4–8 m apart | Even distribution |
| Rare spawner spacing | 15–25 m apart | Semi-hidden |
| Boss spawner spacing | 25–40 m apart | Dramatic locations |
| Danger zone radius | 10–15 m | Large enough to block routes |
| Auto-collect zone radius | 5–8 m | Near dense spawner clusters |
| Button spacing (in row) | 2–3 m apart | Easy to read + interact |
| Billboard height | 3–4 m above button | Readable from 10 m away |

---

## 🔄 Flow Verification Checklist

After building, walk the map and verify:

### Pathing
- [ ] Can reach deposit zone from every point in < 15 seconds (at base speed)
- [ ] Running loop has no dead ends (continuous circuit)
- [ ] Can reach every spawner without getting stuck on geometry
- [ ] Danger zones don't completely block all routes (alternate paths exist)
- [ ] Deposit landmark VFX is visible from every point on the map

### Risk Gradient
- [ ] Center = safest (deposit + upgrades)
- [ ] Mid ring = moderate (collection, easy power-ups)
- [ ] Outer rim = riskiest (bosses, legendaries, doubles)
- [ ] Players feel tension increasing as they move outward

### Sight Lines
- [ ] Deposit beacon visible from anywhere (tall glowing pillar)
- [ ] Boss beacon visible when active (red beam)
- [ ] Legendary beacon visible when active (gold beam)
- [ ] Upgrade shop signs readable from 10+ m
- [ ] Neon signs guide players toward zones naturally

### Device Check
- [ ] All 16 modulators hidden (not visible to players)
- [ ] All SFX/accolade devices hidden
- [ ] Spawner items visually distinct: common(phone) → rare(tablet) → legendary(golden) → boss(giant brain)
- [ ] Power-up tokens visually distinct: shield(bubble) → magnet(spiral) → double(2X orb)
- [ ] Vault VFX props stacked at deposit zone (code toggles the right one)

---

## 🏗️ Example Map Layout (Top-Down ASCII)

```
┌──────────────────────────────────────────────────────────────┐
│                                                              │
│    [Boss2★]         ◆Rare        [Boss3★]                    │
│         ╲          ╱                ╱                         │
│          ╲  ●────●────●────●      ╱                          │
│    ⚠Danger╲/                \────╱     ♦Legendary            │
│    Zone    ●    COLLECTION    ●                              │
│            │     LOOP         │      ⚠Danger                │
│     🛡Shield●                  ●     Zone                    │
│            │  ┌────────────┐  │                              │
│     ●──────┤  │  SPEED     │  ├──────●                       │
│            │  │  SHOP      │  │                              │
│    🧲Magnet●  │            │  ●   ×2Double                   │
│            │  │  DEPOSIT   │  │                              │
│     ●──────┤  │   HUB     │  ├──────●                       │
│            │  │  ☆beacon☆  │  │                              │
│            │  │            │  │                              │
│     🛡Shield●  │  MULT     │  ●   🧲Magnet                   │
│            │  │  SHOP      │  │                              │
│     ●──────┤  │            │  ├──────●                       │
│            │  │ PRESTIGE   │  │                              │
│            │  └────────────┘  │                              │
│            ●                  ●                              │
│     ⚠Danger╲                ╱       ⚠Danger                 │
│     Zone    ╲●────●────●──●╱        Zone                    │
│              ╲           ╱                                   │
│    [Boss1★]   ╲  ◆Rare  ╱    ♦Legendary    [Boss4★]         │
│                                                              │
│  ● = Common Spawner    ◆ = Rare    ♦ = Legendary    ★ = Boss │
│  🛡 = Shield   🧲 = Magnet   ×2 = Double   ⚠ = Danger Zone  │
└──────────────────────────────────────────────────────────────┘
```

---

## 🎮 Cinematic Camera Paths

### Tutorial Sequence (15 s, first-time players)
1. **Shot 1** (0–5 s): Wide overhead showing entire map, deposit beacon glowing
   - Text: "🧠 WELCOME TO BRAINROT RUSH! 🧠"
2. **Shot 2** (5–10 s): Pan across the collection loop with items visible
   - Text: "📱 COLLECT PHONES → DEPOSIT FOR CASH 💰"
3. **Shot 3** (10–15 s): Fly through upgrade shops, end on prestige altar
   - Text: "🚀 BUY UPGRADES → PRESTIGE → GET RICH! 💎"

### Spectacle Sequence (5 s, viral events)
1. **Shot 1** (0–3 s): Dramatic zoom-out from deposit zone, screen shake
   - Text: "🌊 VIRAL EVENT INCOMING! 🌊"
2. **Shot 2** (3–5 s): Quick montage of items spawning everywhere
   - Text: "GRAB EVERYTHING! 2× EARNINGS!"

---

## 🏗️ Custom 3D Asset Placement Guide

If you're creating custom meshes, here's where each one goes:

| Asset | Where to Place | Size | Notes |
|-------|---------------|------|-------|
| Wooden Crate | Deposit hub center | 2×2×2 m | Vault Tier 1 (start) |
| Steel Safe | Same spot as crate | 2×2×2 m | Vault Tier 2 (code swaps) |
| Golden Fortress | Same spot | 3×3×3 m | Vault Tier 3 (code swaps) |
| Beacon Pillar (gold) | At each legendary spawner | 0.5 m wide, 20+ m tall | Visible from everywhere |
| Beacon Pillar (red) | At each boss spawner | 0.5 m wide, 25+ m tall | Taller than legendary |
| Deposit Landmark | Above deposit zone | 1 m wide, 30+ m tall | Tallest beam on map |
| Trophy Bronze | Prestige altar shelf | 0.5 m | Display only |
| Trophy Silver | Prestige altar shelf | 0.5 m | Display only |
| Trophy Gold | Prestige altar shelf | 0.5 m | Display only |
| Phone props (common) | Inside spawner devices | 0.2 m | Various colors |
| Tablet props (rare) | Inside rare spawners | 0.3 m | Glowing edge |
| Golden brain (golden) | Inside golden spawners | 0.3 m | Gold material |
| Giant brain (boss) | Inside boss spawners | 0.5 m | Oversized, glowing |
| Shield orb | Inside shield spawners | 0.3 m | Translucent sphere |
| Magnet token | Inside magnet spawners | 0.3 m | Horseshoe or spiral |
| 2X orb | Inside double spawners | 0.3 m | "2X" text, glowing |
| Bounty crown | `BountyCrownVFX` attached | Fits head | Holographic, floating |
| Shield bubble | `ShieldVFX` attached | 2 m sphere | Translucent blue |
| Magnet aura | `MagnetVFX` attached | 3 m radius | Purple swirl |
| Danger floor panels | Under DangerZone volumes | 10–15 m tiles | Red/lava texture |

---

## ✅ Final Map QA

Before publishing, run through this:

- [ ] Played a full 20-min solo session on the built map
- [ ] Deposit zone is the clear center of attention
- [ ] Players never get lost (signs + beacon guide them)
- [ ] All 4 spawn types are reachable and visible
- [ ] Power-ups are tempting but don't break flow
- [ ] Danger zones create excitement without frustration
- [ ] Upgrade shops feel organized (clear tier progression)
- [ ] Prestige altar feels special and earned
- [ ] No geometry traps (players can't get stuck)
- [ ] All hidden devices are truly invisible
- [ ] Frame rate holds at 60 fps with 16 players
- [ ] Beacons (deposit, boss, legendary) are visible from every corner

---

## 🎨 Meshy 3D Model Prompts

Copy-paste these directly into [Meshy](https://www.meshy.ai) (Text to 3D) to generate every custom asset needed for the game. All assets target a **stylized / cartoon / neon-cyberpunk** aesthetic to match the Gen Z brainrot theme.

> **Settings tip**: Use "Cartoon" or "Stylized" art style in Meshy. Set topology to **quad** for game-ready models. Export as `.fbx` for UEFN import.

---

### 1. Deposit Vault — Wooden Crate (Tier 1)

**Meshy Prompt:**
```
A small stylized wooden shipping crate with metal corner brackets and rusty nails, cartoon game prop style. The wood planks are slightly warped with visible grain texture. A faint cyan glow leaks through the cracks between planks. A hand-painted dollar sign "$" is stenciled on the front in faded white paint. Low-poly game asset, clean topology, bright and colorful, isometric RPG style. No background.
```
**Size in-game:** 2 × 2 × 2 m | **Placement:** Deposit hub center

---

### 2. Deposit Vault — Steel Safe (Tier 2)

**Meshy Prompt:**
```
A heavy-duty stylized steel bank safe with a large circular vault dial on the front door, cartoon game prop. Polished brushed-metal surface with green LED indicator lights along the edges. The handle is a thick chrome lever. Small holographic dollar signs float above it. Riveted panels, industrial look, slightly futuristic. Low-poly game asset, clean geometry, vibrant colors. No background.
```
**Size in-game:** 2 × 2 × 2 m | **Placement:** Same spot as crate (code swaps)

---

### 3. Deposit Vault — Golden Fortress (Tier 3)

**Meshy Prompt:**
```
An extravagant miniature golden fortress vault, stylized cartoon game prop. Ornate golden walls with gemstone inlays (emeralds, rubies, sapphires). A grand vault door at the front with a glowing diamond-shaped keyhole emitting bright white light. Piles of gold coins and gem clusters visible at the base. Crown ornament on top. Luxurious, over-the-top rich aesthetic, low-poly stylized game asset. Shiny metallic gold material with iridescent highlights. No background.
```
**Size in-game:** 3 × 3 × 3 m | **Placement:** Same spot (code swaps)

---

### 4. Deposit Landmark Beacon

**Meshy Prompt:**
```
A tall futuristic holographic beacon tower, stylized sci-fi game prop. Slim hexagonal base with a vertical energy beam shooting straight up. The beam is bright cyan-white with swirling particle rings traveling upward along the column. The base has neon cyan circuit-board patterns and a floating holographic dollar sign rotating above it. Looks like a waypoint marker from a sci-fi game. Clean low-poly, emissive glow materials. No background.
```
**Size in-game:** 1 m wide base, 30+ m tall beam | **Placement:** Directly above deposit zone

---

### 5. Boss Beacon Pillar (Red)

**Meshy Prompt:**
```
A dramatic vertical energy pillar beacon, stylized game VFX prop. Hexagonal dark metal base with pulsing red-orange energy beam shooting upward. The beam has fire-like tendrils and ember particles spiraling around it. Skull icon embossed on the base plate. Ominous red glow, dark fantasy meets cyberpunk. The pillar pulses between bright red and dark crimson. Low-poly game asset with emissive materials. No background.
```
**Size in-game:** 0.5 m wide, 25+ m tall | **Placement:** At each boss spawner (3–4 total)

---

### 6. Legendary Beacon Pillar (Gold)

**Meshy Prompt:**
```
An elegant vertical energy pillar beacon, stylized game VFX prop. Circular ornate golden base with a bright golden-yellow energy beam shooting upward. The beam has star-like sparkle particles and golden rings ascending the column. Diamond icon floating at the base. Majestic golden glow, fantasy treasure aesthetic. Warm gold and white light. Low-poly game asset with emissive metallic gold materials. No background.
```
**Size in-game:** 0.5 m wide, 20+ m tall | **Placement:** At each legendary spawner (1–2 total)

---

### 7. Common Pickup — Brainrot Phone (Multiple Colors)

**Meshy Prompt:**
```
A stylized cartoon smartphone floating and slightly tilted, game collectible prop. Bright glowing screen showing a TikTok-style scrolling feed icon. Rounded edges, chunky proportions, glossy plastic material. The phone case is [NEON PINK / ELECTRIC BLUE / LIME GREEN / HOT ORANGE] with small brain emoji sticker on the back. Cute, fun, collectible game item style. Low-poly, clean topology. No background.
```
> Generate 4 variants by swapping the color in brackets  

**Size in-game:** 0.2 m | **Placement:** Inside CommonSpawners

---

### 8. Rare Pickup — Glowing Tablet

**Meshy Prompt:**
```
A stylized glowing tablet device floating in the air, rare game collectible. The screen displays a bright diamond icon. The edges emit a pulsing purple-magenta neon glow. The tablet body is sleek dark chrome with holographic rainbow shimmer on the back panel. Small sparkle particles surround it. Premium feel, clearly more valuable than a phone. Stylized cartoon game prop, low-poly, emissive materials. No background.
```
**Size in-game:** 0.3 m | **Placement:** Inside RareSpawners

---

### 9. Legendary Pickup — Holographic Crystal Brain

**Meshy Prompt:**
```
A floating holographic brain made of translucent crystal with golden veins of light running through it, legendary game collectible. The brain slowly rotates and emits a bright golden-white aura. Geometric facets like a cut gemstone. Small orbiting star particles. Ethereal, mystical, extremely valuable-looking. Stylized fantasy game prop, iridescent and emissive materials, low-poly clean mesh. No background.
```
**Size in-game:** 0.3 m | **Placement:** Inside LegendarySpawners

---

### 10. Golden Brain (Mega Moment Exclusive)

**Meshy Prompt:**
```
A solid gold cartoon brain with exaggerated folds and a mirror-polished surface, floating game collectible. Bright golden metallic material with warm specular highlights. A small golden crown sits on top of the brain. Tiny gold coins orbit around it like electrons. Luxurious, flashy, over-the-top rich. Fun stylized cartoon game prop, low-poly, clean topology. No background.
```
**Size in-game:** 0.3 m | **Placement:** Inside GoldenSpawners

---

### 11. Boss Pickup — Giant Neon Brain

**Meshy Prompt:**
```
An oversized pulsating brain, boss-tier game collectible. The brain is dark purple-black with bright neon red and orange veins of energy crackling across the surface like lightning. Significantly larger than other pickups. Floating above a small dark energy vortex at the base. Menacing red eye-like glow in the center. Intimidating but stylized cartoon proportions. Boss-level game prop, emissive neon materials, low-poly. No background.
```
**Size in-game:** 0.5 m | **Placement:** Inside BossSpawners

---

### 12. Shield Pickup Token

**Meshy Prompt:**
```
A floating translucent force-field sphere with a shield icon inside, game power-up collectible. The outer sphere is glass-like with hexagonal honeycomb patterns visible on the surface, glowing cyan-blue. Inside the sphere, a small stylized medieval shield icon floats and rotates. Soft blue particle ring orbits the equator. Protective, defensive feel. Stylized cartoon game prop, transparent and emissive materials, low-poly. No background.
```
**Size in-game:** 0.3 m | **Placement:** Inside ShieldSpawners

---

### 13. Magnet Pickup Token

**Meshy Prompt:**
```
A floating cartoon horseshoe magnet with swirling magnetic field lines, game power-up collectible. Classic red and silver horseshoe shape but with neon purple energy arcing between the poles. Small metallic debris particles are being pulled toward the magnet, orbiting around it. Electric purple glow. Fun, powerful, magnetic energy feel. Stylized cartoon game prop, emissive materials, low-poly clean mesh. No background.
```
**Size in-game:** 0.3 m | **Placement:** Inside MagnetSpawners

---

### 14. Double Pickup Token — 2X Orb

**Meshy Prompt:**
```
A floating glowing orb with a large bold "2X" text inside, game power-up collectible. The orb is translucent bright gold-yellow with sparkle particles inside like a snow globe. The "2X" text is holographic white and slowly rotates. Two small golden rings orbit the orb at perpendicular angles. Exciting, valuable, jackpot feel. Stylized cartoon game prop, emissive transparent materials, low-poly. No background.
```
**Size in-game:** 0.3 m | **Placement:** Inside DoubleSpawners

---

### 15. Bounty Crown (Player-Attached VFX)

**Meshy Prompt:**
```
A floating holographic crown hovering above a character's head, game status indicator. The crown is translucent gold with bright glowing edges and a floating diamond at the crown peak. Holographic scan-line effect across the surface. Small golden particle trail falling like fairy dust below the crown. Regal but digital/cyber aesthetic. Must look like a HUD indicator floating in the game world. Stylized game prop, emissive holographic materials, low-poly. No background.
```
**Size in-game:** Fits above player head | **Placement:** Attached to `BountyCrownVFX`

---

### 16. Shield Bubble (Player-Attached VFX)

**Meshy Prompt:**
```
A translucent protective bubble sphere surrounding a character, game shield effect. Hexagonal honeycomb grid pattern visible on the sphere surface with soft cyan-blue glow. Occasional ripple distortion waves travel across the surface. The bottom of the sphere fades to transparent. Sci-fi force-field aesthetic, like a personal energy shield. Clean sphere geometry, transparent and emissive materials. No background.
```
**Size in-game:** 2 m diameter sphere around player | **Placement:** Attached to `ShieldVFX`

---

### 17. Magnet Aura (Player-Attached VFX)

**Meshy Prompt:**
```
A swirling magnetic vortex effect surrounding a character, game magnet power-up aura. Purple and pink energy tendrils spiral inward toward the character center like a whirlpool. Small glowing item silhouettes (phones, coins) are caught in the vortex, orbiting inward. Electric purple lightning crackles between the spiral arms. Dynamic, powerful suction feel. VFX game asset, emissive particle-style materials. No background.
```
**Size in-game:** 3 m radius around player | **Placement:** Attached to `MagnetVFX`

---

### 18. Prestige Trophy — Bronze

**Meshy Prompt:**
```
A stylized bronze trophy cup on a small pedestal, game achievement prop. Classic two-handled trophy shape with brushed bronze metallic material. A single star engraved on the front. The pedestal has a small plaque reading "P1". Subtle warm orange glow from the star. Simple, clean, first-achievement feel. Cartoon game prop, low-poly, metallic materials. No background.
```
**Size in-game:** 0.5 m | **Placement:** Prestige altar display shelf

---

### 19. Prestige Trophy — Silver

**Meshy Prompt:**
```
A stylized silver trophy cup on a pedestal, game achievement prop. Taller and more ornate than the bronze version with additional decorative wings on the handles. Polished silver chrome material with two stars engraved on the front. "P2" on the pedestal plaque. Cool blue-white specular highlights. More impressive, intermediate achievement feel. Cartoon game prop, low-poly, shiny metallic. No background.
```
**Size in-game:** 0.5 m | **Placement:** Prestige altar display shelf

---

### 20. Prestige Trophy — Gold

**Meshy Prompt:**
```
An extravagant gold trophy cup on a marble pedestal, ultimate game achievement prop. Largest of the three trophies with ornate angel-wing handles and a crown topper. Polished 24k gold material with three diamond stars on the front. "P3" on a golden plaque. Bright golden aura glow emanating from the trophy. Small orbiting sparkle particles. Maximum prestige, ultimate flex. Cartoon game prop, low-poly, emissive gold materials. No background.
```
**Size in-game:** 0.5 m | **Placement:** Prestige altar display shelf

---

### 21. Prestige Crown Aura — Bronze

**Meshy Prompt:**
```
A simple floating bronze circlet crown above a character's head with a single warm ember particle trail, game prestige indicator. Thin bronze metal band with minimal decoration, small triangular points. Subtle orange glow. Understated but visible status symbol. Low-poly game VFX prop, metallic material. No background.
```
**Placement:** `PrestigeCrownVFX[0]`

---

### 22. Prestige Crown Aura — Silver

**Meshy Prompt:**
```
A floating ornate silver crown above a character's head with cool blue sparkle particles trailing downward, game prestige indicator. More detailed than bronze with gemstone inlays and taller points. Silver chrome material with blue-white highlights. Impressive mid-tier status symbol. Low-poly game VFX prop, shiny metallic material. No background.
```
**Placement:** `PrestigeCrownVFX[1]`

---

### 23. Prestige Crown Aura — Gold

**Meshy Prompt:**
```
A majestic floating golden crown with radiating golden light rays above a character's head, ultimate game prestige indicator. Elaborate golden crown with large gemstones (ruby, sapphire, emerald) and intricate filigree. Bright golden particle aura and small orbiting stars. Maximum status flex, unmistakable from across the map. Low-poly game VFX prop, emissive gold material with gemstone accents. No background.
```
**Placement:** `PrestigeCrownVFX[2]`

---

### 24. Death VFX — Brain Explosion

**Meshy Prompt:**
```
An exploding cartoon brain bursting apart into scattered pieces, game death VFX prop. Multiple brain chunk fragments flying outward from a central burst point. Pink brain matter with neon purple energy trails behind each piece. Small skull icon at the center of the explosion. Dramatic, funny, over-the-top cartoon violence (no gore). Stylized game VFX asset, bright colors, low-poly pieces. No background.
```
**Placement:** `DeathVFX` — triggers on player death

---

### 25. Danger Zone Floor Panel

**Meshy Prompt:**
```
A large square floor tile with hazard warning pattern, game danger zone prop. Bright red and black chevron stripes around the border. Center of the tile has a glowing lava-crack texture with orange-red emissive light seeping through. Yellow warning triangle with exclamation mark embossed in each corner. Industrial hazard aesthetic meets neon cyberpunk. Flat square game prop, emissive materials, tileable. No background.
```
**Size in-game:** 10–15 m tiles | **Placement:** Under `DangerZone` damage volumes

---

### 26. Neon Sign — "DEPOSIT HERE"

**Meshy Prompt:**
```
A neon sign reading "DEPOSIT HERE" in bold blocky letters, game environment prop. Bright cyan-white neon tubes mounted on a dark metal backplate. A large glowing dollar sign "$" icon on the left side of the sign. The neon tubes have a soft bloom glow. Slight flickering aesthetic. Urban cyberpunk neon sign style, game prop. No background.
```
**Placement:** Above deposit zone

---

### 27. Neon Sign — "SPEED ZONE"

**Meshy Prompt:**
```
A neon sign reading "SPEED ZONE" in italic speed-line styled letters, game environment prop. Bright blue neon tubes with a rocket icon on right side. Mounted on a dark brushed-metal backing plate. Motion lines behind the text suggesting speed. Soft blue neon bloom glow. Urban cyberpunk style, game environment prop. No background.
```
**Placement:** Above speed upgrade shop

---

### 28. Neon Sign — "MULTIPLIER HUB"

**Meshy Prompt:**
```
A neon sign reading "MULTIPLIER HUB" in bold block letters, game environment prop. Bright green neon tubes with an upward-trending chart/arrow icon on the left. Mounted on dark metal backplate. The chart icon pulses with bright lime-green glow. Stock market / money printer aesthetic. Game environment prop, neon materials. No background.
```
**Placement:** Above multiplier upgrade shop

---

### 29. Neon Sign — "PRESTIGE"

**Meshy Prompt:**
```
A neon sign reading "PRESTIGE" in elegant serif letters, game environment prop. Bright gold neon tubes with a star icon on each side. Mounted on a polished dark marble backplate. The stars emit warm golden particle sparkles. Luxurious, achievement-oriented aesthetic. More refined than other signs. Game environment prop, emissive gold neon materials. No background.
```
**Placement:** Above prestige altar

---

### 30. Speed Upgrade Button Prop (5 tiers)

**Meshy Prompt:**
```
A large stylized arcade-style push button on a pedestal, game interaction prop. Chunky round button with [GREEN / YELLOW / ORANGE / RED / PURPLE] glowing rim. A rocket icon is embossed on the button face. The pedestal is sleek dark metal with a small price display screen on the front showing "$" in pixel font. Satisfying, chunky, "press me" feel. Cartoon arcade style, game prop, emissive colored rim. No background.
```
> Generate 5 variants using the color progression in brackets  

**Placement:** Speed shop, 5 in a row (Tier 1 → 5)

---

### 31. Multiplier Upgrade Button Prop (5 tiers)

**Meshy Prompt:**
```
A large stylized arcade-style push button on a pedestal, game interaction prop. Chunky round button with [LIME / TEAL / CYAN / BLUE / DIAMOND-WHITE] glowing rim. An upward arrow chart icon is embossed on the button face. The pedestal is sleek dark metal with a small price screen on the front. Satisfying, chunky, investment/money theme. Cartoon arcade style, game prop, emissive colored rim. No background.
```
> Generate 5 variants using the color progression in brackets  

**Placement:** Multiplier shop, 5 in a row (Tier 1 → 5)

---

### Asset Checklist

| # | Asset | Meshy Prompt # | Generated? |
|---|-------|---------------|------------|
| 1 | Wooden Crate (Vault T1) | #1 | ☐ |
| 2 | Steel Safe (Vault T2) | #2 | ☐ |
| 3 | Golden Fortress (Vault T3) | #3 | ☐ |
| 4 | Deposit Landmark Beacon | #4 | ☐ |
| 5 | Boss Beacon (Red) | #5 | ☐ |
| 6 | Legendary Beacon (Gold) | #6 | ☐ |
| 7 | Common Phone ×4 colors | #7 | ☐ |
| 8 | Rare Tablet | #8 | ☐ |
| 9 | Legendary Crystal Brain | #9 | ☐ |
| 10 | Golden Brain | #10 | ☐ |
| 11 | Boss Giant Brain | #11 | ☐ |
| 12 | Shield Token | #12 | ☐ |
| 13 | Magnet Token | #13 | ☐ |
| 14 | Double 2X Orb | #14 | ☐ |
| 15 | Bounty Crown | #15 | ☐ |
| 16 | Shield Bubble | #16 | ☐ |
| 17 | Magnet Aura | #17 | ☐ |
| 18 | Trophy Bronze | #18 | ☐ |
| 19 | Trophy Silver | #19 | ☐ |
| 20 | Trophy Gold | #20 | ☐ |
| 21 | Crown Aura Bronze | #21 | ☐ |
| 22 | Crown Aura Silver | #22 | ☐ |
| 23 | Crown Aura Gold | #23 | ☐ |
| 24 | Death Brain Explosion | #24 | ☐ |
| 25 | Danger Floor Panels | #25 | ☐ |
| 26 | Neon Sign — Deposit | #26 | ☐ |
| 27 | Neon Sign — Speed | #27 | ☐ |
| 28 | Neon Sign — Multiplier | #28 | ☐ |
| 29 | Neon Sign — Prestige | #29 | ☐ |
| 30 | Speed Buttons ×5 | #30 | ☐ |
| 31 | Mult Buttons ×5 | #31 | ☐ |

> **Total unique Meshy generations needed:** ~35 (counting color variants)

---

> **Next**: [Balancing Guide](BALANCING_GUIDE.md) | [Game Flow](GAME_FLOW.md) | [Device Setup](DEVICE_SETUP_GUIDE.md)

**With the map built and all devices assigned, the game is ready to play. Follow [DEVICE_SETUP_GUIDE.md](DEVICE_SETUP_GUIDE.md) for the device assignment step, and [QUICK_START.md](QUICK_START.md) for the testing checklist.**
