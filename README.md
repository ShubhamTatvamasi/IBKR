# IBKR India Tax

A private, in-browser tool that turns Interactive Brokers Activity Flex Query exports into the
figures an Indian resident needs to file Schedule FA, capital gains, dividends, and the foreign tax
credit — with the SBI TT buying rate behind every number.

**Use it:** https://shubhamtatvamasi.com/IBKR/

There is no backend, no account and no analytics. Statements are parsed in the browser and never
leave the device; a Content Security Policy limits network access to the site's own origin.

## What it produces

- **Form 67 / Form 44** — foreign tax credit, by country and income
- **Schedule CG** — short-term (A5) and long-term (B8) gains on unlisted foreign shares, Table F
- **Schedule OS** — gross dividends and broker interest, with the 234C quarterly split
- **Schedules FSI and TR** — per-country foreign income and treaty relief
- **Schedule FA A2/A3** — the IBKR account and every purchase lot held during the calendar year
- **ITR-2 JSON** — Schedule FA/FSI/TR objects checked against the official schema (AY 2026-27)
- **Filing pack** — portal-ordered CSVs, working papers, exchange-rate appendix and a year-end file

The step-by-step walkthrough, method notes and address book live at `/IBKR/guide/`, `/IBKR/method/`
and `/IBKR/assets/`.

## Development

```sh
npm install
npm run dev      # http://localhost:4321/IBKR/
npm test         # unit tests for the tax engine
npm run build    # astro check + static build into dist/
```

`npm run rates` records the day's SBI Forex Card rates into `public/data/ttbr/`; the GitHub Actions
workflow runs it twice a day and deploys the static site to GitHub Pages.

Architecture, tax rules and the decisions taken where the law is open are in
[`docs/DESIGN.md`](docs/DESIGN.md).

## Not tax advice

A calculation aid. Review every figure with your Chartered Accountant before filing.
