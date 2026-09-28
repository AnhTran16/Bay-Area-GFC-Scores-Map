# Bay Area GFC Cycle Scores Map

Interactive map of how the nine Bay Area counties and their cities moved through the housing cycle from 2000 to 2026: home values and jobs scored on one 0 to 100 scale, and new supply measured as permits relative to the housing stock.

Live map: https://anhtran16.github.io/Bay-Area-GFC-Scores-Map/

## What the map shows

Three layers.

| Layer | Level | What is shown | Source |
|---|---|---|---|
| Home values | 104 cities | ZHVI cycle score (combined, downturn, upswing); Zillow Home Value Index, all homes, mid-tier, smoothed, seasonally adjusted, monthly 2000 to Aug 2026 | Zillow Research |
| Jobs | 9 counties | Jobs cycle score (combined, downturn, upswing) on QCEW total covered employment, 2000 to 2025; hover shows 2025 jobs by sector (ten private supersectors plus Government) with share of county total | BLS QCEW |
| Supply rate | 90 incorporated cities | Average units permitted per year 2000 to 2025 divided by average January 1 housing stock over the same years; Combined, Single-family (1 to 4 unit structures) and Multifamily (5+ units). A percentage, not a score; green = low, red = high, scale capped at 2% | U.S. Census Bureau Building Permits Survey; California Department of Finance E-8 / E-5 housing stock |

Use the toggles at the top of the map (or in the side panel) to switch layer, series and score. Hover or click a city or county for the numbers behind it. A search box above the list filters cities by name on the Home values and Supply rate layers. Deep links: append `#zhvi-comb`, `#jobs-down`, `#supply-sf` and so on to the page address.

## Scoring method

The same method is applied to home values and jobs. It was built for the ZHVI ranking and reused unchanged for county employment. The supply rate layer is not scored.

**Windows**

- Pre-GFC peak: highest value from 2004 through 2008
- GFC trough: lowest value from the peak through 2013
- Recovery: first month or year at or above the pre-GFC peak
- Later-cycle peak: highest value from 2020 to the latest observation
- Latest: Aug 2026 for ZHVI, 2025 for QCEW jobs

**Nine metrics and weights**

| Group | Metric | Weight | Direction |
|---|---|---|---|
| Downturn | GFC drawdown: trough / pre-GFC peak - 1 | 0.20 | higher is better |
| Downturn | Recovery time: months (ZHVI) or years (jobs) from peak to first regained observation | 0.10 | lower is better |
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

City scores are ranked across the 104 ZHVI cities. County jobs scores are ranked across the nine counties, so each percentile step is 11.1 points and scores within about 10 points are effectively tied.

**Jobs (annual data)**

QCEW annual averages need no smoothing; recovery time is in years and volatility is the standard deviation of negative year-over-year changes.

**Supply rate**

Single-family = permits in 1-unit, 2-unit and 3-4 unit structures; multifamily = permits in structures of 5 or more units. Denominator is the DOF January 1 housing stock (all units including mobile homes). City figures exclude unincorporated areas; the workbook behind the map also carries county figures that include them.

## Coverage notes

- 13 of the 104 map cities are census-designated places (unincorporated) and permit through their county; Lafayette is incorporated but absent from the Census place file. These have ZHVI scores but no supply rate.
- Employment data exists only at county level, so on that layer the counties are shaded and city outlines are kept for reference. BLS withholds a few sectors for disclosure (Contra Costa and Marin: natural resources, manufacturing, information); they show as n/d and their total appears as "Not disclosed / unclassified".
- QCEW counts jobs where they are located; ZHVI, permits and housing stock are tied to where homes are.

## Sources

- Zillow Research, ZHVI: https://www.zillow.com/research/data/
- U.S. Census Bureau, Building Permits Survey: https://www.census.gov/construction/bps/index.html (county files https://www2.census.gov/econ/bps/County/, place files https://www2.census.gov/econ/bps/Place/West%20Region/)
- U.S. Bureau of Labor Statistics, Quarterly Census of Employment and Wages: https://www.bls.gov/cew/
- California Department of Finance, E-8 and E-5 Population and Housing Estimates: https://dof.ca.gov/forecasting/demographics/estimates/
- City and county boundaries: U.S. Census Bureau 2023 cartographic boundary files (1:500k), generalized: https://www.census.gov/geographies/mapping-files/time-series/geo/cartographic-boundary.html

The page is a single self-contained HTML file; all data is embedded as values as of September 28, 2026 (version 3).
