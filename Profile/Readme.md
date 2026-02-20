# Synapse AntiCheat
> In Development, Do not expect a release anytime soon

**Bleeding-edge automated cheat detection & launcher for Team Fortress 2**

Synapse AntiCheat is an advanced automated system that analyzes TF2 gameplay to detect cheaters in real-time with high accuracy. Using our replay analyzer and integrated community databases, it identifies suspicious behavior patterns and helps keep your games clean. Synapse also serves as a comprehensive TF2 launcher with all known launch arguments pre-configured and ready to customize.

![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-blue)
![Status](https://img.shields.io/badge/status-Active%20Development-green)

> **⚠️ Important:** Synapse will forever be free software. If you have purchased it, you have been scammed and should report it to us immediately!

---

## 🎯 Features

### Automated Detection Engine
- **Real-time replay analysis** - No second TF2 instance required by default!
- Multi-method detection system with comprehensive cheat coverage
- Confidence-based rating system verified through human review
- Automatic reporting with demo file evidence

### Integrated TF2 Launcher
- **All known launch arguments** pre-configured and ready to use
- **Automatic configuration** of required settings for Synapse
- **User-customizable** launch options for personal preference
- **One-click launch** straight into TF2 with optimal settings

# TF2 Demo Analysis — Cheat Detection Checklist

> **How to use this document:**
> Each cheat type has a checklist item. Expand the dropdowns to see detection methods.
> Nested dropdowns break detection down by cheat *variant*, then by *automated* (algorithmic) vs *manual* (human reviewer) approach.
>
> **Confidence system:** No single signal should result in a flag. Signals are tagged:
> - 🔴 **High confidence** — very low false positive rate, strong signal alone
> - 🟡 **Medium confidence** — meaningful but needs corroboration
> - 🟢 **Low confidence** — weak alone, but powerful when combined with others

---

## Legend

| Symbol | Meaning |
|--------|---------|
| ✅ | Detection method implemented |
| 🚧 | Detection method in progress |
| ❌ | Not yet implemented |
| 🔴 | High confidence signal |
| 🟡 | Medium confidence signal |
| 🟢 | Low confidence signal |
| 🤖 | Automated detection |
| 👁️ | Manual / human review |

---

## Table of Contents

- [Hitscan Aimbot](#hitscan-aimbot)
  - [Snap Aimbot](#-snap-aimbot)
  - [Smooth Aimbot](#-smooth-aimbot)
  - [Silent Aim](#-silent-aim)
  - [Aim Assist / Correction](#-aim-assist--correction)
  - [Triggerbot](#-triggerbot)
- [Projectile Aimbot](#projectile-aimbot)
  - [Direct Hit Prediction](#-direct-hit-prediction)
  - [Splash Optimisation](#-splash-optimisation)
  - [Auto-Detonate](#-auto-detonate)
  - [Auto-Airblast](#-auto-airblast)
- [Crithack](#crithack)
  - [Force Crits](#-force-crits)
  - [Melee Always Crit](#-melee-always-crit)
  - [Avoid Random Crits](#-avoid-random-crits)
- [Spread Removal (NoSpread)](#spread-removal-nospread)
- [Backtrack](#backtrack)
- [Fakelag / Packet Choking](#fakelag--packet-choking)
  - [Plain Fakelag](#-plain-fakelag)
  - [Random Fakelag](#-random-fakelag)
  - [Adaptive / Conditional Fakelag](#-adaptive--conditional-fakelag)
- [Anti-Aim](#anti-aim)
  - [Pitch Anti-Aim](#-pitch-anti-aim)
  - [Yaw Anti-Aim — Static / Offset](#-yaw-anti-aim--static--offset)
  - [Yaw Anti-Aim — Spin](#-yaw-anti-aim--spin)
  - [Yaw Anti-Aim — Jitter](#-yaw-anti-aim--jitter)
  - [Yaw Anti-Aim — Edge / Peek-based](#-yaw-anti-aim--edge--peek-based)
  - [Fake Yaw (Desync)](#-fake-yaw-desync)
  - [Minwalk](#-minwalk)
- [Doubletap / Warp](#doubletap--warp)
- [Speedhack](#speedhack)
- [Resolver (Counter-Anti-Aim)](#resolver-counter-anti-aim)
  - [Static Offset Resolver](#-static-offset-resolver)
  - [Cycling Resolver](#-cycling-resolver)
  - [View-Based Resolver](#-view-based-resolver)
  - [Minwalk Resolver](#-minwalk-resolver)
- [ESP / Wallhack (Behavioral)](#esp--wallhack-behavioral)
  - [Player ESP](#-player-esp)
  - [Object / Pickup ESP](#-object--pickup-esp)
  - [Spy / Cloak ESP](#-spy--cloak-esp)
- [Movement Exploits](#movement-exploits)
  - [Bunny Hop Hack](#-bunny-hop-hack)
  - [Strafe Hack](#-strafe-hack)
  - [EdgeJump](#-edgejump)
  - [CTap](#-ctap)
  - [Auto Rocket Jump](#-auto-rocket-jump)
  - [AutoPeek](#-autopeek)
  - [FastStop / FastAccelerate](#-faststop--fastaccelerate)
- [Automation / Bot Behavior](#automation--bot-behavior)
  - [NavBot (Pathfinding Bot)](#-navbot-pathfinding-bot)
  - [Followbot](#-followbot)
  - [Auto-Queue / Session Management](#-auto-queue--session-management)
- [Medic Automation](#medic-automation)
  - [AutoHeal / Target Prioritization](#-autoheal--target-prioritization)
  - [AutoVaccinator](#-autovaccinator)
  - [Auto-Uber Deployment](#-auto-uber-deployment)
  - [Auto-Arrow (Crusader's Crossbow)](#-auto-arrow-crusaders-crossbow)
- [Engineer Automation](#engineer-automation)
  - [Auto-Repair](#-auto-repair)
  - [Auto-Upgrade](#-auto-upgrade)
- [Spy Automation](#spy-automation)
  - [AutoBackstab](#-autobackstab)
  - [Anti-Backstab Detection Bypass](#-anti-backstab-detection-bypass)
- [Account / Meta Signals](#account--meta-signals)

---

## Hitscan Aimbot

> Hitscan aimbots assist with instant-travel weapons: scattergun, pistol, minigun, sniper rifle, SMG, shotguns, syringe gun, etc.
> There are several distinct subtypes with meaningfully different behavioral signatures.

---

### ◆ Snap Aimbot

- [✅] **Snap aimbot detected**

<details>
<summary>📋 Detection Methods</summary>

The snap aimbot instantly teleports the viewangle to a target hitbox with no intermediate frames. It is the most aggressive and most detectable type.

<details>
<summary>🤖 Automated — Zero-Acceleration Angular Jump Detection</summary>

**What to measure:**
- Compute viewangle delta (degrees/tick) each tick for both yaw and pitch
- Compute the second derivative — rate of change of angular velocity
- Record any tick where angular delta exceeds a threshold AND the second derivative is near zero (instant full velocity, no ramp-up)

**What to look for:**
- 🔴 Angular velocity appearing at full magnitude on tick 0 with no preceding acceleration phase — physically impossible with a mouse
- 🔴 Angle snapping to within <1° of an enemy hitbox center and stopping on the exact tick of snap
- 🟡 Snap magnitude distribution clustering at values matching common target distances (aimbot always snaps to hitbox center)

**Implementation notes:**
- Human flicks DO produce large angular deltas but always with a non-zero acceleration phase of at least 1–2 ticks
- Build per-sensitivity baselines — high DPI players have higher tick-to-tick deltas but still ramp
- Weight snaps that coincide exactly with an enemy becoming visible or entering FOV

</details>

<details>
<summary>🤖 Automated — Snap-to-Hitbox Center Bias</summary>

**What to measure:**
- After a large angular jump, compute the offset between the final resting angle and the nearest enemy hitbox center
- Collect this offset distribution across the entire session

**What to look for:**
- 🔴 Offset distribution tightly clustered near zero — always snapping to exactly the hitbox center
- 🟡 Specific hitbox bone preference — always landing precisely on the head bone, never on the body

</details>

<details>
<summary>🤖 Automated — Post-Snap Stillness</summary>

**What to measure:**
- Measure angular velocity in the ticks immediately following a large snap
- Human flicks are followed by micro-corrections; aimbot snaps are followed by near-zero movement

**What to look for:**
- 🔴 Zero angular movement for 2+ ticks immediately after a snap, then resuming normal movement
- 🟡 Post-snap movement that is purely cosmetic jitter rather than genuine correction behavior

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Crosshair visibly jumping frame-to-frame directly onto enemy heads with zero travel
- Multiple rapid snaps to different targets in quick succession with no search movement
- Snapping toward a target position before the enemy is fully visible

</details>

</details>

---

### ◆ Smooth Aimbot

- [✅] **Smooth aimbot detected**

<details>
<summary>📋 Detection Methods</summary>

The smooth aimbot interpolates the viewangle toward a target over several ticks to mimic natural aim movement. Significantly harder to detect than snap — hardest to distinguish from a skilled human.

<details>
<summary>🤖 Automated — Aim Path Linearity Analysis</summary>

**What to measure:**
- When the crosshair is moving toward a target, compute the curvature of the angular path
- Humans produce curved, non-linear paths (varying speed, corrections, overshoots); smooth aimbots produce perfectly linear or constant-rate paths

**What to look for:**
- 🔴 Angular path that is a perfect straight line in both yaw and pitch simultaneously across 3+ ticks
- 🟡 Constant rate of angular change (identical delta every tick) toward a target — matches a `lerp` smoothing algorithm
- 🟡 Path that arrives exactly at the target and stops with zero overshoot — humans almost always overshoot slightly

</details>

<details>
<summary>🤖 Automated — Smooth Rate Fingerprinting</summary>

**What to measure:**
- When tracking a moving target, measure how angular velocity changes as the target moves
- Smooth aimbots recalculate direction each tick, producing a predictable velocity profile

**What to look for:**
- 🟡 Angular velocity that always matches `(target_angle - current_angle) × smooth_factor` — the exact formula used by lerp-based smooth aimbots
- 🟡 Tracking speed that scales perfectly proportionally with distance between crosshair and target

</details>

<details>
<summary>🤖 Automated — Tracking Consistency Under Evasion</summary>

**What to measure:**
- When a target strafes or reverses direction, measure how quickly and accurately the crosshair follows
- Humans lag behind direction changes, overshoot, and require correction time

**What to look for:**
- 🟡 Zero lag on direction reversals — crosshair changes tracking direction on the exact tick the target does
- 🟡 No overshoot when a target stops — crosshair stops on the same tick as the target

</details>

<details>
<summary>🤖 Automated — FOV Boundary Activation Behavior</summary>

**What to measure:**
- Smooth aimbots typically have a configured FOV radius — they only activate when the target is within N degrees of center
- Measure whether aim assistance appears and disappears at a consistent angular distance from the crosshair

**What to look for:**
- 🟡 Aim suddenly locking onto or abandoning a target at a consistent angular threshold — the configured FOV radius
- 🟢 FOV values matching common cheat defaults (typically 10°–30°)

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Aim that moves toward targets too smoothly — no micro-corrections, no overshoot, no human noise
- Crosshair that "slides" onto moving targets and sticks with inhuman consistency
- Tracking that never loses a target even during aggressive evasion
- Aim speed always proportional to target distance — closer targets tracked more slowly, further ones more quickly

</details>

</details>

---

### ◆ Silent Aim

- [✅] **Silent aim detected**

<details>
<summary>📋 Detection Methods</summary>

Silent aim fires at a target without visually moving the crosshair. The player's viewangles remain unchanged but the server-side shot direction is modified to hit the target. Nearly invisible to spectators but leaves network-level traces.

<details>
<summary>🤖 Automated — Shot Direction vs Viewangle Mismatch</summary>

**What to measure:**
- At the tick of each damage event, compare the shooter's recorded viewangle with the vector from shooter to victim
- These should agree within a small margin (weapon spread + server lag tolerance)

**What to look for:**
- 🔴 Consistent hits where the shooter's viewangle is pointing 5°+ away from the victim's position at time of impact
- 🔴 Hits landing on targets completely outside the weapon's maximum spread cone from the recorded viewangle

**Implementation notes:**
- Must account for weapon spread cone — a hit 2° off-center is normal; 30° is not
- Must account for tick timing — the viewangle used server-side may be 1 tick earlier than the recorded damage event

</details>

<details>
<summary>🤖 Automated — Damage Without Prior Tracking Behavior</summary>

**What to measure:**
- Identify damage events where the player's viewangle shows no movement toward the victim in the N ticks before firing

**What to look for:**
- 🔴 Player dealing damage to a target they are visibly looking away from
- 🟡 Damage events during periods where the crosshair is stationary and not pointed at any target

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Player visibly looking away from a target and still landing hits or kills on them
- Crosshair not on any player at the moment of a kill
- Death cam showing the killer facing the wrong direction

</details>

</details>

---

### ◆ Aim Assist / Correction

- [✅] **Aim assist / correction detected**

<details>
<summary>📋 Detection Methods</summary>

Aim assist performs small angle corrections on the player's existing aim — it does not snap or smooth from scratch but nudges the crosshair when it is close to a target. The hardest aimbot type to detect as the output looks nearly human.

<details>
<summary>🤖 Automated — Micro-Correction Toward Hitbox</summary>

**What to measure:**
- Identify ticks where natural aim movement is slightly deflected toward a nearby enemy hitbox
- Measure the frequency and magnitude of small angle adjustments (<5°) that improve crosshair-to-hitbox alignment

**What to look for:**
- 🟡 Statistically abnormal rate of small corrections that happen to improve target alignment — too frequent to be coincidence
- 🟡 Micro-corrections that only occur when a target is within N degrees of the crosshair center (the assist FOV threshold)

</details>

<details>
<summary>🤖 Automated — Near-Miss Elimination Rate</summary>

**What to measure:**
- Compare how often the player's natural movement would have resulted in a near-miss vs a hit
- With aim assist, near-misses are redirected into hits

**What to look for:**
- 🟡 Shots that should have been near-misses (crosshair passing 1–3° off a hitbox) consistently becoming hits
- 🟢 Near-miss rate significantly below statistical expectation for the observed skill level

</details>

<details>
<summary>🤖 Automated — Assist Strength Fingerprinting</summary>

**What to measure:**
- The `AssistStrength` cheat parameter controls how strongly correction pulls toward the target
- This produces a detectable relationship: corrections always being a fixed fraction of the angular distance to target

**What to look for:**
- 🟡 Angular corrections that are always exactly X% of the distance to the nearest hitbox (e.g. always closing 30% of the gap per tick)

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Aim that looks almost human but seems to lightly "stick" when passing near enemy hitboxes
- Shots that clip targets they should have narrowly missed
- Crosshair gently drifting toward enemies during otherwise normal movement

</details>

</details>

---

### ◆ Triggerbot

- [✅] **Triggerbot detected**

<details>
<summary>📋 Detection Methods</summary>

A triggerbot automatically fires when the crosshair is over an enemy hitbox. The player still aims manually but firing is automated. Common on Sniper and Scout.

<details>
<summary>🤖 Automated — Fire Latency Distribution</summary>

**What to measure:**
- For each shot fired, compute how long the crosshair was over the target hitbox before the attack input registered
- Build a histogram of this latency across the full session

**What to look for:**
- 🔴 Latency distribution spiking at 0–2 ticks (~0–30ms) — human minimum reaction time is ~100ms (~7 ticks)
- 🔴 Near-zero variance in the distribution — humans have high spread in their reaction times
- 🟡 Bimodal distribution: near-zero latency when crosshair is directly on a hitbox, normal latency otherwise — triggerbot only activating on clean overlaps

**Implementation notes:**
- Requires per-tick hitbox reconstruction from demo entity state
- Filter out pre-aim situations where the player is intentionally waiting at a known position

</details>

<details>
<summary>🤖 Automated — Fire Rate Consistency on Mobile Targets</summary>

**What to measure:**
- For manually-fired weapons, measure consistency of fire timing when targets are in motion vs stationary

**What to look for:**
- 🟡 Fire timing that perfectly tracks target hitbox overlap — firing the exact tick overlap begins regardless of target speed
- 🟡 Never missing a window — every time the crosshair passes over an enemy, a shot fires

</details>

<details>
<summary>🤖 Automated — Scope + Fire Timing (Sniper)</summary>

**What to measure:**
- Measure the time between scope input and fire input for Sniper
- Triggerbot fires the instant full charge is reached or the instant the crosshair touches the hitbox while scoped

**What to look for:**
- 🔴 Consistent firing at exactly the minimum scoped charge time with near-zero variance
- 🟡 Fire input always occurring on the first tick the fully-charged reticle overlaps a target

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Firing the instant any sliver of an enemy hitbox clips into the crosshair, even during fast movement
- Never holding or hesitating — every crosshair-on-target moment produces a shot
- Sniper firing at minimum charge time with robotic consistency

</details>

</details>

---

## Projectile Aimbot

> Projectile aimbots assist with weapons whose ammunition has travel time and gravity: rocket launcher, grenade launcher, stickybomb launcher, Huntsman bow, Flare Gun, Cleaver, etc.
> Sub-types have distinct detection signatures.

---

### ◆ Direct Hit Prediction

- [✅] **Projectile direct-hit aimbot detected**

<details>
<summary>📋 Detection Methods</summary>

Predicts target position at projectile arrival time and aims to produce a direct hit. Most applicable to rockets and arrows.

<details>
<summary>🤖 Automated — Lead Angle Accuracy vs Target Velocity</summary>

**What to measure:**
- For each projectile resulting in a hit, reconstruct target velocity at time of firing
- Compute the optimal lead angle required given projectile speed and gravity
- Compare against the player's actual aim angle at moment of firing

**What to look for:**
- 🔴 Actual aim angle consistently matching optimal lead to within <1° across many shots on moving targets
- 🔴 Lead accuracy that does not degrade at range (humans lead worse at longer distances)
- 🟡 Perfect accounting for gravity — aim angle exactly offsetting projectile drop at the fired range

**Implementation notes:**
- Requires per-weapon projectile speed and gravity values (well-documented for TF2 weapons)
- Reconstruct target velocity from position delta over 2–3 ticks before the shot

</details>

<details>
<summary>🤖 Automated — Direct Hit Rate on Evasive Targets</summary>

**What to measure:**
- Separate direct hits on stationary vs moving targets
- Compare direct hit rate on moving targets against top-percentile human performance baselines

**What to look for:**
- 🟡 Direct hit rate on fast-moving targets (Scout, airborne players) exceeding the human 99th percentile baseline
- 🟡 Direct hit rate that does not drop as target speed increases

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Rockets or arrows consistently intercepting Scout-speed targets in the air at long range
- Aim that visibly leads targets by a precisely correct amount that adjusts with range and speed
- Extended sequences of direct hits on evasive targets with no misses

</details>

</details>

---

### ◆ Splash Optimisation

- [✅] **Projectile splash-optimisation aimbot detected**

<details>
<summary>📋 Detection Methods</summary>

Rather than aiming for direct hits, this variant targets the ground or wall position that maximises splash damage on the target. Harder to detect because the projectile never needs to touch the player directly.

<details>
<summary>🤖 Automated — Explosion Origin vs Target Position Efficiency</summary>

**What to measure:**
- For each splash damage event, compute the distance from explosion origin to victim at time of damage
- Compare against the optimal splash position (distance that maximises damage given the weapon's splash radius)

**What to look for:**
- 🟡 Explosion origins consistently at the mathematically optimal splash distance — not direct hits, but not random floor shots either
- 🟡 Damage values clustering at maximum splash efficiency more often than statistical chance would produce

</details>

<details>
<summary>🤖 Automated — Indirect Fire Awareness</summary>

**What to measure:**
- Detect shots where the projectile travels through a doorway or around geometry to reach a target the shooter couldn't directly see
- Measure how often these indirect splash shots are accurate vs random

**What to look for:**
- 🟡 Accurate indirect fire at positions requiring knowledge of the exact target location behind cover — suggests ESP + projectile aimbot
- 🟢 Consistent corner splash shots requiring game sense far beyond the player's observed overall skill level

</details>

</details>

---

### ◆ Auto-Detonate

- [✅] **Auto-detonate (stickybomb) detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically detonates stickybombs at the optimal frame — when a target walks over them or reaches maximum damage range.

<details>
<summary>🤖 Automated — Detonation Timing vs Target Proximity</summary>

**What to measure:**
- For each sticky detonation that deals damage, record target distance from explosion origin at the moment of detonation
- Compare against the optimal detonation distance for maximum damage

**What to look for:**
- 🔴 Detonations consistently occurring on the exact tick the target reaches maximum-damage proximity
- 🔴 Detonation latency of 0–1 ticks from target entering optimal range — impossible human reaction
- 🟡 Damage dealt per detonation consistently at the theoretical maximum value

</details>

<details>
<summary>🤖 Automated — Multi-Sticky Coordination</summary>

**What to measure:**
- When multiple stickies are placed, check whether detonation timing accounts for all targets simultaneously

**What to look for:**
- 🟡 Detonation timing that maximises total damage to multiple targets simultaneously — requires tracking all target positions at once

</details>

</details>

---

### ◆ Auto-Airblast

- [✅] **Auto-airblast detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically airblasts incoming projectiles. Used by Pyro to deflect rockets, stickies, arrows, and other projectiles.

<details>
<summary>🤖 Automated — Airblast Reaction Time vs Projectile Position</summary>

**What to measure:**
- Track incoming projectile positions each tick
- Record the tick of each airblast input
- Compute projectile distance from the Pyro at the moment airblast fires

**What to look for:**
- 🔴 Airblast firing when a projectile is at exactly the optimal deflection distance, consistently, with 0–1 tick reaction time
- 🔴 100% or near-100% deflection success rate across many projectile encounters
- 🟡 Deflecting projectiles not yet visible from the Pyro's perspective (approaching from behind or around a corner)

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Pyro deflecting every incoming rocket, sticky, or arrow with no misses over an extended sequence
- Airblasting projectiles that haven't yet appeared on-screen from the Pyro's viewpoint
- Deflection timing that appears instant regardless of projectile speed or trajectory

</details>

</details>

---

## Crithack

> Critical hit manipulation comes in distinct forms with different detection signatures.

---

### ◆ Force Crits

- [✅] **Force crits detected**

<details>
<summary>📋 Detection Methods</summary>

Manipulates TF2's crit RNG to force crits on every shot or at an inflated rate.

<details>
<summary>🤖 Automated — Crit Rate Statistical Analysis</summary>

**What to measure:**
- Count crits across the session and compute observed crit rate per weapon
- Compare against expected crit rate using TF2's documented formula (base 2% scaling with recent damage dealt)
- Compute z-score of observed vs expected

**What to look for:**
- 🔴 Crit rate exceeding 3+ standard deviations above expected over a session with 50+ eligible shots
- 🔴 Crit rate at or near 100% — no legitimate weapon achieves this outside of specific mechanics
- 🟡 Crit rate that spikes at specific moments (suggesting on-demand activation) rather than appearing randomly

**Implementation notes:**
- Must exclude guaranteed crits: Kritzkrieg uber, Buff Banner/Battalion's Backup/Concheror activation, Killing Gloves of Boxing buffs, etc.
- Must exclude crit boosts from conditions: Jarate, marked-for-death, Fan O'War, etc.
- Minimum sample: 50 eligible shots for meaningful statistics

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Weapons glowing orange/yellow with crit effects on every shot with no uber or buff active
- Kill feed showing repeated crit kills in rapid succession from the same player
- Crit effects persisting across weapon switches with no buff source visible

</details>

</details>

---

### ◆ Melee Always Crit

- [✅] **Melee always-crit detected**

<details>
<summary>📋 Detection Methods</summary>

Forces melee weapons to always deal critical hits regardless of normal conditions.

<details>
<summary>🤖 Automated — Melee-Specific Crit Rate</summary>

**What to measure:**
- Count melee hits and melee crits separately from ranged crits
- Melee base crit chance is 15% (higher than most weapons)

**What to look for:**
- 🔴 Melee crit rate at or near 100% over 10+ swings with no Kritz or crit-boost conditions active
- 🟡 Melee crits occurring on weapons with specific unmet crit conditions (e.g. Disciplinary Action without hitting a teammate first)

</details>

</details>

---

### ◆ Avoid Random Crits

- [✅] **Random crit avoidance detected**

<details>
<summary>📋 Detection Methods</summary>

Suppresses fire on ticks where a random crit would have been granted, preventing the player from ever wasting a crit on an unintended shot.

<details>
<summary>🤖 Automated — Attack Pause at Predicted Crit Windows</summary>

**What to measure:**
- Model TF2's crit RNG to predict which ticks would produce random crits given the player's damage history
- Check whether attack inputs pause or stop on those specific ticks

**What to look for:**
- 🟡 Statistically significant correlation between predicted crit-tick windows and attack input pauses
- 🟢 Zero random crits across a full session of sustained combat — improbable but not conclusive alone

**Implementation notes:**
- TF2's crit seed is partially deterministic from session start — modelling requires knowing full damage history
- This signal is weak alone; combine with other crit-related signals

</details>

</details>

---

## Spread Removal (NoSpread)

- [✅] **Spread removal detected**

<details>
<summary>📋 Detection Methods</summary>

Removes or reduces bullet spread, making every bullet go precisely where the crosshair points regardless of the weapon's spread cone.

<details>
<summary>🤖 Automated — Shot Grouping Analysis</summary>

**What to measure:**
- For shotgun-type weapons, reconstruct pellet landing positions from damage events and victim hitbox data
- Compare the distribution of hits against the expected spread cone for the weapon at the measured range

**What to look for:**
- 🔴 All pellets consistently landing within <1° of crosshair center — no spread cone visible
- 🔴 Damage per shot consistently at theoretical maximum (spread normally distributes pellets, reducing effective damage at range)
- 🟡 Headshot rate on spread weapons far above expectation (spread should scatter pellets away from the head)

</details>

<details>
<summary>🤖 Automated — Damage Per Hit vs Range Curve</summary>

**What to measure:**
- Compare damage per hit against the weapon's expected falloff curve at the measured player-to-target distance

**What to look for:**
- 🟡 Consistently dealing maximum theoretical damage at ranges where falloff and spread should reduce it
- 🟡 Damage distribution clustered at maximum values rather than the variance spread normally introduces

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Scattergun or shotgun hits dealing full damage at ranges where spread would normally cause misses
- Consistent headshots with spread weapons at distances where individual pellets should rarely reach the head hitbox

</details>

</details>

---

## Backtrack

- [✅] **Backtrack detected**

<details>
<summary>📋 Detection Methods</summary>

Allows hitting enemies at positions they occupied several ticks ago by exploiting the server's lag compensation window (up to ~200ms / ~13 ticks on Valve servers).

<details>
<summary>🤖 Automated — Damage Origin vs Historical Target Position</summary>

**What to measure:**
- At each damage event, record the target's current server position and the attacker's viewangle
- Also record target positions for the previous 13 ticks
- Determine which historical position best aligns with the attacker's viewangle at time of firing

**What to look for:**
- 🔴 Consistent pattern of shots aligning with target positions from 3–13 ticks in the past rather than the current position
- 🔴 Temporal offset distribution clustering at a fixed value (the configured backtrack window) rather than near zero

**Implementation notes:**
- Store a circular buffer of entity positions per tick during demo parsing
- For each `player_hurt` event, compute angular offset to current and each historical position
- The best-fit historical tick that minimises angular offset is the "effective" backtrack amount

</details>

<details>
<summary>🤖 Automated — Hit Through Cover Detection</summary>

**What to measure:**
- At the tick of a damage event, check if the target's current position is behind cover from the attacker's perspective
- Then check if the target's historical positions were exposed

**What to look for:**
- 🔴 Damage events where the target is currently behind a wall but was exposed several ticks ago — classic backtrack hit
- 🟡 This pattern repeating consistently across the session

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Shots appearing to hit a player who has already moved behind cover
- Death cam showing the killer's crosshair not on the victim's current position at the moment of the killing blow
- Players being hit mid-teleport or immediately after rounding a corner

</details>

</details>

---

## Fakelag / Packet Choking

> Fakelag deliberately delays position updates sent to the server, making the player's hitbox appear at a stale position to opponents. There are distinct modes with different detectable signatures.

---

### ◆ Plain Fakelag

- [✅] **Plain fakelag detected**

<details>
<summary>📋 Detection Methods</summary>

Holds packets for a fixed number of ticks then releases them all at once, creating a predictable, regular stutter.

<details>
<summary>🤖 Automated — Fixed-Interval Position Burst Detection</summary>

**What to measure:**
- Track position update intervals per player in the demo stream
- Measure whether gaps between updates follow a fixed repeating pattern

**What to look for:**
- 🔴 Position updates arriving in bursts at exact regular intervals (e.g. every 8 ticks) rather than every tick
- 🔴 Player appearing to teleport a consistent distance every N ticks, matching a fixed choke count

**Implementation notes:**
- The `PlainTicks` cheat parameter sets the exact interval — common values are 4–14 ticks
- Demo files record server-observed positions; choking manifests as gaps in the position stream

</details>

</details>

---

### ◆ Random Fakelag

- [✅] **Random fakelag detected**

<details>
<summary>📋 Detection Methods</summary>

Holds packets for a random number of ticks up to a configured maximum, making the stutter irregular and harder to predict.

<details>
<summary>🤖 Automated — Bounded-Random Update Interval Analysis</summary>

**What to measure:**
- Measure inter-update intervals for each player
- Compute the distribution and upper bound of update gaps

**What to look for:**
- 🟡 Update intervals varying randomly but always bounded by a consistent maximum (the configured `RandomTicks` limit)
- 🟡 Update interval distribution that is roughly uniform between 1 and N ticks rather than consistently 1 tick
- 🟢 The maximum observed gap remaining suspiciously consistent across the session even while the distribution varies

</details>

</details>

---

### ◆ Adaptive / Conditional Fakelag

- [✅] **Adaptive fakelag detected**

<details>
<summary>📋 Detection Methods</summary>

Fakelag that activates or changes behavior conditionally — e.g. only while shooting, only while taking damage, or deactivating on attack to preserve hit registration.

<details>
<summary>🤖 Automated — Fakelag State Correlation with Combat Events</summary>

**What to measure:**
- Identify fakelag periods (position update gaps) and correlate them with attack inputs and incoming damage events
- The `UnchokeOnAttack` cheat option causes fakelag to deactivate exactly when the player fires

**What to look for:**
- 🔴 Position updates resuming normal frequency on the exact tick of an attack input, then reverting to choking immediately after — the `UnchokeOnAttack` signature
- 🟡 Fakelag consistently activating after firing and deactivating just before the next shot
- 🟡 Fakelag that stops during incoming damage events (defensive conditional fakelag)

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Player stuttering or teleporting only during active combat, moving smoothly otherwise
- Player's hitbox clearly not where their model is during firefights
- Player appearing immune to hits despite being in the open — hitbox is at a previous position

</details>

</details>

---

## Anti-Aim

> Anti-aim manipulates the player's networked viewangles to distort hitbox positions and make them difficult to target. There are many distinct variants with different detection signatures.

---

### ◆ Pitch Anti-Aim

- [✅] **Pitch anti-aim detected**

<details>
<summary>📋 Detection Methods</summary>

Sets the player's pitch angle to an invalid or extreme value to distort the head hitbox's vertical position.

<details>
<summary>🤖 Automated — Pitch Range Violation Detection</summary>

**What to measure:**
- Record the player's pitch angle each tick from demo usercmd data
- Flag any pitch values outside the range achievable by legitimate player input (~-89° to +89°)

**What to look for:**
- 🔴 Pitch values at exactly ±90° — impossible through normal mouse input
- 🔴 Pitch locked to a constant extreme value for 10+ consecutive ticks that never varies during movement
- 🟡 Pitch flipping between a valid value and an invalid value in a repeating pattern

</details>

<details>
<summary>🤖 Automated — Fake vs Real Pitch Separation at Fire Events</summary>

**What to measure:**
- Compare pitch at the moment of firing against pitch during non-combat movement
- Some implementations use a "real" pitch for hit registration and a "fake" pitch for visual appearance

**What to look for:**
- 🟡 Pitch correcting to a valid value for exactly the tick of an attack input, then returning to an invalid value
- 🟡 Pitch values that are always invalid except during shooting sequences

</details>

</details>

---

### ◆ Yaw Anti-Aim — Static / Offset

- [✅] **Static yaw anti-aim detected**

<details>
<summary>📋 Detection Methods</summary>

Sets the yaw to a fixed offset from the player's movement direction to present the back or shoulder to opponents.

<details>
<summary>🤖 Automated — Yaw-to-Movement-Direction Offset Analysis</summary>

**What to measure:**
- Compute the player's movement direction each tick from velocity vectors
- Compute the offset between movement direction and yaw
- Track whether this offset is maintained with suspicious consistency

**What to look for:**
- 🟡 Yaw consistently offset from movement direction by a fixed value (e.g. always 180° — perpetually facing backwards while moving forward)
- 🟡 Yaw maintaining a relationship to movement direction that is too constant for natural mouse movement

</details>

</details>

---

### ◆ Yaw Anti-Aim — Spin

- [✅] **Spin yaw anti-aim detected**

<details>
<summary>📋 Detection Methods</summary>

Continuously rotates the yaw at high speed to create an unpredictable, constantly-moving target.

<details>
<summary>🤖 Automated — Continuous Constant-Rate Yaw Rotation</summary>

**What to measure:**
- Compute yaw delta per tick
- Look for sustained periods of constant-direction rotation at a consistent rate

**What to look for:**
- 🔴 Yaw rotating at the same speed every tick continuously for 10+ ticks — no human can spin their mouse at a constant rate
- 🔴 Rotation rate matching documented spin speed values (common: 10–20°/tick)
- 🟡 Rotation continuing even during knockback or damage events (a human would break their spin)

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Player model spinning continuously at an unnatural, metronomically constant rate
- Body completing full 360° rotations repeatedly with no variation in speed

</details>

</details>

---

### ◆ Yaw Anti-Aim — Jitter

- [✅] **Jitter yaw anti-aim detected**

<details>
<summary>📋 Detection Methods</summary>

Rapidly alternates the yaw between two fixed angles every tick or every N ticks, causing the hitbox to flicker between two positions.

<details>
<summary>🤖 Automated — Perfect Binary Yaw Alternation</summary>

**What to measure:**
- Track yaw values tick-by-tick
- Look for exact binary alternation between two fixed values

**What to look for:**
- 🔴 Yaw switching between exactly two values (e.g. +90° and -90°) on every tick with zero deviation — mechanically impossible with a mouse
- 🔴 The two alternating values being symmetric around a center point (standard jitter anti-aim configuration)
- 🟡 Alternation frequency matching common jitter configurations (every tick, every 2 ticks)

</details>

</details>

---

### ◆ Yaw Anti-Aim — Edge / Peek-based

- [✅] **Edge / peek-based yaw anti-aim detected**

<details>
<summary>📋 Detection Methods</summary>

Dynamically adjusts yaw to expose the minimum possible hitbox profile to each visible opponent, computed relative to their positions.

<details>
<summary>🤖 Automated — Yaw Optimization Against Opponent Positions</summary>

**What to measure:**
- Record each opponent's position relative to the player each tick
- Compute which yaw angle minimises exposed hitbox profile to all visible opponents
- Compare this optimal anti-aim yaw against the player's actual yaw

**What to look for:**
- 🟡 Player's yaw consistently matching the computed optimal anti-aim angle relative to opponent positions
- 🟡 Yaw updating on the exact tick opponent positions change, accounting for their new angles

</details>

</details>

---

### ◆ Fake Yaw (Desync)

- [✅] **Fake yaw / desync detected**

<details>
<summary>📋 Detection Methods</summary>

Creates a discrepancy between the visual body yaw opponents see and the real yaw used for hit registration, by exploiting the gap between client and server angle processing.

<details>
<summary>🤖 Automated — Body Yaw vs Viewangle Yaw Discrepancy</summary>

**What to measure:**
- The player body yaw is networked separately from the viewangle yaw in TF2's entity system
- Compare the two values each tick

**What to look for:**
- 🔴 Consistent large discrepancy (>45°) between body yaw and viewangle yaw for sustained periods — indicates deliberate desync
- 🔴 Body yaw facing one direction while viewangle yaw faces a significantly different direction

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Player model body facing a completely different direction than where the player appears to be looking or moving
- Damage registering in a position inconsistent with the player's visible model orientation

</details>

</details>

---

### ◆ Minwalk

- [✅] **Minwalk anti-aim detected**

<details>
<summary>📋 Detection Methods</summary>

Moves at the minimum speed that still counts as movement (~5 HU/s), reducing the server-side velocity threshold used in lag compensation and hitbox calculations.

<details>
<summary>🤖 Automated — Speed Clustering at Minimum Walk Threshold</summary>

**What to measure:**
- Measure movement speed when other anti-aim signals are present
- Compare against the known minwalk speed threshold

**What to look for:**
- 🟡 Movement speed clustering exactly at the minimum walk threshold (~5 HU/s) during suspected anti-aim sequences
- 🟡 Speed that never drops to zero but also never meaningfully exceeds the threshold during anti-aim periods

</details>

</details>

---

## Doubletap / Warp

- [✅] **Doubletap / warp detected**

<details>
<summary>📋 Detection Methods</summary>

Fires a weapon twice within a single server tick window or sends movement commands at double the normal rate, effectively doubling fire speed.

<details>
<summary>🤖 Automated — Sub-Fire-Rate Damage Events</summary>

**What to measure:**
- For each weapon, establish the minimum tick count between consecutive shots based on fire rate
- Flag damage events from the same player+weapon occurring faster than the weapon's cycle allows

**What to look for:**
- 🔴 Two damage events from a single weapon within fewer ticks than its fire cycle permits
- 🔴 Two explosion events from a single Soldier/Demoman within the same tick
- 🟡 Attack inputs in the usercmd stream occurring at double the normal rate for the weapon

</details>

<details>
<summary>🤖 Automated — Command Number Sequence Analysis</summary>

**What to measure:**
- Usercmd command numbers should increment by exactly 1 per tick in normal play
- Doubletap/warp can cause command number anomalies detectable in the demo stream

**What to look for:**
- 🔴 Command numbers that skip values, duplicate, or arrive out of sequence
- 🟡 Ticks where the player appears to process more commands than server ticks elapsed

</details>

<details>
<summary>🤖 Automated — Pre-Shot Movement Freeze Signature</summary>

**What to measure:**
- Doubletap requires choking ticks to build up the "warp" — the player position does not update for several ticks before firing
- Measure movement freeze periods immediately preceding damage events

**What to look for:**
- 🟡 Stationary periods of 2–8 ticks immediately before damage events followed by immediate movement resumption
- 🟡 This freeze-fire-move pattern repeating consistently across the session

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Weapon appearing to fire twice before the reload animation plays
- Two explosion or damage numbers appearing at nearly identical timestamps from one player
- Brief movement freezes before shots that aren't explained by scoping or charging

</details>

</details>

---

## Speedhack

- [✅] **Speedhack detected**

<details>
<summary>📋 Detection Methods</summary>

Manipulates the client-side game clock to move faster than server physics allows.

<details>
<summary>🤖 Automated — Displacement Per Tick vs Class Speed Cap</summary>

**What to measure:**
- Compute per-tick movement distance from position deltas in the demo
- Compare against maximum class speed caps, accounting for active conditions

**Class speed caps for reference:**

| Class | Base Max Speed (HU/s) |
|-------|----------------------|
| Scout | 400 |
| Soldier | 240 |
| Pyro | 300 |
| Demoman | 280 |
| Heavy (running) | 230 |
| Engineer | 300 |
| Medic | 320 |
| Sniper | 300 |
| Spy | 320 |

**What to look for:**
- 🔴 Consistent movement distance per tick exceeding the class speed cap with no legitimate explanation
- 🟡 Speed exceeding cap at predictable multiplier values correlating with common cheat settings (1.5×, 2×)

</details>

<details>
<summary>🤖 Automated — Average Speed Over Sustained Movement Windows</summary>

**What to measure:**
- Over a 5–10 second continuous movement window, compute total distance / elapsed time
- Compare implied average speed against class maximum

**What to look for:**
- 🔴 Average speed over sustained movement implying a velocity above class maximum
- 🟡 Intermittent speed bursts suggesting activation rather than constant speedhack

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Player visibly moving faster than their class should allow, especially in straight lines
- Catching up to faster classes with no speed buffs active

</details>

</details>

---

## Resolver (Counter-Anti-Aim)

> Resolvers attempt to predict the "real" yaw of an anti-aiming opponent so the aimbot can correctly target their hitbox. Different resolver strategies leave different detectable patterns.

---

### ◆ Static Offset Resolver

- [🚧] **Static offset resolver detected**

<details>
<summary>📋 Detection Methods</summary>

Applies a fixed angular offset to the target's visible yaw, assuming the anti-aim is a predictable static rotation.

<details>
<summary>🤖 Automated — Consistent Aim Offset Against Anti-Aim Players</summary>

**What to measure:**
- For players confirmed to be using anti-aim, measure the attacker's aim angle relative to the anti-aimer's visible yaw when hits register
- If the attacker uses a static offset resolver, hits consistently land when their aim is at a fixed offset from the target's fake yaw

**What to look for:**
- 🟡 Attacker consistently shooting at a position exactly N degrees offset from where the target appears to be facing
- 🟡 This offset remaining consistent across the session regardless of the target's movement

</details>

</details>

---

### ◆ Cycling Resolver

- [🚧] **Cycling resolver detected**

<details>
<summary>📋 Detection Methods</summary>

Cycles through multiple possible yaw offsets on successive shots until a hit registers, then locks to that offset.

<details>
<summary>🤖 Automated — Sequential Offset Pattern in Shot Angles</summary>

**What to measure:**
- Track the angle between the attacker's viewangle and the target's anti-aim yaw for each consecutive shot against the same target
- Look for a systematic progression through offset values

**What to look for:**
- 🟡 Shots at systematically varying angular offsets in sequence (e.g. 0°, +45°, -45°, +90°, -90°) before a hit registers
- 🟡 After a successful hit, all subsequent shots against the same target using the same offset (lock-in behavior)
- 🟢 Offset sequence matching known `CycleYaw` cycling intervals from documented cheat configs

</details>

</details>

---

### ◆ View-Based Resolver

- [🚧] **View-based resolver detected**

<details>
<summary>📋 Detection Methods</summary>

Uses the direction the anti-aimer appears to be looking (their networked eye position) to infer their real yaw despite the body facing a different direction.

<details>
<summary>🤖 Automated — Hit Correlation with Target Eye Direction</summary>

**What to measure:**
- For each hit on an anti-aiming player, compute the angle from attacker to target's eye position
- Check if hits correlate with shots aimed at the eye direction rather than the body direction

**What to look for:**
- 🟢 Hits consistently occurring when the attacker's aim matches the direction the target's eyes appear to face, despite the body facing elsewhere

</details>

</details>

---

### ◆ Minwalk Resolver

- [🚧] **Minwalk resolver detected**

<details>
<summary>📋 Detection Methods</summary>

Detects whether the target is using minwalk and adjusts resolver behavior accordingly, as minwalk changes which hitbox offset is most effective.

<details>
<summary>🤖 Automated — Resolver Behavior Change at Minwalk Speed Threshold</summary>

**What to measure:**
- Track the target's movement speed
- Track whether the attacker's effective aim offset changes when the target's speed crosses the minwalk threshold

**What to look for:**
- 🟢 Attacker's effective aim offset changing at exactly the speed threshold associated with minwalk activation
- 🟢 Higher hit rate correlated with periods the target is using minwalk speed

</details>

</details>

---

## ESP / Wallhack (Behavioral)

> ESP cannot be directly observed in a demo but leaves consistent behavioral traces. Different ESP types have distinct behavioral signatures.

---

### ◆ Player ESP

- [✅] **Player ESP (behavioral) detected**

<details>
<summary>📋 Detection Methods</summary>

Displays enemy positions through walls. Leaves behavioral traces via pre-aim, routing decisions, and reactions to hidden threats.

<details>
<summary>🤖 Automated — Pre-aim Through Geometry</summary>

**What to measure:**
- Identify ticks where an enemy is behind solid geometry from the player's perspective (no line of sight)
- Check whether the player's crosshair points at the enemy's position despite the wall

**What to look for:**
- 🔴 Crosshair consistently tracking enemy positions through walls — following enemy movement on the other side of geometry
- 🔴 Pre-aiming at non-obvious positions an enemy occupies behind cover before rounding a corner
- 🟡 Statistical correlation between crosshair direction and nearest hidden enemy position exceeding chance

**Implementation notes:**
- Requires visibility computation per tick — expensive; consider sparse sampling
- Build a null hypothesis from known common pre-aim spots to reduce false positives from map knowledge

</details>

<details>
<summary>🤖 Automated — Routing Toward Hidden Enemies</summary>

**What to measure:**
- Track player routing decisions at choice points (intersections, multi-path areas)
- Check whether route choices correlate with hidden enemy positions

**What to look for:**
- 🟡 Consistently choosing routes toward enemy clusters the player cannot see
- 🟡 Avoiding routes that lead into an ambush that hasn't been sprung yet

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Crosshair visibly tracking a player through solid geometry
- Shooting at exactly the right moment as an enemy pushes a doorway, before they appear
- Repositioning away from a flank that hasn't happened yet with no visible or audible cue

</details>

</details>

---

### ◆ Object / Pickup ESP

- [❌] **Object / Pickup ESP (behavioral) detected**

<details>
<summary>📋 Detection Methods</summary>

Displays health pack, ammo, and resupply positions through walls. Leaves navigation traces.

<details>
<summary>🤖 Automated — Pickup Navigation Efficiency</summary>

**What to measure:**
- Track routes taken to health and ammo when the player is low
- Compare against what a player with no information would do

**What to look for:**
- 🟡 Always navigating directly to the nearest pickup by shortest path, even in non-obvious locations, without any search behavior
- 🟡 Never walking past a full health pack without collecting it even when approaching from an angle where it wouldn't normally be visible

</details>

</details>

---

### ◆ Spy / Cloak ESP

- [✅] **Spy / Cloak ESP (behavioral) detected**

<details>
<summary>📋 Detection Methods</summary>

Reveals cloaked or disguised Spy positions. Extremely high-confidence when a player consistently tracks fully cloaked Spies with no information source.

<details>
<summary>🤖 Automated — Cloaked Spy Tracking</summary>

**What to measure:**
- Track Spy cloak state from condition data in the demo
- When a Spy is fully cloaked and silent, check if other players' crosshairs track the Spy's position

**What to look for:**
- 🔴 A player's crosshair following the exact path of a fully cloaked, silent Spy with no audio or visual indicator present
- 🔴 Shooting at the position of a cloaked Spy and landing hits (requires combined ESP + aimbot)
- 🟡 Turning to face a Spy on the exact tick they cloak rather than after a search period

</details>

<details>
<summary>🤖 Automated — Disguise Identification Reaction Time</summary>

**What to measure:**
- Measure time between a disguised enemy Spy entering the player's FOV and the player beginning to target them
- A disguise should introduce hesitation; ESP removes it

**What to look for:**
- 🟡 Instantly targeting a disguised enemy Spy on first sight with zero hesitation or confusion
- 🟡 Never being fooled by a disguise across an entire session

</details>

<details>
<summary>👁️ Manual — Visual Review Signals</summary>

**What to watch for:**
- Player tracking the precise path of a cloaked Spy while apparently looking elsewhere
- Attacking a fully cloaked Spy with no audio cue visible in the demo timeline
- Never showing any uncertainty when encountering a disguised enemy Spy

</details>

</details>

---

## Movement Exploits

---

### ◆ Bunny Hop Hack

- [✅] **Bunny hop hack detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically jumps on the exact first tick of being grounded, achieving near-perfect bhop chains.

<details>
<summary>🤖 Automated — Ground Frame Jump Timing</summary>

**What to measure:**
- Identify each landing event (player transitions from airborne to grounded state)
- Record whether jump input occurs on tick 0, 1, 2, etc. of being grounded
- Compute success rate (jumps on tick 0 / total landing opportunities)

**What to look for:**
- 🔴 Success rate above 85% sustained over 20+ attempts
- 🔴 Jump input always on tick 0 of grounded state — humans have minimum 1–2 tick variance
- 🟡 Success rate that does not degrade with speed (humans struggle more at higher speeds)

</details>

</details>

---

### ◆ Strafe Hack

- [✅] **Strafe hack / auto-strafe detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically synchronises mouse movement with strafe keys to achieve optimal air acceleration every tick.

<details>
<summary>🤖 Automated — Mouse-Strafe Synchronization Coefficient</summary>

**What to measure:**
- During airborne movement, compute the correlation between angular velocity (mouse rate) and strafe key direction per tick
- Compute the Pearson correlation coefficient across the airborne period

**What to look for:**
- 🟡 Correlation coefficient consistently above 0.97 over many airborne sequences — top humans rarely sustain above 0.90–0.95
- 🟡 Acceleration per tick consistently at the maximum achievable value — no suboptimal strafe ticks

</details>

</details>

---

### ◆ EdgeJump

- [🚧] **EdgeJump hack detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically jumps on the last possible grounded tick before walking off a ledge, preserving momentum.

<details>
<summary>🤖 Automated — Last-Ground-Tick Jump Precision</summary>

**What to measure:**
- Detect ledge-drop situations (player moves to the edge of a platform and ground state changes)
- Check whether jump input occurs on the last grounded tick

**What to look for:**
- 🔴 Jump input on the exact last grounded tick consistently across multiple instances
- 🔴 Zero failed edge jumps across a session containing many ledge-edge situations

</details>

</details>

---

### ◆ CTap

- [✅] **CTap hack detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically inputs a 1–2 tick crouch on landing to negate fall damage.

<details>
<summary>🤖 Automated — Crouch Duration at Landing Events</summary>

**What to measure:**
- Detect landing events from fall-damage-eligible heights
- Check duration and timing of crouch input centered on the landing tick

**What to look for:**
- 🔴 Crouch input lasting exactly 1 tick at the landing event, consistently across multiple falls
- 🔴 Fall damage being negated at rates inconsistent with human reaction time capability
- 🟡 Crouch input always occurring on tick 0 of landing with near-zero variance

</details>

</details>

---

### ◆ Auto Rocket Jump

- [✅] **Auto rocket jump detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically executes the crouch + fire + jump input sequence for optimal rocket jumping.

<details>
<summary>🤖 Automated — Three-Input Timing Precision</summary>

**What to measure:**
- Detect rocket jump setups (Soldier shooting downward + crouching + jumping in rapid succession)
- Measure tick-level timing between the three inputs

**What to look for:**
- 🟡 All three inputs consistently within 1–2 ticks of each other with near-zero variance across rocket jumps
- 🟡 Rocket jump height and distance consistently at theoretical maximum — no wasted or suboptimal jumps

</details>

</details>

---

### ◆ AutoPeek

- [✅] **AutoPeek detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically moves the player out to take a shot then returns them to cover, minimising exposure time.

<details>
<summary>🤖 Automated — Peek Duration and Repeatability</summary>

**What to measure:**
- Identify peek sequences (player exits cover, fires, returns to cover)
- Measure exposure duration and consistency across peeks

**What to look for:**
- 🟡 Peek exposure duration consistently at the minimum required to fire — never unnecessarily exposed
- 🟡 Return to cover beginning on the exact tick after firing with near-zero variance
- 🟢 Identical peek distances and timing across multiple peeks at the same corner

</details>

</details>

---

### ◆ FastStop / FastAccelerate

- [✅] **FastStop / FastAccelerate detected**

<details>
<summary>📋 Detection Methods</summary>

Rapidly reduces or increases movement speed beyond what normal input allows by manipulating movement inputs at a tick level.

<details>
<summary>🤖 Automated — Deceleration Rate Analysis</summary>

**What to measure:**
- Measure speed reduction per tick when the player stops
- Compare against normal friction deceleration rates for the surface type

**What to look for:**
- 🟡 Deceleration rates exceeding what friction alone can produce
- 🟡 Stopping from full speed in fewer ticks than the minimum physics-dictated stopping distance

</details>

</details>

---

## Automation / Bot Behavior

---

### ◆ NavBot (Pathfinding Bot)

- [✅] **NavBot / pathfinding bot detected**

<details>
<summary>📋 Detection Methods</summary>

Uses TF2's navigation mesh to automatically pathfind to objectives, health, and enemies without human input.

<details>
<summary>🤖 Automated — Path Straightness and Nav Node Alignment</summary>

**What to measure:**
- Extract movement paths from position data
- Compute ratio of actual path length to straight-line distance between waypoints
- Identify whether turns occur at consistent coordinates across multiple rounds

**What to look for:**
- 🔴 Turns occurring at the same geographic coordinates across multiple respawn cycles — these are nav mesh nodes
- 🔴 Path straightness index consistently above 0.95 — humans meander more
- 🟡 Zero exploration behavior — never backtracking, hesitating, or taking suboptimal routes

</details>

<details>
<summary>🤖 Automated — Objective Interaction Timing</summary>

**What to measure:**
- Time between spawning and beginning to move toward the objective
- Route selection consistency across multiple respawn cycles

**What to look for:**
- 🔴 Identical routes taken every single respawn with zero variation
- 🟡 Objective interaction beginning at mechanically consistent timing
- 🟢 Never stopping to react to unusual situations — ambushes, unusual enemy positions, or flankers

</details>

</details>

---

### ◆ Followbot

- [✅] **Followbot detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically follows a specific target player and mimics their movement or maintains a fixed following distance.

<details>
<summary>🤖 Automated — Target-Relative Position Consistency</summary>

**What to measure:**
- For suspected follower-target pairs, compute distance and relative bearing between players over time

**What to look for:**
- 🔴 Follower maintaining a nearly constant distance behind a specific player across map traversal, objective play, and combat
- 🔴 Follower's movement direction always matching the target's direction with a consistent 1–3 tick delay
- 🟡 Follower never losing the target even in complex environments with multiple path options

</details>

<details>
<summary>🤖 Automated — Look Direction Mimicry</summary>

**What to measure:**
- The `CopyImmediate` followbot mode replicates the target's viewangles directly
- Compare viewangle yaw/pitch between two suspected players tick-by-tick

**What to look for:**
- 🟡 Viewangles of two players matching with a fixed tick delay — the copy mode signature
- 🟢 Two players consistently looking in the same direction during movement segments

</details>

</details>

---

### ◆ Auto-Queue / Session Management

- [❌] **Auto-queue / session cycling bot detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically manages queue, map selection, and reconnection to maintain continuous bot operation with minimal human oversight.

<details>
<summary>🤖 Automated — Disconnect / Reconnect Pattern Analysis</summary>

**What to measure:**
- Track session join/leave timestamps relative to game events
- Correlate disconnects with votekick events against the player

**What to look for:**
- 🟡 Disconnecting consistently within 5–10 seconds of a votekick being called against them
- 🟡 Rejoining the same server repeatedly after consecutive disconnects
- 🟢 Session lengths that are suspiciously consistent — automated time-based rotation

</details>

</details>

---

## Medic Automation

---

### ◆ AutoHeal / Target Prioritization

- [🚧] **AutoHeal / target prioritization detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically switches heal targets based on an optimal priority algorithm rather than human judgment.

<details>
<summary>🤖 Automated — Heal Target Switch Reaction Time</summary>

**What to measure:**
- Track heal target changes relative to triggering events (new target enters range, current target dies, health thresholds cross)
- Measure time between the triggering event and beam switching

**What to look for:**
- 🔴 Beam switching on tick 0 of a new optimal target becoming available — impossible human reaction
- 🟡 Heal target priority always matching the optimal algorithm (lowest HP, highest overheal gap) with zero suboptimal choices

</details>

</details>

---

### ◆ AutoVaccinator

- [✅] **AutoVaccinator detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically switches the Vaccinator's damage resist type to match incoming damage type.

<details>
<summary>🤖 Automated — Resist Switch vs Damage Type Timing</summary>

**What to measure:**
- Track Vaccinator resist state changes from condition events
- Correlate with the first incoming damage event of each type

**What to look for:**
- 🔴 Resist type changing to the correct type within 0–1 ticks of the first incoming damage of that type
- 🔴 Never having the incorrect resist active when taking damage across the entire session
- 🟡 Switching between bullet/blast/fire resist with inhuman precision during complex multi-source-damage scenarios

</details>

</details>

---

### ◆ Auto-Uber Deployment

- [🚧] **Auto-Uber deployment detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically deploys Uber at a configured health threshold or in response to anticipated incoming damage.

<details>
<summary>🤖 Automated — Deployment Health Threshold Distribution</summary>

**What to measure:**
- Record health of Medic and heal target at each Uber deployment tick
- Measure distribution across multiple Uber deployments in the session

**What to look for:**
- 🟡 Uber always deploying at exactly the same health threshold — no early panic pops, no dying without deploying
- 🟡 Deployment timing that precedes incoming damage rather than reacting to it (requires combined ESP)

</details>

</details>

---

### ◆ Auto-Arrow (Crusader's Crossbow)

- [🚧] **Auto-arrow (Crusader's Crossbow) detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically aims the Crossbow at injured teammates, accounting for projectile travel time.

<details>
<summary>🤖 Automated — Arrow Lead Accuracy vs Teammate Velocity</summary>

**What to measure:**
- For healing arrows that hit teammates, compute the optimal lead angle given teammate velocity and Crossbow projectile speed
- Compare against actual aim angle at fire

**What to look for:**
- 🟡 Perfectly optimal lead on moving teammates consistently — accounting for travel time with no error
- 🟡 100% hit rate on moving teammates at range across the session

</details>

</details>

---

## Engineer Automation

---

### ◆ Auto-Repair

- [❌] **Auto-repair detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically switches to wrench and begins repairing buildings the instant they take damage.

<details>
<summary>🤖 Automated — Repair Input vs Damage Event Timing</summary>

**What to measure:**
- Track building damage events
- Measure time between damage event and Engineer beginning to repair (tool switch + repair input)

**What to look for:**
- 🔴 Repair beginning within 0–1 ticks of damage being applied — impossible human reaction
- 🟡 Repair reaction time clustering at a fixed low value consistently across many damage instances

</details>

</details>

---

### ◆ Auto-Upgrade

- [❌] **Auto-upgrade detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically upgrades buildings at exactly the minimum required metal threshold.

<details>
<summary>🤖 Automated — Metal Level at Upgrade Trigger</summary>

**What to measure:**
- Track metal amount each tick
- Record the exact metal value at which upgrade inputs are triggered

**What to look for:**
- 🟡 Upgrade always triggering at exactly the minimum required metal — never waiting, never short
- 🟡 Multi-building upgrade sequences following a perfectly optimal order every time

</details>

</details>

---

## Spy Automation

---

### ◆ AutoBackstab

- [✅] **AutoBackstab detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically executes a backstab on the first tick a valid backstab angle is achieved.

<details>
<summary>🤖 Automated — Backstab Angle Precision at Attack Input</summary>

**What to measure:**
- TF2 backstabs require the Spy to be within approximately ±60° of behind the target (server-side angle check)
- For each backstab, compute the exact angular offset between Spy approach direction and target facing direction at the moment of attack

**What to look for:**
- 🔴 Attack input always occurring on tick 0 of a valid backstab angle being reached — zero delay
- 🔴 100% backstab success rate across all melee attacks from behind — no missed timing windows
- 🟡 Melee attack timing always at the exact first valid frame, never 1–2 ticks into the window

</details>

<details>
<summary>🤖 Automated — Decloak-to-Stab Timing</summary>

**What to measure:**
- Measure time between decloaking and backstab attack input

**What to look for:**
- 🔴 Sequence executing in the minimum physically possible number of ticks with near-zero variance
- 🟡 Timing that consistently maximises the window between the decloak sound and the stab (minimising target reaction time)

</details>

</details>

---

### ◆ Anti-Backstab Detection Bypass

- [✅] **Anti-backstab evasion (Razorback) detected**

<details>
<summary>📋 Detection Methods</summary>

Automatically detects when a target has the Razorback equipped and avoids wasting a backstab attempt on them.

<details>
<summary>🤖 Automated — Weapon Switch Correlated with Razorback Target</summary>

**What to measure:**
- Track which Sniper targets have the Razorback equipped (loadout visible in demo entity data)
- Check whether the Spy avoids or aborts melee attacks against Razorback Snipers

**What to look for:**
- 🟡 Spy consistently switching weapons or diverting when approaching a Razorback Sniper, with no visible in-game cue available
- 🟢 Zero wasted backstab attempts on Razorback targets across a full session

</details>

</details>

---

## Account / Meta Signals

- [✅] **Suspicious account profile**
- [✅] **Cross-session performance anomaly**
- [✅] **Bot network / coordinated account signature**

<details>
<summary>📋 Detection Methods</summary>

<details>
<summary>🤖 Automated — Performance Consistency Across Sessions</summary>

**What to measure:**
- Aggregate key metrics (accuracy, bhop rate, reaction time, etc.) across multiple demos from the same SteamID
- Measure variance in these metrics between sessions

**What to look for:**
- 🟡 Unnaturally flat performance across sessions — legitimate players have good and bad days with significant variance
- 🟡 Performance that does not degrade with high server ping (cheaters using lag compensation abuse may perform better at high ping)
- 🟢 Performance consistent regardless of class or map — legitimate players show skill variation by class and map familiarity

</details>

<details>
<summary>🤖 Automated — Cross-Player Correlation</summary>

**What to measure:**
- Look for groups of accounts consistently appearing in the same sessions together
- Check whether multiple accounts show matching behavioral fingerprints

**What to look for:**
- 🟡 Two or more accounts always queued together with individually borderline but collectively matching signals — common bot herder pattern
- 🟡 Accounts with near-identical movement and aim signatures suggesting the same cheat config and operator

</details>

<details>
<summary>🤖 Automated — Join / Leave Pattern Analysis</summary>

**What to measure:**
- Track session join/leave timestamps relative to game events (votekicks, round ends, score thresholds)

**What to look for:**
- 🟡 Disconnecting within seconds of a votekick being initiated against them — consistent across multiple sessions
- 🟢 Joining and leaving servers at mechanically consistent intervals (automated rotation)
- 🟢 Never voluntarily leaving a server mid-round for any reason across many sessions

</details>

<details>
<summary>🤖 Automated — Loadout / Class Consistency</summary>

**What to measure:**
- Track class and loadout choices across many sessions

**What to look for:**
- 🟢 Always playing the exact same class with the exact same loadout across every session with zero variation
- 🟢 Loadout choices matching known bot operator patterns or cheat-optimized configurations

</details>

<details>
<summary>👁️ Manual — Account Profile Signals</summary>

**What to watch for:**
- Very new account with disproportionately high playtime in a short window
- Private profile with no friends, no game history beyond TF2
- Name matching known bot naming patterns (random character strings, impersonating famous players)
- Prior VAC bans or game bans on the account
- Multiple accounts with similar names or avatars appearing together in the same sessions
- Accounts created in batches with other suspicious accounts — common bot farm indicator

</details>

</details>

---

### Integrated Database Systems

<details>
<summary><b>Supported External Databases</b></summary>

- **MegaAntiCheat (MAC)** - Utilize MAC's database with your masterbase key
- **TF2BD Playerlists** - Import and use existing TF2 Bot Detector lists and rulesets
- **SteamHistory API** - Enhanced user tracking (requires API key)
  - Provides SourceBans integration automatically
  - Shows SourceMod AntiCheat bans
  - Keyword-based ban detection
- **Steam Web API** - Two methods available:
  - RCON-based data gathering (TF2BD-style)
  - Steam Web API key (recommended)
- **Reputation Sites** - Used to determine priority checking for users

</details>

### Smart User Verification

<details>
<summary><b>Account Analysis Factors</b></summary>

- **VAC/Game Ban Assessment**
  - Recent bans: Higher scrutiny
  - 5+ years: Not automatically checked
  - 10+ years: Considered irrelevant
  - VAC bans never result in auto-conviction (could be false positives like ReShade)
  - Game bans only counted on suspected users (developers can issue arbitrary bans)
  
- **Account Age Checking**
  - Identifies potential alt accounts
  - Only flags when suspicious behavior is present
  - New players are not automatically flagged

- **Reputation Analysis**
  - Profile comments analyzed for keywords and patterns
  - Only counted when sufficiently negative or suspicious
  - Not weighted heavily due to abuse potential

</details>

### User Classification System

- **Convicted** - Confirmed cheaters with labeled detection methods
- **Suspicious** - Marked during active analysis by the replay analyzer
- **Advise** - Flagged for manual community review
- **Clean** - No suspicious activity detected

### Automated Response Actions

- **Auto-kick** - Automatically removes convicted cheaters and bots
- **Chat Alerts** - Notifies other players of convicted cheaters
- **Evidence Submission** - Automatic demo file reporting
- **Blacklist Sync** - Real-time synchronization with master database

---

## 💻 System Requirements

### Supported Platforms
- ✅ Windows
- ✅ Linux
- ⚠️ macOS - *May* work via Wine/Proton but **unsupported** (no official support provided)

### Virtual Machine Support
✅ **Fully supported!** Synapse runs perfectly in VMs - we encourage players to use their preferred setup.

### Hardware Requirements
With our new replay analyzer, you **no longer need a second TF2 instance by default**!

**Standard Setup:**
- **CPU:** Multi-core processor recommended
- **RAM:** 8GB+ recommended
- **Storage:** Space for demo file storage

**Optional: Offload Analysis to Secondary System**
Want maximum performance on your main gaming machine? You can optionally leverage a spare system on your local network to handle replay analysis:
- Second computer on the same local network (or connected via Tailscale/similar)
- Synapse provides everything needed for setup
- Keeps your gaming system at peak performance
- Analysis workload completely offloaded

---

## 🚀 How It Works

1. **Launch TF2** - Synapse serves as your TF2 launcher with optimized settings
2. **Game Monitoring** - Synapse connects to your TF2 instance via RCON
3. **Replay Analysis** - Advanced analyzer processes gameplay in real-time (on your machine or optional secondary system)
4. **Multi-Database Checking** - Cross-references players against multiple databases
5. **Detection Engine** - Analyzes gameplay for known cheat signatures and suspicious patterns
6. **Classification** - Players are marked as convicted, suspicious, or clean
7. **Automated Actions** - Kicks, reports, and alerts based on detections
8. **Community Sync** - Convicted cheaters (only those detected by Synapse) are synced to master database

---

## 📋 Installation

### Prerequisites
- Team Fortress 2 installed
- RCON access (Synapse provides setup instructions if connection fails)

### Optional API Keys (Recommended)
- MegaAntiCheat masterbase key
- SteamHistory API key
- Steam Web API key

### Quick Start

<details>
<summary><b>Installation Steps</b></summary>

1. Download the latest release from the releases page
2. Extract to your preferred location
3. Run Synapse AntiCheat
4. Configure RCON connection (Synapse will guide you)
5. Optionally add API keys for enhanced functionality
6. Start playing!

Synapse can:
- **Automatically connect to TF2** - Links to your running game instance
- **Guide RCON setup** - Provides instructions without requiring game restart
- **Import existing lists** - Load your TF2BD playerlists and rulesets

</details>

---

## ⚙️ Configuration

<details>
<summary><b>API Keys Configuration</b></summary>

### MegaAntiCheat Integration
1. Obtain your masterbase key from MegaAntiCheat
2. Enter in Synapse settings
3. Database will sync automatically

### Steam API Setup
1. Get your API key from https://steamcommunity.com/dev/apikey
2. Add to Synapse configuration
3. Enhanced user lookup enabled

### SteamHistory API
1. Request API key from SteamHistory
2. Configure in settings
3. Advanced tracking features unlocked

</details>

<details>
<summary><b>Import Existing Data</b></summary>

### TF2BD Playerlists
- Import your existing player lists
- Maintain your custom rulesets
- Seamless transition from TF2BD

### SourceBans Integration
- Automatically configured
- Checks for SourceMod AntiCheat bans
- Keyword-based ban detection

</details>

---

## 🛡️ Detection Philosophy & Accuracy

### Our Approach

<details>
<summary><b>What We Consider</b></summary>

✅ **Used as Evidence:**
- Replay analysis results
- Multiple suspicious behavior patterns
- Cross-database verification
- Statistical anomalies
- Movement and aim patterns

❌ **What We DON'T Auto-Convict On:**
- VAC bans alone (too many false positives, e.g., ReShade)
- Game bans alone (can be arbitrary)
- TF2BD or MAC listings alone (not curated by us)
- Inventory value (cheaters use expensive items to appear legit)
- Reputation sites alone (easily manipulated)
- Account age alone (new players aren't cheaters by default)

</details>

<details>
<summary><b>Confidence Rating System</b></summary>

Our confidence ratings are based on:
- Confirmed convictions from our detection engine
- Human review of replay footage
- Cross-validation with multiple detection methods
- Community feedback and manual reviews

**Important Notes:**
- TF2BD lists and MAC convictions strengthen our analysis but don't result in auto-conviction
- We only sync users that **Synapse itself** has convicted to our database
- Manual markings are **NOT** synced to prevent abuse
- Users can share custom lists, but these should be taken with a grain of salt

</details>

---

## 🚫 Blacklist Policy

<details>
<summary><b>Important Information</b></summary>

**Blacklisted users CANNOT use Synapse.** 

This is a permanent restriction because:
- We don't want cheaters using our software
- We don't want them using it against others
- Blacklist decisions are final and irreversible

**Technical Implementation:**
- We detect blacklisted users by our own metrics
- Local countermeasures are placed on the system upon detection
- Once detected, the system stays detected (cannot be bypassed)
- **Zero tolerance policy:** If we detect a cheat injected into TF2 while using Synapse, you will be automatically convicted AND blacklisted
- We will NOT disclose how we detect injected cheats or blacklisted users

**If you've been blacklisted:**
- You cannot appeal through normal channels
- You cannot create new accounts to bypass

</details>

---

## 📊 Performance & Accuracy

- **Active Development** - Continuously improving detection algorithms
- **Community-Driven** - Accuracy improves as more users contribute data
- **Human-Verified** - Confidence ratings validated through manual review
- **Multi-Source Validation** - Cross-references multiple databases and detection methods

---

## 🔒 Privacy & Data Collection

**We respect your privacy.** Synapse does NOT collect any account information whatsoever.

<details>
<summary><b>What We Collect</b></summary>

**The ONLY data we collect:**
- ✅ Conviction data (cheaters detected by Synapse)
- ✅ Player markings from replay analysis

**What we DON'T collect:**
- ❌ Your Steam account information
- ❌ Personal data
- ❌ Chat logs
- ❌ Game settings or preferences
- ❌ System information
- ❌ Location data
- ❌ Any identifying information beyond Steam IDs in convictions

</details>

<details>
<summary><b>Replay Analysis & Opt-Out</b></summary>

**All replay analysis is done ON YOUR MACHINE.**

- No replay data is sent to our servers
- Analysis happens locally using your hardware
- You maintain complete control

**Want to opt out of being an analyst?**
Simply disable replay analysis in settings. You'll still benefit from the community database, but your system won't contribute analysis data.

</details>

---

## 🤝 Community Features

- **Shared Blacklist** - All users benefit from centralized cheater database (Synapse-convicted only)
- **Conviction Labels** - See exactly what cheats each player was caught using
- **Manual Review System** - Submit edge cases for community analysis
- **Evidence Storage** - Automatic demo file preservation and reporting
- **Chat Integration** - Alert other players to convicted cheaters
- **Hive Network** *(Coming Soon)* - Link multiple Synapse instances together!
  - Perfect for LAN parties or networked play
  - Works over local networks or via Tailscale/similar
  - Share a single analyst system across multiple users
  - Automatically prompted when Hive is enabled
  - All connected users benefit from shared analysis power

---

## ⚠️ Important Notes & Disclaimers

<details>
<summary><b>About Inventory Value</b></summary>

**We do NOT account for inventory value.** Cheaters frequently use expensive items (Unusual hats, Australium weapons, etc.) to appear more legitimate. A valuable backpack is not evidence of innocence.

</details>

<details>
<summary><b>About Reputation Sites</b></summary>

Profile reputation and comments are only considered when:
- Sufficiently negative ratings exist
- Multiple suspicious keywords are found in comments
- Used as supporting evidence, never primary evidence

Reputation can be easily manipulated and is not reliable as a primary indicator.

</details>

<details>
<summary><b>About VAC & Game Bans</b></summary>

**VAC Bans:**
- Permanent bans for detected cheats
- We **never** auto-convict based solely on VAC bans
- Older bans may indicate reformed players
- False positives exist and are more common than people think:
  - **ReShade** - Graphics injector for visual enhancements
  - **Texture mods** - Custom skins and textures
  - **ENB Series** - Graphics enhancement suite
  - **SweetFX** - Post-processing injector
  - **Cheat Engine** - If left running in background (even unused)
  - **AutoHotkey scripts** - Macro tools for accessibility
  - **DLL injectors** - Even for legitimate modding purposes

**Game Bans:**
- Only counted on already-suspicious users
- Developers can issue arbitrary bans
- Do not constitute definitive proof of cheating

</details>

<details>
<summary><b>Responsibility & Liability</b></summary>

- Synapse is not responsible for abuse of the software
- Manually marked cheaters **will NOT** be synced to our database
- Only Synapse-detected convictions are shared
- User-shared lists should be treated as unverified
- Use responsibly and in accordance with server rules and TF2's Terms of Service

</details>

<details>
<summary><b>Platform Support Policy</b></summary>

**Officially Supported:**
- Windows
- Linux

**Unsupported:**
- macOS (may work via Wine/Proton, but we provide no support)

We focus development on platforms we can properly test and support.

</details>

---

## 🏗️ Technical Details

- **Language:** Written entirely in C++
- **GUI Framework:** QT for native overlay interface
- **Architecture:** Replay analyzer for real-time detection (no second instance required!)
- **Platform Support:** Windows and Linux
- **License:** MIT License

---

## 🔮 Roadmap

- [ ] Enhanced detection algorithms
- [✅] Improved heuristic patterns
- [✅] Additional cheat signature detection
- [ ] **Hive Network** - Multi-user instance linking
- [ ] Expanded community features
- [ ] Performance optimizations
- [✅] Advanced replay analyzer capabilities

---

## 🤔 FAQ

<details>
<summary><b>Do I have to use Synapse as my TF2 launcher?</b></summary>

No! Synapse can work with TF2 instances launched by any method. However, using Synapse as your launcher provides:
- Automatic configuration of required settings
- All known launch arguments pre-configured
- Easy customization of launch options
- One-click launch with optimal settings

You can still use Steam, shortcuts, or other launchers if you prefer.

</details>

<details>
<summary><b>Will this get me VAC banned?</b></summary>

No. Synapse AntiCheat does not modify game files or memory. It only analyzes demo files and RCON data, which are completely legitimate uses of TF2's built-in features.

</details>

<details>
<summary><b>Can I use this on community servers?</b></summary>

Yes! Synapse is perfect for server administrators. It can automatically kick convicted cheaters, alert players via chat, and integrate with your existing ban systems.

</details>

<details>
<summary><b>Do I still need a second computer or TF2 instance?</b></summary>

No! Our new replay analyzer eliminates this requirement. Synapse now works seamlessly with just your main game instance.

</details>

<details>
<summary><b>What about false positives?</b></summary>

False positives are possible with any automated system. That's why we:
- Use confidence ratings
- Support manual review
- Cross-reference multiple databases
- Never auto-convict on single data points
- Allow community verification

</details>

<details>
<summary><b>Will my TF2BD lists work with Synapse?</b></summary>

Yes! Synapse can import and use TF2BD playerlists and rulesets. These help strengthen our analysis but don't result in auto-convictions on their own.

</details>

<details>
<summary><b>I paid for Synapse. What should I do?</b></summary>

**You've been scammed!** Synapse is and always will be free software. Please:
1. Report the scam to us immediately
2. Request a refund/chargeback from your payment provider
3. Help us track down the scammer

</details>

<details>
<summary><b>Can I run Synapse in a Virtual Machine?</b></summary>

Absolutely! We fully support VM usage and encourage players to use whatever setup works best for them.

</details>

<details>
<summary><b>How do I get unbanned from Synapse?</b></summary>

If you believe you've been falsely convicted, you can attempt to initiate our **Redemption Process**:

**Eligible Reasons:**
- False conviction due to system error
- Compromised/hacked account (you were not in control)
- Other legitimate extenuating circumstances

**Process:**
1. Contact us with detailed evidence that you are not cheating
2. Provide context and proof (account security logs, etc.)
3. Our team will review your case

**If Pardoned:**
- You are completely wiped from our database
- It's as if you were never there
- Full restoration of access

This is NOT a guarantee - you must provide compelling evidence. Legitimate false convictions are taken very seriously.

</details>

<details>
<summary><b>What if I was using Synapse and got detected with a cheat?</b></summary>

**Zero tolerance.** If we detect a cheat has been injected into TF2 while you're using Synapse:
- Automatic conviction
- Automatic blacklist
- No appeals
- Permanent ban from using Synapse

We will not disclose how we detect this. Don't try to cheat while using anti-cheat software.

</details>

---

## 📜 License

**This Project intentionally omits a supplementary license.** Exclusive copyright is held by the contributors.
The source code hosted in these repository may not be copied, distributed, or modified without risk of take-downs, shake-downs, or litigation.
For more information regarding the conditions of use where repositories omit a supplemental license; see [GitHub Terms of Service](https://docs.github.com/en/github/site-policy/github-terms-of-service#d-user-generated-content), or [the summary of 'No License' conditions](https://choosealicense.com/no-permission/).

**Remember:** Synapse is FREE SOFTWARE. Anyone charging for it is scamming you!

---

## 🙏 Contributing

Contributions are welcome! Whether it's:
- 🐛 Reporting false positives/negatives
- 💡 Suggesting new features
- 🔧 Improving detection algorithms
- 📚 Documentation improvements
- ⚡ Code optimization
- 🎨 UI/UX enhancements

Please open an issue or pull request on GitHub!

---

## 📞 Support

<details>
<summary><b>Getting Help</b></summary>

- **Issues:** Report bugs via GitHub Issues
- **Discord:** [Join our community server](https://discord.gg/PPTyhTAb6r)
- **Documentation:** Check our Wiki for guides
- **FAQ:** See above for common questions

</details>

---

## 💬 A Message to Cheaters

**We're always watching.** 

You should know:
- We have insiders within your communities
- Every "new" cheat feature gets detected
- Our insiders remain anonymous for obvious reasons
- By the time you think you're safe, we've already adapted
- You're not as clever as you think

The game stays fair. We make sure of it.

---

## ⚖️ Final Disclaimer

Synapse AntiCheat is a community tool designed to improve gameplay experience. It is provided as-is under the MIT License. 

**Use responsibly and in accordance with:**
- Server rules and policies
- Team Fortress 2's Terms of Service
- Valve's community guidelines
- Local laws and regulations

We are not responsible for misuse of this software. Server administrators and users are responsible for ensuring their use complies with all applicable rules and regulations.

---

**Made with 🔧 for the TF2 community**

*Keeping Team Fortress 2 fair, one detection at a time.*
