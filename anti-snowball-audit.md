# Anti-Snowball Systems Audit -- The Commission

> **Reviewer:** Senior Systems Design Review
> **Date:** 2026-03-08
> **Scope:** Seven proposed anti-snowball mechanics for 1v1 PvP balance.
> **Reference Document:** `economy-balance-tables.md` (same directory).
> **Design Target:** 40-minute matches. PvP-first. AoE2 macro + CoH tactics hybrid. Four tiers. Three resources (Cash, Goods, Influence).

---

## Preamble

Anti-snowball mechanics are necessary in any PvP RTS. Without them, the first meaningful engagement decides the match, and the remaining 30 minutes are a formality. The goal is to keep the trailing player in the fight *without* invalidating the leading player's earned advantage.

The danger is overcorrection. Too many rubber-band systems stacked together create a game where winning feels bad and intentional losing becomes optimal. This audit examines each proposed mechanic individually, then considers their cumulative impact. Several of these mechanics have serious exploitability concerns that must be addressed before implementation.

Throughout this review, I reference the economy tables directly. A Speakeasy generates 20 $/min. A Thug squad costs ~75$. An uncontested player reaches T3 by ~minute 20. These numbers matter because anti-snowball mechanics are only as good as the economic context they operate in.

---

## 1. Mechanic-by-Mechanic Audit

### 1.1 Heat System

| Column | Detail |
|---|---|
| **Mechanic Name** | Heat System |
| **Trigger Condition** | Leading player (composite score: territory + income + army value) gradually accumulates Heat. |
| **Effect on Leader** | Unit costs increase by up to 25%. Random police raids temporarily disable buildings (30-60 sec). |
| **Effect on Trailer** | None directly. Indirect benefit: leader's military becomes more expensive, reducing reinforce speed. |
| **Exploitability Risk** | **Medium** |
| **Exploit Scenario** | A skilled player tanks their army value by keeping a lean army of cheap units while holding 60%+ territory with buildings alone. Composite score may not flag them as "leading" even though their economy is dominant. Alternatively, a player could intentionally lose a few buildings to dip below the threshold, build up a massive army during the low-Heat window, then push with full force before Heat ramps back up. |
| **Design Verdict** | **Modify** |
| **Recommended Changes** | (1) Base Heat on *income* and *territory* only -- drop army value from the composite score. Army value is too easy to manipulate by spending or not spending. Income and territory are harder to fake. (2) Clarify Heat's ramp rate. A linear ramp is exploitable (players will hover just below the threshold). Use a quadratic or stepped curve: Heat should feel negligible below 55% territory, noticeable at 60-65%, and punishing above 70%. (3) Police raids should target the *highest-income* building, not a random one. Random raids feel arbitrary and punish the wrong thing; targeting the best building forces strategic building placement. (4) The 25% cost cap is reasonable but should apply to Cash cost only, not Goods or Influence costs. Otherwise Heat punishes tier-up research, which is unrelated to snowballing. |

### 1.2 Diminishing Returns on Territory

| Column | Detail |
|---|---|
| **Mechanic Name** | Diminishing Returns on Territory |
| **Trigger Condition** | Controlling more than 50% of map Turf Points. |
| **Effect on Leader** | Each Turf Point beyond 50% gives -10% income per 10% bracket. At 80% territory, extra points yield only 50% of base income. |
| **Effect on Trailer** | None directly. Their existing territory remains at full value. Indirectly, the leader's economy scales less efficiently, narrowing the income gap. |
| **Exploitability Risk** | **Low** |
| **Exploit Scenario** | Minimal. A player cannot easily exploit this because it only penalizes *excess* territory, not existing holdings. The only concern: in team games (if added later), allies could coordinate to keep each player at exactly 50% for full efficiency, but that is an edge case for 1v1 scope. |
| **Design Verdict** | **Keep** |
| **Recommended Changes** | This is the cleanest mechanic in the set. One minor adjustment: make the diminishing returns apply to *Turf Point income* specifically, not to buildings constructed on that territory. A Casino built at 75% territory control should still generate its full 60 $/min -- the Turf Point itself (the passive territorial income) is what degrades. If building income also degrades, you punish the player for using their buildings, which feels terrible and discourages building placement in forward territory (the opposite of what you want in a map-control game). Confirm that the economy tables treat "Turf Point income" and "building income" as separate streams. |

