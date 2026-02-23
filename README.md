# 🧠 BRAINROT RUSH — Professional UEFN Tycoon

> **Navigation**: **README** | [Quick Start](QUICK_START.md) | [Device Setup](DEVICE_SETUP_GUIDE.md) | [Balancing](BALANCING_GUIDE.md) | [Game Flow](GAME_FLOW.md) | [Map Design](MAP_DESIGN_GUIDE.md) | [Project Summary](PROJECT_SUMMARY.md) | [Improvements](IMPROVEMENTS.md)

The ultimate Gen Z collection tycoon for Fortnite Creative. Sprint, snatch, stack, and flex your way to the top in viral 20-minute sessions packed with spectacle events, power-ups, bounties, revenge mechanics, and pure dopamine-loop gameplay.

**Code**: ~2,300 lines of production-ready Verse | **Status**: Complete, zero compile errors | **Players**: Up to 16 simultaneous

---

## 🔥 Why Players Can't Stop Playing

- **"One more run"** — 20-minute sessions that feel like 5 minutes
- **Lucky drops** — any pickup can randomly be 2×, 5×, or even **10× value** (0.05% jackpot)
- **Revenge mode** — die and come back with **2× collection for 15 seconds** (comeback fuel)
- **Mini-challenges** — random timed challenges pop up every 2 minutes for bonus cash
- **Team combos** — deposit within 10 seconds of your teammate for a **+25% bonus**
- **Bounty hunts** — the richest player gets a crown and everyone chases them for half their cash
- **Photo-finish** — final 60 seconds = **5× earnings**, pure chaos
- **Vault evolution** — watch your team's deposit vault physically upgrade from a wooden crate to a golden fortress
- **Prestige flex** — holographic crowns, permanent bonuses, visible status to flex on noobs

---

## 🎯 Design Goals

- **Monetization**: 20–30 min viral sessions with high return rates
- **Engagement**: 5–10 min reward loops, spectacle moments, social competition
- **Retention**: Cross-session persistence via accolade workaround + prestige system
- **Anti-AFK**: Smart detection warns idle players and docks items after 3 minutes
- **Polish**: Professional audio/visual feedback, Gen Z aesthetic, announcement cooldowns

---

## 🚀 Core Systems

### Collection & Economy
- **Common items** spawn every 8 s across 10–20 spawners ($10 each)
- **Rare items** 3.5% per cycle on 1 random spawner ($1,000 instant)
- **Legendary items** 1.5% per cycle ($5,000 instant)
- **Golden brains** exclusive during Mega Moments ($2,500)
- **Boss items** every 7.5 min ($10,000)
- **Lucky drops** — every pickup rolls for 2× (5%), 5× (0.5%), or 10× (0.05%) multiplier
- **Deposit zone** converts held items → currency (base $10 × multiplier × prestige × combo × event × team combo × lucky × streak)

### Upgrade System (5 Tiers Each)
| Upgrade | Tier 1 | Tier 2 | Tier 3 | Tier 4 | Tier 5 |
|---------|--------|--------|--------|--------|--------|
| **Speed** | $500 (1.2×) | $1.2k (1.5×) | $3k (2.0×) | $8k (2.5×) | $20k (3.0×) |
| **Multiplier** | $1k (1.5×) | $2.5k (2.0×) | $6k (3.0×) | $15k (5.0×) | $40k (10.0×) |

### Prestige System
- Cost: $100,000 (scales per prestige level) → resets currency & upgrades
- Reward: +50% permanent bonus per level (additive: P1=1.5×, P2=2.0×, P3=2.5×, P5=3.5×)
- Unlocks: higher inventory cap (+10 per prestige), reduced death penalty (-5% per level), auto-collect zones
- Visual flex: holographic crown aura (bronze → silver → gold) visible to all players

### Combo System
- 3-second pickup window → every 5 items = +1 tier (max 3 tiers)
- Bonus: +50%/+100%/+150% on next deposit
- Resets on deposit or timeout
- HUD shows 🔥COMBO x3 in real time

