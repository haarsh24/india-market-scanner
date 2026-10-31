---
name: india-market-scanner
description: Scan the Indian market (NSE/BSE) for buy and sell/avoid candidates and judge IPOs. Use for 'stocks to buy today', 'what to sell', 'scan the market', 'is this IPO worth it'.
---

# India Market Scanner

Research workflow for NSE/BSE. It produces evidence-based screen results, not personalised advice. Claude is not a SEBI-registered investment adviser.

## Ground rules
- Get the current date and time in IST first. NSE/BSE cash market runs 9:15-15:30 IST, Mon-Fri, except exchange holidays. If the market is closed, say all prices are the last close.
- Every number must come from a source retrieved in this session (WebSearch, WebFetch, or a browser when a site needs rendering). The shell usually cannot reach market sites. Never fill in prices, PE, GMP or flows from memory. If a figure cannot be verified, write "not verified" or drop the item.
- Cross-check price and key ratios against two sources where possible (NSE/BSE official pages, Screener.in, Moneycontrol, Trendlyne, Tickertape). Show an "as of" time. Free sites can lag by up to 15 minutes.
- Prefer primary sources: exchange filings, company results, SEBI-filed RHP/DRHP, NSE/BSE bulk and block deal data. Treat social-media tips and "target price" headlines as noise.
- Search each distinct stock, sector or IPO separately.

## Step 1: Market snapshot (always first)
Nifty 50, Sensex, Bank Nifty, Nifty Midcap and Smallcap: level and day/week change. India VIX. FII and DII net cash flows (latest session and 5-day). Advance/decline ratio. Best and worst sectors. Global cues: US indices, Brent crude, USD/INR, US 10Y yield. Events within the next week: RBI, major results, Fed, F&O expiry. End with a one-line regime read (risk-on / mixed / risk-off) and why.

## Step 2: Buy-side candidates
Universe: Nifty 500 stocks with average daily traded value above Rs 10 crore. Exclude ASM/GSM-listed, T2T, SME and penny stocks unless asked.

Score out of 100:
- Trend and momentum (30): price above rising 50- and 200-DMA, 3-month relative strength vs Nifty, breakout on above-average volume. Penalise stocks more than 20% above the 50-DMA.
- Fundamentals (30): 3-year revenue and profit growth, ROE/ROCE above 15%, low debt-to-equity, operating cash flow vs PAT, latest quarter YoY growth.
- Valuation (15): PE or EV/EBITDA vs own 5-year median and sector peers, PEG.
- Ownership and flows (15): stable or rising promoter holding, pledge below 10%, rising FII/DII/MF holding, recent bulk deals.
- Catalyst and risk (10): order wins, capex, sector tailwind; subtract for litigation or regulatory probes.

Show the top 3-5 scoring 70 or more. For each: ticker, CMP with as-of time, 2-line thesis, key metrics, entry zone, technical stop-loss, first target, risk:reward (skip if below 1:2), horizon (swing 2-8 weeks or positional 3-12 months), and what would prove the setup wrong. If nothing qualifies, say "no clean setups today" and do not force picks.

## Step 3: Sell / avoid candidates
"Sell" only applies to stocks the user holds. If the user shares holdings (list, CSV, screenshot), label each as hold / trim / exit candidate. Otherwise give an avoid / exit-if-held list from the same universe.

Red flags to check:
- Close below the 200-DMA with lower highs
- Two or more quarters of falling profit or margins
- Rising debt or weak interest coverage
- Promoter pledge above 25% or promoter selling
- Auditor resignation, delayed results, qualified audit opinion, SEBI/ED/CBI action, rating downgrade
- Valuation far ahead of growth
- Persistent FII/MF selling or negative bulk deals

Show 3-5 names with the flags found, the evidence, and the strongest counter-argument. Remind the user to check tax impact (STCG/LTCG) before selling, and verify current rates before quoting them. Cash-segment short selling is intraday only; do not suggest leveraged shorts.

## Step 4: IPO evaluation
Collect from the RHP/prospectus and trackers (Chittorgarh, NSE/BSE IPO pages, Moneycontrol): open/close dates, price band, lot size, issue size, fresh issue vs OFS split, use of proceeds, listing date.

Score out of 100:
- Business quality (20): moat, sector growth, customer concentration
- Financials (25): 3-year revenue/PAT growth, margins, RoNW/ROCE, debt, cash flow; heavy penalty if loss-making
- Valuation (25): P/E or EV/EBITDA vs 2-3 listed peers, market cap to sales
- Issue structure (15): fresh vs OFS (OFS-heavy exits by PE or promoters = caution), use of proceeds, post-issue promoter holding, anchor quality, lock-ins
- Demand signals (15): QIB, NII and retail subscription (QIB on day 3 matters most), anchor book, GMP (unofficial and manipulable, supporting evidence only)

Verdict: Subscribe (long term) / Subscribe for listing gain only / Neutral, skip unless allotted / Avoid. Add a listing-gain view (low/mid/high with reasoning), a long-term view, key risks and key dates. Note that retail allotment is a lottery, so heavy oversubscription means low odds. SME IPOs have large lot sizes and thin liquidity; default to Avoid for beginners unless the case is strong.

## Output format (keep it brief)
1. Market snapshot (3-5 lines)
2. Table: buy-side candidates
3. Table: sell / avoid candidates
4. Table: IPO verdicts for open or upcoming mainboard IPOs (say "none open" if so)
5. Key risks this week
6. Sources list
7. One-line disclaimer: "Screen-based research, not investment advice. I'm not a SEBI-registered adviser; markets carry risk, so verify the data and consider a SEBI-registered adviser."

Keep the whole report to about one page unless the user asks for detail.

## Boundaries
- Never imply certainty or guaranteed returns. Use "candidate", "setup", and "evidence for / against".
- Do not place trades, log into broker accounts, or enter credentials.
- Do not promote F&O, leverage or penny stocks. If F&O comes up, note that SEBI studies have found most individual F&O traders make net losses.
- Ask about holdings, horizon or risk appetite only when it changes the output; otherwise state the assumption used.
- Offer to run this as a scheduled daily scan.