### 1.3 Rat Economy

| Column | Detail |
|---|---|
| **Mechanic Name** | Rat Economy |
| **Trigger Condition** | Player controls fewer than 3 buildings. |
| **Effect on Leader** | None directly. Indirectly, the trailing player remains a threat even when nearly eliminated. |
| **Effect on Trailer** | Gains 20 $/min passive income (unraidable). Saboteur units unlocked at 30% reduced cost. |
| **Exploitability Risk** | **High** |
| **Exploit Scenario** | **The "Intentional Rat" exploit.** A player sells or abandons their own buildings to drop below 3, activating Rat Economy. They then use the unraidable 20 $/min plus Saboteurs to harass the opponent's economy. Meanwhile, the opponent has to defend a sprawling empire against cheap Saboteurs while the "Rat" player has nothing to defend. This is especially dangerous in combination with the Safehouse: a player with 1 Safehouse + Rat Economy + cheap Saboteurs becomes an annoying, unkillable nuisance with no economic downside. A second exploit: a player builds only 2 buildings from the start, never exceeding the threshold, and plays the entire game as a "Rat" -- using the guaranteed 20 $/min as a safe base while investing everything into military. This is a degenerate strategy that bypasses the entire economy system. |
| **Design Verdict** | **Modify (heavily)** |
| **Recommended Changes** | (1) Change the trigger from "fewer than 3 buildings" to "player has lost 60%+ of their peak building count." This prevents intentional Rat play from the start -- you must have *had* buildings and *lost* them. (2) Reduce the flat income to 10 $/min. At 20 $/min, Rat Economy is almost as good as a Corner Store (12 $/min) with zero risk. It should be a lifeline, not a viable strategy. (3) Saboteur discount should be 15%, not 30%. At 30% discount plus unraidable income, Saboteur spam is too cost-effective. (4) Add a timer: Rat Economy activates 60 seconds after dropping below threshold, preventing instant toggling. (5) Rat Economy income should *replace* normal income from remaining buildings, not stack on top of it. If you have 2 buildings generating 30 $/min, you get 30 $/min, not 50 $/min. |

### 1.4 Desperate Measures

| Column | Detail |
|---|---|
| **Mechanic Name** | Desperate Measures |
| **Trigger Condition** | Player drops below 25% territory for the first time in a match. |
| **Effect on Leader** | Must face a temporarily buffed enemy army (+30% DPS, +20% speed for 120 seconds). |
| **Effect on Trailer** | All current units gain a one-time combat buff for 120 seconds. |
| **Exploitability Risk** | **Medium-High** |
| **Exploit Scenario** | **The "Stockpile and Trigger" exploit.** A player masses a large army while intentionally conceding territory. The moment they drop below 25%, their entire stockpiled force gets the buff. They then counterattack with a massive +30% DPS / +20% speed army. If timed correctly (e.g., building a 15-Thug deathball before triggering), this creates a nearly unbeatable timing push. 120 seconds is a long time -- long enough to wipe an unsuspecting opponent's army and recapture significant territory. A second concern: the buff's trigger at "first time below 25%" means it cannot be used strategically later in the match. If a player crosses 25% during an early skirmish (say, minute 5 when territory is still being established), they waste the buff on a 3-unit squad. This feels awful and is effectively random depending on early game map state. |
| **Design Verdict** | **Modify** |
| **Recommended Changes** | (1) Change from a one-time trigger to a conditional buff: active *while* below 25% territory, not a 120-second burst. This removes the "stockpile and trigger" exploit because the buff disappears as soon as you recapture territory. (2) Reduce the numbers. +30% DPS is enormous -- that is essentially a free tier of upgrades on every unit simultaneously. Reduce to +15% DPS and +10% speed. (3) Add a minimum match time before it can activate (e.g., after minute 10). This prevents accidental early triggers during the initial territory scramble. (4) The buff should apply only to units that existed when the threshold was crossed, not to newly produced units. Otherwise the player produces buffed units for the entire duration. Wait -- if you take recommendation (1), this is handled automatically. |

### 1.5 Snitch Mechanic

