## gear_gacha_simulation
# Monte Carlo simulation for obtention of gear through a gacha mechanism

This code runs a simulation for a game's "gacha" (loot box) and item-merging system.

Its main purpose is to model player progression over time. It simulates a large number of players for a set number of days to see how their equipment and "power level" improve.

Here is a breakdown of what it does:

# 1. Configuration
The code starts with a configuration section where you can set the parameters of the simulation:

NUM_USERS: How many players to simulate (e.g., 10,000).

TOTAL_DAYS: How long the simulation runs for each player (e.g., 200 days).

DAILY_RARE_CHESTS / DAILY_EPIC_CHESTS: How many "loot boxes" each player gets per day.

..._PROBS: The percentage chance to get items of different rarities (Common, Rare, Epic) from each chest.

MAX_LEVEL_PER_RARITY: A lookup table to define the "power" or "level" a piece of gear provides based on its rarity.

# 2. Core Classes (Game Logic)
The simulation is built around three main classes that manage the game's rules:

Gacha: This class handles "pulling" items from chests. When called, it uses the defined probabilities to randomly return an item (e.g., "Warrior-Helmet") and its rarity (e.g., "Common 1").

Inventory: This class tracks all the items a single player owns. It keeps a count of every item at every rarity (e.g., 5 "Common 1" Warrior-Helmets, 2 "Rare 1" Rogue-Chests).

Merger: This class contains the logic for upgrading gear. After a player gets new items, this class automatically runs and "merges" them. It includes:

Simple Merges: Combining 3 identical items to make 1 of the next rarity (e.g., 3 "Common 1" -> 1 "Rare 1").

Complex "Fodder" Merges: Using other items of the same type as "fuel" to upgrade a base item (e.g., 1 "Epic 1" Helmet + 1 other "Epic 1" Helmet -> 1 "Epic 2" Helmet).

# 3. Simulation Loop (Main Function)
The main() function executes the simulation:

Loop per User: It loops from 0 to NUM_USERS.

Loop per Day: For each user, it loops from 1 to TOTAL_DAYS.

Daily Actions: On each day, the user:

Opens their daily gacha chests and adds the new items to their Inventory.

Runs the Merger to upgrade all possible items.

Calculates their "Total Theoretical Level". This is done by checking their inventory for the single best item they have for each of the 6 slots (Helmet, Chest, etc.) and adding up the levels for those 6 items.

# 4. Store Results: It saves this daily snapshot (day, best rarity for each slot, total level) for the user.

# 5. Create some avg. progressions to look at convergence from the simulation
