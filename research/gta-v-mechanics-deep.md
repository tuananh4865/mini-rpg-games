# GTA V Mechanics — Deep Research (Subagent Output)

> Detailed research compiled by 3 parallel subagents (2026-06-22). Sources cited inline.

---

## 1. CHARACTER MOVEMENT SYSTEM

**Locomotion modes:** walk / jog / sprint, stamina-gated. Stamina stat: +1% per 18 yards run, +1% per 1 min swim/cycle. Tiers: Lethargic (0-19%), Out of Shape (20-39%), Healthy (40-59%), Athlete (60-79%), Tri-Athlete (80-100%).

**Swimming:** Lung Capacity stat; default ~15s breath-hold; +1% Lung per 1 min underwater; +5s breath per 20% milestone. Yoga also raises it.

**Climbing:** Single Jump button handles jump, vault, climb, dodge-roll — context-sensitive animation selection based on surface angle/height. High Strength speeds up ladder climbing; +1% Strength per 20 punches landed.

**Cover system:** Single button snaps to nearest solid surface; standing vs crouch by height delta. Strafe, blind-fire, pop-out (lean). Cover-to-cover transitions automatic when running along wall. Some cover destructible (wood, vehicles). Health regens ONLY to ~50% out of combat (premium regen via food for full).

**Stealth:** Crouch walk (Ctrl/L3); sprint-tap = silent jog. +1% per 45m stealth walk, +1.5% per 2 stealth kills. Takedown = melee from behind; knife/bat silent kill, fists knock out.

**Melee:** Combo chains from `fistfite.dat` anim streams. Standard: Jab → Punch → Hook → Roundhouse → Long Kick → Special (~6 hits KO most NPCs). Dodge (jump while locked-on) gives ~0.5s counter-attack window with bonus damage.

**Character stats (8 total):** Stamina, Shooting, Strength, Stealth, Flying, Driving, Lung Capacity, Special.

### Sources (Movement)
1. GTA Wiki — *Skills in GTA V*: https://gta.wiki/w/Skills_in_GTA_V
2. IGN — *Increasing Stats in GTA 5*: https://www.ign.com/wikis/gta-5/Increasing_Stats_in_GTA_5
3. GTA Fandom — *Cover System*: https://gta.fandom.com/wiki/Cover_System
4. Game Informer — *Running and Gunning in GTA V*: https://gameinformer.com/games/grand_theft_auto_v/b/ps3/archive/2013/05/02/running-and-gunning-in-grand-theft-auto-v.aspx
5. gamepressure — *GTA 5 Firearms fights*: https://www.gamepressure.com/gtav/firearms-fights/z155e2
6. GTA Fandom — *Statistics in GTA V*: https://gta.fandom.com/wiki/Statistics_in_GTA_V
7. GTA Wiki — *Fistfite.dat*: https://gta.wiki/w/Fistfite.dat/GTAVC
8. GTA Gossip — *How to Dodge in GTA 5*: https://gtagossip.com/blog/how-to-dodge-in-gta-5-master-melee-combat/

---

## 2. VEHICLE PHYSICS

**Architecture:** `handling.meta` (~50 base parameters + sub-handling records for bike/flying/boat/special/trailer).

**Driving model:** Arcade-leaning simulation. G-Force based:
- `fTractionCurveMax` = peak G before sliding
- `fTractionCurveLateral` = slip-angle curve (peak lateral grip at half this value)
- `fDownForceModifier` = speed-sensitive grip
- Weight transfer simulated (leaning wheels gain traction)

**Engine/Transmission:**
- `fInitialDriveForce` ≈ baseline acceleration = 10× value m/s²
- Torque curve: flat until 80% RPM, drops to 60% (1-gear approximation)
- `fInitialDriveMaxFlatVel` ≈ top speed kph; file value = kph × 0.75
- Gears 1-8 (or 1-10 in later patches); final drive ratio fixed
- `fDriveBiasFront`: 0=RWD, 1=FWD, 0.5=4WD
- `HF_CVT` flag = EV behavior

