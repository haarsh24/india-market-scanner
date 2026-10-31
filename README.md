# India Market Scanner

An open-source [Claude skill](https://docs.claude.com) that scans the Indian stock market (NSE/BSE) and produces a one-page research report, a budget-based plan, or an IPO verdict:

- **Market snapshot:** Nifty, Sensex, Bank Nifty, India VIX, FII/DII flows, sector moves, global cues
- **Buy-side candidates:** stocks scored out of 100 on trend, fundamentals, valuation, ownership and catalysts, with entry zone, stop-loss, target and what would invalidate the setup
- **Budget plan:** tell it how much you want to invest ("I want to invest ₹2,000 today") and it builds an illustrative allocation in whole shares across 1 to 8 stocks depending on the amount, with a one-line reason per stock, unspent cash, estimated charges and the worst-case loss if every stop-loss hits
- **Sell / avoid candidates:** red-flag checks (broken trends, falling earnings, promoter pledge, governance issues); labels your holdings as hold / trim / exit if you share them
- **IPO desk:** scores every mainboard IPO on two separate tracks, listing gain (subscription, valuation vs peers, anchors, GMP trend, market mood) and long term (business, financials, valuation, governance), then sorts each into Listing-gain play, Long-term hold, Both, Neutral or Avoid, with a listing outlook, an exit plan and the apply-by deadline

## Disclaimer

**This is an educational research tool, not investment advice.** It is not a SEBI-registered investment adviser or research analyst. Output is screen-based, may be wrong or stale, and carries no guarantee of returns. Budget plans are illustrative allocations from a screen, not a recommendation to buy. Markets involve risk of loss. Verify all data yourself and consider a SEBI-registered adviser before investing. The authors accept no liability for decisions made using this tool.

## How it works

The skill picks a mode from your request (Scan, Budget plan, Sell check, or IPO desk) and tells Claude to:

1. Fetch every price, ratio, flow, charge and IPO detail live from the web (exchange pages, filings, Screener.in, Moneycontrol, Chittorgarh and similar) and **never fill in numbers from memory**
2. Cross-check key figures across two sources and show an "as of" time
3. Drop anything it cannot verify, and say "no clean setups today" instead of forcing picks

Budget plans follow extra rules:

- Whole shares only, because NSE/BSE direct equity has no fractional shares
- Charges are estimated and shown as a % of the budget; small amounts may be better served by an ETF or index-fund SIP
- Fewer positions for small budgets, a 40% cap per stock once there are 3 or more, and at most 2 names per sector
- Delivery only: no margin, F&O or intraday
- It never forces a buy just to use up the budget

It does not place trades, log into broker accounts, or handle credentials.

## Install

**Claude Code**

```bash
git clone https://github.com/haarsh24/india-market-scanner.git
cp -r india-market-scanner/skills/india-market-scanner ~/.claude/skills/
```

**Claude (web / desktop app)**

Zip the `skills/india-market-scanner` folder (so `SKILL.md` sits inside it) and upload it from the Skills section of Claude's settings.

## Usage

Once installed, ask Claude things like:

- "Scan the market"
- "Stocks to buy today"
- "I want to invest ₹2,000 today, what should I buy?"
- "I have ₹25,000, split it across a few stocks"
- "What should I sell?" (paste your holdings as a list, CSV or screenshot for hold/trim/exit labels)
- "Which IPO is good for listing gains?"
- "Which IPO is good for the long term?"
- "Is the [company] IPO worth subscribing to?"

Web access (search/fetch) must be enabled for the skill to get live data.

## Limits to know about

- **Small budgets:** a mainboard IPO lot often costs more than a few thousand rupees, so the skill will say when your amount cannot fund one.
- **Data freshness:** free market sites can lag by about 15 minutes, and the skill shows an "as of" time on every price.
- **GMP:** grey market premium is unofficial and can be manipulated, so it is only ever supporting evidence.

## Repo layout

```
india-market-scanner/
├── LICENSE
├── README.md
└── skills/
    └── india-market-scanner/
        └── SKILL.md
```

## Contributing

Issues and pull requests are welcome, for example better data sources, scoring tweaks, or new checks. Please keep the disclaimer and the "verified data only" rule intact.

## License

[MIT](LICENSE)
