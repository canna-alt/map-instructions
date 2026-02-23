# 📊 BALANCING REFERENCE

All 78 tunable constants and their gameplay impact.

> **Navigation**: [README](README.md) | [Quick Start](QUICK_START.md) | [Device Setup](DEVICE_SETUP_GUIDE.md) | **Balancing** | [Game Flow](GAME_FLOW.md) | [Map Design](MAP_DESIGN_GUIDE.md) | [Project Summary](PROJECT_SUMMARY.md) | [Improvements](IMPROVEMENTS.md)

---

## 💰 Currency Values

| Item Type | Base Value | With Prestige Lv1 (1.5×) | With Prestige Lv2 (2.0×) |
|-----------|------------|---------------------------|---------------------------|
| Common (each) | $10 | $15 | $20 |
| Rare (instant) | $1,000 | $1,500 | $2,000 |
| Legendary (instant) | $5,000 | $7,500 | $10,000 |
| Golden Brain (instant) | $2,500 | $3,750 | $5,000 |
| Boss (instant) | $10,000 | $15,000 | $20,000 |

### Deposit Formula
```
BaseGain = Items × $10 × MultTier × PrestigeBonus × ComboBonus
         × StreakBonus × TeamComboBonus × LuckyMultiplier
AfterDouble = BaseGain × (2 if Double active, else 1)
AfterChallenge = CheckMiniChallengeDeposit(AfterDouble)  # ×3 if deposit-rush active
FinalGain = ApplyEventMultiplier(AfterChallenge)
```

### Example
- 10 items, Mult Tier 3 (3×), Prestige Lv1 (1.5×), Combo Tier 2 (2.0×), Streak 5 (+50%), Team Combo (+25%)
- Base: 10 × $10 × 3 × 1.5 × 2.0 × 1.5 × 1.25 = $1,687
- During Mega Moment (3×): $5,062
- With Double + Deposit Rush (3×): $30,375

---

## 🚀 Speed Upgrade Tiers

| Tier | Cost | Speed | Total Cost to Tier | ROI Break-even |
|------|------|-------|-------------------|----------------|
| 1 | $500 | 1.2× | $500 | ~50 items faster |
| 2 | $1,200 | 1.5× | $1,700 | ~120 items |
| 3 | $3,000 | 2.0× | $4,700 | ~300 items |
| 4 | $8,000 | 2.5× | $12,700 | ~800 items |
| 5 | $20,000 | 3.0× | $32,700 | ~2,000 items |

## 📈 Multiplier Upgrade Tiers

| Tier | Cost | Mult | Example Deposit (10 items) | Total Cost to Tier |
|------|------|------|---------------------------|-------------------|
| 1 | $1,000 | 1.5× | $150 | $1,000 |
| 2 | $2,500 | 2.0× | $200 | $3,500 |
| 3 | $6,000 | 3.0× | $300 | $9,500 |
| 4 | $15,000 | 5.0× | $500 | $24,500 |
| 5 | $40,000 | 10.0× | $1,000 | $64,500 |

**Total cost to max both**: $97,200

---

## ⭐ Prestige System

| Prestige Lv | Cost | Permanent Bonus (additive) | Cumulative | Inventory Cap | Death Penalty |
|-------------|------|---------------------------|------------|---------------|---------------|
| 0 (Start) | — | 1.0× | 1.0× | 50 | 40% |
| 1 | $100k | +50% | 1.5× | 60 | 35% |
| 2 | $200k | +50% | 2.0× | 70 | 30% |
| 3 | $300k | +50% | 2.5× | 80 | 25% |
| 4 | $400k | +50% | 3.0× | 90 | 20% |
| 5 | $500k | +50% | 3.5× | 100 | 15% |

Formula: `PermanentBonus = 1.0 + (PrestigeLevel × 0.5)` (additive, not multiplicative)
Cost formula: `PRESTIGE_COST × (CurrentPrestige + 1)` — scales per level

**Resets on prestige**: Currency, speed tier, mult tier, collected items, speed modulators, deposit streak
**Persists**: Prestige level, permanent bonus, accolade progress

---

## ⏱️ Spawn & Event Timings

