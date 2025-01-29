---
description: OLP Reward Allocations (Epoch 43 Onwards)
hidden: true
---

# Reward Allocations

## Market Reward Allocations

Rewards are allocated to [eligible markets](eligible-markets.md) in three different methods :

1. Static allocations
2. Minimum allocation with a dynamic component
3. Flexible reward allocations

### Static Market Reward Allocations (Preallocations)

12.5% of INJ rewards will be preallocated to each of the BTC/USDT PERP market, ETH/USDT PERP market, and INJ/USDT PERP market. The remaining INJ for the epoch will be allocated to each remaining eligible market with a minimum allocation of 100 INJ:&#x20;

| Market                 | Total Allocation                     |
| ---------------------- | ------------------------------------ |
| BTC/USDT Perp          | 12.5%                                |
| ETH/USDT Perp          | 12.5%                                |
| INJ/USDT Perp          | 12.5%                                |
| Other Eligible Markets | Formula based allocation (see below) |

{% hint style="info" %}
Static allocations may change over time as more markets are added to the eligible list
{% endhint %}

### Dynamic Market Reward Allocations

As of epoch 43, the remaining rewards are allocated to eligible markets (excluding BTC/ETH/INJ Perps) based on the following schematic.

First, each epoch starts fresh, such that every pair has an equal chance of earning the maximum total available reward for that epoch, regardless of trading volume and liquidity from the prior epoch. Each pair starts day 1 of the epoch with a range of possibility, from a minimum of 100 INJ for the epoch to a possible maximum of 1200 INJ. Prior to this change, minimum rewards were 400 INJ, maximum rewards were around 900 INJ, and there was insufficient variation in reward accrual between pairs with low volume and pairs with substantially more volume. With this change, liquidity providers are rewarded for volume in popular markets.

To determine which pair gets the lowest reward for the epoch, which pair gets the maximum reward for the epoch - and everything in-between - each market is assigned a Market Score as follows :&#x20;

$$
MarketScore_i = 0.8 * Volume_i ^{0.8}  + 0.2 * Liquidity_i^{0.2}
$$

where volume and liquidity are both calculated as a moving average of trading volume / orderbook liquidity for a given trading pair since the onset of the epoch.

Market Scores are then ranked, and _x_ values are found using :&#x20;

$$
x = (rank - n) / (1 - n)
$$

where _n_ is the total number of eligible pairs (i.e. total OLP pairs, less pre-allocated pairs like BTC/ETH/INJ perps), such that the lowest performing pair of the epoch has an _x_ value of 0.

Using these variables for each market, rewards per market are found using the formula :&#x20;

$$
R(x)=-180x^3+1270x^2+10x+100
$$

As an example, let's say there are 40 pairs in OLP (less pre-allocated pairs). What is the reward for the 20th best performing pair of the epoch ?

$$
x = (40 - 20) / 39  = 0.513
$$

$$
R(0.513) = -180(0.513)³ + 1270(0.513)² + 10(0.513) + 100 = -24 + 334 + 5.13 + 100 = 415~INJ
$$

What about the 35th (out of 40) ?

$$
x = (40 - 35) / 39 = 0.128
$$

$$
R(0.128) = -180(0.128)³ + 1270(0.128)² + 10(0.128) + 100 = -0.38 + 20.8 + 1.28 + 100 = 122~INJ
$$

Volume and liquidity moving averages are updated daily.

**Markets Added Partway Through an Epoch**

For markets added to the eligible list midway through an epoch, the preallocation will be prorated. For example, if ARB/USDT is added on the 15th day of the epoch, then the market will receive half of the rewards for the epoch (as there are 14 full days remaining out of 28).

## Reward Allocations

Rewards to individual institutional liquidity providers will be allocated based on the following equation:

$$
Rewards_{MM_i} = \sum_{Market}\left(Rewards_{Market} * \frac {TS_{MM_i, \ Market}} {\sum_{MM} TS_{MM,\ Market}} \right)
$$

**Each institutional liquidity provider** **will receive rewards based on their proportional**[ $$TS$$ ](scoring-formula-methodology.md#total-score)**within the market, subject to governance approval.**&#x20;

{% hint style="info" %}
Rewards for addresses totaling < 1 INJ at the end of each epoch will be disregarded to reduce the overhead of the disbursement process.&#x20;
{% endhint %}
