---
description: OLP Reward Allocations to Markets and Market Makers
---

# Reward Allocations

## Market Reward Allocations

Rewards are allocated to [eligible markets](eligible-markets.md) in two different methods:

1. Static allocations
2. Static allocations with a dynamic component

### Static Market Reward Allocations (Preallocations)

17.5% of INJ rewards will be preallocated to the BTC/USDT Perp market, 17.5% will be preallocated to the ETH/USDT Perp market, and 12.5% will be preallocated to the INJ/USDT Perp market. 1% will be preallocated to each remaining eligible market as a minimum allocation:&#x20;

| Market                 | Total Allocation                                                                       |
| ---------------------- | -------------------------------------------------------------------------------------- |
| BTC/USDT Perp          | 17.5%                                                                                  |
| ETH/USDT Perp          | 17.5%                                                                                  |
| INJ/USDT Perp          | 12.5%                                                                                  |
| Other Eligible Markets | 1% each + formula based allocation, with reward cap based on formula (see table below) |

{% hint style="info" %}
Static allocations may change over time as more markets are added to the eligible list
{% endhint %}

### Dynamic Market Reward Allocations

The remaining rewards will be allocated to the eligible markets (excluding BTC/ETH/INJ Perps) based on the following equation:&#x20;

$$
Rewards_{Market_i} = TAR * Preallocation_{Market_i} + TAR * (1- Preallocation_{Total}) *\newline \frac {\sum\limits_{MM} (LS_{MM,\  Market_i})^{0.7} * Volume_{MM,\  Market_i}} {\sum\limits_{Market}\sum\limits_{MM} (LS_{MM,\ Market})^{0.7}*Volume_{MM,\ Market}}
$$

$$
\text{where} \quad Preallocation_{Total} = 0.2+0.2+0.15+Other\  Preallocations
$$

$$
\text{and} \quad TAR = Total\ Available\ Rewards
$$

{% hint style="info" %}
$$Other\ Preallocations$$ refers to the static market reward allocations for non-BTC, ETH, and INJ perp markets.

For more information on $$TAR$$ each epoch, see the [Reward Pool](../olp-rewards.md) page.
{% endhint %}

For each eligible market, the product of the MM[^1]’s $$LS^{0.7}$$ and $$Volume$$ is aggregated across all MMs. Rewards are allocated to each market based on the proportional aggregate products across all applicable markets. The preallocation amount (1%) for the market is also added in.&#x20;

#### Markets Added Partway Through an Epoch

For markets added to the eligible list midway through an epoch, the 1% preallocation will be prorated. For example, if ARB/USDT is added on the 15th day of the epoch, then the market will receive a 0.5% preallocation (there are 14 days left out of 28. If there are 17 days left, then the market will receive $$\frac {17}{28} * 0.01$$).

### Market Allocation Cap

For each market that has dynamic reward allocations, a hard cap will be applied according to the following formula, where $$n$$ is the number of eligible markets excluding BTC, ETH, and INJ perps:

$$
Rewards_{max} = TAR\ *\ \frac{0.45}{n}*2
$$

Any reward allocations that exceed the cap will be redistributed amongst the other eligible markets according to the [dynamic allocation formula](reward-allocations.md#dynamic-market-reward-allocations).

<table><thead><tr><th width="422"># Eligible Markets Excluding BTC/ETH/INJ Perps</th><th>Rewards Cap</th></tr></thead><tbody><tr><td>6</td><td>17.50% of Total Available Rewards</td></tr><tr><td>7</td><td>15.00% of Total Available Rewards</td></tr><tr><td>8</td><td>13.13% of Total Available Rewards</td></tr><tr><td>9</td><td>11.67% of Total Available Rewards</td></tr><tr><td>10</td><td>10.50% of Total Available Rewards</td></tr><tr><td>11</td><td>9.55% of Total Available Rewards</td></tr><tr><td>12</td><td>8.75% of Total Available Rewards</td></tr><tr><td>...</td><td>...</td></tr></tbody></table>

## Market Maker Reward Allocations

Rewards to individual MMs[^2] will be allocated based on the following equation:

$$
Rewards_{MM_i} = \sum_{Market}\left(Rewards_{Market} * \frac {TS_{MM_i, \ Market}} {\sum_{MM} TS_{MM,\ Market}} \right)
$$

**Each** [**MM**](#user-content-fn-3)[^3] **will receive rewards based on the** [**MM**](#user-content-fn-4)[^4]**’s proportional**[ $$TS$$ ](scoring-formula-methodology.md#total-score)**within the market, subject to governance approval.**&#x20;

{% hint style="info" %}
Rewards for addresses totaling < 1 INJ at the end of each epoch will be disregarded to reduce the overhead of the disbursement process.&#x20;
{% endhint %}

[^1]: Market Maker

[^2]: Market Makers

[^3]: Market Maker

[^4]: Market Maker
