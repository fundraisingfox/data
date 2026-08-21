# Fundraising Fox Open Dataset — v2026-08

The open, attribution-required dataset behind [fundraisingfox.com](https://fundraisingfox.com): investment firms, venture rounds, and LP-disclosed fund performance, assembled from public filings and first-party websites. Every row carries a `fundraisingfox_url` linking to its live page, where the always-current, fuller record lives (thesis, team, portfolio, contacts, FAQ).

## Files

| File | Rows | What it is |
|---|---|---|
| `firms.csv` | 16,259 | Investment firms: type, HQ, stages, sectors, check sizes (with source class), track-record counts (portfolio, exits, led rounds) |
| `rounds.csv` | 111,501 | Venture rounds from SEC filings and press-verified reporting: dates, stages, amounts (`amount_is_floor` marks SEC amounts-sold that may still grow) |
| `fund_performance.csv` | 7,721 | Net IRR / TVPI / DPI per private fund, as disclosed by public-pension and foundation LPs — the LPs' own calculations |
| `statistics/` | — | Directly quotable rollups: rounds by year, median round size by stage (trailing 12 months), fund returns by vintage |

## Correctness, measured

This release only ships what passed a two-layer audit — mechanical invariants over **every** row, then an LLM + web-search verification of a 100-row random sample per file:

| File | Mechanical failure rate (excluded) | Sampled error rate |
|---|---|---|
| `rounds.csv` | 0.21% | **0 / 100 incorrect** (28 unverifiable — small SEC-filed rounds nobody wrote about; the filing is the primary source) |
| `fund_performance.csv` | 0.03% | **4 / 100 incorrect** — all manager-attribution edge cases; the four found were corrected before release |
| `firms.csv` | 0.12% | **6 / 100 incorrect** — mostly HQ-city nuances (registered office vs. operating HQ) plus rare identity conflations |

Beyond sampling, before this release every one of ~7,200 fund→manager pairings was checked (mechanical flags + model triage + web-search verification of suspects): ~2,100 wrong or truncated manager strings ship as **null rather than as false facts**, as do pairings we could not settle. All 16,259 firms had their homepage fetched and machine-judged against the recorded identity; contradicted identities are excluded and contradicted HQ cities ship null. A missing value here means "not defensible yet", never "doesn't exist" — the live site may know more, with caveats attached.

Known limitations: HQ cities can reflect filing addresses rather than operating headquarters; firm names follow the firm's own site, which may lag rebrands; `rounds.csv` excludes grant programs (SBIR/STTR) by design.

## Versioning & corrections

Releases are monthly and versioned; each is immutable and supersedes the last. Errors found between releases are fixed upstream at fundraisingfox.com and roll into the next cut. Report errors: corrections@fundraisingfox.com — corrections take priority over all automated sources.

## License & citation

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — reuse freely, including in AI assistants, research, and journalism.

> Fundraising Fox Open Dataset, v2026-08. https://fundraisingfox.com — via github.com/fundraisingfox/data

Methodology: [fundraisingfox.com/methodology](https://fundraisingfox.com/methodology)
