# THE COMMISSION — Game Design Document

**Genre:** PvP-first Real-Time Strategy
**Setting:** Prohibition-era alternate American city (fictional)
**Tone:** Cinematic gangster epic, gritty noir atmosphere
**Target Match Length:** 35-45 minutes (1v1), 40-55 minutes (2v2)
**Player Count:** 1v1, 2v2 (primary); FFA 3-4 player (secondary)
**Platform:** PC (primary), console (stretch)
**Comparable DNA:** Age of Empires II (macro economy, age progression, expansion rhythm) + Company of Heroes (urban tactical combat, cover, suppression, capture points)

---

## 1. Executive Concept

*The Commission* is a competitive real-time strategy game where players control rival mafia families fighting for dominance over a single dense, prohibition-era American city. Players capture and develop urban properties — speakeasies, distilleries, casinos — to fuel a criminal economy that escalates from small-time hustling to full-scale organized crime. Physical goods must be transported through contested streets, creating vulnerable logistics lines that opponents can raid. Combat begins as small skirmishes between street toughs and escalates into pitched battles with armored cars and tommy guns. Victory is achieved not just through military elimination but through economic monopoly, political influence, or raw financial domination.

The core tension: **everything you build is worth fighting over, and everything you move can be stolen.**

**One-sentence pitch:** *Age of Empires meets The Godfather — build a criminal empire block by block, protect your supply lines truck by truck, and crush your rivals street by street.*

---

## 2. Core Design Pillars

### Pillar 1: Vulnerable Prosperity
Every source of income is a target. Every supply line is a risk. Players must balance expansion with defense. The richest player is also the most exposed.

### Pillar 2: The City Is the Map
No procedural wilderness. The city is a handcrafted urban environment with distinct neighborhoods, choke points, back alleys, and landmarks. Terrain is buildings, streets, rooftops, and intersections — not forests and rivers. The map is dense, readable, and rewards spatial knowledge.

### Pillar 3: Escalation, Not Explosion
Matches follow a measured arc from street-corner scuffles to organized warfare. The 4-tier progression system gates unit power and strategic options, creating a rising tension curve rather than a rush-or-die opener.

### Pillar 4: Territory Has Texture
Owning territory is not binary. Street presence gives tactical control (vision, movement safety, pressure). Business ownership gives strategic control (income, production, expansion). A player can have street presence without owning local businesses, or own a distant business without local military control. This creates layered strategic decisions.

### Pillar 5: Readable Conflict
PvP clarity takes priority over thematic flavor. Every unit, building, and vehicle must be visually distinct. The game state — who controls what, where supply lines run, where armies are — must be legible at a glance. If a mechanic is thematically cool but unreadable in competitive play, it gets cut or simplified.

---

## 3. Why This Is Not "AoE in a City"

This is the most important design question to answer upfront. The risk of "AoE reskin syndrome" — where you've just re-themed Age of Empires with gangster art — is real. Here is how The Commission structurally diverges:

| Dimension | Age of Empires II | The Commission | Why It Matters |
|-----------|------------------|----------------|----------------|
| **Resource gathering** | Villagers harvest map resources (wood, food, gold, stone) from fixed deposits | Income flows passively from captured businesses; amount modulated by Influence/Fear | No "villager micro." Economy is about acquisition and protection, not harvesting |
| **Base building** | Construct buildings on open land from scratch | Capture existing urban properties, then upgrade with attachments | You fight over infrastructure, not empty space |
| **Expansion** | Build new Town Centers on open land | Capture anchor properties in contested neighborhoods | Expansion is inherently confrontational — there is no safe "back base" |
| **Resource transport** | Resources teleport to stockpile | Physical goods must be trucked through city streets | Creates a logistics game layer AoE completely lacks |
| **Map structure** | Open terrain with chokepoints (hills, rivers, forests) | Dense urban grid with buildings, alleys, intersections, sightline blocks | Fundamentally different tactical geometry |
| **Combat model** | Mass army clashes on open fields, micro individual units | Squad-based with cover, suppression, garrisons, flanking, and urban terrain advantage | CoH-style tactical depth replaces AoE's formation-based combat |
| **Neutral actors** | Wolves, boar, relics | AI street gangs with their own territory, personality, and allegiance systems | Dynamic third-party actors that shift based on player investment |
| **Territory control** | Implicit (wherever your army is) | Explicit dual-layer system: street presence + business ownership | Territory is a game system, not just a spatial concept |
| **Win conditions** | Mostly elimination + relics/wonder | Four distinct victory paths with counterplay | More strategic diversity, less "bigger army wins" |
| **Catch-up** | Limited (trash units, raiding) | Dedicated anti-snowball suite (Heat, Rat Economy, Desperate Measures, etc.) | Games stay competitive longer |

**The core structural difference:** In AoE, your economy is *behind* your army. In The Commission, your economy *is* the battlefield. Every speakeasy, every truck route, every street corner is simultaneously an economic asset and a military objective. You cannot separate "economy play" from "military play" — they are the same thing.

---

## 4. Match Flow: Opening to Endgame

### Phase 1: The Handshake (Minutes 0-3)
Players start with a Compound (main base) and a small crew of Runners and Thugs. The opening is about scouting: sending Runners to reveal the map, identify your nearest neutral buildings, and locate the opponent's Compound. First economic decisions: which nearby buildings to claim first? Corner Store (immediate cash) or Back-Alley Still (goods production for tier advancement)?

**Tension level:** Low. Exploratory. The calm before the storm.

### Phase 2: Staking Claims (Minutes 3-8)
Players capture their first 3-5 neutral buildings and establish initial income. The map's center is contested — both players want the high-value buildings there. First skirmishes erupt as Thug squads clash over a contested Speakeasy or street corner. AI street gangs in unclaimed neighborhoods react to encroachment. Players make their first strategic choice: fight for center or secure flanks?

**Tension level:** Rising. First blood is drawn.

### Phase 3: The Racket (Minutes 8-15)
Tier 2 unlocks. Players gain access to Enforcers, Tommy Gunners, and the first vehicles. The goods economy starts mattering — players need to establish distillery-to-compound transport routes. First truck ambushes occur. The mid-map territory solidifies into rough frontlines. Players begin investing in building upgrades and defenses.

**Tension level:** Medium-high. Meaningful combat begins.

