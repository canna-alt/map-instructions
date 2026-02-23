# 🚀 QUICK START GUIDE

> **Navigation**: [README](README.md) | **Quick Start** | [Device Setup](DEVICE_SETUP_GUIDE.md) | [Balancing](BALANCING_GUIDE.md) | [Game Flow](GAME_FLOW.md) | [Map Design](MAP_DESIGN_GUIDE.md) | [Project Summary](PROJECT_SUMMARY.md) | [Improvements](IMPROVEMENTS.md)

Get Brainrot Rush up and running in UEFN in under 1 hour (minimum viable game).

---

## ⚡ Express Setup (30–60 min Minimum Viable Game)

### Step 1: Create UEFN Project (2 min)
1. Open UEFN Editor
2. Create new project: **"Brainrot Rush"**
3. Choose **blank island** template
4. Set time-of-day to **Night** or **Dusk** (neon aesthetic)

### Step 2: Place Essential Devices (20 min)

#### Absolute Minimum (Game won't run without these)
```
✅ 10× Item Spawner Device         → CommonSpawners
✅ 16× Movement Modulator Device   → SpeedModulators (hide underground)
✅  1× Trigger Device               → DepositZone (10 m radius, center of map)
✅  1× HUD Message Device           → Hud
```

#### Core Gameplay
```
✅  5× Button Device                → SpeedButtons (in a row, tiers 1–5)
✅  5× Button Device                → MultButtons (in a row, tiers 1–5)
✅  1× Button Device                → PrestigeButton (gold/star themed)
✅  1× Leaderboard Device           → IndividualLeaderboard
✅  1× Announcement Device          → EventAnnouncer
```

#### Polish (Recommended)
```
⭐  3× Item Spawner Device         → RareSpawners
⭐  3× SFX Device                   → PickupSFX
⭐  1× SFX Device                   → DepositSFX
⭐  1× SFX Device                   → EventSFX
⭐  1× Leaderboard Device           → TeamLeaderboard
```

### Step 3: Configure Movement Modulators (5 min)
All 16 must have identical settings:
- Speed Multiplier: **1.0**
- Enabled on Start: **No**
- Persistent: **Yes**
- **Hide them** underground or behind walls

### Step 4: Add Verse Code (5 min)
1. In UEFN, create a **Verse device**
2. Copy all code from `BrainrotRush.verse`
3. Paste into the device
4. Save and compile

### Step 5: Assign Devices (10 min)
Select the Verse device in the Outliner → Details panel:

| Property | Assign To |
|----------|-----------|
| `CommonSpawners` | All 10 item spawners |
| `SpeedModulators` | All 16 modulators **IN ORDER** |
| `DepositZone` | Trigger device |
| `Hud` | HUD device |
| `SpeedButtons` | 5 speed buttons **LEFT-TO-RIGHT** |
| `MultButtons` | 5 mult buttons **LEFT-TO-RIGHT** |
| `PrestigeButton` | Gold button |
| `IndividualLeaderboard` | Leaderboard |
| `EventAnnouncer` | Announcement device |

### Step 6: Test (3 min)
1. Click **"Launch Session"** in UEFN
2. Check console for **"🧠 BRAINROT RUSH LOADED!"**
3. Pick up phone → HUD updates
4. Enter deposit zone → currency appears
5. Buy Speed Tier 1 → move faster

### ✅ If that works: you have a playable game! Now add polish + publish.

---

## 📋 Full Production Checklist

### Phase 1: Core (30–60 min)
- [ ] Project created, island template set
- [ ] 16 movement modulators placed + hidden
- [ ] 10–20 common spawners distributed across map
- [ ] 5 speed buttons + 5 mult buttons + 1 prestige button
- [ ] Deposit zone placed at center
- [ ] HUD + Leaderboard + Announcer placed
- [ ] Verse code added, all critical devices assigned
- [ ] Basic test passed

### Phase 2: Spawning Variety (20–30 min)
- [ ] 3–5 rare spawners in strategic spots
- [ ] 1–2 legendary spawners in contested areas
- [ ] 3–4 boss spawners in hidden/dramatic locations
- [ ] 2–3 golden spawners near center
- [ ] 2–3 shield / magnet / double spawners
- [ ] All spawners assigned in Verse device

### Phase 3: Audio/Visual (30–45 min)
- [ ] 3–5 pickup SFX devices (variety)
- [ ] Dedicated SFX: rare, legendary, golden, deposit, upgrade, event, combo
- [ ] VFX devices: rare sparkle, legendary glow, boss explosion
- [ ] Boss beacon + legendary beacon VFX (co-located with spawners)
- [ ] Deposit VFX + deposit landmark VFX
- [ ] Death VFX, prestige crown VFX (3 tiers)
- [ ] Bounty crown VFX, shield VFX, magnet VFX
- [ ] Deposit vault VFX (3 props: crate, safe, fortress)

