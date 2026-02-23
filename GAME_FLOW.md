# 🎮 GAME FLOW DIAGRAM

> **Navigation**: [README](README.md) | [Quick Start](QUICK_START.md) | [Device Setup](DEVICE_SETUP_GUIDE.md) | [Balancing](BALANCING_GUIDE.md) | **Game Flow** | [Map Design](MAP_DESIGN_GUIDE.md) | [Project Summary](PROJECT_SUMMARY.md) | [Improvements](IMPROVEMENTS.md)

## Player Journey Map

```
┌─────────────────────────────────────────────────────────────┐
│                      PLAYER JOINS GAME                       │
└─────────────────────────────┬───────────────────────────────┘
                              │
                ┌─────────────▼────────────┐
                │  First Time Player?      │
                └──────────┬───────┬───────┘
                     YES ──┘       └── NO
                      │                 │
            ┌─────────▼──────┐   ┌──────▼──────────────┐
            │ FULL TUTORIAL  │   │ ABBREVIATED TUTORIAL │
            │ (15s cinematic)│   │ (quick refresher)    │
            └─────────┬──────┘   └──────┬──────────────┘
                      │                 │
                      └────────┬────────┘
                               │
                    ┌──────────▼───────────┐
                    │ Load Saved Progress  │
                    │ + Late-Join Bonus    │
                    │ ($50/min elapsed)    │
                    └──────────┬───────────┘
                               │
┌──────────────────────────────▼────────────────────────────────┐
│                       CORE GAMEPLAY LOOP                       │
│                        (Every 8 seconds)                       │
└────────────────────────────────────────────────────────────────┘
                               │
         ┌─────────────────────┼─────────────────────┐
         │                     │                     │
┌────────▼───────┐   ┌────────▼────────┐   ┌────────▼────────┐
│ COMMON SPAWNS  │   │  RARE SPAWNS    │   │ LEGENDARY/BOSS  │
│ (Every 8s)     │   │  (3.5% chance)  │   │ GOLDEN SPAWNS   │
│ Value: $10 ea  │   │  Value: $1,000  │   │ $2.5k–$10k     │
└────────┬───────┘   └────────┬────────┘   └────────┬────────┘
         │                     │                     │
         └─────────────────────┼─────────────────────┘
                               │
                    ┌──────────▼───────────┐
                    │  PLAYER COLLECTS     │
                    │  Items: +1 count     │
                    │  Combo check         │
                    │  HUD updates         │
                    │  Power-up check      │
                    └──────────┬───────────┘
                               │
               ┌───────────────┼───────────────┐
               │               │               │
     ┌─────────▼─────┐ ┌──────▼──────┐ ┌──────▼──────────┐
     │Keep Collecting │ │Enter Deposit│ │Pick Up Power-Up │
     │(build stack +  │ │Zone         │ │🛡️ Shield        │
     │ combo)         │ │             │ │🧲 Magnet        │
     └─────────┬──────┘ └──────┬──────┘ │×2 Double        │
               │               │        └──────┬──────────┘
               │      ┌────────▼────────┐      │
               │      │ DEPOSIT & EARN  │      │
               │      │ $= Items × $10  │      │
               │      │  × Multiplier   │      │
               │      │  × Prestige     │      │
               │      │  × Combo        │      │
               │      │  × Event Mult   │      │
               │      │  × Streak       │      │
               │      │  × Double(if 2×)│      │
               │      └────────┬────────┘      │
               │               │               │
               └───────────────┼───────────────┘
                               │
┌──────────────────────────────▼────────────────────────────────┐
│                      UPGRADE DECISIONS                         │
└────────────────────────────────────────────────────────────────┘
              ┌────────────────┼────────────────┐
              │                │                │
    ┌─────────▼──────┐ ┌──────▼───────┐ ┌──────▼───────┐
    │ SPEED UPGRADE  │ │ MULT UPGRADE │ │  PRESTIGE    │
    │ 5 Tiers        │ │ 5 Tiers      │ │  (Reset+50%) │
    │ $500 → $20k    │ │ $1k → $40k   │ │  Cost: $100k │
    │ 1.2× → 3.0×   │ │ 1.5× → 10×   │ │  Unlocks:    │
    └────────────────┘ └──────────────┘ │  +Inv cap    │
                                        │  -Death pen  │
                                        │  +AutoCollect│
                                        └──────────────┘
```

