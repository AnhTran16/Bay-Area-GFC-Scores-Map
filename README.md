# Bay Area GFC Cycle Scores Map

Interactive map of how the nine Bay Area counties and their cities moved through the housing cycle from 2000 to 2026: home values, housing permits, and jobs and income, all scored on one 0 to 100 scale.

Live map: https://anhtran16.github.io/Bay-Area-GFC-Scores-Map/

## What the map shows

Three datasets, each with a combined, downturn and upswing score.

| Dataset | Level | Series | Source |
|---|---|---|---|
| Home values | 104 cities | Zillow Home Value Index (all homes, mid-tier, smoothed, seasonally adjusted), monthly 2000 to Aug 2026 | Zillow Research |
| Permits | 90 incorporated cities (75 / 62 / 58 scored) | Housing units authorized: total, single-family (1-unit), multifamily (2+ units), annual 2000 to 2025 | U.S. Census Bureau, Building Permits Survey |
| Jobs and income | 9 counties | QCEW total covered jobs; QCEW average weekly wage in 2025 dollars; BEA per capita personal income in 2025 dollars | BLS QCEW, BEA CAINC4, BLS CPI-U |

Use the toggles at the top of the map (or in the side panel) to switch dataset, series and score. Hover or click a city or county for the metrics behind its score. Deep links: append `#zhvi-comb`, `#permits-sf-down`, `#employment-inc-up` and so on to the page address.

## Scoring method

The same method is applied to every series. It was built for the ZHVI ranking and reused unchanged for permits and employment.

**Windows**

- Pre-GFC peak: highest value from 2004 through 2008
- GFC trough: lowest value from the peak through 2013
- Recovery: first month or year at or above the pre-GFC peak
- Later-cycle peak: highest value from 2020 to the latest observation
- Latest: Aug 2026 for ZHVI, 2025 for permits and QCEW, 2024 for BEA

**Nine metrics and weights**

| Group | Metric | Weight | Direction |
|---|---|---|---|
| Downturn | GFC drawdown: trough / pre-GFC peak - 1 | 0.20 | higher is better |
| Downturn | Recovery time: months (ZHVI) or years (annual series) from peak to first regained observation | 0.10 | lower is better |
| Downturn | Recent drawdown: latest / maximum since 2020 - 1 | 0.15 | higher is better |
| Downturn | Downside volatility: standard deviation of negative period-over-period changes | 0.05 | lower is better |
| Upswing | Trough to later peak: later peak / GFC trough - 1 | 0.20 | higher is better |
| Upswing | Post-GFC CAGR: annualized growth from trough to later peak | 0.10 | higher is better |
| Upswing | First 36 months (3 years) of recovery from the trough | 0.10 | higher is better |
| Upswing | Latest vs pre-GFC peak: latest / pre-GFC peak - 1 | 0.05 | higher is better |
| Upswing | Share of positive periods from trough to later peak | 0.05 | higher is better |

**Scores**

1. Each metric is converted to a percentile rank across the scored universe: rank / n x 100, ties averaged.
2. Downturn score = weighted average of the four downturn percentiles; Upswing score = weighted average of the five upswing percentiles. Both run 0 to 100.
3. Combined score = average of Downturn and Upswing.

City scores are ranked across the scored cities (104 for ZHVI, 75 / 62 / 58 for permits). County scores are ranked across the nine counties, so each percentile step is 11.1 points and scores within about 10 points are effectively tied.

**Adjustments for annual data**

- Permit counts are lumpy, so the scored permit series is a 3-year trailing average of annual units, the counterpart of Zillow's smoothing. Cities with fewer than 500 permitted units over 2000 to 2025 are shown in grey and not scored. Where the smoothed trough is zero, the trough is floored at 1 unit in the ratio metrics.
- Wages and income are scored in 2025 dollars (U.S. CPI-U), because nominal series rarely fall and would give the downturn metrics nothing to rank.
- QCEW and BEA are annual averages and need no additional smoothing.

## Coverage notes

- 13 of the 104 map cities are census-designated places (unincorporated) and permit through their county; Lafayette is incorporated but absent from the Census place file. These have ZHVI scores but no permit scores.
- Employment data exists only at county level, so on that view the counties are shaded and city outlines are kept for reference.
- QCEW counts jobs where they are located; ZHVI, permits and BEA income are tied to where homes and residents are.

## Sources

- Zillow Research, ZHVI: https://www.zillow.com/research/data/
- U.S. Census Bureau, Building Permits Survey: https://www.census.gov/construction/bps/index.html (county files https://www2.census.gov/econ/bps/County/, place files https://www2.census.gov/econ/bps/Place/West%20Region/)
- U.S. Bureau of Labor Statistics, Quarterly Census of Employment and Wages: https://www.bls.gov/cew/
- U.S. Bureau of Economic Analysis, Local Area Personal Income, table CAINC4: https://apps.bea.gov/itable/?ReqID=70&step=1
- U.S. Bureau of Labor Statistics, Consumer Price Index (CPI-U, U.S. city average): https://www.bls.gov/cpi/
- City and county boundaries: U.S. Census Bureau 2023 cartographic boundary files (1:500k), generalized: https://www.census.gov/geographies/mapping-files/time-series/geo/cartographic-boundary.html

The page is a single self-contained HTML file; all data is embedded as values as of September 2026.