### Bounty System
- Every 30 s the richest player (≥$10k) becomes the bounty target
- Kill the bounty target → steal 50% of their currency
- Bounty crown VFX highlights the target for everyone
- Adds high-stakes PvP drama in late game

### Power-Up System
| Power-Up | Effect | Duration |
|----------|--------|----------|
| 🛡️ **Shield** | Blocks 1 death (no item loss) | Until hit |
| 🧲 **Magnet** | Auto-collects 3 items/second | 10 s |
| ×2 **Double** | 2× next deposit value | 1 use |

### 🆕 Revenge Mechanic
- Die? Come back **angry** — 2× item collection for 15 seconds
- Stackable with combo system for massive comeback potential
- "You killed me? Cool, watch this deposit."

### 🆕 Lucky Drops
- **Every single pickup** rolls for a random multiplier
- 5% chance → 2× value | 0.5% → 5× value | 0.05% → **10× JACKPOT**
- Applies to ALL item types including deposits
- Creates "lottery ticket" excitement on every single interaction

### 🆕 Mini-Challenge System
- Random personal challenges issued every 2 minutes to active players
- **Collect Challenge**: Grab 10 items in 15 seconds → $5,000 reward
- **Deposit Rush**: Deposit within 8 seconds → 3× deposit multiplier
- AFK players don't receive challenges (only active players)
- Announced to server when completed

### 🆕 Team Combo Bonus
- When a teammate deposits, you have a **10-second window**
- Deposit within that window → **+25% team combo bonus** on your deposit
- Encourages coordinated team play and communication
- Stacks with all other multipliers

### 🆕 Passive Income
- Hit $35,000 total → unlock **$10/second** passive income
- Hit $100,000 total → upgrade to **$25/second** passive income
- Rewards skilled players with steady cash flow even between collection runs
- Automatically recalculated on every deposit

### 🆕 AFK Detection
- **2 min idle** → warning message ("Move or lose items!")
- **3 min idle** → penalty (lose 10% of held items)
- Keeps lobbies active and fair
- Activity tracked on every pickup and deposit

### Deposit Vault Evolution
Team currency milestones visually upgrade the deposit zone:
1. **Wooden Crate** (start)
2. **Steel Safe** (team total ≥ $25k)
3. **Golden Fortress** (team total ≥ $75k)

---

## 🎉 Event System

| Event | Trigger | Effect | Duration |
|-------|---------|--------|----------|
| **Mega Moment** | Every 5 min | 3× earnings + golden brains | 30 s |
| **Viral Flood** | Every 10 min | Burst spawns across all spawners + 2× earnings | 20 s |
| **Boss Spawn** | Every 7.5 min | $10k item + beacon VFX + announcement | Until collected |
| **Photo-Finish** | 19 min mark | 5× earnings for final rush | 60 s |
| **Mini-Challenges** | Every 2 min | Personal timed challenges for bonus cash | 8–15 s |
| **End Game** | 20 min mark | Winner + awards announced, stats shown | — |

---

## 🏆 End-Game Awards

At session end, the game announces three special awards:

| Award | Criteria |
|-------|----------|
| **Most Collected** | Player who picked up the most total items |
| **Rare Hunter** | Player who found the most rares + legendaries |
| **Biggest Deposit** | Player with the single highest deposit value |

Each award is announced server-wide with a 2-second reveal delay for dramatic effect.

---

## 💾 Persistence & Progression

- **6-tier accolade system** saves progress across sessions
- **Auto-save on leave** — progress preserved between sessions
- **Session restore** — loads currency/prestige on rejoin
- **Late-join catch-up** — $50/min bonus for players joining mid-session

---

## ⚔️ Risk & Reward

- **Death penalty**: Lose 40% of held items on elimination
- **Revenge boost**: 2× collection for 15 seconds after death (comeback mechanic)
- **Shield power-up**: Blocks 1 death completely
- **Deposit streak**: +10% per consecutive deposit without dying (max +100%)
- **Anti-hoarding cap**: 50 items max (scales with prestige via `GetMaxItems`)
- **Inventory warning**: HUD warns at 80% capacity

---

## 👥 Team & Social

