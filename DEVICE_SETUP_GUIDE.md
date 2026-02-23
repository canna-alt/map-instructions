# 🔧 UEFN DEVICE SETUP CHECKLIST

> **Navigation**: [README](README.md) | [Quick Start](QUICK_START.md) | **Device Setup** | [Balancing](BALANCING_GUIDE.md) | [Game Flow](GAME_FLOW.md) | [Map Design](MAP_DESIGN_GUIDE.md) | [Project Summary](PROJECT_SUMMARY.md) | [Improvements](IMPROVEMENTS.md)

Complete device placement and assignment guide for Brainrot Rush.  
The game has **45 @editable properties** — this doc covers every one.

> **Time estimate**: 2–4 hours for full setup (1 hour for minimal viable game)

---

## ✅ Step-by-Step Setup

### 1. Initial Island Setup
- [ ] Create new UEFN project → blank island template
- [ ] Set time-of-day: **Night or Dusk** (for neon aesthetic)
- [ ] Place 16 player spawn pads
- [ ] Enable team assignment (2–4 teams, auto-assign)

### 2. Core Spawning Devices

#### CommonSpawners — `[]item_spawner_device` (10–20)
- [ ] Place 10–20 Item Spawner devices across the main play area
- [ ] Assign item: **Phone prop** (or custom mesh)
- [ ] Settings: Spawn Delay = 0 (code-controlled), Item Picked Up Event = **Enabled**
- [ ] Spread evenly — don't cluster them

#### RareSpawners — `[]item_spawner_device` (3–5)
- [ ] Place 3–5 in semi-hidden or strategic spots
- [ ] Assign item: **Glowing phone / tablet** (different color than commons)
- [ ] Same settings as CommonSpawners

#### LegendarySpawners — `[]item_spawner_device` (1–2)
- [ ] Place 1–2 in hard-to-reach or contested spots
- [ ] Assign item: **Golden/holographic prop**
- [ ] Same settings

#### BossSpawners — `[]item_spawner_device` (3–4)
- [ ] Place 3–4 in dramatic or hidden locations
- [ ] Assign item: **Giant brain / trophy prop** ($10k value)
- [ ] Same settings

#### GoldenSpawners — `[]item_spawner_device` (2–3)
- [ ] Place 2–3 near the center of the map
- [ ] Assign item: **Golden brain prop** ($2.5k, Mega Moment exclusive)
- [ ] Same settings

### 3. Power-Up Spawners

#### ShieldSpawners — `[]item_spawner_device` (2–3)
- [ ] Place 2–3 in open areas (easy to spot)
- [ ] Assign item: **Shield orb / force-field token**
- [ ] Item Picked Up Event = Enabled

#### MagnetSpawners — `[]item_spawner_device` (2–3)
- [ ] Place 2–3 near dense spawn zones
- [ ] Assign item: **Magnet prop / spinning magnet token**
- [ ] Item Picked Up Event = Enabled

#### DoubleSpawners — `[]item_spawner_device` (2–3)
- [ ] Place 2–3 in risky or contested areas (risk = reward)
- [ ] Assign item: **Glowing "2X" orb**
- [ ] Item Picked Up Event = Enabled

### 4. Deposit Zone

#### DepositZone — `trigger_device` (1)
- [ ] Place at the **center of the map** (anchor point)
- [ ] Set trigger radius: **10 m** (large enough for easy entry)
- [ ] Agent Enters Event = Enabled
- [ ] Team: All teams allowed
- [ ] Add neon lights / particle beams for visibility

#### AutoCollectZones — `[]trigger_device` (1–4)
- [ ] Place 1–4 trigger zones near popular spawn areas
- [ ] Only active for players who've unlocked auto-collect (max mult tier)
- [ ] Trigger radius: 5–8 m

### 5. Upgrades

#### SpeedButtons — `[]button_device` (5)
- [ ] Place 5 buttons in a **row, left to right** (Tier 1 → Tier 5)
- [ ] Color progression: Green → Yellow → Orange → Red → Rainbow
- [ ] Interacted With Event = Enabled
- [ ] Place billboard above each with cost:

```
Button 1: "SPEED UP $500 🚀"
Button 2: "ZOOM $1,200 💨"
Button 3: "SONIC $3,000 ⚡"
Button 4: "FLASH $8,000 🔥"
Button 5: "LIGHTSPEED $20,000 🌟"
```

#### MultButtons — `[]button_device` (5)
- [ ] Place 5 buttons in a row (same layout as speed)
- [ ] Same color progression
- [ ] Billboard costs:

```
Button 1: "STONKS $1,000 📈"
Button 2: "MONEY PRINTER $2,500 💰"
Button 3: "WHALE $6,000 🐋"
Button 4: "CRYPTO KING $15,000 👑"
Button 5: "BILLIONAIRE $40,000 💎"
```

#### PrestigeButton — `button_device` (1)
- [ ] Place in a special elevated area (feels like an achievement to reach)
- [ ] Gold/star themed
- [ ] Billboard: "PRESTIGE — RESET FOR +50 % ⭐ ($100k)"

