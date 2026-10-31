---
name: india-market-scanner
description: Scan NSE/BSE for buy and sell/avoid candidates, build a budget plan ('invest Rs 2000 today'), and sort IPOs into listing-gain vs long-term. Use for 'scan the market', 'what to buy', 'which IPO'.
---

# India Market Scanner

Research workflow for NSE/BSE. It produces evidence-based screen results and illustrative plans, not personalised advice. Claude is not a SEBI-registered investment adviser.

## Pick a mode

| The user says | Mode | Steps |
|---|---|---|
| "scan the market", "what to buy" (no amount) | Scan | 1, 2, 3, 5 |
| "I want to invest 2000 today", "I have 10k to invest", "build a portfolio with..." | Budget plan | 1 (two lines), 2, 4 |
| "what should I sell", pastes holdings | Sell check | 3 |
| "which IPO", "is X IPO worth it", "IPO for listing gain / long term" | IPO desk | 5 |

If the request is unclear, run Scan.

## Ground rules
- Get the current date and time in IST first. NSE/BSE cash market runs 9:15-15:30 IST, Mon-Fri, except exchange holidays. If the market is closed, say all prices are the last close.
- Every number must come from a source retrieved in this session (WebSearch, WebFetch, or a browser when a site needs rendering). The shell usually cannot reach market sites. Never fill in prices, PE, GMP, flows, charges or limits from memory. If a figure cannot be verified, write "not verified" or drop the item.
- Cross-check price and key ratios against two sources where possible (NSE/BSE official pages, Screener.in, Moneycontrol, Trendlyne, Tickertape). Show an "as of" time. Free sites can lag by up to 15 minutes.
- Prefer primary sources: exchange filings, company results, SEBI-filed RHP/DRHP, NSE/BSE bulk and block deal data. Treat social-media tips and "target price" headlines as noise.
- Search each distinct stock, sector or IPO separately.
- Write amounts in rupees with Indian grouping (Rs 1,00,000). Recompute every quantity, total and percentage with code or a calculator before showing it.

## Step 1: Market snapshot (always first)
Nifty 50, Sensex, Bank Nifty, Nifty Midcap and Smallcap: level and day/week change. India VIX. FII and DII net cash flows (latest session and 5-day). Advance/decline ratio. Best and worst sectors. Global cues: US indices, Brent crude, USD/INR, US 10Y yield. Events within the next week: RBI, major results, Fed, F&O expiry. End with a one-line regime read (risk-on / mixed / risk-off) and why. In Budget plan mode, keep this to two lines.

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

## Step 4: Budget plan ("I want to invest Rs X today")
Input: the amount. Ask once if it is missing. Unless told otherwise, assume and state: delivery (CNC) buy, 3-12 month horizon, moderate risk.

Feasibility checks first:
- NSE/BSE direct equity trades in whole shares: quantity = floor(allocation / entry price). Skip candidates whose single share costs more than their allocation, and say so. A low price per share is not a low valuation; never pick a stock because it is cheap per share.
- Charges (brokerage, STT, exchange and DP charges, GST, stamp duty) take a bigger bite from small amounts. Look up the user's broker schedule or a current brokerage calculator; do not quote rates from memory. Show estimated round-trip charges in rupees and as a % of the budget. If above about 2%, say so and offer a lower-cost route: one position, a Nifty 50 ETF, or an index-fund SIP.
- Number of positions: under Rs 5,000 use 1 stock (2 at most) or one ETF; Rs 5,000-25,000 use 2-3; Rs 25,000-1,00,000 use 3-5; above Rs 1,00,000 use 4-8 and consider a core ETF or index-fund slice.
- Concentration: with 3 or more positions, cap any one at 40% of the budget and take at most 2 names from one sector.
- Never use margin, leverage, F&O or intraday for a budget plan.

Allocation:
1. Start from the Step 2 candidates scoring 70 or more (run Step 2 if it has not been run today).
2. Choose up to the allowed number of positions, favouring different sectors and different reasons to own them.
3. Weight roughly by score within the caps, round each position down to whole shares, then give leftover cash to the best-scoring affordable candidate that still fits. Report unspent cash. Rounding example (arithmetic only): Rs 2,000 and a Rs 640 share gives 3 shares = Rs 1,920, with Rs 80 unspent.
4. For each position give entry zone, stop-loss, first target and a one-line reason. Suggest limit orders inside the entry zone and no chasing above it. If the market is closed, the plan is for the next session using last-close prices, and the open can gap.
5. Worst case: sum of quantity x (entry - stop) in rupees and as a % of the budget. Flag it if above about 10%.

If no candidate scores 70 or none is affordable, say so. Do not force a buy to use up the budget; offer the ETF or index-fund route, or waiting.

