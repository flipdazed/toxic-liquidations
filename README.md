# Toxicity Bounds for Dynamic Liquidation Incentives
*arXiv preprint*

## TL;DR

This paper shows how to design liquidation incentives that never make a borrower's position worse.

When a lending protocol sells collateral to repay debt, the trade itself can move the market price.  
If the price impact exceeds the benefit of debt reduction, the borrower’s *health* (collateral value ÷ debt) falls after liquidation.  

This is a **toxic liquidation**. A *linear* health-linked liquidation bonus prevents this as we prove it always improves system health.

---

## Background

In DeFi lending systems:

1. Borrowers lock collateral to obtain loans.  
2. If their position becomes risky, the system liquidates part of it.  
3. Liquidators earn a bonus *i* as a reward.

When liquidations go through automated market makers (AMMs), selling collateral pushes the price down.  
That re-marks the remaining collateral and can worsen the borrower's position.


## Toxicity Condition

Health decreases (the step is toxic) when the loan-to-value ratio *l* exceeds a threshold:

```
l > 1 / ((1 + i) * λ)
```

where  
• *i* = liquidation bonus  
• *λ* = liquidity penalty (captures AMM slippage)

Toxicity increases with larger bonuses or shallower liquidity.


## Linear Incentive Rule

Define the incentive as linear in health *h*:

```
i(h) = i * (1 - h)
```

This choice removes dependence on *i* from the toxicity condition and yields the safety bound:

```
v < 1 / λ
```

Safety now depends only on market depth, not on the incentive curve.  
A linear rule scales rewards smoothly with risk, keeping liquidations health-improving.

## Why Linear Works

| Incentive type | Outcome |
|----------------|----------|
| Fixed bonus | Can cause toxic steps when liquidity is thin |
| Step or exponential | Overreacts, adds instability |
| **Linear bonus** | Balances reward and impact; no health loss |

## Practical Rule

For safe liquidations:

1. Model liquidity with penalty factor λ.  
2. Use linear incentive `i(h) = i * (1 - h)`.  
3. Ensure `v < 1 / λ` at the collateral limit.

Under these conditions, partial liquidations always improve system health.

## Citation

```

@misc{mcfarlane2025toxicity,
author       = {Alexander McFarlane},
title        = {Toxicity Bounds for Dynamic Liquidation Incentives},
year         = {2025},
archivePrefix= {arXiv},
primaryClass = {q-fin.RM}
}

```
