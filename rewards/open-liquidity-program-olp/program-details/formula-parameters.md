---
description: Values for OLP Formula Parameters
---

# Formula Parameters

|   Parameter   |                                                                   Definition                                                                  |                             Value (Subject to Change)                            |
| :-----------: | :-------------------------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------: |
|     $$a$$     |                                   [Liquidity Score](scoring-formula-methodology.md#liquidity-score) exponent                                  |                                        0.4                                       |
|     $$b$$     |                                      [Uptime Score](scoring-formula-methodology.md#uptime-score) exponent                                     |                                         3                                        |
|     $$c$$     |                                            [Volume](scoring-formula-methodology.md#volume) exponent                                           |                                        0.8                                       |
|  $$MinDepth$$ | Minimum [notional order size](#user-content-fn-1)[^1] needed to generate points for [Total Score](scoring-formula-methodology.md#total-score) |                                       $1000                                      |
| $$MaxSpread$$ |  Maximum allowable spread against mid-price[^2] in an order to generate points for [Total Score](scoring-formula-methodology.md#total-score)  | 100 bps[^3] for BTC and ETH perp markets, 200 bps for all other eligible markets |



[^1]: Total underlying amount (position size) on which a derivatives trade is based, or the order size for spot markets

[^2]: Average between best bid price and best ask price in the order book

[^3]: basis points (1 basis point = 1% of 1%, or 0.0001)
