# Rare Adventures

A choose-your-adventure game that gives Rare Friends a progression loop through equipment, dangerous expeditions, party battles, and a simulated $RAREFRIENDS economy.

**[Play the demo](https://bludmoneyy.github.io/rare-adventures/)** · **[Source code](https://github.com/bludmoneyy/rare-adventures)** · **[Rare Friends Vibeathon](https://github.com/spokesz/rarefriends-vibeathon)**

| Submission detail | Rare Adventures |
| --- | --- |
| Builder / contact | [@bludmoneyy on GitHub](https://github.com/bludmoneyy) |
| Proposed category | **Economy Potential** |
| Approach | Standalone web game; **does not use FriendSDK** |
| Stack | React 18, TypeScript 5.7, Vite 6, CSS and SVG assets; GitHub Pages hosting |
| Wallet / network requirements | None for the playable demo. No NFT ownership check, wallet connection, transaction signature, or funded account is required. |
| Economy status | All RF balances, purchases, sinks, wagers, rewards, and marketplace trades are simulated locally. |

## What did we build?

Choose a demo Friend, buy equipment and potions, and attempt one of eight adventure tiers. Each room asks you to trade simulated RF for safer progress or take a free, riskier action. Clear the expedition to receive a reward from the visible pool; die and lose that Friend's carried inventory. Purchases and entry fees replenish the pool and record a separate RF sink.

The wider prototype adds party battles with replayable combat, raids with simulated teammates, elemental loot, a marketplace, and weekly guild competition. These systems explore how preparation, item loss, rewards, and social goals could create reasons to spend and reuse $RAREFRIENDS across repeated sessions.

**Why Economy Potential:** the central experiment is a traceable economy with costs, rewards, consumables, item attrition, and pool accounting. The demo records simulated spending and burning; it does not claim real token activity or a proven sustainable return. The [economy operator guide](https://github.com/bludmoneyy/rare-adventures#economy-operator-guide) includes parameters, break-even estimates, and production work still needed.

## How it connects to Rare Friends

Friends are the persistent characters carrying equipment, run history, and RF metrics. The demo uses preset Generations and Genesis identities, Rare Friends-themed visuals, and eight land scenes derived from Generations scenery. Party battles give a land-matching pet a 10% damage/healing bonus; Genesis pets receive that bonus on every land.

The current roster and land assignments are demo data. The default sprite is a bundled fallback, not a wallet-selected NFT's verified original artwork. Verified ownership, token metadata, individual character artwork, and real settlement remain future integrations. The custom interface uses responsive pages for inventories, economy information, and multiple game modes rather than the FriendSDK runtime.

## Try the core interaction

1. Open the [public demo](https://bludmoneyy.github.io/rare-adventures/). A fresh save starts with **250 simulated RF** and a reward pool of **18,420 simulated RF**.
2. Open **Friends** and select a character. Use **Shops** to buy equipment or a potion for that Friend; the item cards show costs, power, and durability.
3. Open **Adventures**, select the first tier, and enter for **12 RF**. It contains five rooms and advertises an **18–32 RF** clear reward, limited by the available pool.
4. Choose paid or free actions in each room. Fight enemies until their HP reaches zero, and use carried potions during the run as needed. Paid choices improve survival but do not guarantee a clear.
5. Finish the adventure or encounter death, then inspect the Friend's inventory, history, and RF metrics. Open **Docs** for the economy explanation and **Metrics** for the content overview.
6. Explore **Battles**, **Raids**, **Marketplace**, **Guild**, and **Guild Wars** for the connected systems. Other participants, listings, and standings are local simulations, not live multiplayer.

**Controls:** click or tap buttons and cards; use Tab to focus controls and Enter/Space to activate buttons. On small screens, use the menu button to open navigation. Characters roam automatically; there are no WASD movement controls. Battle playback supports pause, next action, show result, and replay, with reduced-motion handling.

Progress is saved in this browser's `localStorage`. To start over, use **RESET DEMO** in the navigation drawer, preferably after leaving an active run. Reloading does not preserve an in-progress expedition.

## Costs, chances, and consumables

- Adventure entry ranges from **12 to 155 RF** across eight tiers; the complete room counts and reward ranges are in [current tier economics](https://github.com/bludmoneyy/rare-adventures#current-tier-economics).
- A room has a **42% enemy chance**. Trap, loot, and story rooms each account for approximately **19.33%**. Paid choices cost 6 RF per focused combat strike, 5 RF for traps, 8 RF for loot rooms, and 7 RF for story rooms. Free choices cost 0 RF before any optional preparation.
- Surviving a free choice in a loot room gives a **35% item-drop chance**; a Fortune charge guarantees that eligible drop. Combat and damage also depend on tier, equipment, potion effects, and random rolls, so there is no single fixed adventure win probability.
- Entry, ordinary shop purchases, and paid adventure actions contribute `ceil(payment × 0.5)` to the reward pool; the remainder is recorded as a simulated sink. Optional guild tithes add a separate charge. Raids, marketplace fees, and wagers have their own rules below.
- Potions are single-use items with nine effects and three strength tiers. Effects include healing, attack, armor, defense, evasion, loot fortune, revival, repair, and maximum HP. Run buffs last for that expedition; charges are consumed by their relevant events.
- Equipment has limited durability. Gear carried into a successful adventure loses one use; depleted gear is removed. Fatal death clears the Friend's carried inventory. Abandoning does not refund entry.
- Rewards are simulated, capped by available funds, and have no cash or token redemption. Client-side randomness and storage are suitable for this demo only.

## Checks and known limitations

Submission-day checks (September 30, 2026): TypeScript checking and a Vite production build with `/rare-adventures/` as the base path passed. The public demo returned HTTP 200, and its JS/CSS filenames match the fresh production build. GitHub Pages reports the site as built. A fresh interactive browser playthrough was not performed in this submission session.

Checks previously recorded during deployment preparation:

- TypeScript checking and Vite production builds passed for both `/` and `/rare-adventures/` hosting paths.
- A local asset audit found all **44 referenced public SVG assets**, including dynamically selected potion art. The missing lance reference was corrected, with compatibility for old saved paths.
- Scripted checks passed for asset URL mapping, generated entry links, the web manifest, and service-worker cache isolation and offline fallback behavior.

These were local build and scripted checks, not a full automated browser or gameplay suite. Desktop/mobile gameplay, keyboard accessibility, and every secondary game mode still need a complete reviewer pass. There is no FriendSDK validation result because this project does not use the SDK.

Known limits and future work:

- No wallet access or live funds are involved. Verified NFT selection and original per-token artwork are not implemented.
- Saves, guild chat, opponents, raid wallets, market activity, and balances are local. There is no shared backend, authenticated multiplayer, escrow, or authoritative settlement.
- Local saves and outcomes can be edited; `Math.random()` is not secure randomness. Production would need trusted settlement and prevention of duplicated trades/rewards.
- The initial reward pool is a demo subsidy. Economy tuning and raid-wide payout accounting need playtesting before any real RF integration.
- Browser storage must be available for persistence. Clearing site data removes progress; active expeditions are not restored on reload. Offline support covers cached resources after an online visit.

## Credits

- **Rare Friends:** character/collection concepts and Generations scenery. The extraction script at [`scripts/extract-generation-one-lands.mjs`](https://github.com/bludmoneyy/rare-adventures/blob/main/scripts/extract-generation-one-lands.mjs) reads Generations metadata from Robinhood mainnet and extracts/adapts scenery into `src/assets/lands/`. This is an optional asset-generation tool; the playable demo uses committed SVGs and does not call that RPC.
- **Font Awesome / Fonticons:** the `fa-*.svg` navigation icons retain their attribution and CC BY 4.0 notices. See [Font Awesome Free licensing](https://fontawesome.com/license/free).
- **Google Fonts and their designers:** Archivo, Silkscreen, and Sometype Mono, loaded through Google Fonts.
- Item illustrations and the fallback walking sprite are bundled under `public/`; additional UI SVGs are in `src/assets/svgs/`. These credits do not assert ownership of Rare Friends artwork or grant additional rights to third-party assets.

## Run locally

Use Node.js 22 (the version used by the deployment workflow) and npm. No API keys or environment variables are required.

```bash
git clone https://github.com/bludmoneyy/rare-adventures.git
cd rare-adventures
npm ci
npm run dev
```

Use `npm run build` and `npm run preview` to test the production build. Demo state is stored in `localStorage` under `rare-adventures-save-v1`.


## Full economy documentation

See the [economy operator guide](https://github.com/bludmoneyy/rare-adventures#economy-operator-guide) for tier economics, party battles, raids, elemental gear, marketplace fees, guild wars, and production integration work.

Source revision checked for submission: [`efd6029`](https://github.com/bludmoneyy/rare-adventures/commit/efd60298b0b6152f75fc133568b37121b4e043f4).
