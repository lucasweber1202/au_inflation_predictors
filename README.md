# Australia inflation predictors: operational universe

This repository governs the target and selected predictor IDs; it is not a substitute collector and does not train a model. `universe.csv` distinguishes `active` IDs verified in collector PRs from `candidate` sources that remain unimplemented. The active target is still a **draft target collector**, pending official weights and release monitoring.

The published matrix gives source, native series identity, frequency, observed history, release lag, point-in-time limitation, rationale/sign and priority. Blank ID means no collector output is verified. A sign is a hypothesis for research, not a forecast claim. Check each collector's current PR and original source before using data in a backtest.

Sources: [ABS monthly CPI](https://www.abs.gov.au/statistics/economy/price-indexes-and-inflation/consumer-price-index-australia/jul-2026), [RBA F1.1/F15](https://www.rba.gov.au/statistics/tables/), [AIP terminal gate prices](https://aip.com.au/pricing/terminal-gate-prices). Authority: Masuko template main `8e4613b36c2808a7de234934a81bb26f7a22d367`; AUD vocabulary pending upstream PR #1.