| Column | Detail |
|---|---|
| **Mechanic Name** | Snitch Mechanic |
| **Trigger Condition** | Player has lower Influence than their opponent. Costs 50 Influence. 180-second cooldown. |
| **Effect on Leader** | All unit positions revealed for 20 seconds. |
| **Effect on Trailer** | Full map vision of enemy army for 20 seconds. |
| **Exploitability Risk** | **Low** |
| **Exploit Scenario** | The self-correcting cost structure limits abuse. Spending 50 Influence when you are already behind in Influence is painful -- it widens the Influence gap, which per the economy tables means worse Fear effects, worse income multiplier, and delayed access to T3/T4 buildings. The 180-second cooldown also prevents spam. The only concern: at high levels of play, 20 seconds of full vision might be *too* strong. A skilled player can react to full vision by dodging every engagement and sniping undefended buildings. However, 20 seconds is short enough that this requires exceptional micro, which is probably fine for a skill-expression mechanic. |
| **Design Verdict** | **Keep** |
| **Recommended Changes** | Minor tweaks only. (1) Consider reducing vision duration to 15 seconds. 20 seconds is generous; 15 still gives actionable information without allowing complete repositioning. (2) Add a visual indicator to the leading player: "Your positions have been compromised" with a brief screen flash. They should know the Snitch was used so they can react (move hidden units, cancel flanks). Surprise is fine, but invisible information asymmetry breeds frustration. (3) The Influence cost (50) is appropriate at mid-game but devastating in early game. Consider scaling the cost: 30 Influence before minute 15, 50 after. This makes it usable when it matters most (the early snowball window). |

### 1.6 Black Market

| Column | Detail |
|---|---|
| **Mechanic Name** | Black Market |
| **Trigger Condition** | Player drops below 30% territory. Black Market appears at Compound. |
| **Effect on Leader** | Must deal with higher enemy unit throughput (more bodies, slightly weaker individually). |
| **Effect on Trailer** | Units cost 20% less Cash but have 10% reduced HP. |
| **Exploitability Risk** | **Medium** |
| **Exploit Scenario** | The 20% cost reduction with only 10% HP penalty is mathematically favorable. A Thug at 75$ with full HP vs. a Thug at 60$ with 90% HP -- the cheap Thug is better value in almost every engagement because you field more of them. Mass quantity beats slight quality in most RTS engagements (focus fire and overkill math favor the larger army). This means a player at 29% territory with Black Market access actually has *better* cost-efficiency than a player at 31% without it, creating a perverse incentive to stay below 30%. Additionally, the HP reduction does not affect units that rely on alpha damage (first-strike assassins, snipers). Units that kill before taking return fire do not care about 10% less HP. |
| **Design Verdict** | **Modify** |
| **Recommended Changes** | (1) Equalize the trade-off: 20% less Cash should come with 20% less HP, not 10%. The discount must feel like a genuine desperation trade, not a mathematical upgrade. (2) Black Market units should have a visual indicator (different model tint, "contraband" tag) so the leading player can identify them and adjust tactics. (3) Black Market should only apply to T1 and T2 units. Discounted T3/T4 elite units are too strong and remove the tier advantage that the leading player earned. (4) Consider adding a Goods cost to Black Market units (even 2-3 Goods per unit) to prevent pure Cash-spam when the trailing player has no Goods infrastructure left. This adds friction that slows down the spam without eliminating the mechanic. |

### 1.7 Safehouse Persistence

