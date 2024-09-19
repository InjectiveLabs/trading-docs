# Election Perpetual Futures

An election perpetual futures contract - or an election perp - is a type of derivative financial instrument on Injective that allows users to gain leveraged exposure to an elections market. An election perp is a perpetual futures contract that tracks the price of a market on Polymarket, rather than a traditional crypto asset.

Unlike traditional futures, these contracts don't have an expiry date. They can be held indefinitely. Trades are settled in USDT. LIke other perps, election perps use a funding rate mechanism to keep the contract price close to the underlying index price.

### How do Election Perpetual Futures Work?

* The contract tracks a market on Polymarket (e.g., 2024 Presidential election).
* Traders can go long (buy) or short (sell) the election perp, with up to 3x leverage.
* Periodic funding payments occur between long and short holders to align the contract price with the index.

Expiry futures require mark prices to track liquidation and settlement prices. Because mark prices are typically based on the spot prices of the underlying assets, regular oracle price feeds cannot be used for Election Perpetual Futures as the index price typically does not exist in popular oracle feeds. However, an mark price is still needed prior to this time to inform liquidation prices. To solve this, Election Perpetual Futures will use a proprietary oracle feed as the mark price.

### Mark Price Mechanism

The mark price for election perps on Injective is based on a proprietary oracle feed provided by Stork. In the example of the 2024ELECTION PERP, Stork queries the midpoint of [the market on Polymarket](election-perpetual-futures.md#how-do-election-perpetual-futures-work). They then apply a six-hour time weighted average price (TWAP) to prevent drastic swings in the mark price. That price is then scaled down to a more human readable format (i.e. a price between $0 and $1), and used as the mark price.

### Market Settlement

Election Perpetual Futures are not expiry instruments, however the trading pairs have roughly specific lifespans. When the underlying market on Polymarket reaches settlement (i.e. the token price settles to $0 or $1), trading activity on an election perp will likely trend towards zero. At that point, an interested party may submit a governance proposal to settle the market. If and when such a proposal passes, the market would be settled and any users with outstanding positions would be force liquidated at the mark price of the oracle, which will have settled at $0 or $1 accordingly.

In regard to 2024ELECTION PERP specifically, the trading pair was listed with TRUMPWIN as the underlying asset. Rather than listing two or more assets (i.e. one for both the Democratic party's and Republican party's Presidential candidates, or potentially more parties) and fragmenting liquidity, a decision was made to list one asset. For this asset, the mark price will settle to $1 if the market on Polymarket settles to "yes" for Donald J. Trump, and $0 if the market on Polymarket settles to "no" for Donald J. Trump (i.e. if Kamala Harris or another candidate wins the Presidential election).
