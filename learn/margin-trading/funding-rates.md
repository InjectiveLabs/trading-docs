# Funding Rates

While margin trading unlocks the door to amplified gains, it also introduces another layer of complexity - funding requirements. Often overshadowed by margin requirements, understanding funding rates is crucial for responsible leveraged trading on Helix.

**What are Funding Rates?**

In traditional futures contracts, the price on the exchange converges with the spot price over time. In contrast, perpetual futures on Injective never expire, creating a potential disconnect between the contract price and the underlying asset's spot price. To keep these prices in sync, a mechanism called funding payments kicks in.

Funding rates are essentially periodic fees exchanged between long and short positions. The direction of these payments depends on the prevailing market sentiment:

* **Positive Funding Rates:** If a significant majority of traders are long, short positions pay funding fees to long positions. This incentivizes trading activity that could potentially bring the contract price down towards the spot price.
* **Negative Funding Rates:** Conversely, if most traders are short, long positions receive funding fees from short positions. This encourages trading activity that could potentially push the contract price up towards the spot price.

The specific calculation of funding rates is a formula that considers the difference between the contract price and the index price (a reference point representing the spot price), along with an interest rate component. While these rates may seem small at first glance, they can accumulate over time and significantly impact your trading experience.

For **long position holders**, positive funding rates represent an additional cost. You'll be paying funding fees to short positions on each funding interval. Conversely, negative funding rates translate to receiving payments, essentially earning passive income on your open position.

For **short position holders**, the funding dynamic flips. Positive funding rates become a source of income, while negative funding rates translate to periodic payments you owe to long positions. Therefore, it's crucial to factor potential funding costs into your margin calculations and risk management strategies.
