# Source fiches and collection decisions

The [source registry](source_registry.csv) records publisher, page, native table/series identity, cadence, release lag, revision exposure, point-in-time quality, automation feasibility, licence status, economic channel, and owning collector. `PENDING_VERIFICATION` is a deliberate gate, not a native identifier. Candidate rows cannot enter the experiment merely because a publisher page exists.

## Verified within an existing collector

- **National rents index (ABS_CPI_A130390094A)**: live metadata from `collector_abs_cpi` identifies the native monthly series and official source URL. The existing export already supplies it; no new ingestion branch is needed. Strict as-of experiments start with collected vintages, and the feature uses only observations available by the forecast origin.

## Next publisher-owned implementations

- **Demand**: ABS Monthly Household Spending Indicator (the current monthly series; historical Retail Trade ceased July 2025). Assign to the existing ABS publisher collector. Resolve native table ID, downloadable format, first reference period, release-date calendar, revisions, licence, and source-specific assertions before activating a series.
- **Costs and expectations**: RBA G3 Inflation Expectations CSV and I2 Commodity Prices: assign to collector_rba_au; G3 mixes cadences, so select each native series and its publication date before feature aggregation. ABS WPI, PPI and International Trade Prices remain quarterly candidates under collector_abs_cpi.
- **Additional sources**: AEMO aggregate electricity data and ABARES weekly commodities require publisher-specific ownership and licence/release validation; do not open new collectors just to list sources.

## Acceptance gate for any candidate

Record the exact official native ID and download URL, cadence and earliest history, publication timing, revision behavior, unattended retrieval result, data format and licence. Add a parser and a known-answer source validation to the owning collector, persist the standard observation/vintage contract, and run a live smoke before marking it active. Historical publisher backfills are sensitivity data, never silently relabeled as contemporaneously observed vintages.
