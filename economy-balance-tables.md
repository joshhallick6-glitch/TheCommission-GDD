# Economy Balance Tables -- The Commission

> **Target match length:** 40 minutes (1v1). **Starting Cash:** $500.
> **Resources:** Cash ($), Goods, Influence.
> **Tiers:** Street Crew (T1) -> The Outfit (T2) -> The Syndicate (T3) -> The Empire (T4).
> An uncontested economic player reaches Tier 3 by ~minute 20 and Tier 4 by ~minute 30.

---

## 1. Income Buildings

Income buildings are the backbone of the macro economy. Tier 1 buildings are cheap and fast to establish, giving players immediate returns that fund early aggression or a fast tech path. Higher-tier buildings produce dramatically more Cash and Goods but require significant investment and map control to protect. The number of upgrade slots per building creates a secondary decision layer: do you invest in maxing out a few key buildings, or spread your economy wide across the map?

Buildings that generate Goods require a functioning transport chain to a processing hub before those Goods become usable -- raw production sitting in an unconnected building is dead weight. Influence-generating buildings are rarer and tend to be contestable map objectives rather than safe backline investments.

| Building | Tier | Capture/Build Cost ($) | Build Time (sec) | Base Income ($/min) | Goods Production (units/min) | Influence Gen (/min) | Upgrade Slots | Notes |
|---|---|---|---|---|---|---|---|---|
| Corner Store | T1 | $75 | 15 | 12 | 0 | 0 | 1 | Protection racket. Cheapest income building. Map capturable -- no construction needed on neutral ones. |
| Speakeasy | T1 | $120 | 25 | 20 | 0 | 1 | 1 | Generates minor Influence from neighborhood presence. Upgradeable to Nightclub at T2. |
| Back-Alley Still | T1 | $100 | 20 | 5 | 4 | 0 | 1 | Primary early Goods source. Low Cash income but essential for tier-up. Must connect to transport. |
| Bookie Joint | T1 | $90 | 18 | 15 | 0 | 0.5 | 1 | Income fluctuates +/-30% per cycle (simulates gambling variance). Slight Influence from street cred. |
| Nightclub | T2 | $250 | 35 | 35 | 0 | 2 | 2 | Major Cash earner. Can be upgraded from Speakeasy for $130 and 10 sec instead of full cost. |
| Distillery | T2 | $280 | 40 | 10 | 10 | 0 | 2 | Industrial-scale Goods production. Replaces Back-Alley Still in the supply chain. Loud -- visible on minimap to enemies. |
| Trucking Depot | T2 | $200 | 30 | 8 | 0 | 0 | 2 | Does not produce resources directly. Increases transport capacity +50% in its radius. Spawns Delivery Trucks. |
| Pawn Shop | T2 | $180 | 25 | 22 | 3 | 0 | 1 | Dual income: moderate Cash plus light Goods. Useful as a flexible mid-tier filler building. |
| Boxing Gym | T2 | $220 | 30 | 5 | 0 | 4 | 1 | Low Cash, high Influence. Also provides a passive +10% melee damage aura to nearby friendly units. |
| Casino | T3 | $500 | 50 | 60 | 0 | 3 | 3 | Top-tier Cash generator. Requires 20 Influence to unlock construction. High-value raid target. |
| Import Dock | T3 | $450 | 55 | 15 | 20 | 0 | 3 | Massive Goods throughput. Must be built on a waterfront tile. Vulnerable to naval/dock raids. |
| City Hall Contact | T3 | $400 | 45 | 25 | 0 | 6 | 2 | Primary Influence engine. Unique limit: 1 per player. Enables political actions (bribe police, zone permits). |
| Newspaper Office | T3 | $350 | 40 | 20 | 0 | 5 | 2 | Influence generator with active ability: "Smear Campaign" -- reduces target enemy's Influence by 8 (120 sec cooldown). |
| Grand Hotel | T4 | $800 | 65 | 80 | 5 | 4 | 3 | Elite Cash building. Generates all three resources. Requires 50 Influence to unlock construction. |
| Federal Warehouse | T4 | $700 | 60 | 20 | 30 | 0 | 3 | End-game Goods powerhouse. Stockpiles up to 200 Goods locally (acts as buffer against transport disruption). |
| The Mint | T4 | $1,200 | 90 | 120 | 0 | 5 | 4 | Money laundering mega-building. Unique limit: 1 per player. Converts 10 Goods/min into +60 bonus $/min on top of base income. |

**Aggregate early-game note:** A standard T1 opening of 2 Corner Stores + 1 Speakeasy + 1 Back-Alley Still + 1 Bookie Joint costs $385 (from $500 start, leaving $115 for units) and yields ~62 $/min + 4 Goods/min + 1.5 Influence/min once all buildings are online (~80 sec).

---

## 2. Goods Transport