---

## 7 → 12 Concurrent Async Loops

```
LOOP                    INTERVAL       WHAT IT DOES
─────────────────────────────────────────────────────────────────
SpawnLoop               8 seconds      Spawns commons, checks rare/legendary
MegaMomentLoop          5 minutes      3× earnings + golden brains for 30s
ViralEventLoop          10 minutes     Burst flood spawns + 2× earnings 20s
BossSpawnLoop           7.5 minutes    $10k boss item + beacon VFX
SessionTimerLoop        20 min total   Photo-Finish at 19min, EndGame at 20min
ItemDespawnLoop         90 seconds     Batched disable/enable of standard spawners
BossDespawnLoop         3 minutes      Separate longer cycle for boss items
PowerUpDespawnLoop      1 minute       Faster cycle for shield/magnet/double spawners
BountyCheckLoop         30 seconds     Updates bounty target (richest player)
AFKCheckLoop            30 seconds     Warns at 2min idle, penalizes at 3min
PassiveIncomeLoop       1 second       Awards $/sec to qualifying players
MiniChallengeLoop       2 minutes      Issues random timed challenges to active players
```

All loops check `if (GameEnded): return` to stop cleanly.

---

## Event Timeline (20-Minute Session)

```
MIN  EVENT                         EFFECT
───  ─────────────────────────     ──────────────────────────────
0:00 Player joins                  Tutorial + load progress
     SpawnLoop starts              Commons every 8s
     BountyCheckLoop starts        Target evaluation every 30s
     ItemDespawnLoop starts        Cleanup every 90s

1:30 ─── Despawn cycle #1 ───     Clears uncollected items

3:00 ─── Despawn cycle #2 ───

5:00 ⚡ MEGA MOMENT               3× earnings for 30s
     Golden brains spawn            $2.5k each

7:30 🏆 BOSS SPAWN                $10k boss item + beacon

10:00 🌊 VIRAL FLOOD              Burst waves + 2× earnings 20s
      ⚡ MEGA MOMENT #2            (may overlap with flood)

15:00 ⚡ MEGA MOMENT #3
      🏆 BOSS SPAWN #2

19:00 🏁 PHOTO-FINISH             5× earnings for 60s
      FINAL RUSH                    Everyone scrambles

20:00 🎉 END GAME                 Winner announced
      All spawners disabled         Session stats shown
      All power-ups cleared         Progress saved
      Leaderboard finalized
```

---

## Active Systems Per Player

### Always Running
```
├── HUD Updates (throttled to 0.15s)
├── Leaderboard Updates (throttled to 2s)
├── Inventory Cap Check (50 + prestige bonus)
├── Combo Timer (3s window)
└── Bounty Target Status
```

### On Player Action
```
├── Item Pickup → +1 item, combo update, HUD refresh, SFX, AFK activity reset
│   └── Lucky Drop Roll → 5% for 2×, 0.5% for 5×, 0.05% for 10× value
├── Common Pickup → +1 item, revenge boost check (2× if active), mini-challenge check
├── Rare Pickup → $1k× lucky mult instant, announcement (with cooldown), beacon VFX
├── Legendary Pickup → $5k× lucky mult instant, announcement, beacon VFX
├── Boss Pickup → $10k× lucky mult instant, announcement
├── Golden Pickup → $2.5k× lucky mult instant, announcement
├── Shield Pickup → ShieldActive = true, 🛡️ in HUD
├── Magnet Pickup → 10s auto-collect loop starts, 🧲 in HUD
├── Double Pickup → DoubleNextDeposit = true, ×2 in HUD
├── Deposit → Convert items × all multipliers + team combo + lucky + mini-challenge
│   ├── Record team deposit time (for team combo window)
│   ├── Update passive income rate
│   └── Check deposit-rush mini-challenge (3× bonus if active)
├── Upgrade → Apply effect, deduct cost, SFX
├── Prestige → Reset + additive bonus (+50%/level), stats shown, speed reset
├── Death → 40% item loss (blocked if shield), revenge boost activated (2× for 15s)
├── Kill Bounty → 50% currency steal
├── Mini-Challenge Issued → Collect 10 in 15s ($5k) or deposit-rush in 8s (3×)
└── AFK → Warning at 2min, -10% items at 3min
```

