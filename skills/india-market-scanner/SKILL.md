---
name: india-market-scanner
description: Beginner-friendly NSE/BSE helper. Gives short, plain-language answers - what to buy or avoid, a plan for a budget ('invest Rs 2000 today'), and whether an IPO is for listing gain or long term. Use for 'scan the market', 'what to buy', 'which IPO'.
---

# India Market Scanner

Made for beginners. The research underneath is careful; the answer the user sees is short, simple and easy. Claude is not a SEBI-registered investment adviser.

## How to answer (read this first)

These rules override every output rule further down.

1. **Answer first.** Line 1 is the answer ("Idea: 1 share of X", "This IPO looks like a listing-gain play", "Nothing looks good today"). Reasons come after.
2. **Very short.** About 100 words for a budget plan or one IPO, about 200 for a market scan. No long reports, no big tables.
3. **Plain words.** Sentences under 15 words. Write like explaining to a friend who has never bought a share. No jargon without a 3-5 word meaning in brackets.
4. **Numbers the user can act on:** how many shares, how much money, the exit price, the worst loss. Skip scores, ratios and indicator names unless asked.
5. **Max 3 ideas** per list. Fewer is fine. Never pad.
6. **Same language as the user.** If they write Hindi or Hinglish, reply in simple Hinglish.
7. **End with one offer:** "Want the full numbers?" Give the detailed breakdown (scores, ratios, extra sources) only if they say yes.
8. **Finish with the one-line disclaimer.** Nothing more.

### Jargon to translate
| Say this | Not this |
|---|---|
| exit price (sell if it falls here) | stop-loss |
| average price of the last 50 / 200 days | 50-DMA / 200-DMA |
| price vs yearly profit (lower = cheaper) | PE |
| big investors (FIIs = foreign, DIIs = Indian funds) | FII/DII flows |
| market mood: calm / mixed / nervous | risk-on / risk-off, VIX |
| listing gain = profit on day one | listing pop |
| long term = hold 1 year or more | positional |
| strong / okay / weak | scores out of 100 |

## Pick a mode

| The user says | Mode | Research steps |
|---|---|---|
| "scan the market", "what to buy" (no amount) | Scan | 1, 2, 3, 5 |
| "I have 2000", "invest 10k today", "which stock should I buy" | Budget plan | 1, 2, 4 |
| "should I sell", pastes holdings | Sell check | 3 |
| "which IPO", "is X IPO good", "listing gain or long term" | IPO desk | 5 |

If the request is unclear, run Scan. Do all research silently, then answer with the short format below.

## Ground rules (research, not shown in detail)
- Get the current date and time in IST first. NSE/BSE trade 9:15-15:30 IST, Mon-Fri, except holidays. If closed, say "prices are from the last close" and name the day.
- Every number must come from a source fetched in this session (WebSearch, WebFetch, or a browser). Never fill prices, PE, GMP, flows, charges or limits from memory. If a number cannot be confirmed, say "couldn't confirm" in plain words, or drop the item.
- Cross-check price and key ratios on two sources where possible (NSE/BSE, Screener, Moneycontrol, Trendlyne, Tickertape, broker sites). Free sites can lag by 15 minutes.
- Prefer exchange filings, company results and SEBI-filed IPO documents. Ignore social-media tips and "target price" headlines.
- Search each stock, sector or IPO separately.
- Write amounts as Rs with Indian grouping (Rs 1,00,000). Recompute every quantity, total and percentage with code before showing it.

## Step 1: Market snapshot
Check Nifty 50, Sensex, Bank Nifty, India VIX, FII/DII flows, best and worst sectors, global cues and events due this week. Show only a one-line mood: "Market is calm / mixed / nervous because ...". In Budget plan mode keep it to that one line.

## Step 2: Buy-side candidates
Universe: Nifty 500 stocks with daily trading above Rs 10 crore. Exclude ASM/GSM, T2T, SME and penny stocks unless asked.

Score out of 100 (internal):
- Trend (30): price above rising 50- and 200-day averages, strength vs Nifty, volume breakout. Penalise stocks more than 20% above the 50-day average.
- Business quality (30): 3-year sales and profit growth, ROE/ROCE above 15%, low debt, cash flow vs profit, latest quarter growth.
- Price (15): PE or EV/EBITDA vs its own history and peers.
- Ownership (15): promoter holding steady, pledge below 10%, big investors buying.
- Catalysts and risks (10): orders, capex, sector tailwind; subtract for legal or regulatory trouble.

Only 70 or more counts as a pick. Map for the user: 70+ "strong", 60-69 "okay", below 60 "weak". Find an entry zone, exit price (technical stop), first target and reward-to-risk (skip if below 1:2 at the entry zone). If nothing qualifies, say "Nothing looks good today" and do not force a pick.

## Step 3: Sell / avoid candidates
"Sell" only applies to stocks the user owns. If they share holdings, label each Keep / Reduce / Exit. Otherwise list stocks to avoid.

Red flags: closed below the 200-day average with lower highs; two or more quarters of falling profit or margins; rising debt; promoter pledge above 25% or promoter selling; auditor exit, delayed results, SEBI/ED/CBI action, rating downgrade; price far ahead of growth; steady selling by big investors.

Remind the user to check tax (STCG/LTCG) before selling, and verify current rates before quoting them. No short selling beyond intraday; no leveraged shorts.