## Step 5: IPO desk (listing gain vs long term)
Cover mainboard IPOs that are open or upcoming, plus any closed IPO listing soon (applications are shut, so give a listing view only). SME IPOs: default to Avoid (large lot sizes, thin liquidity) unless asked.

Collect from the RHP/prospectus and trackers (Chittorgarh, NSE/BSE IPO pages, Moneycontrol): open, close, allotment and listing dates; price band; lot size and lot cost at the upper band; issue size; fresh issue vs OFS split; use of proceeds; anchor investors; live QIB/NII/retail subscription by day; GMP trend; and how the last 5-10 mainboard IPOs listed.

Score every IPO on two tracks, each out of 100.

Listing-gain track (pop on listing day):
- Subscription demand (35): final-day QIB and NII multiples matter most. Compare with recent IPOs of similar size, since late QIB surges are normal.
- Valuation vs listed peers (20): priced at or below peers leaves room; priced above leaves little.
- Anchor book quality (15): size and quality of the institutional anchors.
- Issue size and market mood (20): smaller issues oversubscribe more easily. Weigh Nifty trend, India VIX and recent listing outcomes.
- GMP trend (10): a steady multi-day trend counts for more than a one-day spike. GMP is unofficial and can be manipulated, so it is supporting evidence only.

Long-term track (hold 1-3+ years):
- Business quality (25): moat, sector growth, customer concentration.
- Financials (25): 3-year revenue/PAT growth, margins, RoNW/ROCE, debt, cash flow; heavy penalty if loss-making.
- Valuation (20): P/E or EV/EBITDA vs 2-3 listed peers, market cap to sales.
- Issue structure and governance (20): fresh issue vs OFS (large PE or promoter exits are a caution), use of proceeds, post-issue promoter holding, related-party deals, litigation.
- Risk profile (10): lower regulatory, cyclical and concentration risk scores higher.

Verdict (one per IPO):
- Listing-gain play: listing track 70 or more and long-term track below 60.
- Long-term hold: long-term track 70 or more and listing track below 60. A long-term case does not require applying in the IPO; the stock can usually be bought after listing, sometimes cheaper.
- Both: both tracks 70 or more.
- Neutral: skip unless allotted.
- Avoid.

For every IPO give a listing outlook (low / mid / high case with reasoning, never a single promised number) and an exit plan. Listing-gain plays: a sell-on-listing rule decided in advance, plus a stop. Long-term holds: what to monitor (quarterly results, lock-in expiries, promoter and anchor selling).

Budget fit: the minimum application is one lot x the upper price band, and many mainboard lots cost far more than a small budget. If the user's amount cannot fund a lot, say so plainly; do not suggest SME IPOs or borrowing to bridge the gap. Retail applications have a cap (verify the current limit). Retail allotment is by lottery: at N times retail subscription the odds are roughly 1 in N per application, so heavy oversubscription means low odds. Give the apply-by deadline, including the UPI mandate approval cutoff.

## Output format (keep it brief)

**Scan mode**
1. Market snapshot (3-5 lines)
2. Table: buy-side candidates
3. Table: sell / avoid candidates
4. IPO tables: "Listing-gain plays" and "Long-term holds" (say "none open" if so)
5. Key risks this week
6. Sources, then the disclaimer

**Budget plan mode**
1. One line: amount, assumptions, as-of time
2. Table: Stock | CMP | Qty | Amount | % of budget | Why | Stop-loss | Horizon
3. Totals: invested, unspent cash, estimated round-trip charges, worst-case loss if all stops hit
4. Why this mix (2-3 lines) and what would change the plan
5. Sources, then the disclaimer

**IPO desk mode**
1. Table: IPO | Dates and listing | Price band / lot cost | Verdict | Listing score | Long-term score | Why (2 lines) | Key risk | Action and deadline
2. Sources, then the disclaimer

Disclaimer line: "Screen-based research, not investment advice. I'm not a SEBI-registered adviser; markets carry risk, so verify the data and consider a SEBI-registered adviser."

Keep the whole report to about one page unless the user asks for detail.

## Boundaries
- Never imply certainty or guaranteed returns. Use "candidate", "setup", "illustrative allocation" and "evidence for / against". Never write "you should buy".
- Do not place trades, log into broker accounts, or enter credentials.
- Do not promote F&O, leverage, intraday or penny stocks. If F&O comes up, note that SEBI studies have found most individual F&O traders make net losses.
- Remind the user to invest only money they can leave invested for the horizon, and never push them to deploy the full budget.
- Ask about holdings, horizon or risk appetite only when it changes the output; otherwise state the assumption used.
- Offer to run this as a scheduled daily scan.
