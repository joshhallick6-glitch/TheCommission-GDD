# Red-Team Design Review — The Commission
**Reviewer role:** Senior competitive RTS designer (adversarial)
**Documents reviewed:** GDD v1, economy-balance-tables, unit-vehicle-stats, match-pacing-timeline, victory-conditions, anti-snowball-audit
**Date:** 2026-03-08

---

## Preamble

This is an adversarial review. The goal is to find what breaks before a prototype exposes it. The Commission has a coherent concept and borrows proven DNA intelligently, but several of its systems contain latent problems that will surface the moment players start min-maxing. A design doc that does not identify them is not protecting the project — it is delaying a reckoning that happens in front of investors or launch-window players instead of now.

---

## 1. Snowball Analysis

### Do the Numbers Actually Prevent Snowballing?

The short answer is: not reliably, and the anti-snowball audit already knows it.

Work through a concrete scenario. Player A wins the minute-5 neutral building contest (match-pacing-timeline, min 5). They now hold one extra Corner Store ($12/min) and one extra Speakeasy ($20/min) versus Player B who conceded both and went to two Speakeasies. At minute 8, the income difference is approximately $32/min in Player A's favor. Over the next 10 minutes that is $320 in accumulated advantage — roughly four Thug squads' worth of production. That extra production lets Player A deny Player B's second Distillery capture at minute 14, which delays Player B's T3 by 2-3 minutes (per the economy table's T2→T3 Goods requirement of 350 units, versus the 10 Goods/min a single Distillery produces). A 2-minute T3 delay at minute 20 is the difference between having Hitmen and Armored Sedans during the minute-22 "power spike" engagement or not. That single skirmish at minute 5 has propagated into a decisive late-game quality gap — and this is without any combat victory Influence bonuses accelerating the multiplier toward 1.15x or 1.35x.

### The Two-Building Advantage at Minute 8 — Can the Trailer Catch Up?

The aggressive vs. economic build table (match-pacing-timeline, section 5) claims both builds converge by minute 25-30. Let's audit that claim.

At minute 10, the Econ player has $1,050 vs the Aggro player's $900. That is a 16% surplus. But the Econ player has 5 units vs the Aggro player's 8. The Aggro player reaches T2 later but controls more territory. Now suppose Player A is not "Aggro" but simply "better at the minute-5 fight" — they have the territory advantage AND the economic investment. The pacing table assumes Aggro concedes income to build army; a player who is both winning fights AND expanding buildings does not fit either column. That player's advantages stack instead of trading off, and the table provides no scenario for it.

Concrete math on the 2-building advantage specifically: two extra buildings at minute 8 might be a Corner Store ($12/min) and a Bookie Joint ($15/min) = $27/min extra. Over 12 minutes until T3 becomes relevant, that is $324. T2→T3 costs $1,200 Cash + 350 Goods. The cash gap alone will cause the trailer to hit T3 approximately 3.5 minutes later (at $80-90/min income, $324 buys about 3.5-4 minutes of delay). A 3.5-minute T3 delay means the leader reaches T3 at minute ~18 vs the trailer at minute ~21.5. During those 3.5 minutes the leader has Hitmen and Machine Gun Cars against the trailer's Enforcers and Getaway Cars. The counter matrix shows Machine Gun Car as "++" vs most T2 infantry compositions in the open. A 3.5-minute window with asymmetric T3 access is probably enough to destroy 2-3 of the trailer's income buildings and widen the gap further.

**The verdict: yes, a 2-building advantage at minute 8 is self-compounding. The $324 income gap delays T3, the T3 delay allows income-building destruction, and that destruction further delays T3. This is textbook snowball and the anti-snowball systems do not fire until the gap is already severe.**

### Does Heat + Diminishing Returns Actually Slow the Leader?

Heat fires at the composite score threshold, but the anti-snowball audit (section 1.1) correctly identifies that army value is easy to manipulate. If we accept the audit's recommended modification (income + territory only), Heat becomes more robust, but it still has a response lag problem: Heat ramps gradually while income gaps compound immediately.

Diminishing returns on territory (>50% control) is the cleanest mechanic but it only kicks in at extreme map control. In a 2-building advantage scenario, the leader might hold 55-60% territory — enough for mild diminishing returns but not enough to neutralize the income multiplier from Influence reaching 60+ ("Feared" at 1.15x). The leading player's Feared-territory buildings earn 1.15x their base rate while the trailer's same buildings earn 0.85x (minimal presence) — a 35% swing on every building in contested space. Diminishing returns on Turf Points does not offset this because, per the audit's key recommendation, it only applies to Turf Point income, not building income. The Influence multiplier compound that the economy table documents (section 4) is the actual snowball engine, and neither Heat nor Diminishing Returns targets it directly.

**Concrete gap that survives all anti-snowball systems:** A player with Feared-level Influence (60+) running a Casino ($60/min base) earns $69/min from that building. Their opponent's Casino in minimal-Influence territory earns $51/min. That $18/min difference per building, multiplied across a full late-game economy of 6-8 income buildings, is $108-144/min — more than the cost of 1 Thug squad every 45 seconds, indefinitely. Heat's 25% unit cost increase on the leader pushes a Thug from $75 to $93.75, which is partially offset by the $18-27/min per-building income surplus. The numbers do not stack up to a genuine handicap.

---

## 2. Degenerate Strategies

### Strategy 1: The T1 Blitz Rush (Korvak Variant)

**Description:** The Korvaks receive +15% unit speed and -20% training time. A Korvak player builds one Speakeasy, skips the second, and immediately queues 6 Thug squads in rapid succession (-20% training time means 12-second Thugs vs the standard 15). At minute 3-4 they have a 5-6 Thug army (versus the opponent's 2-3) and throw it directly at the enemy Compound before any neutral building captures have settled the economy. The Korvak speed bonus means Thugs close ground 15% faster, reducing the defender's window to retreat into garrison. At minute 4, the defending player has $575 in cumulative cash and 2-3 Thug squads — insufficient to hold against 5-6 Thugs at +15% speed with the attacker having chosen the engagement location.

**Why it works:** The pacing timeline treats the first contact (minute 5) as "light skirmishes over a contested block." It does not account for a player who is not contesting a block but instead driving directly at the HQ. The Compound is described as having "high HP and can be fortified" but no HP value or capture time is specified in any document. Without a concrete Compound HP number, we cannot know if 5 Thugs can dent it meaningfully in 2 minutes.

**Severity: 4/5.** Potentially game-ending if Compound is not sufficiently durable. Counter-play exists (garrison defenders, retreat to Compound) but requires the defending player to not have expanded at all.

**Fix:** Specify minimum Compound HP (suggest 800+ HP with a 75% damage resistance during the first 5 minutes of the match). Alternatively, Korvak speed bonus should not apply to units trained in the first 4 minutes, activating only after first Tier 2 advance.

---

### Strategy 2: Turtle-Boom to Tier 4

**Description:** A player concedes all contested neutral buildings, builds only inside a 2-3 block radius of their Compound, and invests every dollar into economic buildings with Sandbag Wall and Fortified Entrance attachments. With -15% Heat generation (Ashford bonus) or simply by staying below the Heat composite threshold, they avoid most Heat penalties. They reach T3 by minute 20 and T4 by minute 30, at which point The Mint ($1,200/min with Goods conversion) and Grand Hotel ($80/min) create an income disparity that no raiding can overcome. The turtle's army is minimal but backed by Safehouse Persistence and Armored Trucks with Lockdown ability covering chokepoints.

**Why it works:** The aggressive build table (pacing timeline, section 5) shows the Econ player winning at minute 40 by out-teching — the turtle is simply an extreme version of that. The "boom vs. pressure" fork at minute 13-14 is explicitly described as viable. The design does not specify a hard limit on how defensively a player can play. The $5/min maintenance cost per building is too small to punish overbuilding defensively (10 buildings = $50/min drain vs $300-400/min income from those buildings at T2-T3).

**Severity: 3/5.** Viable but not degenerate — the aggressor can win the minute-12-20 window. However, the Ashford faction makes this significantly safer (-25% Heat, +30% Influence from buildings means income multipliers reach maximum faster from a passive backline).

**Fix:** Require minimum territory control percentage (e.g., 25%) to advance tiers. A player who holds only 10% of the map should not be able to peacefully advance to Tier 4. This forces turtles to at least contest some territory, creating vulnerability windows.

---

### Strategy 3: Perpetual Logistics Denial Loop

**Description:** A player skips military composition entirely above T2 and maintains a force of exclusively Saboteurs ($160 each, -20% with Black Market = $128) and Getaway Cars. They ignore their own economy past basic subsistence and dedicate all production to running Saboteur teams in 2-man kill squads that intercept enemy Delivery Trucks. One Delivery Truck carries 20 Goods (economy table). At T2 the opponent needs approximately 350 Goods for T3 advancement. If Saboteurs intercept 4-5 Delivery Trucks (destroying 80-100 Goods each time), they can delay T3 indefinitely. Saboteurs are stealthy (do not appear on minimap when stationary), hard to spot, and their "Plant Charge" one-shots Delivery Trucks (500 damage vs Delivery Truck's 350 HP per unit stat sheet).

**Why it is stronger than it looks:** The Delivery Truck has 350 HP and costs $150 + 20 Goods. A Saboteur squad costs $160 and can one-shot a Delivery Truck with a Plant Charge (500 damage, 5-second arm time). If the Saboteur team destroys the truck, the opponent loses 20 Goods AND $150 Cash AND $80 from the Trucking Depot build cost amortized. The Saboteur costs $160. That is a 2:1 cost-efficiency trade in the Saboteur's favor per truck kill, and Saboteurs can be reused. A player running 3-4 Saboteur teams can effectively zero out an opponent's Goods economy while spending perhaps 30% of what the opponent spends on logistics.

**Severity: 4/5.** This is the most realistic degenerate meta strategy because it does not require a specific faction, is available at T2, and is economically efficient.

**Fix:** Delivery Trucks need a Bootlegger Run equivalent that is not a 90-second cooldown (current stat sheet lists the Bootlegger Run ability but the 90-second cooldown means only 1 in 7.5 minutes of operation benefits from it). Reduce Bootlegger Run cooldown to 45 seconds or add a passive "route memorization" system where frequently-used routes develop AI escorts. Alternatively, Saboteur Plant Charge should require 10 seconds arm time (not 5) against moving targets to prevent instant-kills on trucks in motion.

---

### Strategy 4: Neutral Gang Army (Free Force Multiplier)

**Description:** The GDD describes allied gang benefits as: "their units will not attack you and will attack your enemies in their territory." A gang of "strong" rating has 10-12 Enforcer-equivalents. The cost to ally a Mercenary gang via gift is $200-500 Cash plus completing a job (a mini-objective). If a player allies 2-3 gangs early, they command 20-36 Enforcer-equivalent units that cost them nothing in maintenance and are replaced by the gang's slow regeneration system. These gangs patrol their territory, which covers 1-2 neighborhoods each. A player who routes their economy through gang-held territory gets free armed escorts. The gang units also generate Influence for the player in their neighborhood.

**Why it is broken:** The anti-snowball audit notes that "AI gangs resist the dominant player" (+50% allegiance costs). But this only applies once the player is dominant. In the early game (minutes 3-8) when gangs are most valuable, neither player is dominant and both can recruit at standard cost. The player who spends $300 on gang gifts at minute 4 instead of Thug squads gets 8-10 free fighters immediately. That is equivalent to spending $300 on Thugs (four squads) without the training time. Gangs also occupy territory passively, which generates Influence for the recruiting player and contributes to the Monopoly victory condition counter — a gang-held Turf Point counts for the allied player.

**Severity: 3/5.** Powerful but requires cash investment and job completion (time cost). However, the Morelli faction's "gangs are 30% harder for enemies to turn" compounds this: Morelli + early gang recruitment = a semi-permanent free army that resists counter-diplomacy.

**Fix:** Allied gang units must be explicitly excluded from contributing to Monopoly victory condition Turf Point counts. Gang recruitment should have a minimum time gate (no gifts before minute 5). Gang job objectives need clear scope limits (they cannot be trivially completable in under 2 minutes).

---

### Strategy 5: Hostile Takeover Invisible Win

**Description:** The Hostile Takeover victory requires $5,000 Cash stockpiled, triggered instantly at the Compound. The victory condition is hidden — the opponent cannot see your Cash total. The Solomons reduce this to $3,500. A Solomon player with +25% Cash income and -15% maintenance optimizing purely for Hostile Takeover at T3 (minimum tier requirement) needs $3,500 at approximately minute 32-38 per the victory conditions table. At T3 with a Casino ($60/min), Nightclubs ($35/min x2), Grand Hotel unlocking shortly, and the +25% Solomon bonus, a Solomon player can reach $600+/min income by minute 28-30. At $600/min, they accumulate $3,500 in approximately 5.8 additional minutes — so from minute 30, they win at minute 36 with no warning.

**Why it is problematic for competitive play:** The victory condition table notes the Hostile Takeover is "Hidden — opponent cannot see your Cash total; payment is instant." The document itself recommends adding a tell at $3,500. But for Solomons, $3,500 IS the victory threshold. There is no tell possible. The opponent has zero counterplay window. A Hostile Takeover from a Solomon player is a binary surprise-loss state with no counterplay once the economic conditions are met.

**Severity: 5/5 for competitive viability.** Instant-win with zero counterplay window is anti-competitive regardless of how long the setup takes.

**Fix:** Hostile Takeover must require a countdown for all factions (suggest 60 seconds). For Solomons specifically, either raise their threshold to $4,000 (a smaller discount than the current 30% reduction) or add a mandatory public announcement at $3,000 Cash ("The Solomons are consolidating their finances..."). The instant-win mechanic is the problem, not the threshold.

---

### Strategy 6: Intentional Losing for Anti-Snowball Benefits

**Description:** A player who is slightly behind intentionally concedes 2-3 Turf Points to drop below 25% territory, triggering Desperate Measures (+30% DPS, +20% speed for 120 seconds). They have pre-positioned a 10-15 unit army during the concession phase. The Desperate Measures buff fires on a fully-mustered army. At +30% DPS, a Thug squad deals 20.8 DPS instead of 16 — effectively making T1 units perform at T2 levels. Combined with the +20% speed, the pre-massed force executes a push that is essentially impossible to hold against.

The anti-snowball audit (section 1.4) identifies this "Stockpile and Trigger" exploit and recommends converting Desperate Measures to a persistent conditional buff. **The GDD (section 12) describes Desperate Measures as a one-time trigger and does not incorporate the audit's recommendation.** This is a direct contradiction between documents. The GDD says "once per match"; the audit says this design is exploitable and recommends changing it. The document conflict means the final spec is ambiguous on which version is canonical.

**Severity: 4/5.** The stockpile-and-trigger is a game-winning exploit in the hands of anyone who discovers it in the first week post-launch.

**Fix:** The audit's recommendation is correct — convert to persistent conditional buff active while below 25%, not a timed burst. Document the GDD accordingly. This is not optional tuning; it is a required change before any competitive play.

---

## 3. Pacing Failures

### Is the Early Game (0-8 min) Boring?

Functionally yes, in a specific way. The pacing timeline describes minutes 0-3 as "The Handshake" with tension rated 2/10 and the AoE2 analogy being "dark age sheep scouting." The design explicitly embraces this slow opening. The problem is that in AoE2, the dark age has constant micro demands: sheep control, boar luring, villager queue management, build order optimization. The Commission's equivalent — training Thugs, capturing one building, sending a scout — has perhaps 20% of that decision density.

The minute-by-minute timeline shows:
- Minute 0: Queue Speakeasy, train Thugs, have $225 left
- Minute 1: Speakeasy finishes, train second Thug squad
- Minute 2: Scout contact
- Minute 3: Capture first neutral building

That is three decisions in three minutes. An AoE2 player makes three decisions in 30 seconds during dark age. The Goods system does not provide early-game complexity because Goods are not relevant until T2. The first four minutes will feel slow to RTS veterans, and "slow" in an early access launch is "negative Steam review."

**Fix:** Add 2-3 optional micro decisions in the first 3 minutes. Options: Runner gossip missions (send a Runner to a specific location for a small Cash bonus, like AoE2 sheep relocation), early gang interaction (Paranoid gangs can be accidentally triggered by scout movement), or a randomized "tip" system where your Compound starts with an intel note revealing one of the opponent's first two buildings.

### Is the Mid-Game (8-20 min) a Real Fork or Does One Path Dominate?

The "boom vs. pressure" fork at minute 14 is the design's most important strategic decision. The pacing timeline explicitly states the Aggressive build "must attack in the minute 12-20 window or lose." This is correct, but it creates a problem: if every Aggressive player must attack in an 8-minute window, every Defensive player knows that attacks are coming in an 8-minute window and builds accordingly. The fork stops being a strategic surprise and becomes a solved metagame position. After 100 games, both players know the attack is coming at minute 14-18. The Defensive player builds Sandbag Walls and Fortified Entrances; the Aggressive player masses units. This is not a fork; it is a predetermined script with two known halves.

Genuine strategic forks require information asymmetry — neither player should know which path the opponent is taking until it is too late to fully prepare. The Commission's visible income multiplier (the GDD states "a player should be able to estimate their opponent's income by observing their territory") inadvertently removes that asymmetry. A player who can see that the opponent has built three income buildings and no Distillery by minute 12 knows the opponent is not going for T3 and can safely mass military. The design's own legibility goal undermines its strategic depth goal.

### Is the Late Game (25+ min) a Slog?

The War phase (22-35 min) and Endgame (35-40 min) assume both players reach T3-T4. Per the pacing timeline, the Aggressive player does not reach T4 until minute 33; the Economic player reaches it at minute 30. A 3-minute T4 window is described as decisive ("The Empire unlocks: The Don, Tommy Gun squads, Armored Trucks, and victory condition buildings").

The problem: if both players reach T3 at roughly minute 22-24, and neither can afford T4 until minute 30, there is an 8-minute period (22-30) where both players are at T3 with maxed economies and no new unlocks. That is the design's longest same-tier standoff. Unit training times at T3 (Made Men: 32 sec, Hitmen: 30 sec) are long enough that army replacement is slow. Two evenly-matched T3 armies in an urban environment with heavy cover will produce attritional stalemates — trading squads at 1:1, rebuilding, trading again. This does not match the "Power Play" phase description of "peak territorial tension" and "major engagements." It is more likely to produce cautious jockeying.

### Are 40 Minutes the Right Length?

For competitive 1v1 ranked play, 40 minutes is probably 8-10 minutes too long. The pacing timeline itself identifies that "most 1v1 games conclude between minutes 35-42." That is not a tight distribution. Competitive RTS games target match length variance of less than 25% (a 40-minute target should produce games of 35-45 minutes; the design's own description suggests 35-55 minutes). More importantly: if T4 is reached by minute 30 and victory conditions trigger at minute 32-38, the last 5-8 minutes of a decided game still have to be played out. Games that feel decided but aren't over are the primary driver of player frustration and "gg no re" concession culture.

### Mismatched Skill Level Games

This is the design's most serious unaddressed gap. There is no discussion of what happens when a significantly better player meets a significantly worse one. In AoE2, skill gaps produce fast games (the better player rushes, wins at minute 12-15) because the meta has well-known dominant aggressive timings. In The Commission, the anti-snowball systems actively prevent fast endings. A dominant player facing Heat penalties, diminishing returns, and an opponent with Black Market units who hides in a Safehouse could be forced into a 45-minute mop-up of an already-won game. The GDD's Surrender Timer (section 12, "5 minutes after losing the Compound") is the only mechanism, but losing the Compound is a late-game event. A mismatched game that is decided at minute 20 might still run to minute 40. That is bad for the better player's ranked experience and terrible for the worse player's morale.

---

## 4. Logistics Frustration

### Will Truck Management Be Fun or a Chore?

Honest answer: it will feel like a chore for a significant portion of the player base, and the design does not take this risk seriously enough.

Let's count the active logistics decisions a player manages at peak (minute 20-25, T2-T3 transition):
- 1 Distillery producing 10 Goods/min, needs 1 Delivery Truck on a 2-minute rotation (economy table: "fills a Delivery Truck every 2 minutes")
- 1 Import Dock (if on waterfront) producing 20 Goods/min, needs "1 Armored Truck on a short route or 2 Delivery Trucks"
- Runners carrying early-game Goods
- Convoy scheduling at T4

That is 3-5 transport units requiring periodic attention, route verification, and escort decisions, simultaneously with 10-15 combat squads requiring tactical micro. Company of Heroes, the design's tactical combat reference, has no logistics layer — all resources are generated passively. The Commission is asking players to do CoH-level combat micro AND AoE2-level economic macro AND a logistics sub-game simultaneously. That is a lot.

The GDD's anti-frustration measures (auto-routing, preferred routes, route warnings) are necessary but not sufficient. Route warnings tell you that a truck's path goes through enemy territory. They do not tell you that the enemy has positioned a Saboteur at a chokepoint and is waiting. The player must either manually escort every truck (attention cost) or accept ambush risk. In the current design there is no middle option — the Armored Truck is the "set and forget" choice but costs $200 + 40 Goods, which is not available at T2 launch.

### How Many Trucks at Peak?

At peak economy (T3, minute 25): 1-2 Distilleries + 1 Import Dock = 3-5 Delivery Trucks or Armored Trucks in simultaneous operation. Each truck needs a route, possibly an escort, and periodic attention. This is on top of 12-16 combat squads, 3-4 buildings under construction, and gang allegiance management. Total simultaneous "attention items": approximately 20-25. For comparison, StarCraft II players at Masters level manage approximately 60-80 attention items per minute. But The Commission is targeting AoE2's audience, not StarCraft's. AoE2 Masters players manage perhaps 30-40 attention items per minute. The 20-25 number is plausible for a skilled player but will overwhelm the casual-competitive player the design is presumably targeting.

### What Is the Feel When You Lose a Loaded Truck?

The GDD open questions section (question 2) acknowledges this is the design's most critical validation point. The framing is: "does it feel like losing a villager (annoying but manageable) or losing a StarCraft game (devastating)?"

Based on the numbers: a Delivery Truck carries 20 Goods. T2→T3 requires 350 Goods total. Losing one truck is 5.7% of your T3 total requirement — annoying. But losing a truck at minute 19 when you have 300 Goods saved and needed 350 to advance in 60 seconds sets back your T3 by 2-3 minutes. 2-3 minutes at the T3 transition window (the highest-stakes period in the match) is potentially catastrophic. The loss is not proportional to its narrative moment — the same truck destruction at minute 12 vs minute 19 has wildly different consequences. This unpredictable consequence severity will produce tilt regardless of objective balance.

**Fix:** Consider a "Goods insurance" passive mechanic — when a transport unit is destroyed, 30% of its Goods cargo is dropped on the ground and can be recovered by either player for 30 seconds. This keeps the loss painful but gives the owning player a recovery action (dash a Runner to the drop site) and keeps the raider engaged (do they grab the goods or fall back?). More importantly it caps the worst-case loss at 70% instead of 100%.

### Is the Auto-Routing Enough?

No. Auto-routing solves the "where does the truck go" problem but not the "when does the truck go" problem. A Distillery fills a Delivery Truck every 2 minutes. If the auto-route truck is ambushed and destroyed, the Distillery continues producing into overflow. The player does not know the truck is gone unless they are watching — and they probably are not watching because they are managing a combat engagement. The result: the player discovers at minute 22 that their T3 save is 60 Goods short because two trucks were destroyed while they were fighting. This is not a strategic consequence of a decision they made — it is a consequence of limited attention bandwidth. Punishing attention limits rather than strategic choices feels unfair.

**Fix:** Add a "logistics alert" system that pushes a notification (with screen ping) when a transport unit is destroyed, not just when a route is blocked. The distinction between "route warning" (pro-active) and "destruction alert" (reactive) is meaningful.

---

## 5. Faction Asymmetry Risk

### The Solomons: Too Much Economic Advantage

The Solomons receive +25% Cash income from all sources AND -15% building maintenance. Let's calculate the actual effect at peak economy.

At T3 (minute 25), a standard player earns approximately $200-320/min (economy table, phase summary). A Solomon player earns $250-400/min from the +25% bonus alone. Additionally, maintenance drain at 10 buildings is $50/min for standard players; Solomons pay $42.50/min — a $7.50/min savings that is negligible. The income advantage is the problem: $50-80/min additional income at T3 translates to an extra Hitmen squad every 4.4-7 minutes indefinitely. Combined with the Hostile Takeover threshold reduction (30% off = $3,500 vs $5,000), the Solomons have both the fastest path to one victory condition AND the largest economy. This is not soft asymmetry — it is hard advantage. Every other family must either outplay the Solomons economically or win before T3, because from T3 onward the Solomon income gap produces units faster than any other family can replace losses.

Verdict: **Yes, the Solomons are too strong.** The combination of +25% income, -15% maintenance, AND Hostile Takeover threshold reduction is three economic advantages that all point the same direction. One of these three must be removed or significantly reduced.

### The Korvaks: Rush Dominance Risk

+15% speed and -20% training time is the most competitively dangerous bonus combination in the game because it affects the metric that matters most in early RTS: reaction time. Korvak Thugs cross a city block 15% faster. Korvak Enforcers exit training 3.6 seconds faster (25 sec standard vs ~20 sec Korvak). In a game where the tier-2 punish window is described as "30-45 seconds" (pacing timeline, minute 9), shaving 3-4 seconds per unit off production time is meaningful. Over 10 units, the Korvaks have produced their army approximately 36 seconds faster — essentially a free "age-up" timing advantage without spending anything.

The Korvak +20% Heat generation weakness is a legitimate nerf but it fires too late. Heat matters most at 60%+ territory control. A Korvak rush wins or loses before the player reaches 60% territory. The weakness does not punish the strategy it is supposed to balance.

**Verdict: The rush dominance risk is real but not binary.** Reduce the training time bonus to -12% or make it apply only to T2+ units (not T1 Thugs, which are the rush units).

### The Ashfords: The -15% DPS Penalty Is Too Harsh

Ashford units deal -15% DPS across the board. A Street Thug squad deals 13.6 DPS instead of 16. An Enforcer squad deals 27.2 instead of 32. At every tier, the Ashford player is in a disadvantaged direct combat position. Their compensations are -25% Heat generation and +30% Influence from all sources.

The Influence bonus is strong for Commission Vote victory and political actions. But it does not help in fights, and fights are unavoidable. A player can try to play the Ashford "avoid combat and win through Influence" strategy, but the design explicitly states "a passive turtle player will fall behind in Influence" — and the Ashfords' best path is accumulating Influence from territory control (requiring combat) and buildings (requiring construction in contested areas). The Ashfords are expected to fight for territory to win the Commission Vote, but they fight at -15% DPS.

Compare to Morellis: +20% building HP and gangs 30% harder to turn. The Morelli weakness is "10% longer capture times" — which is a minor inconvenience. The Ashford weakness is -15% DPS in all fights — which is a continuous penalty affecting every engagement from minute 1 to minute 40. The trade-offs are not symmetric.

**Verdict: Reduce Ashford DPS penalty to -8% or convert it to a narrower penalty (e.g., -15% DPS in the open, standard DPS in cover) that matches their "political operator" identity better.**

### Unique Units: Balance Check

The Blitz Squad (Korvak) is a 6-man Tommy Gunner squad with Sprint on a 15-second cooldown. Standard Tommy Gunners are 3-man squads at $200. A Blitz Squad at 6-man is effectively two Tommy Gunner squads' worth of DPS (6-man x 14 DPS/man = 84 DPS vs standard 42 DPS) plus the Sprint mobility to close or escape. Assuming cost is $350-400, that is better than buying two Tommy Gunner squads at $400 total, with added mobility. The Blitz Squad is very likely the strongest unique unit and reinforces that the Korvaks' bonuses are already pointed in the same direction.

The Accountant (Solomon) that steals 30% of an enemy building's income for 120 seconds — on a $60/min Casino, that is $18/min stolen for 2 minutes = $36 stolen plus your own income continues. If the Accountant can chain from building to building with any cooldown shorter than 120 seconds, this is a passive income vacuum that a skilled Solomon player exploits across 3-4 enemy buildings simultaneously.

---

## 6. "AoE Reskin" Test

**Honest verdict: It is approximately 65% reskin, 35% novel.**

The core loop — capture buildings, generate resources, advance tiers, build army, fight for dominance — is AoE2's loop with a crime skin. The tier names are different; the mechanic is identical. The "comparable DNA" framing in the GDD is accurate: this is a hybrid, not a departure.

**What is genuinely novel:**
1. **Physical Goods transport.** No major RTS requires you to physically move a secondary resource through contested space. This is the design's genuine innovation and its biggest risk. AoE2's trade carts are analogous but are not a primary resource — Goods are critical for tier advancement.
2. **Dual-layer territory (Street Presence + Business Ownership).** The distinction between tactical presence and strategic ownership is interesting. A player can own a building without defending it, creating a "remote income" concept that AoE2 does not have. This is a real differentiation.
3. **The gang diplomacy system.** Semi-autonomous AI actors with allegiance meters that react to player behavior is not a standard RTS feature. This creates a third-party dimension to map control that feels genuinely novel.

**What is cosmetically different:**
1. Tier advancement is AoE2's age advancement. "Street Crew → The Outfit" is "Dark Age → Feudal Age." The costs (Cash + Goods + Influence = Food + Gold + Stone) are structurally identical.
2. The Compound is the Town Center. The Safehouse is the Castle. The HQ producing all unit types is standard AoE2 TC behavior.
3. The cover system and suppression are Company of Heroes, not innovated here.
4. The counter matrix (infantry beats cavalry beats siege beats infantry) is genre convention with different units.

**Would an AoE2 veteran feel they are playing something new?**

For the first 10 minutes: no. They are in familiar macro loop territory. For minutes 10-25: yes, once logistics raiding becomes central. The gang diplomacy system will feel different. By minute 30: mostly familiar again (tier 3-4 feels like Castle-Imperial Age escalation). The novelty window is 10-25 minutes — the exact window that must feel good to retain players for replayability.

**Is the logistics system alone enough differentiation?**

For a niche hardcore audience: yes. For mainstream RTS or potential esport audience: it depends entirely on execution feel. If truck management is satisfying micromanagement, it is enough. If it is a frustrating chore (see Section 4), the game collapses onto its familiar skeleton and offers nothing over AoE2 except a crime skin. The logistics system is both the game's most original contribution and its biggest technical risk. Everything rides on making it feel good.

---

## 7. Competitive Viability

### Are 4 Victory Conditions Too Many?

For casual play: no, they add richness. For competitive play: potentially yes, for one specific reason — spectator legibility.

In AoE2, spectators can immediately understand the game state: who has the bigger army, who is winning. In StarCraft II, the same is true — army size and economic lead are visible. In The Commission with 4 victory conditions, a spectator must simultaneously track: military position, Monopoly timer, Influence totals, and whether any player is approaching $5,000 Cash (hidden). The last one is permanently invisible to spectators. A Hostile Takeover victory can come with no visible warning to spectators, which is anti-esport. The moment a Hostile Takeover fires, every spectator will need a 30-second explanation of what just happened. That breaks broadcast narrative.

**Fix:** In tournament/spectator mode, the Hostile Takeover Cash counter should be visible to spectators (not to opponents) so broadcasters can build narrative around it.

### Map Generation Reliability for Ranked Play

The "modular tile system" where neighborhood tiles snap together in randomized configurations is promising but raises a hard balance question. The GDD states: "The generator enforces distance-from-start parity and total resource balance." This is a claim without a specification. What algorithm enforces this? If two Waterfront neighborhoods (Import Docks, major Goods source) are both adjacent to one player's start versus neither being adjacent to the other, that is not balanced even if the total resource count is equal — spatial distribution matters as much as total count.

Validated modular map generation that produces competitively balanced layouts is a research problem solved by almost no games in this genre. AoE2 uses procedural generation that produces notoriously unbalanced maps (Arabia has 20 years of player complaints about tree blocking, gold placement, and water presence). The Commission should not assume the generator will produce competitive-grade maps at launch.

**Recommendation:** For ranked play, begin with 5-8 hand-crafted maps rather than relying on the generator. Use generated maps only after the generator has been validated across 1,000+ outputs with formal balance checking.

### Unit Roster Learnability

The current roster is 14 infantry units + 8 vehicles = 22 unit types across 4 tiers. AoE2 has approximately 35 unit types with 43 civilizations; StarCraft II has approximately 60 unit types across 3 races. The Commission's 22 units is on the low end but appropriate for a launch roster. The counter matrix is 13x13 — learnable. The concern is that the roster may feel thin for the game's 40-minute target length. At minute 30, a player has access to the same units they had at minute 22 (T3 unlocks the same 4 infantry types). No new tactical options appear between T3 arrival and T4 arrival except The Mint and political actions. 8 minutes of T3 without new unlocks is a long time.

### Esport Watchability

Overall assessment: moderate. The gangster aesthetic is strong (high visual clarity for a mass audience unfamiliar with RTS). The cinematic camera cuts for tier advancement are a good broadcast feature. The HUD showing all victory condition progress is excellent for spectators.

The main watchability failure is the logistics layer. Truck interceptions are individually exciting (narrative micro-moments: "the Saboteurs are waiting in the alley — will the truck take this route?") but truck management is small-scale and hard to read on a broadcast overlay. Spectators need a "Goods flow" indicator showing each player's net Goods per minute rather than individual truck status.

---

## 8. Contradictions and Gaps

### Direct Contradiction 1: Desperate Measures

The GDD (section 12) describes Desperate Measures as "a one-time trigger per match." The anti-snowball audit (section 1.4) recommends converting it to "a conditional buff active while below 25%" and explicitly states the one-time burst "is exploitable via stockpile-and-trigger." The audit is a "Senior Systems Design Review" of the same design. These documents cannot both be canonical. The implementation spec must choose one — and the one-time burst is the wrong choice (audit is correct on this).

### Direct Contradiction 2: Rat Economy Trigger Condition

The GDD (section 12) states Rat Economy triggers when a player has "fewer than 3 owned buildings." The audit (section 1.3) recommends changing this to "player has lost 60%+ of their peak building count." The audit also recommends that the Saboteur discount be reduced from 30% to 15%. The GDD still shows the original 30% discount. Again, one spec must prevail, and the audit's version is demonstrably safer.

### Direct Contradiction 3: Delivery Truck Capacity

The economy table (section 2) states: "Delivery Truck: Capacity 20 Goods." The unit-vehicle stat sheet (vehicle table) states: "Delivery Truck: Carries up to 200 Goods." This is a 10x discrepancy. If the unit-vehicle stat sheet is correct, then the economy table's math ("fills a Delivery Truck every 2 minutes" from a 10 Goods/min Distillery) is wrong — a 200-Goods truck takes 20 minutes to fill. If the economy table is correct, the stat sheet is wrong. This is not a tuning difference — these are completely incompatible numbers in two documents that are supposed to describe the same vehicle.

### Direct Contradiction 4: Armored Truck Capacity

Economy table: "Armored Truck: Capacity 35 Goods." Unit-vehicle stat sheet: "Armored Truck: Carries 100 Goods." Another significant discrepancy (35 vs 100). The stat sheet also gives the Armored Truck a "Lockdown" ability and a rear-mounted MG, while the economy table gives it a "rear-gunner upgrade ($100)." These might be intentional (the transport economy table vs the combat stat sheet describing different vehicle variants) but this is not explained anywhere and creates implementation ambiguity.

### Contradiction 5: Convoy as Transport vs Economy Table

The economy table (section 2) lists the Convoy as a T4 transport (80 Goods capacity, $500 cost, 180-second cooldown). The unit-vehicle stat sheet does not include the Convoy as a vehicle entry at all — the War Wagon is the T4 vehicle. If the Convoy is a distinct vehicle from the War Wagon, it needs a stat sheet entry. If the Convoy IS the War Wagon configured as transport, this needs to be stated. Currently there is a T4 transport vehicle in one document that does not exist in another.

### Gap 1: No Compound HP Specified Anywhere

The GDD states the Compound has "high HP and can be fortified." No HP value appears in any document. The unit stat sheet does not include it. The economy table does not include it. This is critical for evaluating rush viability (Degenerate Strategy 1 above). A designer writing a production task from this spec cannot set the Compound HP.

### Gap 2: Victory Condition "Turf Point" Count Undefined

The Monopoly victory condition requires "70%+ of Turf Points." Neither the GDD nor the victory conditions document specifies how many total Turf Points exist on a standard map. The GDD says "each neighborhood has 4-8 Street Corners" and the map has "16-20 neighborhoods" — that implies 64-160 Street Corners, but Street Corners and Turf Points are distinct concepts (mentioned separately in section 5 of the GDD). The number of Turf Points, their spatial distribution, and how they relate to neighborhoods is not specified. A developer cannot implement the Monopoly victory condition from these documents.

### Gap 3: The Goods "Drop on Destruction" Mechanic

When a loaded truck is destroyed, do the Goods it carried drop on the ground for recovery? The economy table says "destroying a loaded truck destroys the Goods it carried." The GDD says "Capturing an enemy truck (surrounding it with units) steals the Goods." So Goods can be stolen but not recovered from a destroyed truck. This is a design choice but an unexamined one — the alternative (partial Goods drop) would significantly reduce truck loss frustration and is worth explicit consideration.

### Gap 4: Production Queue at Compound vs Safehouses

The GDD states the Compound produces all unit types. The Safehouse produces T1 units only. But what happens when a player has built a Secondary Compound ($1,000 at T3)? Can it produce all unit types including T4? Can it execute tier advancement? Can it trigger Hostile Takeover? The Secondary Compound is mentioned in section 6 with one sentence and nowhere in the victory conditions or economy documents.

### Gap 5: Maintenance Cost vs Anti-Snowball Diminishing Returns

The $5/min maintenance per building is deducted from income before or after the Influence multiplier? If before: a building earning $20/min base has a $15/min effective rate, then multiplied by 1.5x (Untouchable Influence) = $22.50/min. If after: $20/min x 1.5x = $30/min, then minus $5/min = $25/min. The $2.50 difference per building is small but across 15 buildings at maximum Influence it is $37.50/min — not negligible over a 40-minute match.

---

## 9. Production Feasibility

### Is the 28-Week Vertical Slice Realistic?

The vertical slice milestone plan (GDD section 14) is deliberately scoped: one neighborhood, one family, Tier 1-2 only, elimination victory only, one AI gang. For a team with RTS experience, 28 weeks for this scope is realistic but not comfortable. The risk is the simultaneous development of systems that have complex interactions: logistics (routing, auto-routes, truck ambush), territory (Street Corners, Influence calculation, dual-layer toggle), gang AI (allegiance system, dynamic behavior), and competitive combat (cover, suppression, flanking, garrison, retreat, veterancy). Each of these systems individually requires 3-6 weeks. They interact with each other in ways that produce emergent bugs that take weeks to diagnose.

**Biggest technical risk:** Pathfinding on an urban grid. The 256x256 map with road tiles, alley shortcuts, building interiors, and blocked routes for different unit types (Runners can use alleys, vehicles cannot) requires a pathfinding solution that handles multiple agent types with different movement rule sets simultaneously, at RTS scale (20+ units pathfinding in real time during combat). Standard A* will not perform adequately. Hierarchical pathfinding (HPA*) or navigation mesh (NavMesh) with multiple layers will be required, and this is 4-8 weeks of solo engineering even for an experienced pathfinding developer. The vertical slice plan allocates 4 weeks to "pre-production: isometric tile renderer, basic pathfinding on urban grid" — that is almost certainly insufficient.

**What Should Be Cut if Scope Shrinks:**

Priority cut list:
1. **AI street gangs.** The allegiance system, gang personality types, job objectives, and dynamic reaction behaviors are a complete sub-game. Cut from vertical slice (stub as static neutral units that become hostile when attacked) and build post-prototype.
2. **Influence/Fear multiplier.** Replace with flat income rates for the prototype. Add the multiplier system in iteration 2 after the base loop is validated.
3. **Multiple cover levels.** Binary cover (in cover / not in cover) is sufficient for vertical slice validation. CoH-style directional cover adds development time without answering the prototype's core questions.
4. **Auto-routing and preferred routes.** Manual truck dispatch is sufficient for a 5-building prototype. Build auto-routing when the map expands.

What must NOT be cut: physical Goods transport and truck ambush. This is the design's core differentiator and the primary thing the prototype must validate. If truck ambush is fun, the game has a unique selling point. If it is not, everything else is moot.

---

## 10. Final Verdict

### Commercial Viability

Conditionally viable. The core concept is strong — the crime setting is visually distinctive, the logistics layer is genuinely novel, and the gang diplomacy system creates a third-party dynamic absent from the genre. However, the design has enough open exploits, document contradictions, and tuning uncertainties that shipping from this spec would produce a broken competitive experience. The anti-snowball audit correctly identifies most of the mechanical risks; the GDD has not incorporated the audit's recommendations. These documents are in conversation but not yet in agreement, and a development team building from both will produce a design that inherits the problems the audit identified.

### Three Strongest Design Elements

1. **Physical Goods transport as a skill axis.** Making the secondary resource physically vulnerable to interdiction is the design's most original and most interesting contribution to the genre. If the implementation feels good (and that is genuinely uncertain), it creates a skill expression dimension that AoE2 does not have.

2. **Dual-layer territory (Street Presence + Business Ownership).** The distinction between tactical unit presence and strategic building ownership creates interesting decisions that persist even when you are not fighting. A player can own profitable enemy-adjacent buildings as a constant provocation, or leave them uncontested as bait. This is a richer territory system than AoE2's or CoH's.

3. **The Prohibition-era aesthetic with mechanical justification.** The setting is not merely cosmetic — speakeasies, distilleries, trucks of bootleg goods, gang allegiance, police raids, and political corruption all map directly onto game systems. The world and the mechanics are genuinely coherent, which is rarer than it sounds.

### Three Weakest / Highest-Risk Elements

1. **The Solomon faction and Hostile Takeover interaction.** A faction with +25% income, -15% maintenance, and a 30% reduced Hostile Takeover threshold combined with an instant-win mechanic is a competitive meta-warper that will define the ranked experience within days of launch. This needs to be fixed before any public playtest.

2. **The anti-snowball suite's mutual stacking.** The audit is unambiguous: all seven systems active simultaneously creates "a death sentence for being ahead" and incentivizes maintaining exactly 50% territory indefinitely. The GDD acknowledges the Zombie Problem and proposes a Surrender Timer solution, but the Surrender Timer only fires after Compound loss — far too late. The unified Pressure System approach recommended by the audit must be adopted.

3. **Truck management peak complexity.** At T2-T3 (the game's most critical window), players manage 3-5 transport units simultaneously with combat micro demands. The design's anti-frustration measures address route planning but not attention bandwidth. If a majority of playtesters report that truck management "pulled them away from the fight," the mechanic needs a more automated management system (not auto-route, but something closer to Offworld Trading Company's market auto-sell). The current implementation spec puts the burden entirely on player attention during the game's highest-stakes phase.

### Single Most Important Thing to Get Right in the Prototype

**Truck ambush — specifically the emotional feel of losing a loaded truck to an interception.**

This one interaction determines the viability of the entire logistics system, which is the only thing making this game not-AoE2-with-a-skin. If playtesters say "that was a great attack, well played" when their truck gets ambushed, the game works. If they say "I can't believe that happened while I was fighting, I give up," the game does not. No amount of balance tuning fixes that emotional response after the fact — it has to be designed correctly from the first playtest. That means: fast feedback when a truck is attacked (audio ping, screen flash), a recoverable-goods mechanic (30% drops on destruction), clear minimap visibility of the ambush location, and a rapid respawn time on replacement trucks ($40-50, 12-second build time). The player must feel like they lost a battle, not like the game punished them for being busy.

---

*This review was conducted adversarially. The design has merit. The goal of identifying problems is not to dismiss the project but to make it better before real money and real player time are spent on the wrong version of it.*
