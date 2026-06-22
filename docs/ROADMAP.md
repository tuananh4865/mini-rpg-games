# 🗺️ ROADMAP — GTA V Mini Evolution

> **Last updated:** 2026-06-22
> **Source:** Synthesis from `gta-v-mechanics-deep.md` (16KB, 24 sources cited)
> **Goal:** City Drift prototype → full GTA V-lite open world RPG trong 6-9 tháng

---

## 🎯 North Star

**Trong 6-9 tháng**, biến `city-drift.html` (40KB prototype) thành một **GTA V-style open world RPG** chạy trên browser, single-file HTML, với core mechanics:
- Điều khiển mượt + tương tác trau chuốt
- Open world rộng với NPCs/Traffic AI
- Wanted system 5 sao với police escalation
- Combat có chiều sâu (cover, combos, abilities)
- Sinh tồn + kinh tế
- Story missions + heists
- (Optional) Multiplayer P2P

---

## 📊 Version Plan

### 🎯 v1.1 — Polish & Juice (1-2 tuần)

**Theme:** Trau chuốt cái đã có. Không thêm tính năng mới phức tạp.

**Deliverable:** `city-drift.html` 40KB → ~55KB, feel mượt hơn rõ rệt.

**Tasks:**
- [ ] **Web Audio engine** — synthetic SFX (no asset files):
  - Engine pitch: `oscillator.frequency.value = baseRPM * speed_ratio`
  - Gun SFX: noise burst with envelope
  - Crash SFX: filtered noise impulse
  - Ambient: filtered brown noise (city hum)
- [ ] **Vehicle damage visual** — smoke at <50% HP, fire at <20% (particle effect)
- [ ] **Save/load state** — localStorage: HP, money, position, current vehicle, wanted level
- [ ] **Drift mechanic** — handbrake key (Shift) + over-steer
- [ ] **Police roadblock** — at 3+ stars, patrol car parks perpendicular to road
- [ ] **Mission variety expansion** — timed race, escort, eliminate
- [ ] **Health regen to 50%** — auto-regen out of combat (matches GTA V)
- [ ] **Mobile testing** — touch controls verification

**Acceptance criteria:**
- Audio plays correctly (no clicks/pops)
- Save state survives page refresh
- Vehicle visual smoke + fire on low HP
- Drift works (visible over-steer)
- Roadblocks appear at 3+ stars
- 3 new mission types playable

---

### 🌅 v1.2 — Day/Night + Weather (1 tuần)

**Theme:** World feel "alive" với chu kỳ thời gian.

**Deliverable:** World cảm giác khác nhau theo giờ trong ngày.

**Tasks:**
- [ ] **Game time** — 1 real min = 30 game min (fast progression)
- [ ] **3 visual states** — day (warm yellow), evening (orange), night (dark blue + street lights)
- [ ] **Street lights** — auto ON at night (decorative + tactical)
- [ ] **NPC density scaling** — day 100%, night 60%
- [ ] **Weather system** — clear / rain (rain = visual + slip + pedestrians with umbrellas)
- [ ] **Dynamic events** — night = more crime spawns, day = more traffic

**Acceptance criteria:**
- Visible time change in 2-3 minutes of play
- Street lights at night
- Rain visibly affects scene
- Crime spawn rate varies by time

---

### 🤖 v2.0 — AI & World Expansion (3-4 tuần)

**Theme:** World rộng hơn, NPCs/traffic thông minh hơn.

**Deliverable:** Map 50×50 → 80×80 tiles, 5 districts, traffic AI

**Tasks:**
- [ ] **Traffic AI** — NPC drivers đi theo lane, dừng đèn đỏ
- [ ] **Traffic lights** — 6 ngã tư chính (downtown)
- [ ] **NPC schedules** — 4 archetypes (worker, student, retiree, criminal)
- [ ] **Accidents** — 0.05%/sec → spawn crashed car + police called
- [ ] **Map expansion** — 80×80 tiles với 5 districts:
  - Downtown (skyscrapers, suits, density cao)
  - Beach (sand, surfers, slow vehicles)
  - Hills (hilly, mansions, expensive cars)
  - Industrial (factories, trucks, low-income)
  - Suburb (residential, families, mixed)
