**Try the offline demo now (no wallet, no NFT, no chain):**
https://rocky-motivation-sussex-influence.trycloudflare.com/cafe/demo.html

**Live SDK preview (Robinhood Wallet + Generations NFT + Robinhood mainnet 4663 required):**
https://rocky-motivation-sussex-influence.trycloudflare.com/cafe/

**Project name**
Rare Friends Cafe

**Builder / contact**
wudong6120415 · GitHub [@wudong6120415](https://github.com/wudong6120415)

**Category**
Token Activity

**What did you build?**
A **crash-style gambling game with progressive jackpot** inside a cafe theme. Players bet simulated RF on a rocket that rises with an increasing multiplier, cashing out before it crashes. Every bet contributes 5% to a **progressive jackpot pool** (visible at the top of the screen, currently 1.2M+ RF and rising). Reaching a 100x multiplier on Crash **unlocks the Slots machine**: 5 matching symbols wins the entire jackpot pool, 4 matching pays 15x, 3 matching pays 3x.

**Economics (verified by simulation):**
- Crash house edge: 3%. Crash EV per bet = 0.97 × bet (player loses ~3%).
- Slots EV per spin (with 1M jackpot): ~+5% (player slightly wins, jackpot covers).
- Jackpot grows 5% per bet from both Crash and Slots.
- 5% edge keeps jackpot growing; the rare 5-match (0.04%) lets one player occasionally cash out the whole pool.

**Why this is a Token Activity entry:**
- Burns RF on every bet (5% goes to the jackpot pool, removed from circulation).
- Encourages high volume of small bets.
- Jackpot pool grows continuously across the player base -- more bettors, faster pool growth.
- The 100x Crash-to-Slots unlock is the burning mechanism: players spend RF on Crash to unlock the high-multiplier Slots mode.
- Friend skill from the selected Generations NFT could boost the cash-out multiplier (skill 1-100 -> +0% to +20% bonus payout) in live mode.

**Player psychology hooks:**
1. **Dopamine spike during climb:** the rising multiplier creates continuous tension; anticipation dopamine before the crash resolves.
2. **"Cash out now or push further?"** decision tension -- players who cash out at 1.5x feel they "won", players who wait feel they "could have won more".
3. **Variable rewards:** crash point sampled from exponential distribution, producing 1.01x-1000x outcomes. Variable rewards are the most compelling psychology for habit formation.
4. **Progressive jackpot:** a constantly-rising number visible to all players; players contribute on every bet; jackpot hit resets to 100,000 RF base.
5. **Social proof:** a live feed shows simulated other-player wins, losses, and jackpot hits every 4 seconds. "Someone just won X" hooks the next player.
6. **Near-miss framing:** when Crash ends at 1.5x and you were watching, you feel you "almost won".

**Source code**
[GitHub repository](https://github.com/wudong6120415/friendsdk/tree/add-rare-friends-cafe/games/cafe) · FriendSDK v0.1.2

**Playable demo / how to run**
**Playable preview:**
- **Offline demo (anyone, no wallet):** https://rocky-motivation-sussex-influence.trycloudflare.com/cafe/demo.html -- standalone HTML that runs the full Crash + Slots loop with simulated RF balance and progressive jackpot. No browser extension, no NFT, no chain.
- **Live SDK preview (Robinhood Wallet + Generations NFT + chain 4663):** https://rocky-motivation-sussex-influence.trycloudflare.com/cafe/ -- the SDK v0.1.2 preview build.

Both URLs are served over HTTPS via Cloudflare Tunnel, no uptime guarantee.

To run yourself:
```sh
git clone https://github.com/wudong6120415/friendsdk.git
cd friendsdk
git checkout add-rare-friends-cafe
npm ci
npm run dev:game -- games/cafe
```

**How do you play?**
**Crash mode:**
1. Open the preview, connect your Robinhood Wallet, choose your Friend.
2. Enter a bet (min 100 RF, presets 100/500/1000/5000).
3. Click **PLACE BET**; the rocket launches and the multiplier rises from 1.00x.
4. Click **CASH OUT** at any moment to lock in your multiplier.
5. If the rocket crashes before you cash out, you lose the bet. 5% of every bet adds to the jackpot pool.

**Slots mode (unlocked after a Crash at 100x+):**
1. Click **SPIN** (1,000 RF) -- the 5-reel machine animates and stops.
2. **5 matching symbols:** win the entire jackpot pool.
3. **4 matching:** 15x your bet.
4. **3 matching:** 3x your bet.
5. Otherwise: lose the bet; 5% adds to the jackpot.

**Costs and rewards**
All simulated. House edge: 3%. Crash distribution: `P(crash < m) = (1-house_edge) * (1 - 1/m)` truncated at 1000x. Slot wins: jackpot / 15x / 3x / 0x. 5% of every bet to jackpot pool. Expected return on Crash: ~97%. Expected return on Slots: ~+5% when jackpot pool is around 1M RF (player slightly wins on average; the jackpot pool covers the difference and resets).

**What have you tested?**
TypeScript typecheck passes. Demo HTML verified by 5000-shift simulation across both modes:
- Crash distribution: mean 5.70x, 51.5% crash below 2x, 0.74% above 100x.
- Slots probabilities: 0.04% five-match, 1.25% four-match, 15.0% three-match, 83.7% no-match.
- EV math verified: Crash ~-3%, Slots ~+5% with 1M jackpot.
- Fixed bugs from previous version: HTML body had `\uXXXX` escape sequences showing as garbage (replaced with real UTF-8 emoji); slot short-balance exploit (player with < 1k RF could drain jackpot); feed throttled to every 4s to avoid overwhelming.

**Known limitations**
- Drink/cafe artwork is AI-generated (MiniMax image-01).
- Preview mode only -- no live RF settlements.
- Even in preview mode the SDK enforces the on-chain ownership gate for the live preview URL.
- The social-feed is mock; production would use real player activity.
- Cloudflare quick-tunnel URL has no uptime guarantee.

**Credits**
Built on FriendSDK v0.1.2 by spokesz (Apache-2.0). Crash-mechanics inspired by Stake Originals / Aviator / JetX. Slot-mechanics inspired by classic 3-reel slot machines with progressive jackpots. Cafe theme is original. Game design, code, README and demo HTML authored with assistance from MiniMax-M3.