---

## Deposit Value Formula

```
BaseGain = Items × $10 × MultiplierTier × PrestigeBonus × ComboBonus
         × DepositStreakBonus × TeamComboBonus × LuckyMultiplier

AfterDouble = BaseGain × (2 if DoubleNextDeposit active, else 1)

AfterMiniChallenge = AfterDouble × (3 if deposit-rush challenge active, else 1)

FinalGain = ApplyEventMultiplier(AfterMiniChallenge)

Where:
  MultiplierTier   = 1.0 / 1.5 / 2.0 / 3.0 / 5.0 / 10.0
  PrestigeBonus    = 1.0 + (PrestigeLevel × 0.5)  → 1.0, 1.5, 2.0, 2.5, 3.0...
  ComboBonus       = 1.0 + (ComboTier × 0.5)       → 1.0, 1.5, 2.0, 2.5
  StreakBonus       = 1.0 + min(DepositStreak × 10%, 100%)
  TeamComboBonus   = 1.25 if teammate deposited within 10s, else 1.0
  LuckyMultiplier  = 1 (95%), 2 (5%), 5 (0.5%), 10 (0.05%)
  EventMult        = 3× during Mega, 5× during Photo-Finish, 2× during Viral
```

---

## Player Progression State Machine

```
[JOIN] → [Tutorial/Load] → [Collecting] ⟷ [Depositing]
                               ↕                ↕
                         [Upgrade Shop]    [Check Prestige]
                               ↕                ↕
              [Tier 1] → [Tier 2] → ... → [Tier 5 Max]
                                                ↓
                                        [Reach $100k]
                                                ↓
                                          [PRESTIGE]
                                                ↓
                                  [Restart with +50% bonus]
                                  [Higher inv cap, less death pen]
                                                ↓
                                        [Climb faster]
```

---

## Decision Tree: What Should I Do?

```
┌─ Do I have items collected?
│
├─ NO → Patrol spawn points, grab everything
│
└─ YES → How full is my inventory?
    │
    ├─ < 50% → Keep collecting (build combo)
    │
    ├─ 50-80% → Decision point
    │   ├─ Near deposit? → DEPOSIT NOW (lock in streak)
    │   ├─ Combo active? → Keep going (maximize bonus)
    │   └─ Bounty on me? → DEPOSIT ASAP (reduce steal risk)
    │
    └─ > 80% (warning shown) → HEAD TO DEPOSIT IMMEDIATELY
        └─ At 100% → Can't pick up more, MUST deposit

┌─ I just deposited. Now what?
│
├─ Can afford upgrade? → BUY (Speed early, Mult mid-game)
├─ Have $100k+? → Consider PRESTIGE
├─ Power-up nearby? → Grab it (shield = safety, magnet = efficiency)
├─ Boss/rare beacon visible? → CHASE IT
└─ Nothing special → Back to collecting
```

---

## Player Psychology Map

```
Emotion              Design Element
─────────────────────────────────────────────────────────────
😊 Fun               Core collecting loop + combo system
🎯 Achievement       Tiered upgrades (clear goals) + mini-challenges
🤩 Excitement        Rare/legendary/boss spawns + lucky drop jackpots
😮 Surprise          Random event timing + lucky 10× drops + mini-challenges
🏆 Competition       Leaderboards + bounty system + end-game awards
💪 Progression       Prestige system + vault evolution + passive income
🎉 Spectacle         Viral events + announcements + VFX
👥 Social            Team combo deposits + public callouts + team scoring
😌 Satisfaction      Audio/visual feedback on every action
🔄 Return Incentive  Saved progress + prestige bonuses
😰 Tension           Death penalty + bounty target fear + AFK warnings
🛡️ Relief            Shield power-up + streak protection
😤 Comeback          Revenge boost after death (2× for 15s)
🤝 Teamwork          Team combo bonus (+25%) + team deposit window

---

> **Next**: [Improvements](IMPROVEMENTS.md) | [Project Summary](PROJECT_SUMMARY.md) | [Quick Start](QUICK_START.md)
```