### 6. Movement Modulators (CRITICAL)

#### SpeedModulators — `[]movement_modulator_device` (16)
- [ ] Place exactly **16** Movement Modulator devices
- [ ] **Hide them** — underground, in the sky, or inside geometry
- [ ] Settings for ALL 16:
  - Speed Multiplier: **1.0** (code changes this)
  - Enabled on Start: **No**
  - Persistent: Yes
- [ ] **Assign in array order** — each one maps to a player slot

> ⚠️ **Why 16?** One dedicated modulator per player. Using a shared modulator was the #1 multiplayer bug in the original code.

### 7. UI Devices

#### Hud — `hud_message_device` (1)
- [ ] Place 1 HUD Message Device
- [ ] Position: Top-center recommended
- [ ] Text is set dynamically by code (shows currency, inventory, combos, power-ups)

#### IndividualLeaderboard — `leaderboard_device` (1)
- [ ] Title: "💰 Top Earners"
- [ ] Sort: High to Low
- [ ] Show top 10

#### TeamLeaderboard — `leaderboard_device` (1)
- [ ] Title: "🏆 Team Battle"
- [ ] Sort: High to Low

#### EventAnnouncer — `announcement_device` (1)
- [ ] Duration: 5 seconds
- [ ] Style: Large/Bold
- [ ] Sound: Enabled

### 8. Audio Devices (8 total)

#### PickupSFX — `[]sfx_device` (3–5)
- [ ] 3–5 SFX devices with different pickup sounds
- [ ] Volume: 0.5 (subtle, repeating frequently)
- [ ] Code plays a random one each pickup

#### Single SFX Devices (5)
| Device | Sound Style | Volume |
|--------|-------------|--------|
| `RareSFX` | Epic fanfare | 0.8 |
| `LegendarySFX` | Legendary fanfare | 1.0 |
| `GoldenSFX` | Magical chime | 0.8 |
| `DepositSFX` | Cash register | 0.6 |
| `UpgradeSFX` | Level-up / power-up | 0.7 |
| `EventSFX` | Air horn / alarm | 0.9 |
| `ComboSFX` | Combo riser / ding | 0.7 |

### 9. Visual Effects (12 slots)

| Device | Effect | Color | Notes |
|--------|--------|-------|-------|
| `RareVFX` | Particle burst | Purple/Pink | 2 s duration |
| `LegendaryVFX` | Big particle explosion | Gold/Rainbow | 3 s duration |
| `BossVFX` | Explosion + shockwave | Red/Orange | On boss spawn |
| `BossBeaconVFX` (3–4) | Vertical beam/pillar | Red | 1 per boss spawner (co-located) |
| `LegendaryBeaconVFX` (1–2) | Vertical beam/pillar | Gold | 1 per legendary spawner |
| `TrophyVFX` (3) | Trophy display | Bronze/Silver/Gold | Prestige showcase |
| `DepositVFX` | Vault door + coins | Gold | On deposit |
| `DepositLandmarkVFX` | Glowing pillar/ATM | Cyan | Always on, visible from far |
| `DeathVFX` | Scattered explosion | Red | On player death |
| `PrestigeCrownVFX` (3) | Crown/aura | Bronze/Silver/Gold | On player head/body |
| `DangerZones` (2–4) | Damage volume | Red glow | Active during viral events |
| `DepositVaultVFX` (3) | Prop swap | — | Crate → Safe → Fortress |

### 10. Power-Up VFX (3)

| Device | Effect | Notes |
|--------|--------|-------|
| `BountyCrownVFX` | Holographic crown | Follows bounty target |
| `ShieldVFX` | Bubble force-field | Around shielded player |
| `MagnetVFX` | Vortex/swirl aura | During magnet active |

### 11. Cinematic Sequences (2)

#### TutorialSequence — `cinematic_sequence_device`
- [ ] 15-second camera path: shows deposit zone → upgrade zone → play area
- [ ] Text overlays: "Pick up phones 📱" → "Deposit for CASH 💰" → "Buy upgrades 🚀"
- [ ] Auto-play: No (triggered by code for first-time players only)

#### SpectacleSequence — `cinematic_sequence_device`
- [ ] 5-second dramatic zoom/pan
- [ ] Effects: screen shake, particles
- [ ] Text: "MASSIVE EVENT!" with emojis
- [ ] Auto-play: No (triggered during viral events)

### 12. Persistence (6 Accolades)

#### PersistenceAccolades — `[]accolade_device` (6)

| Index | Name | XP | Triggers At |
|-------|------|----|-------------|
| 0 | "Brainrot Rookie" | 100 | $1k–$5k currency |
| 1 | "Brainrot Grinder" | 250 | $5k–$20k |
| 2 | "Brainrot Pro" | 500 | $20k–$50k |
| 3 | "Brainrot Elite" | 1000 | $50k–$100k |
| 4 | "Brainrot Legend" | 2000 | Prestige 1 |
| 5 | "Brainrot God" | 5000 | Prestige 2+ |

---

