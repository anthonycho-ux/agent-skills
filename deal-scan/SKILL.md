---
name: deal-scan
description: "Scan vendors for a better price than a benchmark. Universal."
version: 1.0.0
author: Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [shopping, prices, vendors, research, universal]
---

# Deal scan

Answer one question before any purchase: **is the benchmark price actually the
best available deal for this exact item?** Works for any agent with web access —
use subagents/delegation if you have them, sequential web search if you don't.

## When to use

- User asks "is this a good price", "find me a better deal", "scan other vendors".
- A benchmark exists: product + price + vendor (from a prior recommendation or the user).

## Procedure

1. **Pin the benchmark exactly.** Product name, model/size/specs, condition
   (new/refurb/open-box), region, warranty terms, and the all-in price
   (taxes, shipping, install, required subscriptions). Wrong variant or wrong
   region = not a deal, no matter how cheap.
2. **Define lanes and fan out.** Two lanes minimum:
   - Local physical retailers (what is actually near the user)
   - Online retailers + marketplaces that ship to the user's region
   Run lanes in parallel via subagents if available; otherwise sequential web
   searches. Require machine-readable output (JSON/CSV rows) from each lane:
   vendor, product, variant, price, fees, stock, URL, beats-benchmark.
3. **Verify with code, not trust.** Parse every results file; recompute
   beats-benchmark comparisons yourself. Agents routinely flag prices HIGHER
   than the benchmark as beating it — catch this in aggregation, not in prose.
4. **Deliver verdict-first.** Answer first (does anything beat the benchmark?),
   then ranked alternatives with all-in prices and caveats (warranty, install,
   return window, marketplace seller risk), one next action, timestamp.

## Pitfalls

- **Variant trap**: cheapest hit is often a different size, lower spec,
  winter vs all-season, or carrier-locked model. Filter by exact variant
  before comparing.
- **Price-basis mismatch**: online prices exclude shipping/tax/install;
  in-store prices may include them. Normalize or state the basis per row.
- **Region lock**: a great price abroad may void warranty or not ship.
  Check shipping region and warranty terms before counting a hit.
- **Marketplace vs retail**: third-party sellers vary in returns and
  authenticity — note seller type, not just the headline price.
- **Missing lane = missing data**: if a lane fails or returns nothing,
  re-run it or report the gap; never let silence read as "no deals".
- **Promo stacking**: coupon/promo codes can undercut listed prices —
  check for current codes before the final verdict.

## Verification

- Every results file parses; row count matches what each lane claimed.
- Every "beats benchmark" row recomputed in code against the normalized
  all-in benchmark.
- Verdict names the benchmark's all-in price and each alternative's basis.