- **Dual leaderboards**: Individual + Team totals
- **Team combo deposits**: +25% bonus when depositing within 10s of a teammate
- **Team announcements**: Milestone callouts, deposits, rare finds
- **Bounty system**: Richest player gets targeted by everyone
- **Winner + awards announcement**: End-of-session MVP callout with three special awards
- **Session stats**: Total collected, highest deposit, rares, legendaries
- **Announcement cooldown**: Prevents notification spam (1.5s minimum gap)

---

## 🔊 Audio/Visual Polish

- **SFX arrays** — multiple pickup sounds for variety (plays random)
- **Dedicated SFX** — rare, legendary, golden, boss, deposit, upgrade, event, combo
- **VFX devices** — rare sparkle, legendary explosion, boss beacon, legendary beacon
- **Trophy display** — 3-tier prestige crown VFX (bronze/silver/gold)
- **Death VFX** — scattered brain explosion
- **Deposit landmark** — glowing vault marker visible from across the map
- **Cinematic sequences** — tutorial intro + viral event spectacle
- **HUD icons** — 🛡️ 🧲 ×2 👑 for active power-ups/bounty

---

## 📋 Device Summary (45 @editable Properties)

### Core Spawning (5)
| Property | Type | Count | Purpose |
|----------|------|-------|---------|
| `CommonSpawners` | `[]item_spawner_device` | 10–20 | Phone/item spawns |
| `RareSpawners` | `[]item_spawner_device` | 3–5 | Rare item spawns |
| `LegendarySpawners` | `[]item_spawner_device` | 1–2 | Golden/legendary spawns |
| `BossSpawners` | `[]item_spawner_device` | 3–4 | $10k boss item spawns |
| `GoldenSpawners` | `[]item_spawner_device` | 2–3 | Golden brain (Mega Moment) |

### Interaction (4)
| Property | Type | Count | Purpose |
|----------|------|-------|---------|
| `DepositZone` | `trigger_device` | 1 | Deposit held items for currency |
| `AutoCollectZones` | `[]trigger_device` | 1–4 | Auto-collect (unlocks at max mult) |
| `Hud` | `hud_message_device` | 1 | Currency/inventory/power-up/combo display |
| `EventAnnouncer` | `announcement_device` | 1 | Viral moment callouts |

### Leaderboards (2)
| Property | Type | Count | Purpose |
|----------|------|-------|---------|
| `IndividualLeaderboard` | `leaderboard_device` | 1 | Personal rankings |
| `TeamLeaderboard` | `leaderboard_device` | 1 | Team competition board |

### Upgrades (4)
| Property | Type | Count | Purpose |
|----------|------|-------|---------|
| `SpeedButtons` | `[]button_device` | 5 | Speed tier 1–5 |
| `MultButtons` | `[]button_device` | 5 | Multiplier tier 1–5 |
| `PrestigeButton` | `button_device` | 1 | Prestige reset |
| `SpeedModulators` | `[]movement_modulator_device` | 16 | Per-player speed (1 per slot) |

### Audio (8)
| Property | Type | Count | Purpose |
|----------|------|-------|---------|
| `PickupSFX` | `[]sfx_device` | 3–5 | Random pickup sound variety |
| `RareSFX` | `sfx_device` | 1 | Rare pickup fanfare |
| `LegendarySFX` | `sfx_device` | 1 | Legendary pickup fanfare |
| `GoldenSFX` | `sfx_device` | 1 | Golden brain pickup |
| `DepositSFX` | `sfx_device` | 1 | Cash-in sound |
| `UpgradeSFX` | `sfx_device` | 1 | Purchase confirmation |
| `EventSFX` | `sfx_device` | 1 | Air horn / event alert |
| `ComboSFX` | `sfx_device` | 1 | Combo tier-up |

