# Keeper

The AlloyKeeper contract is a permissionless distribution engine.
Anyone can call it; the first caller per interval pays gas but earns no extra reward.

## How it works

1. Swaps in the Uniswap V3 pool accumulate a 1% fee.
2. The keeper calls `collectFees(coin)` on the launchpad.
3. Those fees are swapped into the backing stock token via spot buy.
4. The keeper calls `distribute(amount)` on the coin, advancing the global dividend index.
5. Holders call `claimDividends()` proportional to their balance and index delta.

## Running your own keeper

```bash
cp .env.example .env
npx hardhat run scripts/keeper.ts --network robinhood
```

The script polls every `KEEPER_INTERVAL` seconds (default 3600).
