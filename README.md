# India Market Scanner

An open-source [Claude skill](https://docs.claude.com) that scans the Indian stock market (NSE/BSE) and produces a one-page research report:

- **Market snapshot:** Nifty, Sensex, Bank Nifty, India VIX, FII/DII flows, sector moves, global cues
- **Buy-side candidates:** stocks scored out of 100 on trend, fundamentals, valuation, ownership and catalysts, with entry zone, stop-loss, target and what would invalidate the setup
- **Sell / avoid candidates:** red-flag checks (broken trends, falling earnings, promoter pledge, governance issues); labels your holdings as hold / trim / exit if you share them
- **IPO verdicts:** scores mainboard IPOs on business quality, financials, valuation vs peers, issue structure and subscription demand, then gives a verdict (Subscribe / Listing gain only / Skip / Avoid)

## Disclaimer

**This is an educational research tool, not investment advice.** It is not a SEBI-registered investment adviser or research analyst. Output is screen-based, may be wrong or stale, and carries no guarantee of returns. Markets involve risk of loss. Verify all data yourself and consider a SEBI-registered adviser before investing. The authors accept no liability for decisions made using this tool.

## How it works

The skill tells Claude to:

1. Fetch every price, ratio, flow and IPO detail live from the web (exchange pages, filings, Screener.in, Moneycontrol, Chittorgarh and similar) and **never fill in numbers from memory**
2. Cross-check key figures across two sources and show an "as of" time
3. Drop anything it cannot verify, and say "no clean setups today" instead of forcing picks

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
- "What should I sell?" (paste your holdings as a list, CSV or screenshot for hold/trim/exit labels)
- "Is the [company] IPO worth subscribing to?"

Web access (search/fetch) must be enabled for the skill to get live data.

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