### Phase 4: Power Play (Minutes 15-25)
Tier 3 unlocks for well-managed economies. Hitmen, Made Men, Machine Gun Cars enter the field. Combat becomes serious. Players launch organized raids on enemy logistics. Major battles erupt over key neighborhoods. Street gangs become significant — a well-allied gang can hold a flank. The player who controls the center has income advantage; the flanking player has mobility advantage.

**Tension level:** High. This is where matches are often decided.

### Phase 5: The War (Minutes 25-35)
Tier 4 is available for dominant economies. War Wagons, Capos, and ultimate upgrades enter play. Full-scale street wars with vehicles, suppressive fire, and coordinated attacks. Victory conditions become pursuable — a territorial player pushes for Monopoly, an economic player accumulates for Hostile Takeover, a political player builds toward Commission Vote. The losing player activates anti-snowball mechanics and looks for openings.

**Tension level:** Maximum. Cinematic climax.

### Phase 6: Endgame (Minutes 35+)
If no victory condition has triggered, the map is largely carved up. Desperate battles over the last contested zones. The game reaches a tipping point where one player either locks in a victory condition or breaks through for elimination. Extended games past 45 minutes indicate either very close skill levels or a design problem to investigate.

**Tension level:** Resolution. One way or another, it ends here.

---

## 5. City Map Structure and Territorial Control Model

### Map Architecture

The city is a single contiguous urban environment, approximately 200x200 tiles (exact size TBD through playtesting). It is divided into **16-20 neighborhoods**, each with a distinct visual identity and gameplay character.

**Neighborhood Archetypes:**