- [ ] **District-specific NPCs** — visual styles + dialogue theo khu

**Acceptance criteria:**
- Traffic lights stop NPC drivers
- NPC workers go to "work" in morning
- 5 visually distinct districts
- Map 2.5× larger than current

---

### ⚔️ v2.5 — Combat Depth (2 tuần)

**Theme:** Combat juicy hơn, có chiều sâu như GTA V.

**Deliverable:** Combat cảm giác "GTA" — cinematic, varied.

**Tasks:**
- [ ] **Cover system** — context-sensitive snap to nearest wall (auto-detect tile edge)
- [ ] **Melee combos** — 3-hit chain: jab → hook → kick (with i-frame window)
- [ ] **Dodge roll** — dash with i-frames (0.5s)
- [ ] **Weapon wheel** — number keys 1-5 + scroll to cycle
- [ ] **Bullet Time ability** — single key with cooldown (most fun special from GTA V)
- [ ] **Helicopter police** — 3+ stars spawn Police Maverick (new vehicle type)
- [ ] **FIB agents (4 stars)** — faster, smarter police cars
- [ ] **Bribe system** — pay $500-$5000 to clear wanted

**Acceptance criteria:**
- Cover works (auto-snap + strafe)
- 3-hit melee combo visible
- Bullet Time slow-mo works
- Helicopter appears at 3 stars
- Can bribe to clear wanted

---

### 🍔 v3.0 — Sinh Tồn & Kinh Tế (3-4 tuần)

**Theme:** Player phải quản lý resources để sống sót và giàu có.

**Deliverable:** Sandbox có depth — player chọn lifestyle.

**Tasks:**
- [ ] **Hunger/Thirst/Energy bars** — decay over time (real-time, not just gameplay time)
- [ ] **Restaurants + food trucks** — buy food to restore hunger ($5-$20)
- [ ] **Bars + clubs** — buy drinks, meet NPCs
- [ ] **Hotels + safehouses** — sleep to restore energy ($50-$100)
- [ ] **Vehicle shop** — buy/sell cars, garage storage (4 vehicle types expand to 8)
- [ ] **Weapon shop** — buy better guns, ammo (5 weapon types)
- [ ] **Bank robbery** — high reward ($10K), high wanted (5 stars), 30s window
- [ ] **Jobs** — pizza delivery, taxi, garbage truck, tow truck (each $50-$200/job)
- [ ] **Radio stations** — 3-4 synth music loops via Web Audio (engine pitch synced)

**Acceptance criteria:**
- 3 vitals visible + decay
- Food/water/beds restore them
- Vehicle shop buyable
- Bank robbery works (5 stars triggered)
- At least 3 jobs playable

---

### 📖 v4.0 — Story & Heists (4-6 tuần)

**Theme:** Mission structure có narrative. GTA-style heists.

**Deliverable:** Game có story arc, chơi 8-12 hours.

**Tasks:**
- [ ] **Story mode** — 5-8 main missions với dialogue (text-based)
- [ ] **Heist system** — 1 heist finale với 2 approaches (Stealth/Loud)
  - Setup mission → finale mission → $50K payout
- [ ] **Companion NPCs** — AI co-driver, AI gunner
- [ ] **Cutscenes** — text-based dialogues between missions (1-line per character)
- [ ] **Achievements** — 20+ achievements for completion (localStorage tracking)
- [ ] **Mission replay** — replay completed missions for fun/score

**Acceptance criteria:**
- 5+ story missions completable
- 1 heist with both approaches working
- 3 companions recruitable
- 20 achievements tracked

---

### 🌐 v5.0 — Multiplayer & Polish (4-6 tuần)

**Theme:** Play with friends + final polish.

**Deliverable:** Share-able, install-able, mobile-friendly.

