# The Commission — GDD v1.1 Errata & Revisions

**Date:** 2026-03-08
**Responding to:** Red-Team Design Review (same date)
**Status:** All critical findings addressed. Changes marked for incorporation into GDD v2.

---

## Design Directive: Logistics Loss Philosophy

**Ruling:** Losing a truck should feel like losing a battle — a hit, a setback, a reason to adapt — not a reason to quit. If a player's supply lines are completely cut but they have enough Goods banked, they should still be okay. This mirrors Age of Empires II, where losing your trade route or gold miners to a raid stings but doesn't end the game if you have resources stockpiled.

**Concrete design rules derived from this directive:**

### Rule 1: No single truck loss should exceed 6% of a tier advancement cost
- Delivery Truck (20 Goods) vs T2→T3 (350 Goods) = 5.7%. **Passes.**
- Delivery Truck (20 Goods) vs T3→T4 (800 Goods) = 2.5%. **Passes.**
- With Goods Insurance (40% drop recovery), effective loss = 12 Goods = 3.4% of T3 cost. **Comfortable.**

### Rule 2: Banking must provide a meaningful buffer
- **Compound stores up to 150 Goods** by default (enough for ~7 truck loads of buffer)
- **Warehouse stores up to 100 Goods** (expanded to 200 at T4 via Federal Warehouse)
- **Design target:** A player at T2 with a functioning Distillery (10 Goods/min) should be able to bank 100+ Goods at their Compound before needing to spend them. If their supply line is then completely cut, they have **10 minutes of banked Goods** before running dry — long enough to rebuild or fight for a new route.

### Rule 3: Truck rebuilds must be fast and cheap
- Delivery Truck rebuild: **$80, 12-second build time** (current spec). Losing one and replacing it costs less than a Thug squad.
- Armored Truck rebuild: **$200, 20-second build time**. More painful but still manageable.
- A player should be able to lose 2 trucks in a raid and have replacements rolling within 30 seconds.

### Rule 4: Complete supply line cuts are temporary, not permanent
- Supply lines can be cut by destroying trucks and controlling route chokepoints. But:
  - The city always provides **2+ viable routes** between any production building and any processing hub (map generation constraint)
  - Runners can carry 5 Goods through alleys that vehicles can't use — a slow fallback that's always available
  - The Compound and Warehouses act as Goods banks that smooth out disruption
- A player whose lines are completely cut should feel pressure to act (reclaim a route, escort the next truck, counterattack) — not helpless

### Rule 5: Cumulative raid damage must be significant over time
- While single losses are minor, a sustained logistics campaign (destroying 5-6 trucks over 5 minutes) should materially delay tier advancement by 2-4 minutes
- This creates the AoE2 dynamic: raiding is worth doing, but it's a war of attrition, not an instant kill
- The raider pays an opportunity cost (Saboteur squads tied up on ambush duty instead of frontline combat)

### Emotional benchmark (from AoE2 analog):
| AoE2 Equivalent | The Commission Equivalent | Feel |
|-----------------|--------------------------|------|
| Losing 3 trade carts to a knight raid | Losing a Delivery Truck to Saboteurs | "Damn, need to escort better" |
| Gold miners killed, mine still standing | Distillery untouched, trucks destroyed | "Route's hot, switch paths or fight" |
| All gold mines exhausted | All supply lines cut, Goods banked | "I have time, need to break through" |
| TC destroyed, villagers scattered | Compound destroyed, trucks orphaned | "I'm in trouble but not dead yet" |

---

## Critical Fixes (Must-Do Before Prototype)

### Fix 1: Solomon Faction Rebalance

**Problem:** Three economic bonuses pointing the same direction (+25% Cash, -15% maintenance, $3,500 Hostile Takeover) makes Solomons dominant at all competitive levels.

