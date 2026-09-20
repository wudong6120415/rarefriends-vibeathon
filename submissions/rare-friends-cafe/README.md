**Try the offline demo now (no wallet, no NFT, no chain):**
https://rocky-motivation-sussex-influence.trycloudflare.com/cafe/demo.html

**Live SDK preview (Robinhood Wallet + Generations NFT + Robinhood mainnet 4663 required):**
https://rocky-motivation-sussex-influence.trycloudflare.com/cafe/

**Project name**
Rare Friends Cafe

**Builder / contact**
wudong6120415 · GitHub [@wudong6120415](https://github.com/wudong6120415)

**Category**
Character Spotlight

**What did you build?**
A daily-coffee-shop **tycoon**. The player pays 1 RF per shift (simulated), serves 5 customers, banks tips, and spends them on 7 permanent cafe upgrades. Each upgrade unlocks new content: Espresso Machine boosts Espresso tips, Live Music boosts all tips, VIP Booth unlocks VIP customers (4 beans, 3 RF base tip, only take the Daily Special), Renovate boosts streak chance. Customers you serve at Happy or Delighted become collectibles (24 unique faces across 4 rarities: common/rare/epic/legendary). Complete the full set to permanently boost your Friend's skill. Hit a 7-day shift streak to unlock a +10% Friend skill bonus. Daily play loops into a weekly streak, monthly collection, and a public leaderboard of top cafes.

**How does it use Rare Friends?**
You play as your own Generations NFT, chosen via the SDK's standard picker (preserved original sprite, drawn from the canonical Generations character set, never altered). The token ID drives the barista skill badge and the +0% to +20% tip multiplier applied to every cup. Long-term Friend buffs (collection bonus, 7-day streak bonus) make the Friend itself more valuable through gameplay. Preview rolls use the SDK's `outcomeForRoll + samplePreviewRoll` (browser entropy, no chain). Live mode would settle tips via the SDK Dice contract.

**Why players will keep playing (reward loops):**
1. **Daily entry** (-1 RF simulated) creates commitment and stakes.
2. **5 upgrades** unlock content progressively (each gives a tangible gameplay advantage).
3. **24 collectibles** give a long-term goal (10+ shifts minimum).
4. **8 badges** give short-term achievements (first brew, 3-day streak, etc.).
5. **7-day streak bonus** is a permanent Friend buff; once you have it, you don't want to break the streak.
6. **VIP customers** are only available post-upgrade, gating the most profitable plays.
7. **Leaderboard** creates competitive pressure without PvP.

**Source code**
[GitHub repository](https://github.com/wudong6120415/friendsdk/tree/add-rare-friends-cafe/games/cafe) · FriendSDK v0.1.2 · [Game README](https://github.com/wudong6120415/friendsdk/blob/add-rare-friends-cafe/games/cafe/README.md)

**Playable demo / how to run**
**Playable preview:**
- **Offline demo (anyone, no wallet):** https://rocky-motivation-sussex-influence.trycloudflare.com/cafe/demo.html -- standalone HTML that runs the full daily-tycoon loop (entry fee, 5-customer shifts, upgrade tree, collection, badges, leaderboard) with a sample Friend (token ID 7730, skill 85). No browser extension, no NFT, no chain.
- **Live SDK preview (Robinhood Wallet + Generations NFT + chain 4663):** https://rocky-motivation-sussex-influence.trycloudflare.com/cafe/ -- the SDK v0.1.2 preview build. Even in preview mode the SDK enforces the on-chain ownership gate; if your wallet has no Generations NFT on Robinhood mainnet, the picker shows "No playable Friends found."

Both URLs are served over HTTPS via Cloudflare Tunnel from a public preview build, no uptime guarantee. I can re-host on GitHub Pages for a stable URL if the review team prefers.

To run yourself, with Node.js 22+ installed:

```sh
git clone https://github.com/wudong6120415/friendsdk.git
cd friendsdk
git checkout add-rare-friends-cafe
npm ci
npm run dev:game -- games/cafe
```

Open the printed URL. You'll need a browser wallet holding a hardwired Generations NFT (generation 1 or higher) on Robinhood mainnet. No RF funding or transaction signature is needed for the preview.

**How do you play?**
**Daily loop:**
1. Open the preview, connect your Robinhood Wallet, choose your Friend.
2. Tap **Open Cafe (-1 RF)**. Five customers will arrive over the next 30 seconds.
3. Each customer orders a drink; tap any drink you can afford (button disabled if you can't) before the 10-second timer hits zero.
4. Serve the right drink -> rolled tier applies directly. Wrong drink -> tier downgraded by one step.
5. Banked tips are added to your total. Spend them in the **Cafe** tab to buy upgrades.
6. After 5 customers, you see your shift grade (S-F based on tip ratio), your streak count, and your collection progress.
7. Come back tomorrow for the next shift. The streak counter only advances on consecutive days.

**Upgrades (cost in tips, permanent):**
| Upgrade | Cost | Effect |
|---|---|---|
| Espresso Machine | 5 RF | +20% tip on Espresso |
| Pastry Menu | 12 RF | +15% tip on Latte + Cappuccino |
| Free WiFi | 18 RF | +3s customer patience timer |
| Live Music | 25 RF | +10% tip on all drinks |
| VIP Booth | 40 RF | Unlocks VIP customers (20% spawn, 4 beans, 3 RF base) |
| In-house Roastery | 50 RF | +25% tip on Daily Special |
| Renovate | 100 RF | Streak chance x1.5 |

**Collection:** 24 unique customer faces across common / rare / epic / legendary. Served at Happy or Delighted tiers get added to your collection. Complete all 24 for a permanent Friend skill bonus (off-chain in this preview).

**Badges (8 total):** First Brew, 3-Day Streak, 7-Day Streak, Collector I (10), Master Collector (24), Cafe Tycoon (100 RF banked), VIP Service (5 VIPs served), 5-Star Service (3 S-grade shifts).

**Costs and rewards**
Everything is simulated. Daily entry: 1 RF. Drinks:

| Drink | Beans | Base Tip |
|---|---|---|
| Espresso | 1 | 0.20 RF |
| Latte | 2 | 0.50 RF |
| Cappuccino | 3 | 0.80 RF |
| Mocha | 4 | 1.50 RF |
| Daily Special | 5 | 2.50 RF |

Tier multipliers (correct drink): Furious 0%, Disappointed 20%, Satisfied 50%, Happy 100%, Delighted 200%. Wrong drink downgrades tier by one step. Friend skill adds +0% to +20% on top. Upgrade bonuses stack. 10-second patience timer per customer; walk-out = Furious no tip.

**What have you tested?**
TypeScript typecheck passes; `node scripts/dev-game.mjs build games/cafe` succeeds; preview built and deployed at the URLs above. The offline demo's daily-tycoon loop (entry fee, 5-customer shift, upgrades, collection, badges, leaderboard) was verified end-to-end. The v3 reward loops (5 upgrades, 24 collectibles, 8 badges, 7-day streak, leaderboard) are all reachable from the demo.

**Known limitations**
- Drink and cafe artwork is AI-generated (MiniMax image-01) and may benefit from manual refinement.
- Preview mode only -- no live RF settlements. Production deployment requires an explicit chain deployment.
- **Even in preview mode the SDK enforces the on-chain ownership gate**, so the live preview URL requires a real wallet + NFT + chain 4663. The offline demo (`demo.html`) does not.
- Leaderboard in demo is mock-NPCs (not real players); production would persist scores server-side.
- Cloudflare quick-tunnel URL has no uptime guarantee; stable host on request.

**Credits**
Built on FriendSDK v0.1.2 by spokesz (Apache-2.0) -- runtime, chance game, wallet integration, sound kit, Generations sprite manifest. Drink and cafe artwork generated with MiniMax image-01. Game design, code, README and demo HTML authored with assistance from MiniMax-M3.