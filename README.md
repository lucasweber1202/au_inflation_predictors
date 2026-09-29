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
Authority: Masuko template main `4bc65765cedd9c14aec196cff382df6dfb318c77`
(`AUD` is in its `metadata.country` vocabulary). Last verified 2026-09-27.

## Research execution

The repository now includes an independent CSV contract engine in `scripts/engine.py`. Export persisted collector `time_series` columns `series_id,reference_date,vintage_date,value,collected_at` into a CSV, and supply one ISO forecast origin per line. Optional `release_date` must come from verified source evidence. For example: `python -m scripts.engine rows.csv --country AUD --target ABS_CPI_A130393720C --horizon 0 --origins origins.txt --truth-as-of 2026-09-29 --model last`. Run `python -m pytest -q` for synthetic contract tests. No empirical rankings are claimed without exported real vintages. The output is deterministic JSON; `--window N` selects rolling instead of expanding history.

Source acquisition smoke tests of the implemented collectors passed on 2026-09-29 for ABS, RBA and AIP. These smokes do not establish Databricks corporate execution or a new PostgreSQL certification.

The target frequency is read from `target_registry.csv`. `--horizon 0` nowcasts the origin period; `--horizon 1` forecasts the next period. ARX requires `--predictor ID` with an approved row in `predictor_map.csv`. `mean`/`last`/`ar` need no predictor. See `METHODOLOGY.md` for feature windows and common-sample comparison.
