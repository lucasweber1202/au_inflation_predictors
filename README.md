# Australia inflation predictors: operational universe

This repository governs the target and selected predictor IDs; it is not a
substitute collector and does not train a model. `universe.csv` lists `active`
IDs verified end to end (official source, collector run on PostgreSQL,
observations spot-checked against the source file) and `candidate` sources that
remain unimplemented (blank `series_id`).

The target is the ABS monthly all-groups CPI (`ABS_CPI_A130393720C`), validated
by `collector_abs_cpi` before every write: the official group index-points
contributions add up to it, and from the September 2025 quarter the quarterly
all groups (`ABS_CPI_A2325846C`, history from 1948) equals the mean of its three
months.

The matrix gives source, native series identity, frequency, observed history,
release evidence, point-in-time limitation, rationale/sign and priority. A sign
is a hypothesis for research, not a causal or forecast claim. Every collector
stores the collection date as `vintage_date`; current-file backfills are not
historical point-in-time snapshots.

Sources: [ABS monthly CPI](https://www.abs.gov.au/statistics/economy/price-indexes-and-inflation/consumer-price-index-australia/jul-2026),
[RBA F1.1/F15](https://www.rba.gov.au/statistics/tables/),
[AIP terminal gate prices](https://aip.com.au/resources/historical-ulp-and-diesel-tgp-data/).
Authority: Masuko template main `723f8633bbd367ad9cca0a199e84b10fd355da36`
(`AUD` is in its `metadata.country` vocabulary). Last verified 2026-09-27.