## 🔗 Verse Device Assignment

After placing all devices, select the Verse device in the Outliner and assign every property:

### CRITICAL (Game won't start without)
```
CommonSpawners    → All 10–20 common item spawners
SpeedModulators   → All 16 modulators (IN ORDER!)
DepositZone       → Trigger device
Hud               → HUD message device
```

### REQUIRED (Core features)
```
SpeedButtons      → 5 speed buttons (Tier 1–5 IN ORDER!)
MultButtons       → 5 mult buttons (Tier 1–5 IN ORDER!)
PrestigeButton    → Prestige button
IndividualLeaderboard → Leaderboard #1
TeamLeaderboard   → Leaderboard #2
EventAnnouncer    → Announcement device
```

### IMPORTANT (Gameplay systems)
```
RareSpawners      → 3–5 rare spawners
LegendarySpawners → 1–2 legendary spawners
BossSpawners      → 3–4 boss spawners
GoldenSpawners    → 2–3 golden spawners
ShieldSpawners    → 2–3 shield pickup spawners
MagnetSpawners    → 2–3 magnet pickup spawners
DoubleSpawners    → 2–3 double pickup spawners
AutoCollectZones  → 1–4 auto-collect triggers
DangerZones       → 2–4 damage volumes
```

### AUDIO (All SFX)
```
PickupSFX         → 3–5 pickup sound devices
RareSFX           → Rare sound
LegendarySFX      → Legendary sound
GoldenSFX         → Golden brain sound
DepositSFX        → Deposit sound
UpgradeSFX        → Upgrade sound
EventSFX          → Event alert sound
ComboSFX          → Combo tier-up sound
```

### VISUAL EFFECTS
```
BossVFX               → Boss spawn VFX
RareVFX               → Rare pickup VFX
LegendaryVFX          → Legendary pickup VFX
BossBeaconVFX         → 3–4 beacon pillars (at boss spawners)
LegendaryBeaconVFX    → 1–2 beacon pillars (at legendary spawners)
TrophyVFX             → 3 trophy displays (bronze/silver/gold)
DepositVFX            → Deposit zone effect
DepositLandmarkVFX    → Deposit landmark glow
DeathVFX              → Death explosion
PrestigeCrownVFX      → 3 crown/aura effects
DepositVaultVFX       → 3 vault props (crate/safe/fortress)
BountyCrownVFX        → Bounty target crown
ShieldVFX             → Shield bubble
MagnetVFX             → Magnet vortex
```

### PERSISTENCE & TUTORIAL
```
PersistenceAccolades  → 6 accolade devices (IN ORDER!)
TutorialSequence      → Tutorial cinematic
SpectacleSequence     → Event cinematic
```

---

## ✅ Testing Checklist

### Solo Test
- [ ] Console shows "🧠 BRAINROT RUSH LOADED!"
- [ ] Pick up common item → HUD updates, SFX plays
- [ ] Enter deposit zone → currency increases, SFX plays
- [ ] Buy Speed Tier 1 → movement faster
- [ ] Buy Mult Tier 1 → next deposit worth more
- [ ] Collect 5 items fast → combo appears in HUD
- [ ] Wait 5 min → Mega Moment event fires
- [ ] Wait 7.5 min → Boss spawn + beacon VFX
- [ ] Wait 10 min → Viral Flood event
- [ ] Pick up Shield/Magnet/Double → power-up icon in HUD

### Multiplayer Test (4+ players)
- [ ] Each player's speed is independent (no modulator conflicts)
- [ ] Leaderboards update for both individual & team
- [ ] Bounty crown appears on richest player
- [ ] Kill bounty target → currency transfer
- [ ] Rare/legendary announcements visible to all
- [ ] Team totals trigger vault evolution

### Performance Test (16 players, 30 min)
- [ ] Stable 60 fps
- [ ] No console errors
- [ ] Items despawn properly (no map clutter)
- [ ] Players joining/leaving don't cause issues

---

## 🐛 Troubleshooting

| Problem | Likely Cause | Fix |
|---------|-------------|-----|
| Game doesn't start | Missing critical devices | Check console, assign CommonSpawners + SpeedModulators + DepositZone + Hud |
| Speed not changing | Modulator issue | Verify all 16 assigned in array, Enabled on Start = No |
| No items spawning | Spawner config | Check item spawner has item assigned, "Item Picked Up Event" enabled |
| HUD shows $0 | Normal at start | Pick up + deposit to see currency |
| Can't buy upgrades | Button config | Check "Interacted With Event" enabled, verify you have enough currency |
| Events never trigger | Timer not elapsed | Wait full interval (5/10 min), check EventAnnouncer assigned |
| No boss spawns | BossSpawners empty | Assign 3–4 boss spawners |
| Power-ups not working | Spawners unassigned | Assign ShieldSpawners, MagnetSpawners, DoubleSpawners |

---

> **Next**: [Map Design](MAP_DESIGN_GUIDE.md) → [Balancing](BALANCING_GUIDE.md) → [Game Flow](GAME_FLOW.md)
