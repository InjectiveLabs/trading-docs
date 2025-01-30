---
hidden: true
---

# Helix AI Index

**Overview**

The Helix "AI Index" is a cryptocurrency index designed to provide investors with diversified exposure to the most promising AI blockchain projects and AI Equities. The index comprises 50% of 10 selected AI blockchain tokens and 50% of 6 AI Equities.

***

#### **Index Composition - AI Tokens**

* **Components**: 10 AI tokens, including Near (NEAR), Internet Computer (ICP), Bittensor (TAO), Render (RENDER), Virtuals Protocol (VIRTUALS), Artificial Superintelligence Alliance (FET), Injective Protocol (INJ), Akash Network (AKT), Ai16Z (Ai16z) and Grass (GRASS)
* **Weighting Methodology**: Market capitalization-weighted.
* **Rebalancing Frequency**: Monthly.

#### **Index Composition - AI Stocks**

* **Components**: 6 AI stocks, including Nvidia (NVDA), Taiwan Semiconductor Manufacturing Company Ltd (TSM), Palantir (PLTR), Arista Networks (ANIT), Super Micro Computer Inc (SMCI), and SenseTime (SNTMF)
* **Weighting Methodology**: Market capitalization-weighted.
* **Rebalancing Frequency**: Monthly.

***

#### **How the Index is Priced**

#### **1. Initial Calculation:**

* **Market Cap Calculation**: For each token, its market capitalization is calculated by multiplying the token's price by its circulating supply. Tokens represent 50% of the index. For each stock, the market capitalization is taken from Bloomberg Terminal. Equities represent 50% of the index.
* **Initial Weights**: Each token’s weight is determined by dividing its market cap by the total token market cap. Likewise, each equity’s weight is determined by dividing its market cap by the total equity market cap.

#### **2. Price Calculation:**

* **Index Value**: The index is priced by aggregating the weighted prices of each component token and equity.
* **Formula**: First we divide the market capitalization for each asset by the sum of the market capitalization in each asset sector, equities and crypto. This gives us the asset-specific weight for for the index. Then we sum the market capitalization for all equity assets and all crypto assets. Next, we multiple each asset-specific weight by the sum of the market capitalization of all assets to get the normalized market capitalizations for each asset. This normalizes the assets so that 50% of the index represents AI Equities and 50% of the index represents AI Tokens. Lastly, we add up the normalized market capitalizations and divide by 1,000,000,000 (10^9) to get an index price for the asset.

Here are the steps in formula form:

1. **Calculate the total market capitalization for each sector:**

$$$
TMC_{equity}=\sum_{i=1}^{m}MC^{i}_{equity} $$
$$$

$$
TMC_{crypto}= \sum_{j=1}^{n} MC^{j}_{crypto}
$$

$$
MC_{T}=TMC_{equity}+TMC_{crypto}
$$

where $$TMC_{equity}$$ represents the total market cap of the equity companies in the said basket, and $$TMC_{crypto}$$ represents the total market cap of the crypto companies in the basket. $$MC^{i}{equity}$$ _represents the element with index_ $$i$$ _in the real valued vector_  $$MC{equity} \in \R^{m}$$ and similarly $$MC^{j}{crypto}$$ _represents the element with index_ $$j$$ _in the real valued vector_ $$MC{crypto} \in \R^{n}$$

2. **Calculate asset-specific weights:**

$$
w^{i}{crypto} = \frac{MC^{i}{crypto}}{TMC_{crypto}}
$$

$$
w^{j}{equity} = \frac{MC^{j}{equity}}{TMC_{equity}}
$$

where $$w^{i}{crypto}$$ _and_ $$w^{j}{equity}$$ represents each element of the real valued vectors $$w_{crypto} \in \R^{n\times1}$$ and $$w_{equity} \in \R^{m \times 1}$$

3. **Adjust the weights to a scaled value of 50% crypto and 50% equity:**

$$
nw_{crypto}=w_{crypto}\times 0.5
$$

$$
nw^{equity} = w_{equity} \times 0.5
$$

where $$nw_{crypto} \in \R^{n \times 1}$$ and $$nw_{equity} \in \R^{m \times 1}$$ where $$n$$ and $$m$$ represent the total number of crypto and equity companies, respectively, $$nw_{crypto}$$ and $$nw_{equity}$$ is the adjusted weight metric.

Now let us introduce another variable $$nw$$ which represents the entire basket of equity and crypto whose dimensions are now a direct sum of $$nw_{crypto} \oplus nw_{equity}$$ as $$nw \in \R^{(n + m)\times 1}$$

4. **Calculate normalized market capitalizations:**

Based on the new $$nw$$ we calculate the total normalized market cap:

$$
nmc = MC_{T} \ nw
$$

where

$$
nmc \in \R^{(n+m) \times 1}
$$

5. **Calculate the index price:**

The index price is now:

$$
S_t^{index} = \frac{\sum_{i=1}^{n+m} nmc}{\text{divisor}}
$$

where the numerator is a vector summation, and the $$\text{divisor} = 10^{9}$$.

***

#### **Index Operation and Investor Use**

#### **1. Index Usage:**

* **Benchmarking**: Investors can use the "AI Index" as a benchmark to measure the performance of their portfolios.
* **ETFs and Derivatives**: The index can serve as the basis for financial products like ETFs or derivatives that track its performance.

#### **2. Risk Management:**

* **Cap on Dominance**: The representative caps prevent any single token or equity from dominating the index, reducing concentration risk.
* **Diversification**: By including 10 tokens, the index mitigates the impact of poor performance in any one project.

#### **3. Performance Monitoring:**

* **Real-Time Tracking**: The index value is updated in real-time based on the latest prices of the component tokens.
* **Historical Data**: Historical index values are available to analyze trends and performance over time