### Spawning
| Constant | Value | Notes |
|----------|-------|-------|
| `COMMON_SPAWN_INTERVAL` | 8.0 s | Base spawn cycle |
| `COMMON_SPAWN_CHANCE` | 0.6 (60%) | Per spawner per cycle (scaled by player count) |
| `RARE_CHANCE` | 0.035 (3.5%) | Single random spawner per cycle |
| `LEGENDARY_CHANCE` | 0.015 (1.5%) | Single random spawner per cycle |

### Events
| Constant | Value | Notes |
|----------|-------|-------|
| `MEGA_MOMENT_INTERVAL` | 300.0 s (5 min) | 3× earnings for 30 s |
| `MEGA_MOMENT_DURATION` | 30.0 s | |
| `MEGA_MOMENT_MULTIPLIER` | 3.0× | |
| `VIRAL_EVENT_INTERVAL` | 600.0 s (10 min) | Burst floods + 2× |
| `VIRAL_EVENT_DURATION` | 20.0 s | 2× earnings window |
| `VIRAL_EVENT_MULTIPLIER` | 2.0× | |
| `VIRAL_BURST_SPAWN_CHANCE` | 0.3 (30%) | Per spawner per burst tick |
| `BOSS_SPAWN_INTERVAL` | 450.0 s (7.5 min) | $10k boss item |
| `PHOTO_FINISH_TIME` | 1200.0 s (20 min) | Session timer triggers at 19 min |
| `PHOTO_FINISH_DURATION` | 60.0 s | |
| `PHOTO_FINISH_MULTIPLIER` | 5.0× | |

### Cleanup (Split Despawn Timers)
| Constant | Value | Notes |
|----------|-------|-------|
| `ITEM_DESPAWN_INTERVAL` | 90.0 s | Cycles standard spawners (batched) |
| `BOSS_DESPAWN_INTERVAL` | 180.0 s (3 min) | Boss items persist longer |
| `POWERUP_DESPAWN_INTERVAL` | 60.0 s (1 min) | Power-ups cycle faster |

---

## 🎲 Lucky Drops

| Constant | Value | Notes |
|----------|-------|-------|
| `LUCKY_2X_CHANCE` | 0.05 (5%) | 2× value on any pickup/deposit |
| `LUCKY_5X_CHANCE` | 0.005 (0.5%) | 5× value |
| `LUCKY_10X_CHANCE` | 0.0005 (0.05%) | 10× JACKPOT |

Applied via `GetLuckyMultiplier()` on every rare/legendary/boss/golden pickup and on deposits.

---

## ⏳ AFK Detection

| Constant | Value | Notes |
|----------|-------|-------|
| `AFK_WARNING_TIME` | 120.0 s (2 min) | First warning message |
| `AFK_PENALTY_TIME` | 180.0 s (3 min) | Lose 10% of held items |
| `AFK_CHECK_INTERVAL` | 30.0 s | Loop check frequency |

Activity is tracked on every pickup and deposit via `LastActivityTime`.

---

## 🎯 Mini-Challenges

| Constant | Value | Notes |
|----------|-------|-------|
| `MINI_CHALLENGE_INTERVAL` | 120.0 s (2 min) | New challenge issued |
| `MINI_CHALLENGE_COLLECT_TARGET` | 10 | Items to collect |
| `MINI_CHALLENGE_COLLECT_TIME` | 15.0 s | Time limit for collect challenge |
| `MINI_CHALLENGE_COLLECT_REWARD` | $5,000 | Reward for completing |
| `MINI_CHALLENGE_DEPOSIT_TIME` | 8.0 s | Time limit for deposit-rush |
| `MINI_CHALLENGE_DEPOSIT_MULT` | 3.0× | Deposit multiplier bonus |

Only issued to active (non-AFK) players. 50/50 chance of collect vs deposit-rush.

---

## 💵 Passive Income

| Constant | Value | Notes |
|----------|-------|-------|
| `PASSIVE_INCOME_TIER_1` | $35,000 | Unlock $10/sec |
| `PASSIVE_INCOME_RATE_1` | 10 | $/sec rate at tier 1 |
| `PASSIVE_INCOME_TIER_2` | $100,000 | Unlock $25/sec |
| `PASSIVE_INCOME_RATE_2` | 25 | $/sec rate at tier 2 |
| `PASSIVE_INCOME_INTERVAL` | 1.0 s | Award frequency |