| Neighborhood Type | Quantity | Key Buildings | Strategic Value | Typical Gang? |
|-------------------|----------|--------------|-----------------|---------------|
| **The Waterfront** | 1-2 | Import Docks, Warehouses, Fish Market | Goods import point, logistics hub | Dockworkers Gang |
| **Downtown** | 1 | Grand Hotel, Casino, City Hall | Highest income, political influence | None (contested) |
| **Industrial District** | 1-2 | Factories, Rail Yard, Trucking Depot | Production + logistics | Union Thugs |
| **Entertainment Row** | 1-2 | Nightclubs, Speakeasies, Theater | High cash income | Jazz Cats (musicians' gang) |
| **The Heights** | 1-2 | Mansions, Private Clubs, Law Offices | Protection racket income, Influence | None (wealthy residents) |
| **The Bottoms** | 2-3 | Tenements, Pawn Shops, Corner Stores | Cheap territory, gang-heavy | Multiple small gangs |
| **Market District** | 1 | Open Market, Shops, Bank | Trade bonuses, economic hub | Street Vendors |
| **Rail District** | 1 | Train Station, Freight Yard | Secondary import point, fast transport | Hobos/Transients |
| **Residential** | 3-4 | Houses, Apartments, Churches | Buffer zones, moderate income | Neighborhood Watch |
| **Player Starts** | 2-4 | Compound (pre-built), nearby Safehouses | Home territory | None |

Each player starts in a corner/edge Compound with 2-3 nearby claimable buildings. The center is always contested, with Downtown as the prime objective. The map is **not symmetrical** in layout but is **balanced** in resource distribution — each player has equal access to the same total value of buildings, just in different spatial configurations.

### Map Generation

Maps use a **modular tile system**: neighborhoods are hand-crafted tiles that snap together in randomized configurations. This provides:
- **Variety:** Different neighborhood arrangements per match
- **Quality:** Each neighborhood is hand-designed for tactical interest
- **Balance:** The generator enforces distance-from-start parity and total resource balance
- **Learnability:** Players learn neighborhood types, not specific maps

### Dual-Layer Territory

**Layer 1: Street Presence (Tactical)**

Street Presence is established by having units stationed at **Street Corners** — designated points at intersections throughout the city. Each neighborhood has 4-8 Street Corners.

Controlling a Street Corner means having the only military units within its radius (roughly 1 city block). Street Corners provide:
- **Vision:** Fog of war is lifted in the corner's radius
- **Movement safety:** Your logistics units (trucks, runners) move at full speed through controlled corners; they slow down and become more visible in uncontrolled territory
- **Intimidation pressure:** Contributes to your Influence in the neighborhood
- **Early warning:** Alerts you when enemy units enter the area

Street Presence is **fluid** — it shifts as units move. It is the tactical layer of control, maintained by military commitment. Pull your troops out and you lose it instantly.

**Layer 2: Business Ownership (Strategic)**

Business Ownership is established by capturing **Anchor Properties** — specific buildings that generate income, produce goods, or provide strategic benefits. Each neighborhood has 2-5 Anchor Properties.

Capturing an Anchor Property requires:
1. Moving a squad to the building
2. Clearing any defenders (enemy units or neutral occupants)
3. Holding the building for a capture timer (15-30 seconds depending on building)
4. The building is now yours — it generates income and can be upgraded

Business Ownership is **durable** — it persists until the building is captured by an enemy or destroyed. You own a building even if you have no units nearby, but undefended buildings are vulnerable.

**The Interaction Between Layers:**

This is where strategic depth emerges:

| Scenario | Street Presence | Business Ownership | Outcome |
|----------|----------------|-------------------|---------|
| Full control | Yours | Yours | Maximum income, safe logistics, high Influence. Ideal. |
| Military occupation | Yours | Enemy's | You can see and pressure the area but gain no income. Good staging position for capture. |
| Remote business | Enemy's | Yours | You own the building but can't protect it easily. Income flows but at reduced rate (no Influence bonus). Building is vulnerable to raids. |
| Contested | Mixed | Mixed | Active combat zone. Income disrupted. Fog of war gaps. High tension. |
| No man's land | Neither | Neither | Neutral territory. AI gangs may control it. First to commit claims it. |
| Gang territory | Gang's | Gang's | Must deal with the gang first — through diplomacy, intimidation, or force. |

**Remote Business Rule:** A player can own a business in a neighborhood where they have no street presence. This represents bribing a distant business owner, planting a mole, or running a protection racket by reputation alone. However:
- Income is reduced by 40% (no Influence bonus, no fear multiplier)
- The building does not generate Influence for you
- Enemy units can capture it 50% faster (no local defense)
- The building does not provide vision

This creates a strategic choice: do you spread thin for maximum income coverage, or concentrate for maximum control quality?

---

## 6. Base Building, Anchor Properties, and Expansion

### The Compound

Each player starts with a **Compound** — their main base of operations. The Compound:
- Is pre-placed at a map edge/corner
- Produces all unit types (appropriate to current tier)
- Stores Goods (processing hub)
- Cannot be rebuilt if destroyed (losing it is devastating but not instant-loss)
- Has high HP and can be fortified with defensive upgrades
- Acts as the "Town Center" equivalent

### Anchor Properties

Anchor Properties are the buildings you capture and develop. They fall into five categories:

**Income Properties** — Generate Cash passively
- Corner Store, Speakeasy, Nightclub, Casino, Grand Hotel
- Higher-tier income properties generate more but cost more to capture and upgrade

**Production Properties** — Produce Goods
- Back-Alley Still, Distillery, Import Dock, Federal Warehouse
- Goods must be physically transported to your Compound or a Warehouse

**Military Properties** — Train units or enhance combat
- Boxing Gym (infantry training speed), Gun Range (accuracy upgrade), Garage (vehicle production), Safehouse (forward spawn point for Tier 1 units)

**Logistics Properties** — Support transport and supply
- Trucking Depot (cheaper/faster trucks), Warehouse (secondary goods storage/processing), Gas Station (vehicle staging/repair)

**Strategic Properties** — Provide non-economic advantages
- City Hall Contact (Influence generation), Newspaper Office (reveals enemy building locations), Police Station (reduces your Heat), Church (increases neighborhood loyalty — harder for enemy to convert local gang)

### Building Attachments

Each Anchor Property has **2-4 attachment slots** that can be filled with upgrades:

| Attachment | Effect | Cost | Tier Required |
|------------|--------|------|---------------|
| Sandbag Wall | +50% building HP, provides cover for nearby units | $100 | 1 |
| Lookout Post | +30% vision radius from building | $75 | 1 |
| Back Room | +25% income generation | $200 | 2 |
| Armory | Units produced here gain +10% DPS | $250 | 2 |
| Fortified Entrance | Building takes 50% longer to capture | $300 | 2 |
| Speakeasy Expansion | +50% income, +1 Influence/min | $400 | 3 |
| Underground Tunnel | Units can deploy from this building to any other tunneled building | $500 | 3 |
| Panic Room | Building survives at 1 HP once per match (auto-repairs slowly) | $350 | 3 |
| Wire Tap | Reveals all enemy units within 2 blocks of this building | $300 | 3 |

### Expansion Rules

1. **Capture range:** You can attempt to capture any unowned building anywhere on the map, but buildings far from your nearest owned property take 2x capture time.
2. **Building limits:** No hard cap on buildings, but each building requires ongoing "management overhead" — a flat $5/min maintenance cost. Overexpansion without income to match is punished.
3. **Upgrade progression:** Attachment slots unlock as you advance tiers. Tier 1 buildings get 1 slot, Tier 2 adds a second, Tier 3 adds a third, Tier 4 unlocks the fourth.
4. **Destruction vs. capture:** Attacking a building can either destroy it (faster, denies it to everyone) or capture it (slower, you gain it). The attacker chooses. Destroyed buildings rebuild as neutral after 120 seconds.
5. **Compound relocation:** At Tier 3, players can designate one owned building as a **Secondary Compound** for $1000. This provides a second production point and goods processing hub but does not replace the original Compound.

---

## 7. Economy Model

### Resource Overview

| Resource | Type | Generation | Spent On | Transport Required? |
|----------|------|-----------|----------|-------------------|
| **Cash ($)** | Primary | Passive from income properties, protection rackets | Units, buildings, upgrades, attachments, tier advancement, Hostile Takeover victory | No (abstracted) |
| **Goods** | Secondary | Produced at production properties | Tier advancement, vehicle production, elite units, building upgrades | **Yes — must be physically moved** |
| **Influence** | Tertiary | Passive from territory control, active from objectives | Gang recruitment, political actions, tier advancement, Commission Vote victory, Snitch ability | No (abstracted) |

### Cash Economy

Cash is the bread and butter. It flows in passively from owned income properties at rates determined by:
- **Base rate:** Intrinsic to the building type
- **Influence multiplier:** 0.7x (no influence in the neighborhood) to 1.5x (maximum influence)
- **Fear bonus:** Up to +30% in neighborhoods where you've recently won fights or destroyed enemy assets
- **Maintenance drain:** -$5/min per owned building

Cash is spent on everything — units, upgrades, attachments, tier advancement. It's the "wood and food" equivalent from AoE: always needed, never enough.

**Design intent:** Cash flow should be legible. A player should be able to estimate their opponent's income by observing their territory. "They own 6 buildings in high-influence zones — that's roughly $120/min."

### Goods Economy

Goods are the strategic resource. They are **physical objects** that exist on the map and must be transported. This is the mechanic that most differentiates The Commission from other RTS games.

**Goods Production Chain:**
1. A production property (Distillery, Import Dock, etc.) produces Goods at a fixed rate
2. Goods accumulate at the production property up to its storage limit
3. A truck or runner must physically pick up the Goods and transport them
4. Goods are delivered to the Compound or a Warehouse for processing
5. Processed Goods are added to the player's stockpile and can be spent

**Transport vulnerability:**
- Trucks carrying Goods are visible to enemies who have vision on the route
- Trucks can be ambushed — destroying a loaded truck destroys the Goods it carried
- Capturing an enemy truck (surrounding it with units) steals the Goods
- Escorts (military units guarding the truck) make transport safer but cost resources
- Route selection matters: the shortest path may go through enemy territory

**Anti-frustration measures:**
- Trucks can be given standing orders (auto-route between two buildings)
- Players can set "preferred routes" that trucks follow automatically
- Route warnings: the UI highlights if a truck's auto-route passes through enemy-controlled territory
- Goods production doesn't stop if transport is delayed — it just piles up at the source building (up to storage cap)
- **Goods Insurance:** When a truck is destroyed, 40% of its cargo drops on the ground as a recoverable pickup (persists 45 seconds). Either player can grab it. Caps worst-case loss at 60%.
- **Destruction Alert:** Audio ping + minimap flash when any transport unit is destroyed. Distinct from combat alerts.
- **Auto-Replacement:** When a truck is destroyed, the producing building auto-queues a replacement if the player has Cash. Toggleable.
- **Banking Buffer:** The Compound stores up to 150 Goods; Warehouses store 100 each. A well-managed player always has a buffer against supply disruption.

**Design intent:** Losing a truck should feel like losing a battle in AoE2 — a hit, a setback, a reason to adapt and fight back — **never** a reason to quit. If supply lines are completely cut but the player has Goods banked, they should still be okay. Sustained raiding over many minutes should delay tier advancement by 2-4 minutes (significant, worth doing) but never instantly end the game. The city always provides 2+ viable routes between any two points, and Runners can carry small loads through alleys as a slow fallback. Logistics raiding is a war of attrition, not an assassination.

### Influence Economy

Influence is the "political capital" resource. It represents your family's reputation, fear, and connections.

**Influence Generation:**
- **Passive:** +1 per controlled Street Corner per minute. A player with 15 controlled corners earns 15 Influence/min.
- **Buildings:** Strategic properties (City Hall Contact, Newspaper Office) generate bonus Influence.
- **Fights:** Winning a battle in a neighborhood gives a one-time Influence burst (+5-15 based on battle size).
- **Objectives:** Completing mini-objectives (see section on street gangs) gives Influence.

**Influence Spending:**
- **Tier advancement:** Each tier requires an Influence threshold
- **Gang recruitment:** Spending Influence to turn AI street gangs to your side
- **Political actions:** Reducing Heat, blocking enemy buildings from generating income temporarily, revealing enemy positions (Snitch)
- **Commission Vote victory:** Accumulating 500 Influence triggers the victory countdown

**Design intent:** Influence rewards active play and territorial control. A passive turtle player will fall behind in Influence. An aggressive player who fights and expands earns Influence naturally.

### Income Efficiency: Influence and Fear

Income from a building is not just its base rate. It's modified by your **Influence** in that neighborhood:

| Neighborhood Influence | Income Multiplier | Additional Effect |
|----------------------|-------------------|-------------------|
| 0 (no presence) | 0.7x | Building is flagged as "vulnerable" on your UI |
| 1-20 (minimal) | 0.85x | Basic awareness of local activity |
| 21-40 (establishing) | 1.0x | Nominal income. This is "break even" on the building. |
| 41-60 (respected) | 1.15x | Local gang becomes open to negotiation |
| 61-80 (dominant) | 1.3x | Enemy units move slower in this neighborhood (-15% speed) |
| 81-100 (total control) | 1.5x | Enemy units suffer -20% speed and -10% DPS (fear/demoralization) |

**Fear** is a temporary bonus earned by winning fights in a neighborhood. Destroying an enemy squad grants +5 Fear in that neighborhood for 120 seconds. Fear stacks up to +30% income bonus and decays over time. This rewards aggression but doesn't compound permanently.

---

## 8. Faction Model

### Mafia Families (Player Factions)

The Commission features **4 playable families** with **soft asymmetry** — identical core mechanics with unique bonuses, a unique Boss unit, and a unique Tier 4 ability. The asymmetry level is comparable to AoE2 civilizations: meaningful but not overwhelming.

| Family | Identity | Core Bonus | Unique Unit | Tier 4 Ability | Weakness |
|--------|----------|-----------|-------------|----------------|----------|
| **The Morellis** | Old-world traditionalists. Loyalty and honor. | +20% building HP, gangs are 30% harder for enemies to turn | *Famiglia Guard* — elite defensive infantry that gain +50% DPS when near a Morelli-owned building | *Omertà* — All enemy Snitch abilities are blocked for 180 sec; your buildings are hidden from enemy intel abilities | Slower expansion (10% longer capture times) |
| **The Ashfords** | Political operators. Old money, new power. | -25% Heat generation, +30% Influence from all sources | *The Fixer* — single unit that can "bribe" an enemy building to stop producing for 60 sec | *City Hall Coup* — Instantly gain 100 Influence and reduce all enemy Influence by 50 for 60 sec | -15% unit DPS across the board |
| **The Korvaks** | Ambitious upstarts. Speed and aggression. | +15% unit speed, -20% unit training time | *Blitz Squad* — 6-man tommy gun squad with Sprint ability on 15 sec cooldown | *Shock and Awe* — All your units gain +40% DPS for 30 sec, then suffer -20% DPS for 30 sec (cooldown: 300 sec) | +20% Heat generation |
| **The Solomons** | Financial masterminds. The bank always wins. | +25% Cash income from all sources, -15% building maintenance | *The Accountant* — single unit that "audits" an enemy building, stealing 30% of its income for 120 sec | *Hostile Leverage* — Hostile Takeover victory costs 3,500 instead of 5,000 (unique to Solomons) | -20% unit HP |

**Design rationale:** Soft asymmetry provides distinct strategic identities without creating hard-counter matchups. Every family can pursue every victory condition. The bonuses create *tendencies*, not *requirements*. A Solomon player is naturally inclined toward Hostile Takeover but can absolutely win through Elimination.

### AI Street Gangs

Street gangs are **semi-autonomous AI actors** that control neighborhoods and can be influenced by players. They are NOT player-controlled units. They are a dynamic system that creates unpredictability and rewards diplomacy.

**Each gang has:**
- **Territory:** 1-2 neighborhoods they patrol and defend
- **Personality:** Aggressive, Mercenary, Loyal, or Paranoid (affects their reactions to player actions)
- **Allegiance meter:** Per-player. Ranges from -100 (hostile) to +100 (allied). Starts at 0 (neutral).
- **Strength:** A fixed number of units that regenerate slowly. Ranges from "weak" (4-6 Thug-equivalents) to "strong" (10-12 Enforcer-equivalents).
- **Services:** Each gang offers something unique if allied: combat muscle, logistics protection, intelligence, or special unit access.

**Influencing Gangs:**

| Action | Allegiance Effect | Cost | Risk |
|--------|-------------------|------|------|
| Gift (Cash) | +10-20 | $200-500 | None. But opponent can outbid you. |
| Gift (Goods) | +15-25 | 50-100 Goods | None. Same. |
| Complete a Job | +20-30 | Time + units | Jobs are mini-objectives: clear out a rival gang, escort a VIP, deliver goods |
| Intimidation | +15 or -30 | Military presence (3+ squads in their territory) | Works on Mercenary/Paranoid gangs. Backfires on Aggressive/Loyal gangs (becomes hostile). |
| Spend Influence | +10-15 | 30-50 Influence | Reliable but expensive |
| Attack them | -50 to -100 | Combat losses | Gang becomes hostile. May ally with your opponent out of spite. |

**Allied Gang Benefits:**
- Their units will not attack you and will attack your enemies in their territory
- You get vision in their territory
- Their "service" activates (e.g., a dockworkers' gang provides +20% goods throughput at nearby docks)
- They contribute to your Influence in their neighborhood

**Balancing mechanic:** AI gangs resist the dominant player. If one player has significantly more territory/income, gangs become harder to recruit (+50% allegiance costs). This provides a natural underdog advantage.

### Neutral City Actors

Beyond street gangs, the city has **neutral systems** that affect gameplay:

- **Police:** Not a player or faction. Police are an environmental hazard triggered by the Heat system. They raid buildings, chase visible criminals, and temporarily disrupt operations. Police presence increases in neighborhoods with recent combat. **They affect everyone equally** and cannot be "allied" — only avoided or endured.

- **Civilians:** Abstracted as neighborhood population. Higher civilian density = higher income potential but also higher Heat generation from combat. Civilians don't appear as units — they're a system variable. A neighborhood's civilian density drops after major battles, reducing its income value temporarily. This models "people fleeing the violence" without depicting civilian harm.

- **City Services:** Fire trucks respond to arson (extinguishing building fires over time), construction crews repair damaged roads. These are cosmetic systems that provide flavor and help reset the map state. Players cannot interact with them.

---

## 9. Unit Classes, Vehicle Roles, Tactical Combat, and Escalation

### Combat Philosophy

Combat in The Commission follows **Company of Heroes principles** adapted for the crime setting:
- **Squads, not individuals:** Most infantry come in squads of 2-4 members. The squad is the atomic unit. Individual members can die, weakening the squad.
- **Cover matters:** Units behind walls, in doorways, behind cars, or in buildings take reduced damage. Moving in the open is dangerous.
- **Suppression:** Automatic weapons (Tommy guns, machine gun cars) can pin down enemy squads, reducing their movement speed and DPS. Suppressed units must retreat or be flanked.
- **Garrison:** Infantry can enter buildings, gaining cover and elevated firing positions. Garrisoned units are very strong defensively but vulnerable to Arsonists, Saboteurs, and building destruction.
- **Flanking:** Attacking from the side or rear negates the defender's cover bonus. Positioning matters more than raw numbers.
- **Retreat:** Units can be ordered to retreat to the nearest owned building at increased speed but reduced combat effectiveness. Retreating preserves the squad (and its veterancy) rather than fighting to the last man.
- **Veterancy:** Squads that survive combat gain experience and become stronger (up to 3 veterancy levels: +10%/+20%/+30% combat stats). This rewards careful unit preservation.

### Unit Roster Summary

**Tier 1 — Street Crew**
| Unit | Role | Key Trait |
|------|------|-----------|
| Runners | Scout, goods carrier | Fastest unit. No combat value. Sprint ability. |
| Street Thugs | Basic fighting | Cheap, disposable. Pistols and melee. |
| Lookouts | Recon, spotter | Long sight range. Can detect stealthed Saboteurs. |
| Arsonists | Anti-building | Molotovs. Set buildings on fire. Useless in field combat. |

**Tier 2 — The Outfit**
| Unit | Role | Key Trait |
|------|------|-----------|
| Enforcers | Core combat infantry | Shotguns. Devastating in close range and building fights. |
| Tommy Gunners | Suppression, area damage | High DPS but fragile. Suppress enemy squads. |
| Saboteurs | Anti-vehicle, demolition | Stealth approach. Plant charges on vehicles/buildings. |
| Wheelman | Vehicle crew | Boosts vehicle speed and durability when crewing a vehicle. |

**Tier 3 — The Syndicate**
| Unit | Role | Key Trait |
|------|------|-----------|
| Hitmen | Assassination, sniper | Very high single-target damage. "Mark for Death" ability. |
| Made Men | Elite heavy infantry | Tough. "Rally" aura buffs nearby allies. |
| Crooked Cops | Control, disruption | "Arrest" disables an enemy squad. Uniform confuses enemy targeting briefly. |
| Consigliere | Officer, support | Heals nearby squads' morale. Increases veterancy gain rate. |

**Tier 4 — The Empire**
| Unit | Role | Key Trait |
|------|------|-----------|
| The Don's Guard | Elite bodyguard | Highest infantry stats. "Last Stand" — fights harder at low HP. |
| Capo | Hero unit | Powerful combat + abilities. "Call in a Favor" spawns temporary Thug squad. Only one per player at a time. |

### Vehicle Roster

| Vehicle | Tier | Role | Key Trait |
|---------|------|------|-----------|
| Scout Car | 1 | Recon, fast response | Very fast. Light pistol armament. 2-seat transport. |
| Delivery Truck | 2 | Goods transport | No weapons. Durable. Carries 10 Goods. |
| Getaway Car | 2 | Infantry transport | Fast. Carries 1 squad. Light firepower. "Bootleg Turn" — instant 180. |
| Armored Truck | 2 | Protected transport | Mounted gun. Carries 5 Goods. Medium armor. |
| Machine Gun Car | 3 | Fire support | Suppression. Devastating vs exposed infantry. Weak vs Saboteurs. |
| Armored Sedan | 3 | Heavy assault | Tough. Good vs buildings. Slow. |
| War Wagon | 4 | Mobile fortress | Extremely durable. Multiple weapon mounts. Very slow. Can garrison 1 squad inside. |
| Dynamite Truck | 4 | Siege/desperation | Drives to target and detonates. Massive AoE damage. One-use. Can be shot and destroyed en route. |

### The Counter Web

Rather than a simple rock-paper-scissors, The Commission uses a **soft-counter web** where most units have favorable and unfavorable matchups but nothing is an automatic win.

**Core Counter Relationships:**
- **Infantry in cover** beats **infantry in the open** (cover advantage ~60/40)
- **Garrisoned infantry** beats **attacking infantry** (garrison advantage ~70/30)
- **Arsonists/Saboteurs** beat **garrisoned infantry** and **vehicles** (specialist counter)
- **Vehicles** beat **infantry in the open** (mobility + firepower)
- **Saboteurs** beat **vehicles** (stealth demolition charges)
- **Lookouts** beat **Saboteurs** (detection reveals stealth)
- **Tommy Gunners** beat **massed infantry** (suppression + AoE)
- **Enforcers** beat **garrisoned defenders** (close-range building assault)
- **Hitmen** beat **single high-value targets** (assassination burst)
- **Squads** beat **Hitmen** (Hitmen can't efficiently fight groups)

**Design note:** No unit should ever be a "useless" choice. Even Tier 1 Thugs remain relevant in late game for street corner control, goods running, and screening. The tier system adds *options*, not *obsolescence*.

### Escalation Structure

Combat intensity is gated by tier progression:

| Tier | Typical Engagement | Scale | Lethality |
|------|-------------------|-------|-----------|
| 1 | 2-4 Thug squads clashing over a building | Small skirmish | Low. Fights are sloppy and slow. |
| 2 | 6-10 mixed squads with vehicle support | Organized firefight | Medium. Tommy guns and shotguns kill fast. |
| 3 | 12-20 squads, vehicles, and specialists in multi-block battles | Full-scale street war | High. Hitmen assassinate, cars suppress, buildings burn. |
| 4 | Everything above plus War Wagons, Capos, and Dynamite Trucks | Epic showdown | Very high. Decisive battles that end games. |

---

## 10. Age/Tier Progression Model

### Tier System

The Commission uses a **4-tier progression** that gates unit access, building upgrades, and strategic options. Advancing a tier is a major economic commitment that temporarily weakens your military spending but opens new capabilities.

| Tier | Name | Fantasy | Advancement Cost | Research Time | Key Unlocks |
|------|------|---------|-----------------|---------------|-------------|
| 1 | **Street Crew** | Small-time hustlers | (Starting tier) | — | Runners, Thugs, Lookouts, Arsonists, Scout Car. Basic income buildings. 1 attachment slot per building. |
| 2 | **The Outfit** | Organized operation | ~$400 + 100 Goods + 30 Influence | 60 sec | Enforcers, Tommy Gunners, Saboteurs, Wheelman. Delivery Truck, Getaway Car, Armored Truck. Mid-tier income buildings. 2 attachment slots. Goods transport routes. |
| 3 | **The Syndicate** | Major criminal enterprise | ~$1,200 + 350 Goods + 100 Influence | 90 sec | Hitmen, Made Men, Crooked Cops, Consigliere. Machine Gun Car, Armored Sedan. High-tier buildings. 3 attachment slots. Secondary Compound. Victory conditions become pursuable. |
| 4 | **The Empire** | Untouchable dynasty | ~$3,000 + 800 Goods + 250 Influence | 120 sec | Don's Guard, Capo. War Wagon, Dynamite Truck. Ultimate buildings. 4 attachment slots. Family-specific Tier 4 ability. |

### Tier Advancement Strategy

Advancing a tier is a **meaningful choice**, not an automatic milestone. The costs are designed so that:

- **Tier 1→2** is a standard transition that happens in every game by ~minute 10. Delaying past minute 12 means you'll face Enforcers with Thugs — bad.
- **Tier 2→3** is the most important strategic decision. It costs enough that you're militarily vulnerable during the research period. A well-timed attack during an opponent's Tier 3 research can be devastating.
- **Tier 3→4** is a luxury. Many games end before anyone reaches Tier 4. Reaching it is a statement of dominance — but the opponent has time to win through other means while you invest.

### Tier Advantage Curve

A key design parameter: **how much stronger is a Tier N+1 player than a Tier N player?**

| Matchup | Advantage | Notes |
|---------|-----------|-------|
| Tier 2 vs Tier 1 | ~1.5:1 | Tier 2 units are individually stronger, but a Tier 1 player with more units can fight. Window of ~2 minutes where mass can overcome quality. |
| Tier 3 vs Tier 2 | ~1.8:1 | Significant advantage. Hitmen and Machine Gun Cars are qualitatively different. A Tier 2 player needs strong positioning and numbers to compete. |
| Tier 4 vs Tier 3 | ~1.4:1 | Smaller jump. Tier 4 is about special capabilities (Capo, War Wagon, Dynamite Truck, faction ability) rather than raw stat increase. |

**Design note:** The Tier 2 vs Tier 1 gap is intentionally smaller to prevent "rush to Tier 2 or die" metas. The Tier 3 vs Tier 2 gap is the largest because this is where the game's strategic fork happens — committing to Tier 3 should be a rewarded gamble.

---

## 11. Victory Conditions and Competitive Implications

### Four Victory Paths

| Victory | Requirement | Tier Req | Typical Timing | Counterplay |
|---------|------------|----------|----------------|-------------|
| **Elimination** | Destroy all enemy Compounds + Safehouses | None | 30-40 min | Defend your buildings; maintain a Safehouse far from your Compound |
| **Monopoly** | Control 70%+ of Turf Points for 5 uninterrupted minutes | 2+ | 28-35 min | Contest any single Turf Point to reset the timer; guerrilla raids |
| **Commission Vote** | Accumulate 500 Influence, then survive a 3-minute countdown | 3+ | 30-38 min | Kill enemy units to deny Influence gain; spend Influence to delay (Snitch drains their stockpile) |
| **Hostile Takeover** | Spend $5,000 Cash in a single lump sum at your Compound | 3+ | 35-42 min | Raid their income properties; destroy trucks to choke their Cash flow |

### Victory Condition Design Philosophy

1. **Elimination** is the default — it's always available and can't be "turned off." It rewards military dominance.
2. **Monopoly** rewards territorial control and map presence. It's the most visible victory path — the opponent can see you capping Turf Points and has time to respond.
3. **Commission Vote** rewards consistent Influence generation through territory, fighting, and gang diplomacy. The 3-minute countdown provides counterplay time.
4. **Hostile Takeover** rewards economic play and is the least visible — the opponent may not realize how close you are to $5,000 until the countdown starts.

**Competitive mode note:** For tournament play, all four victory conditions should remain active. They create strategic diversity and prevent single-strategy dominance. If playtest data shows one path is too easy or too reliable, adjust its numbers (e.g., increase Monopoly threshold to 75%, or Commission Vote to 600 Influence) rather than removing it.

---

## 12. Anti-Snowball Systems and Comeback Design

### Design Philosophy

Snowballing is the #1 risk to competitive viability. If every game is decided by minute 10, the remaining 30 minutes feel pointless. The Commission uses **layered anti-snowball systems** that activate progressively as the gap widens, without making it impossible to close out a won game.

### Anti-Snowball Suite

| System | Trigger | Effect | Exploitability |
|--------|---------|--------|----------------|
| **Heat** | Leading player (composite score) | Unit costs +5% to +25%; random police raids on buildings | Low — you can't avoid generating Heat by winning |
| **Diminishing Returns** | >50% territory control | Each point beyond 50% gives less income per point | Low — natural economic physics |
| **Rat Economy** | <3 owned buildings | Flat $20/min passive income; Saboteurs cost -30% | Medium — intentional building sacrifice? (See audit) |
| **Desperate Measures** | Drop below 25% territory (once per match) | All units +30% DPS, +20% speed for 120 sec | Low — one-time trigger, can't be re-exploited |
| **Snitch** | Lower Influence than opponent | Spend 50 Influence to reveal all enemy units for 20 sec (180 sec CD) | Low — information alone doesn't win games |
| **Black Market** | <30% territory | Units cost 20% less but have 10% less HP | Medium — are cheap units always bad? (Probably fine) |
| **Safehouse Persistence** | Always active | Very tough building that produces Tier 1 units. Hard to find, hard to destroy. Prevents instant elimination. | Low — it only produces Tier 1 units |

### Cumulative Effect Analysis

At maximum disadvantage (a player with <25% territory, <3 buildings, lower Influence), they receive:
- Rat Economy ($20/min passive)
- Desperate Measures (+30% DPS for 120 sec, once)
- Black Market (20% cheaper units)
- Snitch access (information advantage)

Meanwhile, their dominant opponent faces:
- +20-25% unit costs from Heat
- Police raids disrupting buildings
- Diminishing returns on excess territory
- AI gangs resisting their recruitment

This is a **meaningful but not decisive** swing. The trailing player has tools to fight back, but they still need to play well. A 70/30 game might become 60/40 — the leader still has advantage, but the trailer has hope.

### The Zombie Problem

The biggest risk: games that are effectively over but can't end because the losing player hides in a Safehouse with Rat Economy, endlessly producing Tier 1 units that can't actually win but can delay forever.

**Solution:** After a player loses their Compound, a **Surrender Timer** starts (5 minutes). If they don't recapture or build a Secondary Compound within 5 minutes, they lose via "The family is broken — you are eliminated." The Safehouse keeps them in the game long enough for a dramatic comeback attempt, but not long enough to troll.

---

## 13. Art Direction, UI/UX Readability, and Atmosphere

### Visual Identity

**Period:** Late 1920s to early 1930s. Art deco architecture, prohibition-era fashion, early automobiles, jazz-age signage.

**Palette:** Muted earth tones (browns, grays, deep reds) with accent neon from speakeasy signs, car headlights, and fire. Night scenes lit by streetlamps and building windows. Rain is common. Fog rolls in from the waterfront.

**Camera:** Isometric or slight-angle top-down (similar to AoE2/CoH). The camera must be pulled back far enough to read tactical situations across 2-3 city blocks while still showing unit detail.

**Architectural style:** Each neighborhood has a distinct look — brownstones in The Bottoms, art deco towers Downtown, brick warehouses in the Industrial District, mansions in The Heights. This serves readability: players should be able to identify a neighborhood type at a glance.

### Atmosphere

**Audio:** Jazz, blues, and big band music as ambient score. Dynamic mixing: music intensifies during combat, becomes mournful after losses, swells during tier advances. Sound design emphasizes gunshots (punchy, not realistic), car engines, shattering glass, and rain.

**Weather:** Cosmetic weather system. Rain, fog, overcast, clear. Rain slightly reduces vision range (thematic, minor tactical impact). Night maps (stretch goal) with reduced base vision but lit streets.

**Cinematics:** Short (3-5 second) cinematic camera cuts for key moments: tier advancement, Boss unit deployment, Dynamite Truck detonation, victory condition activation. These can be toggled off for competitive play.

### UI/UX Readability

**Core readability requirements** (PvP-critical):

| Element | Readability Solution |
|---------|---------------------|
| **Faction ownership** | Color-coded building outlines and unit highlights. Your buildings glow your color. |
| **Territory control** | Minimap shows Influence heatmap per player. Toggle between "street presence" and "business ownership" views. |
| **Logistics routes** | Optional overlay shows truck routes as dotted lines. Friendly = green, enemy = red (if visible). |
| **Unit types** | Silhouette-distinct designs. Each unit type has a unique posture and weapon that's identifiable at max zoom-out. |
| **Building types** | Building category icons displayed above each building (dollar sign for income, gear for production, fist for military, etc.) |
| **Combat state** | Suppressed units have a visible "pinned" indicator. Veterancy shown as chevrons. Health bars above squads. |
| **Victory progress** | Persistent HUD element showing progress toward each active victory condition for all players. |
| **Tier status** | Player tier shown in scoreboard. Audio/visual announcement when any player advances a tier ("The Morellis have formed a Syndicate"). |
| **Goods in transit** | Trucks carrying Goods have a visible cargo indicator (stacked crates on the truck bed). |

**Competitive UI mode:** Strips visual noise, maximizes information density. Health bars always on, unit icons always shown, cinematic cameras disabled.

---

## 14. Prototype Vertical Slice Plan

### Goal

Build a playable 1v1 prototype that validates the **three core pillars**: territory capture, logistics vulnerability, and urban tactical combat. If these three systems feel good in isolation and in combination, the game has legs.

### Vertical Slice Scope

**Map:** One hand-crafted neighborhood (~40x40 tiles, roughly 4 city blocks). Two player start positions. 6 capturable buildings. 1 AI street gang (3 Thug squads). 3-4 Street Corners.

**Factions:** Mirror match only. No faction asymmetry. One generic "Family."

**Units:**
- Runner (scout/goods carrier)
- Thugs (basic combat)
- Enforcers (upgraded combat)
- Arsonist (anti-building)
- Delivery Truck (goods transport)

**Buildings:**
- Compound (start building, unit production)
- Speakeasy (income)
- Back-Alley Still (goods production)
- Warehouse (goods storage)
- Boxing Gym (faster infantry training)
- Corner Store (income)

**Systems:**
- Building capture with timer
- Street Corner control (vision + influence)
- Cash income from owned buildings with basic Influence multiplier
- Goods production and physical truck transport
- Truck ambush/capture mechanic
- Tier 1→2 progression only
- Cover system (basic: in cover / out of cover)
- Building garrison
- Squad retreat
- One AI street gang with gift/intimidation allegiance
- Elimination victory only

**NOT in vertical slice:**
- Tier 3-4
- Vehicles other than Delivery Truck
- Faction asymmetry
- Multiple victory conditions
- Anti-snowball systems
- Weather, cinematics, music
- Map generation (one fixed map)
- 2v2 or FFA

### Milestone Plan

| Phase | Duration | Deliverable |
|-------|----------|-------------|
| **Pre-production** | 4 weeks | Core technical architecture. Isometric tile renderer. Basic pathfinding on urban grid. Unit movement and selection. |
| **Core Loop** | 6 weeks | Building capture. Cash income. Unit production. Basic combat (damage, HP, death). Truck movement. |
| **Tactical Layer** | 4 weeks | Cover system. Garrison. Suppression (basic). Flanking bonus. Squad retreat. |
| **Economy Loop** | 4 weeks | Goods production chain. Truck transport with auto-routing. Goods delivery and stockpiling. Tier advancement (1→2). |
| **Territory System** | 3 weeks | Street Corner control. Influence calculation. Income multipliers. Minimap heatmap. |
| **AI Gang** | 3 weeks | Basic gang AI (patrol, defend, allegiance system). Gift and intimidation interactions. |
| **Polish & Playtest** | 4 weeks | Balance tuning. UI/UX iteration. 20+ internal 1v1 playtests. Bug fixing. |
| **TOTAL** | ~28 weeks | Playable vertical slice for internal evaluation and investor/publisher demo |

### Key Validation Questions for Prototype

1. **Does truck ambushing feel rewarding for the attacker and not infuriating for the defender?** (If logistics raiding is too frustrating, the game dies.)
2. **Does urban cover combat feel tactical or fiddly?** (If microing cover positions is tedious, simplify.)
3. **Does territory feel valuable?** (If street presence doesn't matter, the dual-layer system fails.)
4. **Is the pacing right?** (If the first 5 minutes are boring, the game won't retain players.)
5. **Can a losing player see a path back?** (Even without anti-snowball systems, does the core design create comeback opportunities through raiding and ambush?)

---

## 15. Highest-Priority Open Questions

These are the design questions that cannot be fully answered on paper and require playtesting or further research:

| # | Question | Why It Matters | Proposed Test |
|---|----------|----------------|---------------|
| 1 | **How many Street Corners per neighborhood?** | Too few = territory feels binary. Too many = micro-intensive whack-a-mole. | Test with 3, 5, and 8 corners per neighborhood. Measure player attention overhead. |
| 2 | **Truck ambush feel.** | The entire logistics system depends on this being fun to execute AND recover from. If losing a truck feels like losing a villager in AoE (annoying but manageable), good. If it feels like losing a game of StarCraft (devastating and unrecoverable), bad. | Playtest with different Goods values per truck and recovery times. |
| 3 | **Optimal number of AI street gangs.** | Too few = they don't matter. Too many = the map feels crowded with NPC drama. | Test with 2, 4, and 6 gangs on a full map. |
| 4 | **Cover system granularity.** | Binary (in cover / not) is simple but shallow. CoH-style (light cover / heavy cover / negative cover) is deeper but harder to read in a zoomed-out city. | Prototype both. Let playtesters judge. |
| 5 | **1v1 vs 2v2 balance.** | 2v2 changes everything: shared economy? Separate economies? Shared victory conditions? | Start with separate-everything 2v2 and iterate. |
| 6 | **Victory condition tuning.** | Are all four paths viable, or does one dominate? The numbers (70% Monopoly, 500 Influence, $5000 Hostile Takeover) are placeholder. | Extensive competitive playtesting. Track win rates by victory condition. |
| 7 | **Heat system intensity.** | Too harsh = winning feels punished. Too gentle = snowballing happens anyway. | Parameterize Heat and test at multiple intensity levels. |
| 8 | **Map generation quality.** | Modular neighborhood tiles are promising but unproven. Can the generator consistently produce balanced, interesting maps? | Build the generator and produce 50 maps. Evaluate by hand. |
| 9 | **Match length in practice.** | 40 minutes is the target but hard to guarantee. What if games consistently run 55 minutes? What if they end at 20? | Track match lengths across 100+ playtests. Adjust income rates and tier costs to converge on target. |
| 10 | **Faction asymmetry depth.** | How different should families feel? AoE2 level (slight) or StarCraft level (dramatic)? Starting with slight is safer; the question is whether to deepen it post-launch. | Ship with slight asymmetry. Monitor community feedback. |

---

## Appendix A: Design Assumptions Log

These are assumptions made during this document's creation that should be validated:

| Assumption | Confidence | Rationale |
|-----------|------------|-----------|
| 4 tiers is the right number | High | Matches AoE2's 4-age system. 3 feels too few (not enough escalation), 5 too many (too long to reach endgame). |
| 4 playable families | Medium | Enough for variety without balance nightmare. Could ship with 3 and add the 4th post-launch. |
| 3 resources (Cash/Goods/Influence) is not too many | Medium | AoE2 has 4 (food/wood/gold/stone). Three feels manageable if UI is clear. |
| Physical goods transport is fun | Low-Medium | This is the game's biggest innovation AND biggest risk. Must be validated in prototype. |
| AI street gangs add to PvP rather than distract from it | Medium | They could become "PvE tax" that competitive players resent. Needs careful tuning. |
| Mirror matchups are fine for launch | High | Soft asymmetry means mirror matches play differently based on map/decisions. Full asymmetry can deepen over time. |
| The city setting provides enough tactical variety | High | Urban environments offer more terrain diversity per square meter than open-field RTS maps. |
| Single city map (with procedural neighborhood arrangement) is enough | Medium | Could feel repetitive after 50+ games. Post-launch neighborhood DLC / community maps may be needed. |

---

## Appendix B: Competitive Integrity Checklist

| Requirement | Status | Notes |
|------------|--------|-------|
| No pay-to-win | **Mandatory** | All gameplay content available to all players. Monetize through cosmetics (building skins, vehicle skins, family crests). |
| Deterministic combat | **Recommended** | Minimize RNG in combat resolution. Damage should be predictable, not dice-rolled. Small accuracy variance is OK for feel, but outcomes should be skill-determined. |
| Spectator mode | **Required for esports** | Full map vision, player economy overlay, army value tracker, supply line visualization. |
| Replay system | **Required** | Full game replays with scrubbing and speed control. |
| Ranked matchmaking | **Required** | ELO-based 1v1 and 2v2 ladders. Seasonal resets. |
| Anti-cheat | **Required** | Map hacks are especially devastating in a game with fog of war and logistics routes. |
| Balance patch cadence | **Recommended** | Monthly balance passes for first 6 months. Bi-monthly after stabilization. |
| Observer UI | **Required for esports** | Show both players' income, army value, territory %, and victory condition progress. |

---

*Document version: 1.0*
*Design lead: Claude (Game Design Exercise)*
*Status: First draft — awaiting playtest validation*
*Companion documents: economy-balance-tables.md, unit-vehicle-stats.md, match-pacing-timeline.md, victory-conditions.md, anti-snowball-audit.md*