**Resolution:**
- Reduce Cash income bonus from +25% to +15%
- Remove the maintenance discount entirely (-15% maintenance → no maintenance bonus)
- Change Hostile Leverage (Tier 4 ability) from "$3,500 Hostile Takeover" to "$4,250 Hostile Takeover" (15% discount, not 30%)
- Add new Solomon weakness: -10% Influence generation from all sources (they're money people, not street people)

**Revised Solomon profile:**
| Bonus | Old | New |
|-------|-----|-----|
| Cash income | +25% | +15% |
| Maintenance | -15% | None |
| Hostile Takeover cost | $3,500 (30% off) | $4,250 (15% off) |
| Unit HP weakness | -20% | -15% |
| New weakness | — | -10% Influence generation |

---

### Fix 2: Hostile Takeover Requires Countdown

**Problem:** Instant-win with zero counterplay window is anti-competitive. Invisible to spectators.

**Resolution:**
- Hostile Takeover now triggers a **90-second countdown** visible to all players
- During countdown, the initiating player's Compound glows gold on the minimap
- Opponent can cancel by dealing 50%+ damage to the initiating Compound OR by destroying $2,000+ worth of the initiator's buildings during the countdown
- In spectator/tournament mode, each player's Cash total is visible to observers (not to opponents)
- Solomon's Hostile Leverage still reduces the cash threshold but does NOT shorten the countdown

---

### Fix 3: Desperate Measures — Adopt Audit Recommendation

**Problem:** GDD says one-time burst trigger; audit correctly identifies this as exploitable via stockpile-and-trigger.

**Resolution:** Adopt the audit's recommendation. Desperate Measures is now:
- **Persistent conditional buff** active while the player controls <25% territory
- Effect: +15% DPS and +10% speed (reduced from +30%/+20% burst to prevent pre-positioning abuse)
- Deactivates immediately when territory rises above 25%
- Cannot be exploited by intentional territory loss because the buff is modest and losing territory costs income

This is now canonical. The GDD v1 one-time trigger description is superseded.

---

### Fix 4: Delivery Truck Capacity — Resolve 10x Discrepancy

**Problem:** Economy table says 20 Goods capacity. Unit stat sheet says 200 Goods.

**Resolution:** The economy table's number (20 Goods) is correct. The stat sheet's 200 is a typo. All truck capacities:
| Vehicle | Correct Capacity |
|---------|-----------------|
| Runner (by hand) | 3 Goods |
| Delivery Truck | 20 Goods |
| Armored Truck | 35 Goods |
| Convoy (T4, War Wagon variant) | 80 Goods |

The Convoy IS the War Wagon configured for transport mode. The War Wagon has two configurations: Combat Mode (weapons active, no cargo) and Convoy Mode (weapons disabled, carries 80 Goods, +20% armor). Switching modes takes 10 seconds. This resolves the stat sheet gap.

---

### Fix 5: Specify Compound HP and Turf Points

**Problem:** Compound HP never specified. Turf Point count undefined. Developers cannot implement from current spec.

**Resolution:**

**Compound stats:**
| Property | Value |
|----------|-------|
| HP | 2,000 |
| Armor | Heavy (50% damage reduction from small arms) |
| Passive regen | 5 HP/sec when not under attack for 30 sec |
| First 5 minutes | 75% damage resistance (anti-rush shield) |
| Capture time | Cannot be captured; must be destroyed |

**Turf Points:**
- Each neighborhood contains exactly **3 Turf Points** (located at major intersections/landmarks)
- Standard map: 18 neighborhoods × 3 = **54 Turf Points total**
- Monopoly victory requires controlling **38 Turf Points** (70.4% of 54)
- Turf Points are captured by having military presence (any combat unit within radius for 15 seconds)
- Turf Points are distinct from Street Corners. Street Corners provide vision; Turf Points count toward Monopoly victory
- A building is NOT a Turf Point. Business Ownership and Turf Point control are separate systems

---

### Fix 6: Korvak Rush Mitigation

**Problem:** +15% speed and -20% training time enables a minute-4 all-in rush that may be unanswerable.

**Resolution:**
- Training time bonus changed from -20% to -12%
- Training time bonus applies only to **Tier 2+ units** (Thugs and Runners train at standard speed)
- Speed bonus remains +15% (this is the faction's identity)
- The Compound's 75% damage resistance in the first 5 minutes (from Fix 5) also mitigates HQ rush viability

---

### Fix 7: Ashford DPS Penalty Softened

**Problem:** -15% DPS across the board is too harsh and disproportionate compared to other factions' weaknesses.

**Resolution:**
- DPS penalty reduced from -15% to -10%
- New conditional bonus: Ashford units in cover or garrisoned receive +5% DPS (net -5% DPS in cover, -10% in the open)
- This matches their "political operator" identity: they fight from defensive positions, not open streets
- Their actual effective DPS gap in typical urban combat (mostly in cover) is -5%, which is manageable

---

## Important Fixes (Should-Do Before Alpha)

### Fix 8: Early Game Decision Density

**Problem:** Minutes 0-3 have ~3 decisions vs AoE2's ~30. Too slow for RTS veterans.

**Resolution:** Add three early-game micro systems:
1. **Tip-Off** — At game start, your Compound reveals the location of one high-value neutral building on the map. Both players get different tip-offs. Creates an immediate scouting decision: send your Runner to your tip-off or scout the opponent's start?
2. **Street Hustle** — Runners can perform a "Hustle" at any unclaimed Street Corner: hold for 8 seconds to earn 25 Cash. Creates early-game micro decisions with Runners while scouting.
3. **Stash Discovery** — 3-5 small Cash caches ($50-75 each) are scattered in alleys and back rooms across the map. Runners auto-detect them within 2 tiles. Rewards active scouting in the first 2 minutes.

These add ~6-8 micro decisions in the first 3 minutes without adding system complexity. All three are easily cut if they don't test well.

---

### Fix 9: Goods Insurance (Truck Destruction Recovery)

**Problem:** Losing a loaded truck is 100% loss with potentially game-deciding consequences at T3 transition timing.

**Resolution:**
- When a truck is destroyed, **40% of its Goods cargo drops on the ground** as a recoverable pickup
- Dropped Goods persist for 45 seconds before despawning
- Either player can send any unit to recover dropped Goods
- This caps worst-case truck loss at 60% instead of 100%
- Creates a micro moment: do you send a Runner to recover the dropped Goods or retreat from the ambush?
- The raiding player also has an incentive to stick around and grab the Goods, creating risk

---

### Fix 10: Logistics Alert System

**Problem:** Route warnings address planning but not destruction awareness. Players lose trucks while managing combat and don't notice for minutes.

**Resolution:**
- **Destruction Alert:** When any owned transport unit is destroyed, an audio ping plays and a red flash appears on the minimap at the destruction location. This is distinct from combat alerts.
- **Goods Lost Counter:** A small HUD element shows "Goods lost this minute" as a running tally that decays. If it spikes, the player knows they're being raided.
- **Auto-Replacement Option:** When a truck is destroyed, the producing building auto-queues a replacement truck if the player has enough Cash. The player can toggle this off.

---

### Fix 11: Rat Economy — Adopt Audit Trigger

**Problem:** "Fewer than 3 buildings" is exploitable by intentional building sacrifice.

**Resolution:**
- Trigger changed to: "Player has lost 60%+ of their peak building count AND controls fewer than 3 income buildings"
- Both conditions must be true (prevents gaming by never building more than 4 buildings)
- Saboteur discount reduced from -30% to -15%
- Rat Economy income remains $20/min (approximately 1.3 Speakeasies — enough to rebuild, not enough to thrive)

---

### Fix 12: Surrender Timer Improvement

**Problem:** Current timer only fires after Compound loss (too late). Mismatched skill games drag.

**Resolution:**
- **Concession Incentive:** After a player loses 75%+ of their buildings AND has fewer total units than their opponent, a "Concede?" prompt appears every 60 seconds. Conceding ends the game instantly with a "tactical withdrawal" animation rather than a defeat screen. This is purely cosmetic — concession does count as a loss for ranked — but reduces the stigma of surrendering.
- **Compound Loss Timer remains** at 5 minutes but the Safehouse is now destructible (5x normal building HP, hidden from minimap until scouted)
- **Skill Gap Accelerator:** If one player is 2 tiers ahead of the other AND controls 70%+ territory, match pace accelerates (income +50% for both players). This compresses the endgame into ~5 minutes rather than 15.

---

## Noted But Deferred (Post-Prototype)

### The T3 Stalemate Window (Minutes 22-30)

The red-team correctly identifies an 8-minute same-tier standoff risk at T3. This requires playtesting before a design fix can be proposed. Potential solutions to test:
- Introduce a T3.5 micro-upgrade (single unlock at a Cash cost, e.g., "Squad Veterancy Reset" that instantly promotes all current units one veterancy level)
- Reduce T4 costs by 20% to compress the T3 window
- Add a map objective that spawns at minute 25 (e.g., a neutral arms shipment at the docks that gives 200 Goods to whoever captures it)

### Map Generation vs Hand-Crafted

Accept the red-team's recommendation: **ship ranked with 5-8 hand-crafted maps.** Use procedural generation for casual/unranked modes. Validate generator quality post-launch.

### Maintenance Cost Timing

Maintenance deducted **before** the Influence multiplier is applied. A $20/min building with $5/min maintenance has $15/min effective base, then multiplied by Influence. This is the more conservative choice and slightly nerfs over-expansion.

---

## Document Contradiction Resolution Summary

| Contradiction | Source A | Source B | Resolution |
|--------------|----------|----------|------------|
| Desperate Measures (one-time vs conditional) | GDD §12 | Anti-snowball audit §1.4 | **Adopt audit: persistent conditional buff** |
| Rat Economy trigger | GDD §12 (<3 buildings) | Audit §1.3 (60%+ peak loss) | **Adopt audit: dual condition** |
| Delivery Truck capacity | Economy table (20) | Stat sheet (200) | **Economy table correct: 20 Goods** |
| Armored Truck capacity | Economy table (35) | Stat sheet (100) | **Economy table correct: 35 Goods** |
| Convoy existence | Economy table (listed) | Stat sheet (absent) | **Convoy = War Wagon in transport mode** |

---

*This errata is canonical and supersedes GDD v1 on all points of conflict.*
