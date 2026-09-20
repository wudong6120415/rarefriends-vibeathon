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
A coffee shop staffed by your Rare Friend NFT. Your Friend is the barista; the Friend's token ID determines a deterministic skill level (1-100) that adds a 0-20% bonus to every tip. Five customers per shift, five drink types (Espresso, Latte, Cappuccino, Mocha, Daily Special), five satisfaction tiers (Furious / Disappointed / Satisfied / Happy / Delighted) rolled by the SDK's chance game. Brew drinks, earn simulated RF tips, run the whole shift end-to-end.

**How does it use Rare Friends?**
You play as your own Generations NFT, chosen via the SDK's standard picker (preserved original sprite, drawn from the canonical Generations character set, never altered). The token ID drives the barista skill badge shown on the HUD; the same skill number is the multiplier applied to every tip. Preview rolls use the SDK's `outcomeForRoll + samplePreviewRoll` (browser entropy, no chain). Live mode would settle tips via the SDK Dice contract.

**Source code**
[GitHub repository](https://github.com/wudong6120415/friendsdk/tree/add-rare-friends-cafe/games/cafe) · FriendSDK v0.1.2 · [Game README](https://github.com/wudong6120415/friendsdk/blob/add-rare-friends-cafe/games/cafe/README.md)

**Playable demo / how to run**
**Playable preview:**
- **Offline demo (anyone, no wallet):** https://rocky-motivation-sussex-influence.trycloudflare.com/cafe/demo.html -- standalone HTML that runs the full cafe loop with a sample Friend (token ID 7730, skill 85). No browser extension, no NFT, no chain.
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
Open the preview, connect your Robinhood Wallet, choose your Friend. Tap **Open shop** to start the shift. A customer appears and orders one of five drinks; tap **Brew {drink} ({N} beans)** to serve. The SDK's chance game rolls a satisfaction tier (Furious 5% / Disappointed 15% / Satisfied 40% / Happy 30% / Delighted 10%), the Friend's skill bonus is applied, and tips accumulate. After 5 customers the shift summary shows your total tips and offers **Start new shift**. Sound, mute and reduced-motion are wired through the SDK's `createFriendSoundKit` and `prefers-reduced-motion` media query.

**Costs and rewards**
Everything is simulated. You start with 20 beans; each drink costs 1-5 beans (matches its position on the menu). Base tips per drink:

| Drink | Beans | Base Tip |
|---|---|---|
| Espresso | 1 | 0.20 RF |
| Latte | 2 | 0.50 RF |
| Cappuccino | 3 | 0.80 RF |
| Mocha | 4 | 1.50 RF |
| Daily Special | 5 | 2.50 RF |

Tier multipliers: Furious 0%, Disappointed 20%, Satisfied 50%, Happy 100%, Delighted 200%. Friend skill adds +0% to +20% on top. Expected reward per cup is roughly 0.91 RF plus skill bonus. Full design notes in [the game's README](https://github.com/wudong6120415/friendsdk/blob/add-rare-friends-cafe/games/cafe/README.md).

**What have you tested?**
TypeScript typecheck passes (`npx tsc --noEmit` on `games/cafe/`); `node scripts/dev-game.mjs build games/cafe` succeeds; preview built and deployed at the URLs above. The game flow uses the SDK's documented lifecycle (`buy -> play -> settle -> redeem` in preview mode), tested end-to-end by me with the SDK's mocked preview wallet and a sample Friend.

**Known limitations**
- Drink and cafe artwork is AI-generated (MiniMax image-01) and may benefit from manual refinement.
- One customer at a time by design (no multi-customer queueing yet).
- Bean economy is fixed; no upgrade system in this MVP.
- Preview mode only -- no live RF settlements. Production deployment requires an explicit chain deployment.
- **Even in preview mode the SDK enforces the on-chain ownership gate**, so the live preview URL requires a real wallet + NFT + chain 4663. The offline demo (`demo.html`) does not.
- Cloudflare quick-tunnel URL has no uptime guarantee; stable host on request.

**Credits**
Built on FriendSDK v0.1.2 by spokesz (Apache-2.0) -- runtime, chance game, wallet integration, sound kit, Generations sprite manifest. Drink and cafe artwork generated with MiniMax image-01. Game design, code, README and demo HTML authored with assistance from MiniMax-M3.