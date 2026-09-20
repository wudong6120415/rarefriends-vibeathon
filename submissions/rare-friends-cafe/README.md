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
A **crash-style gambling game with progressive jackpot** inside a cafe theme. Players bet simulated RF on a rocket that rises with an increasing multiplier, cashing out before it crashes. Every bet contributes 5% to a **progressive jackpot pool** (currently visible in the UI as a live counter, 1.2M+ RF and rising). Reaching a 100x multiplier on Crash **unlocks the Slots machine**, where 5 matching symbols wins the entire jackpot pool. 4 matching pays 500x, 3 matching pays 50x.

**Why this is a Token Activity entry:**
- Burns RF on every bet (5% goes to the jackpot pool, removed from circulation).
- Encourages high volume of small bets (entries start at 100 RF, common bets 1000 RF).
- Jackpot pool grows continuously across the player base -- more bettors, faster pool growth.
- The 100x Crash-to-Slots unlock is the burning mechanism: players spend RF on Crash to unlock the high-multiplier Slots mode.
- Friend skill from the selected Generations NFT boosts the cash-out multiplier (skill 1-100 -> +0% to +20% bonus payout).

**How does it use Rare Friends?**
You play as your own Generations NFT, chosen via the SDK's standard picker. The token ID drives the Friend skill badge and the cash-out bonus applied to every Crash win. Long-term Friend buffs (collection bonus, 7-day streak bonus) carry over from the previous design iteration.

**Player psychology hooks (drawn from crash gambling literature):**
1. **Dopamine spike during climb:** the rising multiplier creates continuous tension; the brain releases anticipation dopamine before the crash resolves.
2. **"Cash out now or push further?"** decision tension -- players who cash out at 1.5x feel they "won", players who wait feel they "could have won more".
3. **Variable rewards:** the crash point is sampled from an exponential distribution with house edge, producing 1.01x-1000x outcomes. Variable rewards are the most compelling psychology for habit formation.
4. **Progressive jackpot:** a constantly-rising number visible to all players; players contribute on every bet; jackpot hit resets to 100,000 RF base.
5. **Social proof:** a live feed shows simulated other-player wins, losses, and jackpot hits every 3 seconds. "Someone just won X" hooks the next player.
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
1. Click **SPIN** (1000 RF) -- the 5-reel machine animates and stops.
2. **5 matching symbols:** win the entire jackpot pool.
3. **4 matching:** 500x your bet.
4. **3 matching:** 50x your bet.
5. Otherwise: lose the bet; 5% adds to the jackpot.

**Costs and rewards**
All simulated. House edge: 3%. Crash distribution: `P(crash < m) = (1-house_edge) * (1 - 1/m)` truncated at 1000x. Slot wins: jackpot / 500x / 50x / 0x. 5% of every bet to jackpot pool. Expected return: ~97% on Crash over a large sample; Slots expected return depends on symbol frequencies and pool size at hit time.

**What have you tested?**
TypeScript typecheck passes; `npm run dev:game` builds. The Crash + Slots loop verified end-to-end in the offline demo: bet placement, multiplier animation, cash-out, crash, slot spin, jackpot reset. Simulated social-feed updates run every 3 seconds.

**Known limitations**
- Drink/cafe artwork is AI-generated (MiniMax image-01).
- Preview mode only -- no live RF settlements.
- Even in preview mode the SDK enforces the on-chain ownership gate for the live preview URL.
- The social-feed is mock; production would use real player activity.
- Cloudflare quick-tunnel URL has no uptime guarantee.

**Credits**
Built on FriendSDK v0.1.2 by spokesz (Apache-2.0). Crash-mechanics inspired by Stake Originals / Aviator / JetX. Slot-mechanics inspired by classic 3-reel slot machines with progressive jackpots (IGT Megabucks, etc.). Cafe theme is original. Game design, code, README and demo HTML authored with assistance from MiniMax-M3.