**Drift:** Flag-driven (`CF_ASSIST_TRACTION_CONTROL` 0x2000, `CF_ASSIST_STABILITY_CONTROL` 0x4000). `fHandBrakeForce` 0.4-0.7 typical.

**Damage model (4 multipliers):**
- `fCollisionDamageMult` — collision → body parts
- `fWeaponDamageMult` — bullet/explosive
- `fDeformationDamageMult` — visual mesh deformation
- `fEngineDamageMult` — engine degradation, smoke, fire

Visual: doors/hoods/bumpers fall off; engine catches fire; wheels detach; gas tank leaks/explodes.

**Motorcycle lean** (`CBikeHandlingData`):
- `fLeanFwdCOMMult` / `fLeanBakCOMMult` — COM shift
- `fMaxBankAngle` — max cornering lean
- `fStickLeanMult` — joystick lean
- `fBrakingStabilityMult` — stoppie/endo
- `fWheelieBalancePoint`, `fStoppieBalancePoint`, `fWheelieSteerMult`
- `CF_CAN_WHEELIE` flag for handbrake wheelies

**Helicopters/Planes** (`CFlyingHandlingData`):
- Plane: nose-heavy, autothrottle, turbulence at altitude
- Helicopter: altitude trigger + direction stick + pitch/yaw stick
- VTOLs (Deluxo, Oppressor): landing-gear button toggles hover vs plane
- 100+ weapon hashes for aircraft (rockets, laser, etc.)

**Boats** (`CBoatHandlingData`):
- Aquaplaning params (`fAquaplaneForce`, etc.)
- Rudder params (`fRudderForce`, `fRudderOffsetSubmerge`)
- Buoyancy probes (`fSampleTop`, `fSampleBottom`)
- Hull box (`fBoxFrontMult`, `fBoxRearMult`, `fBoxSideMult`)
- Resistance vectors (`vecMoveResistance`, `vecTurnResistance`)
- Ships heavier, lose control at speed (aquaplaning); jet skis nimble but capsize

**Floats:** `fPercentSubmerged = 85%` for road vehicles; boats excluded.

### Sources (Vehicles)
9. GTAMods Wiki — *handling.meta*: https://gtamods.com/wiki/Handling.meta
10. eddlm — *Handling Tools Guide*: https://eddlm.github.io/Handling-Tools/guide
11. GTACars.net — *GTA 5 Metadata Glossary*: https://gtacars.net/gta5/glossary
12. 1v9 — *How To Fly Planes in GTA 5*: https://1v9.gg/blog/gta-5-how-to-fly-planes-aircraft-helicopters-complete-guide
13. Grand Theft Wiki — *Fixed-Wing Aircraft*: https://www.grandtheftwiki.com/Fixed-Wing_Aircraft

---

## 3. COMBAT SYSTEM

**Aiming presets (3):**
1. Hard snap-to lock-on — reticle sticks
2. Soft targeting — reticle drifts toward target
3. Free aim — full manual

View: over-the-shoulder (Max Payne 3 style).

**Cover-to-cover:** Hold cover + strafe → character runs to next cover point. Combat-roll = dodge button while aiming.

**Health regen:** Auto out of combat, but **caps at 50%** unless snacks/premium items used.

**Ammo:** Shared ammo pools per weapon class (not per-gun). Sniper/Heavy have unique pools.

**Weapon wheel — 8 classes:** Handguns, SMGs, Assault Rifles, Shotguns, Sniper Rifles, Heavy, Melee, Thrown. Criminal Enterprises update added Snacks + Body Armor slots. 59+ weapons total.

**Weapon stats (representative):**

| Weapon | Damage | Fire Rate | Clip | DPS |
|--------|--------|-----------|------|-----|
| Pistol | 26 | 162 RPM | 12 | ~70 |
| AP Pistol | 26 | 600 RPM | 18 | ~250 |
| Assault Rifle | 30 | 380 RPM | 30 | ~190 |
| Advanced Rifle | 34 | 500 RPM | 30 | ~283 |
| Sniper Rifle | 101 | – | 10 | ~180 |
| Heavy Sniper | 98 | 50 RPM | 6 | ~180 |
| RPG | ~300 | – | 1 | – |

