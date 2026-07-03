# Domain pack: Finance / Equity Analysis

## Key objects
Company fundamentals (revenue, margin, ROE), factor exposures (value, momentum, quality, turnover), market regime, sector/industry.

## Key metrics
Factor IC (information coefficient), factor return, fundamental ratios (P/E, P/B, ROE), turnover rate, earnings growth rate.

## Common failure modes / root causes
- Factor appears predictive in-sample but fails out-of-sample (overfit to a specific historical regime)
- Fundamental metric change misattributed to company execution when it's a sector-wide or macro effect (always compare against sector/index baseline)
- Survivorship bias in backtests (delisted/failed companies excluded from the historical universe)
- Look-ahead bias (using data that wouldn't have actually been available at decision time)

## Diagnostic approach
This pack assumes and complements the `factor-analyzer` and `fundamental-stock-analysis` skills — Analysis OS's Model phase here means building the causal chain from macro/sector -> company fundamentals -> factor exposure -> return, and testing each link rather than jumping straight from factor to return.