**Tasks:**
- [ ] **WebRTC P2P multiplayer** — 2-4 players
- [ ] **Co-op missions** — 2 players, one drives one shoots
- [ ] **PvP arena** — 4 players, deathmatch/race mode
- [ ] **Voice chat** — WebRTC audio (optional)
- [ ] **PWA install** — offline support, push notifications
- [ ] **Mobile optimization** — virtual joystick, touch-friendly buttons
- [ ] **Telegram Mini App** — embed trong Telegram (@game_bot)

**Acceptance criteria:**
- 2-player co-op works
- PWA installable on mobile
- Touch controls usable on phone
- Telegram Mini App launches

---

## 📈 Cumulative Stats (Estimates)

| Version | Code Size | Build Time | Game Length | Key Features |
|---------|-----------|-----------|-------------|--------------|
| v1.0 (now) | 40KB | 3 hours | 5 min sandbox | Drive + 3 missions + wanted + combat |
| **v1.1** | ~55KB | 1 week | 15 min | + Audio + Save + Damage + Drift |
| **v1.2** | ~65KB | 2 weeks | 20 min | + Day/Night + Weather |
| **v2.0** | ~90KB | 6 weeks | 1 hour | + Traffic AI + 5 districts |
| **v2.5** | ~110KB | 8 weeks | 2 hours | + Cover + Combos + Abilities |
| **v3.0** | ~140KB | 12 weeks | 4 hours | + Survival + Economy |
| **v4.0** | ~180KB | 18 weeks | 8-12 hours | + Story + Heists |
| **v5.0** | ~220KB | 24 weeks | Infinite | + Multiplayer + PWA |

---

## 🎯 GTA V Mechanics → Implementation Mapping

(Synthesized from `gta-v-mechanics-deep.md`)

### WILL replicate (matches scope)

| GTA V Mechanic | 2D Adaptation | Version |
|----------------|---------------|---------|
| Health regen to 50% | Auto-regen out of combat | v1.1 |
| Vehicle damage | Smoke/fire at HP thresholds | v1.1 |
| Drift (handbrake) | Shift key + over-steer | v1.1 |
| Police escalation (5 stars) | Already have, add roadblock | v1.1 |
| Evasion times 30s-90s | Scale to 15s-60s | v1.1 |
| Stamina stat | Sprint meter | v1.2 |
| Cover system | Auto-snap to wall | v2.5 |
| Melee combos | 3-hit chain | v2.5 |
| Dodge roll | Dash with i-frames | v2.5 |
| Weapon wheel | Number keys 1-5 | v2.5 |
| Bullet Time (Michael) | Single key ability | v2.5 |
| Motorcycle lean | Steering angle simulation | v1.1 (improved) |
| Random events | 5-6 event spawns | v2.0 |
| Heist (1 finale) | 2 approaches | v4.0 |

### WILL NOT replicate (out of scope)

- Helicopter/plane physics (3D flight complex)
- Boat buoyancy simulation
- 8-class weapon wheel (simplify to 3-4)
- 600+ vehicles (we have 4-8 max)
- Stock market
- Property business management
- 69 story missions (do 5-10 max)
- Multi-protagonist story (single character)
- Real water physics

---

## 🚀 Immediate Next Steps (v1.1)

**Recommended order:**
1. Setup Web Audio engine (3-4 hours) — biggest feel upgrade
2. Add vehicle damage visual (1-2 hours) — high impact, low effort
3. Save/load state localStorage (1-2 hours) — quality of life
4. Drift mechanic (1-2 hours) — fun factor
5. Police roadblock (2-3 hours) — escalation polish
6. 3 new missions (3-4 hours) — content
7. Health regen to 50% (30 min) — quick win
8. Mobile testing + fixes (1-2 hours)

**Total:** ~15-20 hours focused work → ship v1.1

---

## 📂 Files in Research Folder

- `gta-v-mechanics-deep.md` (16KB) — Raw research from 3 subagents, 24 sources cited
- `gta-v-mini-roadmap.md` (17KB) — Original roadmap draft + 5-version plan
- `gta-v-mini-roadmap.md` — **THIS FILE** — Final synthesis + implementation mapping

---

*Author: Hermes Agent (Tuấn Anh's AI)*
*Date: 2026-06-22*