Damage drop-off: starts ~40m, floor 30% at 120m.

**Special abilities (same input, shared yellow meter under minimap):**
- **Michael — Bullet Time (on-foot)**: slow-mo during gunfights; aiming normal speed. Fills from headshots, stealth takedowns, high-speed driving.
- **Franklin — Driving Focus (road vehicles only)**: slow-mo while driving. NOT for bikes/boats/aircraft. Fills from near-misses, oncoming traffic, high-speed.
- **Trevor — Red Mist (on-foot)**: 2× damage dealt, 0.5× damage taken; effectively unkillable. Fills from kills, damage taken, headshots, taunts, high-speed.

**Duration:** ~10s minimum meter → ~30s maxed.

### Sources (Combat)
- Same as #4, #5, #14, #15, #16 above (already cited)
14. GTA Wiki — *Weapons in GTA V*: https://gta.wiki/w/Weapons_in_GTA_V
15. GTABoom — *GTA V Weapons Database*: https://www.gtaboom.com/gta-v-weapons-database-846c
16. GTA Intel — *GTA 5 Special Abilities Explained*: https://gtaintel.com/news/gta-5-special-abilities-explained

---

## 4. WANTED SYSTEM

**5-star scale** (not 6 like older GTAs). AI more aggressive than GTA IV — PIT maneuver, ram-and-spin, box-in, commandeer civilian cars.

### Star-by-star escalation

| Stars | Response | Vehicles | Min Dispatch |
|-------|----------|----------|--------------|
| ★ | Officers attempt arrest at gunpoint; security/motorcycle fire immediately | Police Cruiser (LSPD), Sheriff Cruiser (Blaine Co.), Police Predator (water), Crusader (Zancudo) | 1-2 vehicles |
| ★★ | Shoot-to-kill. Aggressive ramming. Ambush (lights off, roadside wait) | Patrol cars | 3+ vehicles |
| ★★★ | Roadblocks + spike strips. All officers spawn with bulletproof vests. Police Maverick helicopter joins (spotlight at night) | Roadblocks (cars + transporters), Police Maverick with NOOSE TRU | 4+ cars + 1 heli |
| ★★★★ | NOOSE TRU tactical teams from FIB Granger / Sheriff SUV (3 officers/vehicle, hang off sides firing). NOOSE riot vans at roadblocks. Up to 3 Police Mavericks (typ. 2 deployed). They rappel and engage on foot. NOOSE TRU shoots from inside vehicles unprovoked | NOOSE Granger, Sheriff SUV, Riot Van, Police Maverick | 5+ ground vehicles + 2 helis |
| ★★★★★ | Streets clear of civilians. Up to 3 Police Mavericks, multiple roadblocks. Significantly more NOOSE | All of above, indefinitely | Unlimited |

### Restricted areas (auto-wanted)
- Fort Zancudo: enter = 4★; fly over = 2★→4★; fire rocket = instant 5★
- Bolingbroke Penitentiary: enter = 4★
- Humane Labs and Research: enter = 4★
- LSIA: drive on tarmac = 3★; fire rocket = instant 5★
- Mission Row Police Station: behind desk/rooftop = 3★
- Los Santos Golf Club (SP): trespass after hours = 2★
- Trevor can NEVER buy LSIA hangar → always wanted there

### Evasion mechanic
Cone-search / line-of-sight (not GTA IV radius):
- Each officer has arc FoV; helicopters' FoV much larger
- Radar flashes red/blue when seen; blue cones show searching officers when stars flash
- Flash rate slows as player stays hidden = closer to escape

**Time out of sight to lose:**

| Stars | Time |
|-------|------|
| ★ | 30s |
| ★★ | 45s |
| ★★★ | 60s |
| ★★★★ | 75s |
| ★★★★★ | 90s |