| Column | Detail |
|---|---|
| **Mechanic Name** | Safehouse Persistence |
| **Trigger Condition** | Always active. Each player has one Safehouse with 5x normal building HP. Hidden from minimap (must be scouted). Produces T1 units only. |
| **Effect on Leader** | Cannot fully eliminate the opponent without finding and destroying the Safehouse (or destroying all other buildings + remaining units). Extends the game. |
| **Effect on Trailer** | Can always produce Runners and Thugs. Provides a foothold for comeback attempts even after total economic collapse. |
| **Exploitability Risk** | **Medium-High** |
| **Exploit Scenario** | **The "Hidden Fortress" problem.** If the Safehouse is hidden and has 5x HP, it becomes the optimal building to protect. A player can deliberately invest nothing in defense of their main base, dump all resources into military, and fall back to the Safehouse when pushed. The opponent then has to scout the entire map to find it, and even when found, 5x HP takes significant time to destroy -- time during which the Safehouse player is producing Thugs and harassing. Combined with Rat Economy, a player with just a Safehouse can generate 10-20 $/min (depending on Rat Economy adjustments), produce Thugs every 4-5 minutes, and endlessly stall. This is the core of the "Zombie Problem" (see Section 3 below). A second concern: the hidden placement creates a degenerate meta where both players hide their Safehouse in the most obscure corner of the map, leading to tedious endgame scavenger hunts. |
| **Design Verdict** | **Modify** |
| **Recommended Changes** | (1) The Safehouse should be placed during the first 2 minutes of the match only, and its location is locked permanently. This prevents mid-game repositioning exploits. (2) Reduce HP multiplier from 5x to 3x. 5x is excessive -- for reference, if a normal building has 200 HP, the Safehouse would have 1,000 HP, which takes a full T3 army significant time to chew through. 3x (600 HP) is tough enough to buy time without being a bunker. (3) **Add a "Heat Signature" reveal.** If the Safehouse is the player's last building, it becomes visible on the minimap after 60 seconds. This prevents the scavenger hunt problem while still giving the losing player a 60-second window to rally. (4) Safehouse should NOT interact with Rat Economy. If Rat Economy's trigger is "lost 60%+ of peak buildings" (per the recommended change above), the Safehouse alone should not count as meeting that threshold. (5) Limit Safehouse production to Thugs only, not Runners. Runners as scouts/harassment from an unhuntable building is too annoying. Thugs at least have to commit to a fight. |

---

## 2. Cumulative Impact Analysis