### Visual Effects (12)
| Property | Type | Count | Purpose |
|----------|------|-------|---------|
| `BossVFX` | `vfx_spawner_device` | 1 | Boss spawn explosion |
| `RareVFX` | `vfx_spawner_device` | 1 | Rare pickup sparkle |
| `LegendaryVFX` | `vfx_spawner_device` | 1 | Legendary glow |
| `BossBeaconVFX` | `[]vfx_spawner_device` | 3–4 | Beam pillars at boss spawns |
| `LegendaryBeaconVFX` | `[]vfx_spawner_device` | 1–2 | Beam pillars at legendary spawns |
| `TrophyVFX` | `[]vfx_spawner_device` | 3 | Prestige crown display |
| `DepositVFX` | `vfx_spawner_device` | 1 | Vault door + coin particles |
| `DepositLandmarkVFX` | `vfx_spawner_device` | 1 | Glowing vault marker |
| `DeathVFX` | `vfx_spawner_device` | 1 | Scattered brain explosion |
| `PrestigeCrownVFX` | `[]vfx_spawner_device` | 3 | Crown/aura on player |
| `DangerZones` | `[]damage_volume_device` | 2–4 | Hazard areas during events |
| `DepositVaultVFX` | `[]vfx_spawner_device` | 3 | Crate → Safe → Fortress |

### Power-Ups (6)
| Property | Type | Count | Purpose |
|----------|------|-------|---------|
| `ShieldSpawners` | `[]item_spawner_device` | 2–3 | Shield pickup locations |
| `MagnetSpawners` | `[]item_spawner_device` | 2–3 | Magnet pickup locations |
| `DoubleSpawners` | `[]item_spawner_device` | 2–3 | Double-deposit pickup locations |
| `BountyCrownVFX` | `vfx_spawner_device` | 1 | Holographic crown on bounty target |
| `ShieldVFX` | `vfx_spawner_device` | 1 | Bubble force-field |
| `MagnetVFX` | `vfx_spawner_device` | 1 | Vortex/magnet aura |

### Persistence & Tutorial (3)
| Property | Type | Count | Purpose |
|----------|------|-------|---------|
| `PersistenceAccolades` | `[]accolade_device` | 6 | Cross-session saving |
| `TutorialSequence` | `cinematic_sequence_device` | 1 | First-time intro |
| `SpectacleSequence` | `cinematic_sequence_device` | 1 | Viral event cinematics |

---

## 🎮 Gameplay Timeline (20-Minute Session)

```
0:00  Player joins → Tutorial + late-join catch-up bonus
0–2   Learn mechanics, first pickups, build to $500 for Speed Tier 1
1:00  🎯 Mini-challenges start issuing to active players every 2 min
2:00  💰 First bounty check — richest player gets crowned
5:00  ⚡ MEGA MOMENT — 3× earnings for 30s, golden brains spawn
5–7   Buy Speed Tier 1 + Mult Tier 1, unlock passive income ($10/s at $35k)
7:30  🏆 BOSS SPAWN — $10k item with red beacon VFX
10:00 🌊 VIRAL FLOOD — 5 burst waves + 2× earnings + danger zones
10–15 Push higher tiers, chase rares/legendaries, hit $100k for P1
15:00 ⚡ MEGA MOMENT #2 + 🏆 BOSS SPAWN #2
15–19 Prestige race, revenge comebacks, team combo stacking
19:00 🏁 PHOTO-FINISH — 5× earnings, final 60s chaos rush
20:00 🎉 END GAME — Winner + 3 awards announced, stats shown, progress saved
```

---

## 🐛 Known Limitations

1. **Accolade persistence** — tier-based, not exact currency (UEFN limitation)
2. **16-player max** — due to per-player modulator array
3. **Team queries** — basic calculation (no advanced team device queries)
4. **Device arrays** — must manually assign all 16 modulators in editor

---

## 📝 3D Asset Shopping List (31 Custom Assets)

