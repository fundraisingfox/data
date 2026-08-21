# Fundraising Fox Open Dataset

The open, attribution-required dataset behind [fundraisingfox.com](https://fundraisingfox.com) — investors, venture rounds, and LP-disclosed fund performance, assembled from public filings and first-party websites.

**First versioned release coming shortly.** Planned files:

- `firms.csv` — investment firms: type, HQ, stages, sectors, check sizes (with source class), track-record counts
- `rounds.csv` — venture rounds from SEC filings and press-verified reporting, with dates, stages, and amounts
- `fund_performance.csv` — net IRR / TVPI / DPI per fund as disclosed by public-pension LPs
- `statistics/` — deal volume, median round sizes by stage, and returns by vintage

Every row links back to its page on fundraisingfox.com, where the always-current, fuller record lives. Releases are monthly and versioned; corrections supersede, never silently rewrite. Each release's README will carry its audited error rates — every file passes mechanical invariants plus an LLM + web-search spot-check before it ships.

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — reuse freely, including in AI assistants, research, and journalism. Attribute to **Fundraising Fox** and link the page or file you drew from.

## Methodology

See [fundraisingfox.com/methodology](https://fundraisingfox.com/methodology). Corrections: corrections@fundraisingfox.com