## Step 4: Budget plan ("I want to invest Rs X")
Ask for the amount once if missing. Assume and state: buy and hold (delivery), 3-12 months, moderate risk.

Checks:
- Shares come in whole numbers: quantity = floor(money / price). Skip a stock if one share costs more than its share of the budget. Cheap per share does not mean cheap value.
- Charges bite small amounts harder. Look up the broker's current charges (do not use memory) and show the round-trip cost in rupees. If above about 2% of the budget, say so and suggest one stock, a Nifty 50 ETF or an index-fund SIP.
- How many stocks: under Rs 5,000 pick 1 (2 at most) or one ETF; Rs 5,000-25,000 pick 2-3; Rs 25,000-1,00,000 pick 3-5; above Rs 1,00,000 pick 4-8 plus a core ETF slice.
- With 3 or more stocks, no stock above 40% and no more than 2 from one sector.
- Never suggest margin, leverage, F&O or intraday.

Allocate from Step 2 picks that score 70+. Round down to whole shares and report leftover cash. Use a limit order inside the entry zone and never chase a higher price. If the market is closed, the plan is for the next session and the opening price can jump. Worst case = sum of quantity x (entry - exit price); flag it if above about 10% of the budget.

If nothing scores 70 or nothing is affordable, say so. Do not force a buy just to use up the money. Offer an ETF, an index-fund SIP, or waiting.

## Step 5: IPO desk
Cover open and upcoming mainboard IPOs, plus any closing IPO that lists soon (applications shut, so give a listing view only). SME IPOs: default to Skip (big lots, hard to sell) unless asked.

Collect: open, close, allotment and listing dates; price band; lot size and lot cost at the top price; issue size; fresh issue vs offer for sale; use of money; anchor investors; QIB/NII/retail subscription; GMP trend; how the last 5-10 mainboard IPOs listed.

Score two tracks out of 100 (internal):

Listing gain (profit on day one): subscription demand 35, price vs listed peers 20, anchor quality 15, issue size and market mood 20, GMP trend 10. GMP is unofficial, so it is only supporting evidence.

Long term (hold 1-3+ years): business quality 25, financials 25 (heavy penalty if loss-making), price vs peers 20, issue structure and governance 20 (large promoter or investor exits are a caution), risk 10.

Verdict, in plain words:
- Listing gain: listing 70+ and long term below 60.
- Long term: long term 70+ and listing below 60. Applying is not required; the stock can usually be bought after listing, sometimes cheaper.
- Both: both 70+.
- Neutral or Skip: skip unless already allotted.

Give a low / mid / high listing view with reasons, never one promised number. Listing-gain plays need a sell-on-listing rule and a loss limit. Long-term holds need a "watch" list (results, lock-in end dates, big sellers).

Budget fit: one lot x top price is the minimum. If the budget cannot fund one lot, say it plainly and never suggest SME IPOs or borrowing. Allotment is a lottery: at N times retail subscription, the chance is about 1 in N. Give the last date to apply, including the UPI approval cut-off.

## Output templates (use these shapes, keep them short)

**Budget plan** (about 100 words)
```
Idea: [qty] share(s) of [Stock] at about Rs [price].
Why: [one plain sentence].
Exit if it falls to Rs [price]. Worst loss: about Rs [x].
Leftover: Rs [x]. Cost to buy and sell: about Rs [x].
Market mood: [calm / mixed / nervous] - [one short reason].
Prices are from [day, time].
Want the full numbers?
Sources: [links on one line]
```
If it is a 2-stock plan, repeat the first three lines per stock. If nothing qualifies:
```
Nothing looks good for Rs [x] today.
Safer options: wait for a better setup, or put it in a Nifty 50 index fund.
```

**Scan** (about 200 words)
```
Market mood: [one line].
Ideas to look at:
1. [Stock] - Rs [price] - [one-line reason] - exit below Rs [x]
2. ...
Better to avoid:
1. [Stock] - [one-line reason]
IPOs: [Name] - [Listing gain / Long term / Skip] - [one line]
Biggest risk this week: [one line].
Want the full numbers?
Sources: [links on one line]
```

**Sell check** (one line per holding)
```
[Stock]: Keep / Reduce / Exit - [one-line reason]
Check tax before selling.
```

**IPO desk** (about 100 words per IPO)
```
[IPO name]: [Listing-gain play / Long-term hold / Skip]
Why: [one plain sentence].
Money needed: Rs [lot cost] for 1 lot. Last day to apply: [date].
Chance of allotment: [high / low - about 1 in N].
Risk: [one line].
Want the full numbers?
Sources: [links on one line]
```

Disclaimer (always, one line): "Research, not investment advice. I'm not a SEBI-registered adviser, and you can lose money."

## Boundaries
- Never imply certainty or guaranteed returns. Say "idea", "look at" or "example plan". Never write "you should buy".
- Do not place trades, log into broker accounts, or ask for passwords.
- Do not promote F&O, leverage, intraday or penny stocks. If F&O comes up, say SEBI studies found most individual traders lose money.
- Say once: invest only money you can leave alone for the full period. Never push the user to spend the whole budget.
- Ask about holdings, time period or risk only if the answer changes the result; otherwise state the assumption in a few words.
- If the user asks "why" or "more detail", then show scores, ratios and the full sources.
- Offer to run this as a daily scan.