See [MAP_DESIGN_GUIDE.md](MAP_DESIGN_GUIDE.md#-meshy-3d-model-prompts) for **detailed Meshy AI prompts** to generate every asset.

| # | Asset | Device Property | Description |
|---|-------|-----------------|-------------|
| 1 | Wooden Crate | `DepositVaultVFX[0]` | Tier 1 deposit vault (starter) |
| 2 | Steel Safe | `DepositVaultVFX[1]` | Tier 2 vault at $25k team |
| 3 | Golden Fortress | `DepositVaultVFX[2]` | Tier 3 vault at $75k team |
| 4 | Deposit Landmark Beacon | `DepositLandmarkVFX` | Cyan waypoint beam, visible map-wide |
| 5 | Boss Beacon (Red) | `BossBeaconVFX` | Red beam at boss spawn locations |
| 6 | Legendary Beacon (Gold) | `LegendaryBeaconVFX` | Gold beam at legendary spawns |
| 7 | Common Phone ×4 colors | `CommonSpawners` items | Neon phone collectibles |
| 8 | Rare Tablet | `RareSpawners` item | Glowing purple-chrome tablet |
| 9 | Legendary Crystal Brain | `LegendarySpawners` item | Golden holographic brain |
| 10 | Golden Brain | `GoldenSpawners` item | Crowned gold brain (Mega exclusive) |
| 11 | Boss Giant Brain | `BossSpawners` item | Oversized neon-veined boss brain |
| 12 | Shield Token | `ShieldSpawners` item | Cyan hexagonal force-field orb |
| 13 | Magnet Token | `MagnetSpawners` item | Purple horseshoe with energy arcs |
| 14 | Double 2X Orb | `DoubleSpawners` item | Gold orb with "2X" hologram |
| 15 | Bounty Crown | `BountyCrownVFX` | Holographic floating crown |
| 16 | Shield Bubble | `ShieldVFX` | Hexagonal force-field sphere |
| 17 | Magnet Aura | `MagnetVFX` | Purple magnetic vortex |
| 18–20 | Trophies ×3 | `TrophyVFX` | Bronze/silver/gold prestige trophies |
| 21–23 | Crown Auras ×3 | `PrestigeCrownVFX` | Bronze/silver/gold player crowns |
| 24 | Death Brain Explosion | `DeathVFX` | Cartoon brain burst fragments |
| 25 | Danger Floor Panels | `DangerZones` | Red/black hazard tiles |
| 26–29 | Neon Signs ×4 | Environment | Deposit / Speed / Mult / Prestige |
| 30 | Speed Buttons ×5 | `SpeedButtons` | Color-ramped arcade buttons |
| 31 | Mult Buttons ×5 | `MultButtons` | Color-ramped arcade buttons |

---

## 📂 Documentation

| File | Contents |
|------|----------|
| [README.md](README.md) | This file — project overview + marketing features |
| [MAP_DESIGN_GUIDE.md](MAP_DESIGN_GUIDE.md) | Map layout, zone placement, build instructions, **Meshy 3D prompts** |
| [QUICK_START.md](QUICK_START.md) | 30-minute express setup |
| [DEVICE_SETUP_GUIDE.md](DEVICE_SETUP_GUIDE.md) | Complete device placement checklist |
| [BALANCING_GUIDE.md](BALANCING_GUIDE.md) | All 78 constants, math, and tuning |
| [GAME_FLOW.md](GAME_FLOW.md) | Player journey diagrams, 12-loop overview |
| [PROJECT_SUMMARY.md](PROJECT_SUMMARY.md) | File structure and deliverables |
| [IMPROVEMENTS.md](IMPROVEMENTS.md) | Original vs professional comparison |

---

## 🔧 Technical Details

- **Language**: Verse (UEFN)
- **Lines of Code**: ~2,300 production-ready Verse
- **Architecture**: Event-driven with 58 player/team state maps, 12 concurrent async loops
- **Constants**: 78 tunable values for easy balancing
- **Async Loops**: SpawnLoop, MegaMomentLoop, ViralEventLoop, SessionTimerLoop, BossSpawnLoop, ItemDespawnLoop, BossDespawnLoop, PowerUpDespawnLoop, BountyCheckLoop, AFKCheckLoop, PassiveIncomeLoop, MiniChallengeLoop
- **Player Safety**: Weak-map auto-cleanup on leave, anti-exploit cooldowns, GameEnded flag, AFK detection
- **Performance**: Batched spawner disable/enable (no per-spawner delays), split despawn timers (boss 3min/power-up 1min/standard 90s), throttled HUD/leaderboard updates, announcement cooldowns
