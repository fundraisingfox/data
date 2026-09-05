# Fundraising Fox Open Dataset — v2026-09

The open, attribution-required dataset behind [fundraisingfox.com](https://fundraisingfox.com): investment firms, venture rounds, and LP-disclosed fund performance, assembled from public filings and first-party websites. Every row carries a `fundraisingfox_url` linking to its live page, where the always-current, fuller record lives (thesis, team, portfolio, contacts, FAQ).

## Files

| File | Rows | What it is |
|---|---|---|
| `firms.csv` | 16,272 | Investment firms: type, HQ, stages, sectors, check sizes (with source class), track-record counts (portfolio, exits, led rounds) |
| `rounds.csv` | 126,333 | Venture rounds from SEC filings and press-verified reporting: dates, stages, amounts (`amount_is_floor` marks SEC amounts-sold that may still grow) |
| `fund_performance.csv` | 7,721 | Net IRR / TVPI / DPI per private fund, as disclosed by public-pension and foundation LPs — the LPs' own calculations |
| `statistics/` | — | Directly quotable rollups: rounds by year, median round size by stage (trailing 12 months), fund returns by vintage |

## Correctness, measured

This release only ships what passed a two-layer audit — mechanical invariants over **every** row (failures excluded), then an LLM + web-search verification of a fresh random sample per file, run for this release:

| File | Mechanical failure rate | Sampled error rate |
|---|---|---|
| `rounds.csv` | 0.20% | **3 / 100 incorrect** (24 unverifiable) |
| `fund_performance.csv` | 0.03% | **5 / 100 incorrect** (4 unverifiable) |
| `firms.csv` | 0.12% | **6 / 100 incorrect** (0 unverifiable) |

Beyond sampling, every fund→manager pairing has been checked (mechanical flags, model triage, web-search verification of suspects): wrong, truncated, and unresolvable manager strings ship as **null rather than as false facts**. Every firm's homepage has been fetched and machine-judged against its recorded identity; contradicted identities are excluded and contradicted HQ cities ship null. A missing value here means "not defensible yet", never "doesn't exist" — the live site may know more, with caveats attached.

Known limitations: HQ cities can reflect filing addresses rather than operating headquarters; firm names follow the firm's own site, which may lag rebrands; `rounds.csv` excludes grant programs (SBIR/STTR) by design.

## Versioning & corrections

Releases are monthly and versioned; each is immutable and supersedes the last. Errors found between releases are fixed upstream at fundraisingfox.com and roll into the next cut. Report errors: corrections@fundraisingfox.com — corrections take priority over all automated sources.

## License & citation

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — reuse freely, including in AI assistants, research, and journalism.

> Fundraising Fox Open Dataset, v2026-09. https://fundraisingfox.com — via github.com/fundraisingfox/data

Methodology: [fundraisingfox.com/methodology](https://fundraisingfox.com/methodology)