Recalculated on every deposit. Shown in HUD as "+$N/s".

---

## 🤝 Team Combo

| Constant | Value | Notes |
|----------|-------|-------|
| `TEAM_COMBO_WINDOW` | 10.0 s | Window after teammate deposits |
| `TEAM_COMBO_BONUS` | 0.25 (+25%) | Bonus applied to your deposit |

---

## 👊 Revenge Mechanic

| Constant | Value | Notes |
|----------|-------|-------|
| `REVENGE_DURATION` | 15.0 s | Boost duration after death |
| `REVENGE_MULTIPLIER` | 2.0× | Collection multiplier during revenge |

Stacks with combo system. Shown in HUD as countdown timer.

---

## 📢 Announcement Cooldown

| Constant | Value | Notes |
|----------|-------|-------|
| `ANNOUNCEMENT_COOLDOWN` | 1.5 s | Min gap between global announcements |

---

## 🔥 Combo System

| Constant | Value | Notes |
|----------|-------|-------|
| `COMBO_WINDOW` | 3.0 s | Time between pickups to maintain combo |
| `COMBO_THRESHOLD` | 5 | Items needed per combo tier |
| `COMBO_BONUS` | 0.5 (+50%) | Bonus per tier |
| `MAX_COMBO_TIER` | 3 | Max 3 tiers (+150% total) |

| Tier | Items Needed | Deposit Bonus |
|------|-------------|---------------|
| 0 | 0–4 | +0% |
| 1 | 5–9 | +50% |
| 2 | 10–14 | +100% |
| 3 | 15+ | +150% |

Combo resets on deposit or on timeout (>3 s between pickups).

---

## 👑 Bounty System

| Constant | Value | Notes |
|----------|-------|-------|
| `BOUNTY_CHECK_INTERVAL` | 30.0 s | Re-evaluate bounty target |
| `BOUNTY_KILL_BONUS` | 0.5 (50%) | % of target's currency stolen on kill |
| `BOUNTY_MIN_CURRENCY` | 10,000 | Minimum to become a target |

The richest player above $10k gets a holographic crown VFX. Killing the bounty yields 50% of their currency (vs 25% for normal kills via death penalty).

---

## 🛡️ Power-Ups

### Shield
- Blocks 1 death (no item loss, no death penalty)
- Consumed on hit
- Spawns periodically via `ShieldSpawners`

### Magnet
| Constant | Value | Notes |
|----------|-------|-------|
| `MAGNET_DURATION` | 10.0 s | Active time |
| `MAGNET_COLLECT_INTERVAL` | 1.0 s | Tick rate |
| `MAGNET_COLLECT_AMOUNT` | 3 | Items collected per tick |

Total auto-collected: ~30 items over 10 seconds.

### Double
- Next deposit is 2× value
- Consumed on next deposit
- Stacks with all other multipliers

---

## 🏗️ Deposit Vault Evolution

| Constant | Value | Visual |
|----------|-------|--------|
| Start | — | Wooden Crate |
| `DEPOSIT_VAULT_TIER_1` | $25,000 team total | Steel Safe |
| `DEPOSIT_VAULT_TIER_2` | $75,000 team total | Golden Fortress |

Vault VFX swaps happen live as team currency crosses thresholds.

---

## ⚔️ Risk & Penalty

| Constant | Value | Notes |
|----------|-------|-------|
| `DEATH_PENALTY` | 0.4 (40%) | % of held items lost on death |
| `DEPOSIT_STREAK_BONUS` | 0.1 (+10%) | Per consecutive deposit without dying |
| `MAX_DEPOSIT_STREAK` | 10 | Cap at +100% |
| `INVENTORY_WARNING_PERCENT` | 0.8 (80%) | HUD warns at 80% capacity |
| `MAX_ITEMS_HELD` | 50 | Base cap (scales with prestige) |
| `LATE_JOIN_BONUS_PER_MIN` | $50 | Catch-up currency per min elapsed |

---

## 🎚️ Player Scaling

