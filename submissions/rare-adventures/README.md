# Rare Adventures

A choose-your-adventure game that gives Rare Friends a progression loop through equipment, dangerous expeditions, party battles, and a simulated $RAREFRIENDS economy.

**[Play the demo](https://bludmoneyy.github.io/rare-adventures/)** · **[Source code](https://github.com/bludmoneyy/rare-adventures)** · **[Rare Friends Vibeathon](https://github.com/spokesz/rarefriends-vibeathon)**

| Submission detail | Rare Adventures |
| --- | --- |
| Builder / contact | [@bludmoneyy on GitHub](https://github.com/bludmoneyy) |
| Proposed category | **Economy Potential** |
| Approach | Standalone web game; **does not use FriendSDK** |
| Stack | React 18, TypeScript 5.7, Vite 6, CSS and SVG assets; GitHub Pages hosting |
| Wallet / network requirements | Optional EIP-6963/EIP-1193 browser wallet connection on Robinhood Chain (4663). No wallet, NFT ownership, signature, or funded account is required to play the simulated demo. |
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

Wallet update checks (September 30, 2026):

- TypeScript checking and the production build for `/rare-adventures/` passed.
- Ten wallet tests passed: connection, rejection/retry, account/network changes, network addition, declined switching, cancellation, stale balance responses, malformed responses/disconnect, timeout, and provider discovery.
- Automated Chrome checks with an injected test provider passed for missing-wallet guidance, connection, wrong-network display, switching, live balance rendering, account changes, disconnect, keyboard focus restoration, and mobile layout at 375 × 812. No browser runtime errors or signing/transaction requests were observed.
- These wallet checks use a mock provider. A real extension/hardware-wallet acceptance pass and a full gameplay/browser suite remain outstanding.

Checks previously recorded during deployment preparation:

- TypeScript checking and Vite production builds passed for both `/` and `/rare-adventures/` hosting paths.
- A local asset audit found all **44 referenced public SVG assets**, including dynamically selected potion art. The missing lance reference was corrected, with compatibility for old saved paths.
- Scripted checks passed for asset URL mapping, generated entry links, the web manifest, and service-worker cache isolation and offline fallback behavior.

The wallet flow has automated browser coverage; desktop/mobile gameplay, full keyboard accessibility, and every secondary game mode still need a complete reviewer pass. There is no FriendSDK validation result because this project does not use the SDK.

Known limits and future work:

- Optional wallet access reads the selected address, network, and live native ETH balance. No signatures, approvals, or transactions are requested. Verified NFT selection and original per-token artwork are not implemented.
- Saves, guild chat, opponents, raid wallets, market activity, and balances are local. There is no shared backend, authenticated multiplayer, escrow, or authoritative settlement.
- Local saves and outcomes can be edited; `Math.random()` is not secure randomness. Production would need trusted settlement and prevention of duplicated trades/rewards.
- The initial reward pool is a demo subsidy. Economy tuning and raid-wide payout accounting need playtesting before any real RF integration.
- Browser storage must be available for persistence. Clearing site data removes progress; active expeditions are not restored on reload. Offline support covers cached resources after an online visit.

## Credits

- **Rare Friends:** character/collection concepts and Generations scenery. The extraction script at [`scripts/extract-generation-one-lands.mjs`](https://github.com/bludmoneyy/rare-adventures/blob/main/scripts/extract-generation-one-lands.mjs) reads Generations metadata from Robinhood mainnet and extracts/adapts scenery into `src/assets/lands/`. This is an optional asset-generation tool; the playable demo uses committed SVGs and does not call that RPC.
- **Font Awesome / Fonticons:** the `fa-*.svg` navigation icons retain their attribution and CC BY 4.0 notices. See [Font Awesome Free licensing](https://fontawesome.com/license/free).
- **Google Fonts and their designers:** Archivo, Silkscreen, and Sometype Mono, loaded through Google Fonts.
- Item illustrations and the fallback walking sprite are bundled under `public/`; additional UI SVGs are in `src/assets/svgs/`. These credits do not assert ownership of Rare Friends artwork or grant additional rights to third-party assets.

## Wallet connection

Select **Connect wallet** in the header and choose an installed wallet. The app discovers multiple injected wallets through [EIP-6963](https://eips.ethereum.org/EIPS/eip-6963), with a legacy `window.ethereum` fallback, and handles [EIP-1193](https://eips.ethereum.org/EIPS/eip-1193) account, network, and disconnect events. On mobile, open the demo inside your wallet's browser; external WalletConnect/QR sessions are not implemented.

The wallet panel shows the full account address, network, a read-only native ETH balance on Robinhood Chain, and an explorer link. If needed, select **Switch to Robinhood Chain** and approve the network prompt in your wallet. The app requests network addition only when the wallet reports an unknown chain, then verifies the selected chain. [Official network settings](https://docs.robinhood.com/chain/add-network-to-wallet/): chain ID **4663** (`0x1237`), RPC `https://rpc.mainnet.chain.robinhood.com`, native currency **ETH**, explorer `https://robinhoodchain.blockscout.com`.

Account changes immediately clear the previous account/balance; stale asynchronous responses cannot restore them. Declined requests, unsupported methods, timeouts, unavailable accounts, and network failures have recoverable states. **Refresh account** rereads the wallet; **Disconnect** ends the app's connection and removes listeners. Revoking the site's wallet permissions is a separate action inside the wallet. Connections are not persisted or automatically requested after reload.

**Production boundary:** this is a real wallet connection and read-only balance integration, not authenticated login or real-token gameplay. The game retains one browser-local demo save, independent of any connected account. Switching wallets does not assign the demo roster or balances to that wallet. The app never requests a signature, token approval, or transaction. NFT ownership/metadata loading, signed server sessions, authoritative game state, contract settlement, and production economy validation remain future work. Keep all RF purchases/rewards simulated for the Vibeathon.

### Verify the wallet flow

Use Node.js 22.18+:

```bash
npm run test:wallet
npx tsc -p tsconfig.app.json --noEmit
npm run build -- --base=/rare-adventures/
```

For browser checks, start `npm run dev` and a dedicated Chrome instance using `--headless=new --user-data-dir=/tmp/rare-wallet-check --remote-debugging-port=9231 about:blank`, then run `npm run test:wallet:browser`. The test uses a mock wallet in an isolated page, never a real funded wallet. `APP_URL` and `CHROME_DEBUG_URL` override the default local addresses. Screenshots are written to `/tmp/rare-wallet-mobile.png` and `/tmp/rare-wallet-desktop.png`.

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

Wallet integration source revision: [`d1a61ab`](https://github.com/bludmoneyy/rare-adventures/commit/d1a61abf8eb0c2d137810f1c533773d9b01ae8e6).