- Changing appearance (mask/sunglasses) drops 1 star
- Railway easiest escape (cops can't drive on tracks)
- Dying clears wanted (Online)

### Bribe / removal
- **Lester Crest call (story)**: removes wanted, $200/star (Online; SP: free via Lester after a certain mission)
- **CEO/VIP "Bribe Authorities" (Online)**: $15,000 flat, clears org wanted + 2-min immunity
- **Lester "Cops Turn Blind Eye" (Online)**: $5,000 flat — PREVENTS gaining wanted, doesn't remove current
- **Doomsday Heist finale as host**: Lester removal free forever

### Evasion rewards (Online)
+100 RP per star successfully evaded (not removed) — 5 stars = 500 RP

### Sources (Wanted)
17. GTA Wiki — *Wanted Level in GTA V*: https://gta.wiki/w/Wanted_Level_in_GTA_V
18. GTA Wiki — *Wanted Level in GTA Online*: https://gta.wiki/w/Wanted_Level_in_GTA_Online
19. Sportskeeda — *GTA Online: How to bribe Cops*: https://www.sportskeeda.com/gta/how-bribe-cops-gta-5

---

## 5. MISSIONS

### Mission taxonomy (hierarchical)
1. **Story missions** (69 main across 3 protagonists; required for 100%)
2. **Strangers & Freaks** (~60 character missions per protagonist; for 100%)
3. **Random Events** (57 original / 60 Enhanced; 14 needed for 100%)
4. **Heists** (5 main heists + heist setups as prerequisite)
5. **Side activities** — Races, Stunt Jumps, Parachute Jumps, Off-Road Races, Sea Races, Golf, Tennis, Darts, Triathlon, Yoga, Shooting Range, collectibles

### Mission types (concrete examples)
- **Races**: Land (Street/Off-road/Rally/Bike), Sea, Air, Parachute
- **Assassinations (Lester's, stock-market tied)**:
  - Hotel Assassination — $9,000 + Vinewood Hills safehouse
  - Multi Target Assassination — $7,000
  - Vice Assassination — $5,000
  - Bus Assassination — $7,000
  - Construction Assassination — $10,000
- **Deliveries/Taxi-like**: Tonya's *Pulling Favors* (tow), Hao's *Shift Work*
- **Heist Setups**: 2-5 setup missions per heist finale
- **Rampage (Trevor)**: kill X targets within time limit using only supplied weapon

### Heist architecture (5 main)
Pattern: Briefing → Approach Choice → Setups → Finale

| Heist | Approaches | Crew | Max Net Payout |
|-------|-----------|------|----------------|
| Jewel Store Job | Smart / Loud | Gunman, Driver, Hacker | ~$2.45M crew (max gross $4.95M) |
| Merryweather Heist | Freighter / Offshore | – | No payout (job-for-hire) |
| Blitz Play | Single path | – | Reward: new weapons at Ammu-Nation |
| Paleto Score | Single path | Gunman (player choice) | ~$8.0M gross; ~$760K split |
| Bureau Raid | Covert / Roof | Gunman, Hacker, Driver | $149K-$242K (Franklin only) |
| The Big Score | Subtle / Obvious | 2× Drivers, 2× Gunmen, 1× Hacker | Subtle: ~$35.5M each / Obvious: ~$41.7M each |

Crew cut % scales with experience: experienced Packie = 12%, novice = ~17%. Max single Big Score = **$41,664,000 per protagonist** (Obvious + Taliana + Karim + Norm + Daryl).

### Mission design principles
- **Cinematic intros**: Rockstar hallmark — pre-mission cutscenes set stakes
- **Multiple approaches**: choices during planning change mission flow (Stealth/Loud; Covert/Roof; Subtle/Obvious)
- **Fail states**: standard Wasted/Busted + contextual (e.g., *Blow Up III Convoy* fails if convoy escapes)
- **Gold/Silver/Bronze medals**: 3 challenge objectives each, grant completion % + stat boosts
- **Setups gate finales**: heist finales require all setups complete
- **Crew persistence**: surviving crew gain XP, demand smaller cuts

### Random Events (concrete rewards)
- **Armored truck/ranger shootouts** — $5K/briefcase (up to 2), $10K if side with criminals
- **Bicycle thief** — +3% Stamina
- **Altruist Cult sacrifice (Trevor-only)** — $25K/briefcase (up to $100K all pursuer drops)
- **Drug deal gone wrong (Gerald)** — $10K + random weapon
- **ATM mugging** — keep cash ($500-$2K) OR return for full Special meter + 10% of wallet cash
- **Broken-down vehicle delivery** — +5 Driving skill + $100 + 30% Bawsaq stock tip

### Sources (Missions)
20. GTA Wiki — *Missions in GTA V*: https://gta.wiki/w/Missions_in_GTA_V
21. GTA Wiki — *Heists in GTA V*: https://gta.wiki/w/Heists_in_GTA_V
22. GTA Wiki — *Heist Setups*: https://gta.wiki/w/Heist_Setups
23. GTA Wiki — *The Big Score*: https://gta.fandom.com/wiki/The_Big_Score_(GTA_V); *The Jewel Store Job*: https://gta.wiki/w/The_Jewel_Store_Job
24. GTA Wiki — *Random Events in GTA V*: https://gta.wiki/w/Random_Events_in_GTA_V

---

## Cross-cutting Mechanics

- **Character switching**: disabled during most wanted levels and many missions
- **Starting stat affinities**: Michael = Combat/Shooting/Stealth high; Franklin = Driving/Stealth/Shooting high; Trevor = Strength/Driving/Flying/Shooting/Stealth high
- **Armor & Health cap**: Health 100 (boostable via snacks/effects); Armor up to 100, tier-degraded
- **Damage model**: collisions and explosions both deal engine damage; engine damage = smoke → fire → eventual explosion (or instant kill in heavy hits)
- **Three protagonists, one city**: switching free via Character Wheel (hold → tap), outside missions/cutscenes/wanted levels

---

## Synthesis → Application to City Drift

### What we CAN replicate in 1-file HTML (top-down 2D)

| GTA V Mechanic | 2D Adaptation | Priority |
|----------------|---------------|----------|
| Stamina stat | Sprint meter, depletes on run/swim | P1 (v1.2) |
| Cover system | Auto-snap to nearest wall on button press | P1 (v2.5) |
| Melee combos | 3-hit chain: jab → hook → kick | P1 (v2.5) |
| Dodge roll | Dash with i-frames | P1 (v2.5) |
| Health regen to 50% | Auto-regen out of combat, full regen via food | P0 (v1.1) |
| Weapon wheel (8 classes) | Number keys 1-5 + E cycle | P0 (v1.1) |
| Special abilities | Single key with cooldown (Bullet Time most fun) | P2 (v2.5) |
| Wanted 5-star | Already have, but need helicopter/Military tiers | P0 (v1.1) |
| Police evade times 30s-90s | Scale to 15s-60s for shorter sessions | P0 (v1.1) |
| Bribe system | Pay $X to clear wanted (visit ATM) | P1 (v3.0) |
| Vehicle damage visual | Smoke at 50% HP, fire at 20% | P0 (v1.1) |
| Drift (handbrake) | Handbrake key + over-steer | P0 (v1.1) |
| Motorcycle lean | Simulated lean angle based on steering input | P1 (v1.1) |
| Weapon stats (DPS, drop-off) | Damage drop-off by distance, RPM for fire rate | P1 (v2.5) |
| Random events | 5-6 event types spawning on timer | P1 (v2.0) |
| Heists | 1 heist finale with 2 approaches | P3 (v4.0) |
| Character switching | Switch between 3 chars with different abilities | P3 (v4.0) |

### What we should SKIP for scope
- Helicopter/plane physics (too complex for 1 file)
- Boat buoyancy simulation
- 8-class weapon wheel (simplify to 3-4)
- 600+ vehicles (we have 4, fine)
- Stock market
- Property business management
- 69 story missions (do 5-10 max)
- Multi-protagonist story

---

*Compiled 2026-06-22 from 3 parallel subagent research tasks.*