| Constant | Value | Notes |
|----------|-------|-------|
| `BASE_PLAYER_COUNT` | 8 | Baseline for spawn tuning |
| `MIN_SPAWN_MULTIPLIER` | 0.5 | Solo play spawn rate |
| `MAX_SPAWN_MULTIPLIER` | 2.0 | Full lobby (16 players) |

Formula: `SpawnMult = clamp(PlayerCount / 8, 0.5, 2.0)`

---

## 🔒 Anti-Exploit & Throttle

| Constant | Value | Notes |
|----------|-------|-------|
| `PURCHASE_COOLDOWN` | 0.5 s | Between upgrade purchases |
| `DEPOSIT_COOLDOWN` | 0.3 s | Between deposits |
| `AUTO_COLLECT_COOLDOWN` | 3.0 s | Auto-collect zone re-trigger |
| `MAX_CURRENCY` | 999,999 | Hard cap |
| `CURRENCY_CAP_WARNING` | 950,000 | Warn at 95% |
| `HUD_UPDATE_INTERVAL` | 0.15 s | Throttle HUD refreshes |
| `LEADERBOARD_UPDATE_INTERVAL` | 2.0 s | Throttle leaderboard writes |
| `TEAM_ANNOUNCEMENT_THROTTLE` | 0.5 s | Prevent notification spam |
| `FEEDBACK_DURATION` | 2.5 s | How long feedback msgs hold |
| `DEBUG_MODE` | false | Toggle verbose logging |

---

## 🎮 Optimal Progression Path

### Session 1 (New Player, 20 min)
| Time | Action | Earnings |
|------|--------|----------|
| 0–5 min | Collect commons, learn deposit | ~$500–800 |
| 5 min | **Buy Speed Tier 1** ($500) | |
| 5–10 min | Faster collecting + Mega Moment | ~$1,200–1,500 |
| 10 min | **Buy Mult Tier 1** ($1,000) + Viral Flood boost | |
| 10–15 min | Push tiers, chase rares/boss | ~$2,000–3,000 |
| 15 min | **Buy Speed Tier 2** ($1,200) | |
| 15–20 min | Mega + Photo-Finish (5×) | ~$3,000–5,000 |
| **End** | Total: ~$8k–12k | Speed 2, Mult 1 |

### Session 2+ (Returning Player)
- Starts with saved progress + catch-up bonus
- Can reach Speed 3 + Mult 2–3 in one session
- Chase prestige at $100k over 3–5 sessions

### Post-Prestige
- 1.5× permanent bonus makes everything faster
- Each prestige cycle takes fewer sessions
- Endgame: Speed 5 + Mult 5 reached in minutes, $50k+ per session

---

## 🎯 Player Archetypes

| Archetype | Priority | Play Style |
|-----------|----------|------------|
| **Grinder** | Speed > Mult | Never stops, frequent deposits |
| **Efficiency Expert** | Mult > Speed | Large batch deposits, combo focus |
| **Hunter** | Speed for mobility | Patrols rare/boss/legendary spawns |
| **Competitor** | Adaptive | Watches leaderboard, targets bounty |
| **Power-Up Specialist** | Magnet + Double | Combo magnet collection into double deposits |

---

## 🔧 Tuning Knobs (Post-Launch)

### To increase session length
- ⬆️ Increase upgrade costs
- ⬇️ Reduce spawn interval (8 s → 6 s)
- ⬇️ Reduce event intervals

### To reduce grind feel
- ⬇️ Reduce upgrade costs
- ⬆️ Increase rare/legendary chance
- ⬆️ Increase common value ($10 → $15)

### To boost viral moments
- ⬆️ Increase event multipliers
- ⬆️ More VFX / bigger announcements
- ⬇️ Reduce boss interval (spawn more often)

### To improve retention
- ⬆️ Increase prestige bonus (50% → 75%)
- ⬆️ More prestige perks
- Add daily rewards (external device)

---

> **Next**: [Game Flow](GAME_FLOW.md) | [Improvements](IMPROVEMENTS.md) | [Project Summary](PROJECT_SUMMARY.md)

---

**Last Updated**: February 2026
**Balance Philosophy**: Reward active play, create viral moments, provide long-term goals