The Goods transport system is the game's most skill-expressive economic mechanic. Raw Goods must physically travel from production buildings (Stills, Distilleries, Import Docks) to processing hubs or the HQ before they count toward your stockpile. This creates a "supply line" dynamic where aggressive players can raid enemy trucks for enormous economic damage without ever touching the production buildings themselves. Transport choices create a risk-reward spectrum: Runners are cheap and hard to spot but painfully slow; Armored Trucks are fast and durable but expensive and loud.

Speed is measured in tiles per second on the standard 256x256 map grid. A typical cross-map route is ~80-120 tiles.

| Transport Method | Tier | Capacity (Goods) | Speed (tiles/sec) | Cost ($) | Vulnerability | Notes |
|---|---|---|---|---|---|---|
| Runner | T1 | 5 | 2.5 | $25 | Very high -- 1 hit kill from any combat unit. No armor. | Stealthy: does not appear on enemy minimap. Can use alleyways (shortcuts impassable to vehicles). Produced from HQ. |
| Delivery Truck | T2 | 20 | 5.0 | $80 | High -- light armor (50 HP). Destroyed by 2-3 infantry squads or 1 vehicle. | Requires road tiles. Spawned from Trucking Depot. Can be intercepted at chokepoints. Visible on minimap when moving. |
| Armored Truck | T3 | 35 | 4.5 | $200 | Medium -- heavy armor (200 HP). Requires dedicated anti-vehicle to destroy quickly. | Slower than Delivery Truck but far more survivable. Can mount a rear-gunner upgrade ($100) for self-defense. |
| Convoy | T4 | 80 | 4.0 | $500 | Low -- consists of 2 Armored Trucks + armed escort car (400 HP total across vehicles). | Moves as a single formation. Escort car engages attackers automatically. Visible on minimap. 180 sec cooldown between dispatches. |

**Transport economy math:** A single Distillery (10 Goods/min) fills a Delivery Truck (20 capacity) every 2 minutes. A single Import Dock (20 Goods/min) needs either 1 Armored Truck running a short route or 2 Delivery Trucks on rotation to avoid overflow.

---

## 3. Tier Advancement

Tier advancement is deliberately expensive and slow enough that rushing to the next tier without adequate economy or map control is punishable. A player who skips military investment to fast-tech will arrive at Tier 2 with an empty wallet and no board presence -- easy prey for an aggressive opponent. The triple-resource cost ensures that players must develop all three economic pillars (Cash generation, Goods production + transport, and territorial Influence) rather than tunnel-visioning on one. Research time creates a commitment window where the investing player is vulnerable.

| Transition | Cash Cost ($) | Goods Cost | Influence Cost | Research Time (sec) | Key Unlocks (summary) |
|---|---|---|---|---|---|
| T1 -> T2 (Street Crew -> The Outfit) | $400 | 100 | 30 | 60 | Nightclub, Distillery, Trucking Depot, Pawn Shop, Boxing Gym. Delivery Trucks. Tier 2 infantry (Tommy Gunners, Enforcers). First vehicle units (Getaway Car). Upgrade slot +1 on new buildings. |
| T2 -> T3 (The Outfit -> The Syndicate) | $1,200 | 350 | 100 | 90 | Casino, Import Dock, City Hall Contact, Newspaper Office. Armored Trucks. Tier 3 infantry (Hitmen, Demolitions). Armored vehicles (Bulletproof Sedan). Political actions. Building upgrade tier 2 unlocked. |
| T3 -> T4 (The Syndicate -> The Empire) | $3,000 | 800 | 250 | 120 | Grand Hotel, Federal Warehouse, The Mint. Convoys. Tier 4 elite units (Made Men, War Captain). Superweapons/abilities (Federal Raid, City-Wide Lockdown). Max upgrade tier on all buildings. |

**Cumulative cost to reach T4:** $4,600 Cash, 1,250 Goods, 380 Influence, 270 sec total research time.

**Fast-tech benchmark:** An uncontested player optimizing purely for economy reaches T2 at ~6:30, T3 at ~18:00, T4 at ~28:00. A player balancing military and economy hits T2 at ~8:00, T3 at ~20:00, T4 at ~30:00.

---

## 4. Influence and Fear Multiplier

Influence is the "soft power" resource that rewards map control and aggression. Unlike Cash and Goods, Influence cannot be efficiently farmed from a safe backline -- it requires territorial presence, objective completion, and combat victories. The multiplier system means that a player with dominant Influence earns significantly more Cash from the same buildings, creating a snowball mechanic that rewards early aggression. The Fear system adds a tactical dimension: fighting inside a high-Influence enemy zone is actively punishing, discouraging reckless dives into well-held territory.

The Influence scale is 0-100 per player, calculated from total territory held, buildings owned, objectives completed, and combat performance.

