---
description: How to Qualify and Remain Qualified for OLP Rewards
---

# Eligibility

## Clean Slate Qualification

There are two types of OLP qualification:&#x20;

1. Qualification to earn rewards for an **individual** OLP market—to be referred to as **Individual Market Eligibility/Qualification**
2. Qualification to earn rewards for **any** OLP market (automatic qualification for all OLP markets)—to be referred to as **Overall Eligibility/Qualification**

An Injective address can qualify for OLP by meeting the following criteria:

* The **address must be opted out of the Trade & Earn (T\&E) program** prior to the start of the qualification process. The address will not earn T\&E rewards during the qualification process. See examples in [Python](https://github.com/InjectiveLabs/sdk-python/blob/master/examples/chain\_client/24\_MsgRewardsOptOut.py), [Go](https://github.com/InjectiveLabs/sdk-go/blob/master/examples/chain/24\_MsgRegisterAsDMM/example.go), and [TS](https://github.com/InjectiveLabs/injective-ts/wiki/04CoreModulesExchange#msgrewardsoptout) for opting out programatically.
  * Note: Eligibility for the qualification process begins at 00:00 UTC the day after the opt out is complete. To check if an address has been successfully opted out of T\&E, please [cross reference this list](https://lcd.injective.network/injective/exchange/v1beta1/opted\_out\_of\_rewards\_accounts).
* For **Individual Market Qualification**, the address must account for **at least 1% of the individual market's total maker volume each day for 3 consecutive days** in the same epoch. Self trading is strictly prohibited.
* For **Overall Qualification,** the address's maker volume must account for **at least 0.25% of the total daily exchange maker volume of all** [**eligible markets**](program-details/eligible-markets.md) (0.25% of the sum of maker volume in all OLP markets) **for 3 consecutive days** in the same epoch. Self trading is strictly prohibited.

{% hint style="success" %}
Overall Qualification can be achieved after Individual Market Qualification is achieved in the same epoch. Individual market activity prior to Overall Qualification will not be affected by the Overall Qualification itself, though further (in)activity during the epoch will affect reward allocations in the individual market(s). See [Program Details](program-details/) for more information on how rewards are calculated.
{% endhint %}

Assuming these requirements have been met, the address will qualify for OLP rewards on the 4th day at 00:00 UTC. Once qualified, an address will remain eligible for rewards through the rest of the epoch unless special circumstances (e.g. abusing the system) compel the removal of the address. Note that activity prior to qualification will not count towards rewards.

{% hint style="warning" %}
It may be prudent to consolidate trading strategies into a single address to increase maker volume. Otherwise, addresses with less maker volume than the required threshold will not qualify for rewards even if volume on an aggregate level between multiple addresses exceeds the threshold.&#x20;

See [documentation on the Injective `authz` module](https://docs.injective.network/develop/modules/Core/authz/) for a method of executing multiple strategies from a single address while retaining trading [fee discounts](https://helixapp.com/fee-discounts).
{% endhint %}

## Maintaining Next Epoch Eligibility/Pre-Qualification

To automatically qualify (pre-qualify) for the next epoch after qualifying for the current epoch, an address must either:&#x20;

1. **Account for at least 1% of cumulative maker volume** in each individual [eligible market](program-details/eligible-markets.md) from the date of qualification to the last day of the epoch to maintain Individual Market Eligibility for each OLP market, or
2. **Account for at least 0.25% of total cumulative exchange maker volume** of all [eligible markets](program-details/eligible-markets.md) from the date of qualification to the last day of the epoch to maintain Overall Eligibility.

* Example: Address `inj1a` enters epoch 21 ineligible for any OLP rewards. `inj1a` accounts for 1%, 0.1%, and 0.2% of total daily exchange maker volume of [eligible markets](program-details/eligible-markets.md) on days 1, 2, and 3 of epoch 21, respectively. On days 4, 5, and 6, `inj1a` accounts for 0.5% of the applicable volume each day. `inj1a` qualifies on day 7 of the epoch. To maintain Overall Eligibility for epoch 22, `inj1a` must account for at least 0.25% of the cumulative applicable maker volume from day 7 through day 28 of epoch 21. If the cumulative maker volume of [eligible markets](program-details/eligible-markets.md) for this period (days 7 through 28) was $100M, then `inj1a` must account for $250,000 of cumulative maker volume in those markets within the same period. The same idea holds true for Individual Market Eligibility maintenance, though cumulative maker volume contribution is evaluated only on the individual market(s) of interest.

If the address was eligible for the entire epoch for an individual market or all markets through a previous epoch's pre-qualification, that address must account for at least 1% or 0.25% of the cumulative maker volume of an individual market or all [eligible markets](program-details/eligible-markets.md) in the entire epoch, respectively.&#x20;

* Example: Address `inj1a` enters epoch 22 pre-qualified from maintaining Overall Eligibility in epoch 21. Suppose the cumulative maker volume of [eligible markets](program-details/eligible-markets.md) in epoch 22 totals $200M. Then `inj1a` must contribute at least $500,000 of the $200M in [eligible markets](program-details/eligible-markets.md) by the end of epoch 22 to maintain automatic Overall Eligibility for epoch 23.

**If an address** **fails to maintain Overall Eligibility** to pre-qualify for the next epoch **but manages to maintain Individual Market Eligibility** in one or more markets for the next epoch, **that address will lose Overall Eligibility pre-qualification but keep Individual Market Eligibility** **pre-qualification** in the relevant markets for the next epoch.

* Example: Address `inj1a` enters epoch 28 pre-qualified from maintaining Overall Eligibility in epoch 27. Suppose the cumulative maker volume of [eligible markets](program-details/eligible-markets.md) in epoch 28 totals $500M, with $100M from the INJ/USDT market, $100M from the BTC/USDT Perp market, and $300M from 3 other markets. `inj1a` contributes $1M in maker volume to the INJ/USDT market, but only contributes $200,000 in maker volume to the BTC/USDT Perp market, for a total of $1.2M. `inj1a` does not participate in any of the other markets even though it has Overall Eligibility. In this case, `inj1a` would fail to maintain Overall pre-qualification for  epoch 29 since the address only contributed 0.24% of total maker volume during the epoch. However, `inj1a` would maintain Individual Market pre-qualification for epoch 29 in the INJ/USDT market alone since the address contributed 1% of the individual market's maker volume throughout the epoch.

## Disqualification

**Any address that fails to maintain next epoch eligibility will be disqualified from OLP at the start of the next epoch**. If the address wishes to rejoin the program, the address must go through the [clean slate qualification process](eligibility.md#clean-slate-qualification) again (though the address does not have to opt out of T\&E another time). Note that any liquidity contributed on days that the address is ineligible will not be rewarded retroactively once the address requalifies.

{% hint style="info" %}
Disqualification occurs at the end of each epoch, meaning addresses continue to accrue rewards within the epoch regardless of next epoch eligibility.
{% endhint %}

## Tracking Eligibility

The [OLP dashboard](https://trading.injective.network/program/liquidity/eligibility) can be used to track current and future epoch reward eligibility.

{% embed url="https://trading.injective.network/program/liquidity/eligibility" %}