The worst-case scenario for the leading player is this: they hold 70% territory, have the highest income, and possess the largest army. In this state, they face Heat penalties (up to 25% increased unit costs plus random building raids), diminishing territory returns (Turf Points beyond 50% yield reduced income), and the Influence-based Fear effects are at maximum (which benefits them, but this is offset by the opponent's access to the Snitch mechanic). Meanwhile, their opponent at 30% territory or below has access to Rat Economy (if applicable), Black Market discounts, and Desperate Measures buffs. If the trailing player uses the Snitch, the leader's positions are fully revealed. The leader is paying 25% more for units, earning diminished returns on half their territory, losing buildings to police raids every 30-60 seconds, and facing an opponent who produces 20% cheaper units with full vision and a DPS/speed buff. That is not a disadvantage -- that is a death sentence for being ahead.

The fundamental problem is that these seven mechanics were designed independently, each solving the snowball problem on its own, and then stacked on top of each other. Any two or three of them in combination is probably fine. All seven simultaneously will create a game where the optimal strategy is to maintain *exactly* 50% territory, never push further, and wait for the opponent to overextend into their own penalties. This is degenerate gameplay. The solution is not to cut mechanics wholesale, but to create mutual exclusivity: if Heat is active, Black Market should not also be active. If Desperate Measures is triggered, Rat Economy should be locked out. Design these as a single unified "Pressure System" with one set of escalating effects, not seven independent systems that can all fire at once. The leading player should feel pressure, not paralysis.

---

## 3. Intentional Losing Exploits

- **Territory Donation for Desperate Measures.** A player at 30% territory intentionally gives up two Turf Points to drop below 25%, triggering the DPS/speed buff. They then counterattack immediately with a pre-positioned army. **Risk: High.** Mitigation: Change Desperate Measures to a persistent conditional buff (active while below 25%) rather than a timed burst, so recapturing territory removes the advantage.

- **Building Sacrifice for Rat Economy.** A player sells or deliberately lets the enemy destroy their own buildings to drop below 3 (or below 60% of peak, if the recommended change is adopted). They then play as a "Rat" with unraidable income and cheap Saboteurs. **Risk: High.** Mitigation: Require that the buildings were destroyed by the *enemy*, not sold or abandoned by the owner. Track building destruction source and only credit enemy-caused losses toward Rat Economy activation.

- **Influence Dumping for Snitch Access.** A player with high Influence spends it rapidly on unnecessary political actions to drop below their opponent's Influence level, then uses the Snitch to reveal positions. After sniping key targets with perfect information, they rebuild Influence naturally. **Risk: Medium.** Mitigation: Add a "recently spent" Influence cooldown -- the Snitch requires that the player has been at lower Influence for at least 60 consecutive seconds, preventing rapid dump-and-snitch cycles.

- **Hovering at 31% Territory for Black Market Access.** A player deliberately avoids recapturing territory to stay below 30% and maintain Black Market pricing. They field a steady stream of cheap units from a defensible position while the "leading" player is punished by Heat and diminishing returns. **Risk: Medium-High.** Mitigation: Black Market should phase out gradually as territory is recaptured (e.g., discount reduces by 5% per Turf Point recaptured), and if the player has been below 30% for more than 5 minutes, the discount should decay over time (representing supply drying up). Desperation mechanics should not be permanent states.

- **Safehouse-Only Opening.** A player builds only a Safehouse and their starting HQ, then immediately sells the HQ. They now have 1 building, qualify for Rat Economy, and have a hidden, heavily fortified production structure. They play the entire game as a guerrilla force. **Risk: Medium** (depends on whether Rat Economy interaction is patched per recommendations). Mitigation: The HQ should be unsellable, and Rat Economy should require enemy-caused building losses, not self-inflicted ones (see above).

---

## 4. The "Zombie Problem"

The combination of Safehouse Persistence, Rat Economy, and Black Market creates a scenario where a game is functionally decided -- the trailing player has lost their economy, their army, and 85%+ of the map -- but cannot be ended. The trailing player sits on a hidden Safehouse, produces one Thug every few minutes from Rat Economy income, and uses that Thug to capture a single undefended Turf Point before dying. The leading player has to patrol the entire map to find the Safehouse, kill the occasional Thug, and wait. This is not gameplay; this is a chore. The match could drag on 10-15 minutes past the point of decision, violating the 40-minute target. The recommended mitigations help (Heat Signature reveal after 60 seconds as last building, Rat Economy requiring enemy-caused losses, Safehouse HP reduced to 3x), but a structural solution is also needed: implement a **Dominance Timer**. If one player controls 80%+ territory for 180 consecutive seconds, they win via "Total Control" victory. This gives the losing player a clear goal (contest at least one Turf Point every 3 minutes to reset the timer) and gives the winning player a guaranteed endgame clock. The timer should be visible to both players. This is thematically justified as the city's power structure recognizing the dominant faction's control, and it solves the Zombie Problem without removing comeback mechanics -- it just puts a clock on them.

---

## 5. Genre Precedent Comparison

Age of Empires II handles snowball primarily through asymmetric unit costs: trash units (Spearmen, Skirmishers, Light Cavalry) cost no gold, so a player who has lost their gold economy can still field an army. This is elegant because it does not punish the leading player -- it just ensures the trailing player has *something* to work with. Hussar raids give the losing player an action they can take (raiding enemy economy) without a system-granted buff. Company of Heroes uses a veterancy system where surviving units become stronger, which subtly favors the defender (their units survive longer, gaining vet, while the attacker's reinforcements start fresh). CoH's territory point auto-generation also provides baseline income regardless of building count. StarCraft II relies almost entirely on game mechanics rather than rubber-band systems: defender's advantage comes from the inherent asymmetry of attacking vs. defending (the defender chooses the engagement position), worker rebuild speed is fast enough that economic damage is temporary, and macro mechanics (injecting, chronoboost, MULEs) give skilled players tools to recover. The common thread is that the best anti-snowball systems are **structural** (built into the game's core mechanics) rather than **reactive** (triggered by falling behind). The Commission should learn from this: the Influence/Fear system, Goods transport vulnerability, and tier cost structure already provide structural anti-snowball pressure. A skilled raider can cripple a leading player's Goods income by sniping Delivery Trucks. A fast-teching player who neglects military is punished by the tier research time window. These structural elements are superior to the reactive systems proposed here, and the reactive systems should be treated as supplements, not the primary balance tool. Over-reliance on reactive mechanics tells players that the game cannot balance itself, which undermines competitive credibility.

---

## 6. Final Recommendation

### Priority Tier: Implement First

1. **Diminishing Returns on Territory** -- Cleanest mechanic. Low exploit risk. Straightforward to implement and tune. Creates natural map-control equilibrium without punishing the leading player. Ship it with the minor clarification that it affects Turf Point income only, not building income.

2. **Heat System (modified)** -- Strong thematic fit. Requires the recommended changes (income/territory-based scoring, quadratic ramp, targeted raids, Cash-only cost increase) but is fundamentally sound. This is the game's primary anti-snowball lever and should be tunable via a single Heat coefficient.

3. **Snitch Mechanic** -- Low risk, high skill expression, self-correcting cost. The Influence spend ensures it is a meaningful decision, not a free button. Implement with the 15-second vision duration and the "positions compromised" notification to the leading player.

### Priority Tier: Implement with Caution

4. **Safehouse Persistence (modified)** -- Necessary for game-feel (players need to know they always have *something*), but requires all five recommended changes: locked placement, 3x HP, Heat Signature reveal as last building, no Rat Economy interaction, Thugs-only production. Must be paired with the Dominance Timer to prevent Zombie games.

5. **Black Market (modified)** -- Useful as a desperation tool but must have equalized trade-offs (20% cost = 20% HP), T1/T2 unit restriction, and a decay timer. Without these changes, it is a mathematical exploit disguised as a comeback mechanic.

### Priority Tier: Needs Significant Redesign or Playtesting

6. **Desperate Measures (modified)** -- The concept is good (a last stand moment), but the one-time burst design is either wasted on an accidental early trigger or exploited via stockpile-and-trigger. Reworking it as a persistent conditional buff (active only while below 25%) is a fundamental redesign that needs dedicated playtesting. The numbers (+15% DPS, +10% speed in the modified version) must be validated: too low and it is unnoticeable, too high and it makes pushing into a cornered opponent impossible.

7. **Rat Economy (modified heavily)** -- The most dangerous mechanic in the set. Even with all five recommended changes, it creates a play pattern (invisible income that cannot be interacted with) that violates a core RTS principle: the opponent should always be able to attack your economy. Consider cutting the "unraidable" aspect entirely. Instead, Rat Economy could grant a one-time emergency Cash injection ($200) when triggered, rather than a permanent income stream. This gives the trailing player a second chance without creating an invulnerable economic base.

### Structural Addition (not in original proposal)

8. **Dominance Timer** -- Implement a "Total Control" victory condition: holding 80%+ territory for 180 consecutive seconds wins the game. This is not an anti-snowball mechanic per se, but it is the necessary counterweight that prevents anti-snowball mechanics from creating unkillable Zombie states. Without it, mechanics 3, 4, 6, and 7 will extend losing games past the point of fun.

### Summary Table

| Mechanic | Verdict | Exploit Risk (Post-Modification) | Implementation Priority |
|---|---|---|---|
| Diminishing Returns on Territory | Keep as-is | Low | 1st |
| Heat System | Modify, then implement | Low-Medium | 2nd |
| Snitch Mechanic | Keep with minor tweaks | Low | 3rd |
| Safehouse Persistence | Modify heavily, then implement | Medium | 4th |
| Black Market | Modify, then implement | Medium | 5th |
| Desperate Measures | Redesign, then playtest | Medium | 6th |
| Rat Economy | Redesign or consider cutting | Medium-High (even modified) | 7th |
| Dominance Timer (new) | Implement alongside Safehouse | Low | Pair with 4th |

### What Playtesting Must Resolve

These are questions that design documents cannot answer. They require real matches with real players:

- **Heat ramp rate.** How quickly should Heat accumulate? Too fast and the leader never pushes past 60% territory; too slow and it never matters. This needs dozens of matches to calibrate.
- **Desperate Measures numbers.** +15% DPS and +10% speed -- is this noticeable enough to matter? Is it too strong for certain unit compositions (e.g., fast melee units that benefit disproportionately from speed)?
- **Dominance Timer duration.** 180 seconds is a starting point. If the trailing player can always contest one Turf Point with a single Thug, the timer never completes and does not solve the Zombie Problem. The threshold (80% territory) and duration (180 seconds) both need tuning.
- **The "emotional feel" of Heat.** Players who are winning should feel challenged, not punished. The difference is subtle and subjective. If playtesters report that being ahead "feels bad," the Heat numbers are too aggressive, regardless of whether they are mathematically balanced.
- **Rat Economy viability.** Even the modified version (one-time $200 injection) needs testing. Is $200 enough to mount a comeback? Or is it so little that the trailing player resigns anyway, making the mechanic pointless?

---

*This audit identifies significant stacking risks and exploitability concerns in the proposed anti-snowball suite. The individual mechanics range from well-designed (Diminishing Returns, Snitch) to potentially game-breaking (Rat Economy, unmodified Desperate Measures). The most critical recommendation is to treat these not as seven independent systems but as a single unified Pressure System with mutual exclusivity and escalating tiers. The second most critical recommendation is the Dominance Timer, without which several of these mechanics will extend losing games indefinitely.*

*Last updated: 2026-03-08.*