### Phase 4: Social & Events (20–30 min)
- [ ] Team leaderboard placed
- [ ] 2–4 danger zone volumes for viral events
- [ ] 1–4 auto-collect trigger zones
- [ ] Cinematic sequences: tutorial + event spectacle
- [ ] Billboard signs at all buttons with costs
- [ ] Directional signage around map

### Phase 5: Persistence (15 min)
- [ ] 6 accolade devices placed and configured
- [ ] Assigned to `PersistenceAccolades` array in order

### Phase 6: Testing (30–45 min)
- [ ] Solo: full 20-min session, all events fire
- [ ] Solo: prestige works, stats show
- [ ] Multiplayer (4+): no speed modulator conflicts
- [ ] Multiplayer: bounty system works, leaderboards update
- [ ] Multiplayer: power-ups work (shield/magnet/double)
- [ ] Performance: 16 players, 30 min, stable 60 fps

### Phase 7: Publishing (15–30 min)
- [ ] Island name: "BRAINROT RUSH 💎 GET RICH"
- [ ] Description with hook text
- [ ] Thumbnail created (Gen Z neon aesthetic)
- [ ] Tags: Tycoon, Competitive, Collection, Viral
- [ ] Island code generated + published

**Total Time**: 3–5 hours for full professional implementation

---

## 🎯 Priority Device Assignment Order

If short on time, assign in this order:

### CRITICAL (Game breaks without)
1. `CommonSpawners` — at least 1
2. `SpeedModulators` — all 16
3. `DepositZone` — 1
4. `Hud` — 1

### HIGH (Core features)
5. `SpeedButtons` — 5 in order
6. `MultButtons` — 5 in order
7. `IndividualLeaderboard` — 1
8. `EventAnnouncer` — 1
9. `PrestigeButton` — 1

### MEDIUM (Rich gameplay)
10. `RareSpawners` — 3–5
11. `BossSpawners` — 3–4
12. `ShieldSpawners` / `MagnetSpawners` / `DoubleSpawners` — 2–3 each
13. `PickupSFX` — 3–5
14. All other SFX devices

### LOW (Polish — skip for prototyping)
15. `LegendarySpawners`, `GoldenSpawners`
16. All VFX devices
17. Cinematic sequences
18. `PersistenceAccolades` (no persistence but still fun)
19. `DangerZones`, `AutoCollectZones`
20. `DepositVaultVFX`

---

## 🐛 Troubleshooting

### "Game doesn't start"
- Check console for error messages
- Verify `CommonSpawners`, `SpeedModulators`, `DepositZone`, `Hud` are assigned
- Ensure Verse code has no syntax errors (Build → check output)

### "Speed not changing after upgrade"
- **Most common issue!** Verify all 16 SpeedModulators assigned
- They must be in the **array** (not individual properties)
- Each must have Enabled on Start = **No**, Speed = **1.0**

### "No items spawning"
- Check item spawner has an **item assigned** (prop/mesh)
- Verify "Item Picked Up Event" is **Enabled**
- Check spawner is in an **accessible location** (not underground)

### "HUD shows $0 and 0 items"
- This is normal at start!
- Pick up item → count increases
- Enter deposit zone → converts to currency

### "Can't buy upgrades"
- Check button "Interacted With Event" is **Enabled**
- Verify you have enough currency
- Buttons must be assigned to `SpeedButtons`/`MultButtons` in the **correct order**

### "Events never trigger"
- Events are on timers (5 min / 7.5 min / 10 min)
- Wait the full interval
- Check `EventAnnouncer` is assigned

### "Power-ups not working"
- Assign `ShieldSpawners`, `MagnetSpawners`, `DoubleSpawners`
- Each spawner needs "Item Picked Up Event" = Enabled

---

## 💡 Tips

- **Hide modulators** underground — players should never see them
- **Color-code buttons** — visual tier progression helps readability
- **Use particle beams** — guide players to the deposit zone from anywhere
- **Billboard everything** — show costs above every button
- **Test after every 5 devices** — catch issues early
- **Start simple** — get the core loop working, then add polish layers

---

## ⏱️ Time Estimates by Experience

| Level | Setup | Test | Polish | Total |
|-------|-------|------|--------|-------|
| Beginner (first UEFN project) | 4–6 h | 1–2 h | 2–4 h | **8–12 h** |
| Intermediate (some UEFN) | 2–3 h | 30–60 min | 1–2 h | **4–6 h** |
| Advanced (UEFN veteran) | 1–2 h | 30 min | 1 h | **2–3 h** |

---

**Ready to build? Follow the Express Setup above, then refer to [MAP_DESIGN_GUIDE.md](MAP_DESIGN_GUIDE.md) for detailed layout instructions.**

---

> **Next**: [Device Setup](DEVICE_SETUP_GUIDE.md) → [Map Design](MAP_DESIGN_GUIDE.md) → [Balancing](BALANCING_GUIDE.md) → [Game Flow](GAME_FLOW.md)