| Influence Level | Territory Bonus (%) | Income Multiplier | Fear Effect | Unlock Threshold |
|---|---|---|---|---|
| 0 (No Presence) | 0% | 0.70x | None -- your units fight at baseline in all zones. | -- |
| 20 (Known) | +5% territory capture speed | 0.85x | Minimal: enemy units in your territory have -5% move speed. | Enables Bookie Joint Influence upgrade. |
| 40 (Respected) | +10% territory capture speed | 1.00x (baseline) | Moderate: enemy units in your territory have -10% move speed and -5% DPS. | Enables City Hall Contact construction (T3). Enables "Bribe Patrol" political action. |
| 60 (Feared) | +15% territory capture speed | 1.15x | Significant: enemy units in your territory have -15% move speed and -10% DPS. Neutral buildings in your territory generate +20% income. | Enables Newspaper Office "Smear Campaign" ability. Enables "Protection Racket" passive ($5/min per enemy building in your territory). |
| 80 (Notorious) | +20% territory capture speed | 1.35x | Severe: enemy units in your territory have -20% move speed and -15% DPS. Enemy Runners in your territory are revealed on minimap. | Enables Grand Hotel construction (T4). Enables "Intimidation" active ability (force 1 enemy squad to retreat). |
| 100 (Untouchable) | +30% territory capture speed | 1.50x | Crushing: enemy units in your territory have -25% move speed and -20% DPS. Enemy transport units in your territory move at half speed. Neutral buildings auto-convert to you over 60 sec. | Enables The Mint construction. Enables "Federal Raid" superweapon (T4). Victory condition: hold 100 Influence for 120 consecutive seconds to win. |

**Design note on snowball control:** Influence decays at 3 points/min when above 60 if the player is not actively holding majority territory or winning engagements. This prevents runaway leads -- a dominant player must keep pressing to maintain their advantage.

---

## 5. Economic Phase Summary

These phases describe the expected economic trajectory of a competent player in a contested 1v1 match. Actual income depends heavily on map control, raiding, and build order choices. The numbers below assume moderate aggression (some units lost, some raids taken and given) rather than pure boom or pure rush.

| Phase | Time Window | Expected Income ($/min) | Expected Goods Flow (units/min) | Expected Influence | Key Economic Activity |
|---|---|---|---|---|---|
| Early (Street Crew) | 0:00 - 8:00 | 50-70 | 4-6 | 10-25 | Capture neutral Corner Stores. Build Speakeasy + Back-Alley Still. First Bookie Joint. Runners deliver Goods for T2 research. Scout enemy economy. First skirmishes over contested buildings. |
| Mid (The Outfit) | 8:00 - 18:00 | 100-160 | 10-18 | 25-50 | Transition to Nightclubs and Distilleries. Build Trucking Depot for Delivery Trucks. Pawn Shops fill gaps. Boxing Gym for Influence push. Raiding enemy supply lines becomes viable and important. Key map objectives contested. |
| Late (The Syndicate) | 18:00 - 30:00 | 200-320 | 20-35 | 50-75 | Casinos online for major Cash. Import Docks for industrial Goods flow. City Hall Contact and Newspaper Office for Influence dominance. Armored Trucks protect supply chains. Political actions disrupt enemy economy. Territory control determines winner. |
| Endgame (The Empire) | 30:00+ | 400-600+ | 30-50+ | 75-100 | Grand Hotel and The Mint provide overwhelming income. Federal Warehouse buffers Goods against raids. Convoys move massive Goods shipments. Elite units and superweapons deployed. Influence victory condition in play -- hold 100 for 120 sec to win. |

**Total resources generated in a 40-minute match (estimate):** ~$8,000-12,000 Cash, ~800-1,200 Goods, ~200-350 Influence earned.

---

## Quick Reference: Resource Flow Diagram

```
[Corner Store] ---$---> CASH STOCKPILE ----> Units, Buildings, Upgrades, Tier-Up
[Speakeasy]    ---$--->        |
[Nightclub]    ---$--->        |
[Casino]       ---$--->        v
[Grand Hotel]  ---$---> [also Goods + Influence]

[Back-Alley Still] --Goods--> [Runner/Truck] ---> GOODS STOCKPILE ---> Upgrades, Tier-Up, The Mint conversion
[Distillery]       --Goods--> [Runner/Truck] --->        |
[Import Dock]      --Goods--> [Armored Truck] -->        |
[Federal Warehouse] --Goods-> [Convoy] -------->         v
                                               [The Mint: 10 Goods/min -> +$60/min]

[Speakeasy]        --Inf--> INFLUENCE TOTAL ---> Political Actions, Tier-Up, Fear Multiplier
[Bookie Joint]     --Inf-->       |
[Boxing Gym]       --Inf-->       |
[City Hall Contact]--Inf-->       |              Influence also earned from:
[Newspaper Office] --Inf-->       v              - Territory control (passive)
[Grand Hotel]      --Inf-->  [0-100 scale]       - Winning fights (+2 per squad kill)
[The Mint]         --Inf-->                      - Completing objectives (+5-15 per objective)
                                                 - Intimidation actions (+3 per success)
```

---

*Last updated: 2026-03-08. All values are initial balance targets subject to playtesting.*
