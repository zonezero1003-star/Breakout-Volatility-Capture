#  Breakout Volatility Capture
### Bitget AI Hackathon S1 Submission

> An autonomous BTC breakout trading strategy built on **Bitget Playbook** — no code, no manual intervention, just a thesis described in plain English and deployed as a live agent.

🔗 **Live Strategy Demo:** [getagent.studio/strategy/6630a7e7-88fd-4221-b794-e5fe2aa474ab](https://getagent.studio/strategy/6630a7e7-88fd-4221-b794-e5fe2aa474ab)

---

##  Overview

| Field | Detail |
|---|---|
| **Strategy Name** | Breakout Volatility Capture |
| **Market** | BTCUSDT — Bitget USDT-Margined Perpetual Futures |
| **Tool Used** | Bitget Playbook |
| **Status** | Live Paper Trading (since Jun 22, 2026) |
| **Leverage** | 5× |
| **Margin Budget** | $200 per trade |
| **Asset Class** | Crypto Futures |

---

##  Why I Built It

BTC perpetual futures markets follow a recognizable rhythm: extended periods of low-volatility consolidation, followed by sharp, directional impulse moves. Most traders either miss these breakouts entirely or chase them too late — entering at the tail of the move rather than the beginning.

I built this strategy to systematically identify the **compression phase before the move** and enter early, capturing the bulk of the impulse rather than the tail. The goal was to turn a pattern I had observed manually into a disciplined, rules-based agent that executes without hesitation or emotional override.

The entire strategy was described in natural language and deployed through **Bitget Playbook** — no manual coding required. This made it possible to iterate quickly on the thesis without getting lost in implementation details.

---

## Core Thesis

> When price compresses into a tight range with declining volatility, it signals equilibrium between buyers and sellers — a coiled spring. The resolution of that tension tends to be fast and directional.

Markets alternate between consolidation and expansion. This strategy identifies consolidation, waits for a confirmed breakout, and enters in the direction of the move — capturing the initial impulse and the measured continuation that typically follows.

---

## 📡 Why Does the Strategy Work? Signals & Decision Logic

The strategy is grounded in **technical price structure**, not discretion. Here's how each signal contributes:

### Indicators Used

| Signal | Parameter | Role |
|---|---|---|
| **Highest High / Lowest Low** | `consolidation_period = 20` | Defines the resistance/support range boundary over a 20-bar lookback |
| **Bollinger Bands** | `bb_period = 20`, `bb_std = 2.0` | Confirms volatility compression — when bands narrow, the coiled spring is tightening |
| **Volume vs. Volume MA** | `volume_multiplier = 1.5×`, `volume_ma_period = 20` | Validates that a breakout is genuine and not a low-conviction fakeout |
| **ATR** | `atr_period = 14` | Sizes the stop loss dynamically relative to current volatility — wider stops in volatile conditions, tighter in calm conditions |

### How Decisions Are Made

**Entry:**
- **Long:** Price closes *above* the 20-bar highest high AND current volume ≥ 1.5× the 20-bar average volume
- **Short:** Price closes *below* the 20-bar lowest low AND current volume ≥ 1.5× the 20-bar average volume

Bollinger Band narrowing must also be present at entry, confirming we are entering a breakout from compression — not a random price spike.

**Exit:**
- **Take Profit:** Entry price ± the full height of the consolidation range (measured move). This targets the natural extent of a breakout impulse.
- **Stop Loss:** Placed *inside* the broken range. If price re-enters the range after breaking out, the breakout signal is invalidated, and the trade is exited to preserve capital.

No discretionary overrides. Every entry and exit is rule-based and executed autonomously.

---

## Risk Management

- Fixed position size: **0.015 BTC** per trade — consistent across all setups
- Leverage: **5×** — meaningful amplification without extreme exposure
- Margin budget: **$200** — defined maximum at-risk capital per position
- ATR-based dynamic stop prevents oversized losses in high-volatility regimes
- One position at a time — no pyramiding, no overlapping trades
- Stop placement logic automatically invalidates trades if the breakout fails (price re-enters the range), preventing the strategy from holding through full reversals

---

##  Performance (May – Jun 2026)

| Metric | Result |
|---|---|
| **Total Return** | +2.7% |
| **Win Rate** | 58% |
| **Profit Factor** | 1.14× |
| **Max Drawdown** | −9.3% |
| **Avg Round Trip Return** | +0.41% |
| **Total Round Trips** | 12 |
| **Avg Hold Time** | 2d 10h |

---

## Full Execution Log

| Direction | Entry Date | Entry Price | Exit Date | Exit Price | Qty (BTC) | P&L (USD) | Return | Hold Time |
|---|---|---|---|---|---|---|---|---|
| Long | Jun 20 | $63,922 | Jun 22 | $63,866 | 0.015 | −$1.79 | −0.09% | 1d 10h |
| Long | Jun 15 | $67,245 | Jun 18 | $62,340 | 0.015 | −$74.54 | −7.29% | 3d 0h |
| Long | Jun 14 | $65,235 | Jun 15 | $66,554 | 0.015 | +$18.79 | +2.02% | 15h |
| Long | Jun 7 | $62,440 | Jun 14 | $64,542 | 0.015 | +$30.57 | +3.37% | 6d 15h |
| Short | Jun 4 | $64,464 | Jun 5 | $61,628 | 0.015 | +$41.60 | +4.40% | 1d 13h |
| Short | Jun 2 | $68,777 | Jun 3 | $65,719 | 0.015 | +$44.87 | +4.45% | 14h |
| Short | Jun 1 | $71,712 | Jun 2 | $69,404 | 0.015 | +$33.55 | +3.22% | 20h |
| Short | May 31 | $73,574 | Jun 1 | $72,879 | 0.015 | +$9.34 | +0.94% | 17h |
| Short | May 29 | $73,120 | May 31 | $74,101 | 0.015 | −$15.81 | −1.34% | 1d 14h |
| Long | May 23 | $77,232 | May 28 | $73,232 | 0.015 | −$61.13 | −5.18% | 4d 7h |
| Short | May 16 | $78,350 | May 22 | $75,819 | 0.015 | +$36.80 | +3.23% | 6d 12h |
| Long | May 14 | $80,908 | May 16 | $78,624 | 0.015 | −$35.46 | −2.82% | 1d 16h |

*All trades paper traded on Bitget USDT-margined perpetual futures. Timestamps in UTC.*

---

##  Key Observations

- **Short trades significantly outperformed longs** during the May–June BTC downtrend, demonstrating the strategy's ability to adapt to both sides of the market without directional bias
- **Best trade:** Short Jun 2 → Jun 3, +4.45% — caught BTC dropping from ~$68.7K to ~$65.7K on strong volume confirmation
- **Worst trade:** Long Jun 15 → Jun 18, −7.29% — entered before a sharp leg down to ~$62K; the strategy did not have a macro trend filter to avoid counter-trend longs in a downtrend
- The **−9.3% max drawdown** occurred during a choppy period where multiple long breakouts failed in quick succession — the primary known weakness of the approach

---

##  Development Challenges & How I Solved Them

### Challenge 1: Fakeout Filtering
**Problem:** Breakout strategies are notoriously vulnerable to false breakouts — price briefly pierces a level then reverses, triggering an entry right before the wrong move.

**Solution:** Added a volume confirmation filter requiring current volume to be ≥ 1.5× the 20-bar average. Low-conviction breakouts (without volume) are ignored. Combined with Bollinger Band narrowing as a prerequisite, this significantly reduced false signals.

### Challenge 2: Stop Loss Placement
**Problem:** Fixed-distance stops get hit too easily in volatile crypto conditions, while ATR-only stops can be too wide in calm conditions.

**Solution:** Used ATR-based dynamic stop placement with the stop anchored *inside the broken range*. This means the stop has structural logic — if price re-enters the range, the breakout thesis is invalidated and we exit regardless of ATR distance.

### Challenge 3: Directional Bias in Trending Markets
**Problem:** During the sustained BTC downtrend from May to June, long breakout signals frequently failed because the macro environment was bearish.

**Solution (identified, not yet implemented):** A higher timeframe trend filter is the clearest next step — avoid longs when the 4H or daily trend is down. This remains the most impactful improvement in the next iteration.

### Challenge 4: Deploying Without Code
**Problem:** Translating a nuanced trading thesis — with conditional logic, indicator combinations, and dynamic risk parameters — into a running live agent without writing any code.

**Solution:** Bitget Playbook's natural language deployment made this possible. The strategy was described as a plain English brief and deployed directly. The iteration cycle was fast — changing parameters required no redeployment, just updating the configuration values.

---

## Completed Features

- [x] Rule-based breakout entry and exit logic (long and short)
- [x] Bollinger Band volatility compression detection as prerequisite
- [x] Volume confirmation filter (1.5× MA threshold)
- [x] ATR-based dynamic stop loss with structural invalidation logic
- [x] Measured move take profit targeting
- [x] Live paper trading on Bitget Playbook (BTCUSDT perpetual futures)
- [x] Full execution history logged — 12 round trips, all timestamped
- [x] Strategy hosted publicly on GetAgent Studio

## Next Steps

- [ ] **Higher timeframe trend filter** — avoid longs during macro downtrends (biggest priority)
- [ ] **Dynamic leverage scaling** — reduce leverage in high-volatility regimes
- [ ] **Multi-asset expansion** — ETHUSDT, SOLUSDT as additional symbols
- [ ] **Funding rate awareness** — avoid longs when perpetual funding rates are deeply negative (a signal of bearish positioning)
- [ ] **Bitget Skill Hub integration** — additional signal layer for enriched entry confirmation
- [ ] **Bitget Agent Hub integration** — connect to on-chain or sentiment data feeds as supplementary filters

---

## Tools & Frameworks

| Tool | Usage |
|---|---|
| **Bitget Playbook** | Strategy deployment, parameter configuration, and live paper trading — primary tool |
| **GetAgent Studio** | Strategy hosting and live public demo |
| **Bollinger Bands** | Native Playbook indicator — volatility compression detection |
| **ATR (Average True Range)** | Native Playbook indicator — dynamic stop loss sizing |
| **Volume MA** | Native Playbook indicator — breakout confirmation filter |
| **Bitget Skill Hub** | Planned integration for additional signal enrichment |
| **Bitget Agent Hub** | Planned integration for external data feeds |

---

##  Experience with Bitget AI Tools

**What worked well:**
- Bitget Playbook's natural language interface removed the biggest barrier to algo trading — the need to code. Describing a thesis in plain English and having it deploy as a live strategy is a genuinely different way to think about strategy development.
- Parameter configuration was fast and intuitive. Changing `volume_multiplier` or `consolidation_period` required no redeployment.
- GetAgent Studio provided clean, public-facing strategy pages with live NAV tracking and execution history — exactly what's needed for transparent sharing and review.

**Suggestions for improvement:**
- A **higher timeframe context layer** in Playbook would be valuable — the ability to reference daily or weekly trend direction as a filter for intraday signals without needing a separate agent.
- **Post-trade analytics** (breakdown of win rate by direction, time of day, volatility regime) would help identify where a strategy is underperforming without manual calculation.
- Funding rate data as a native Playbook signal would allow crypto-specific risk management natively.

**Views on the future of Agentic Trading:**
The most important shift happening right now is the separation of *strategy thinking* from *implementation* — Bitget Playbook is an early example of this. As these tools mature, the competitive edge in trading will increasingly come from thesis quality and risk management discipline, not from who can write the best backtest framework. That's a meaningful democratization. The next frontier is agents that can adapt their parameters autonomously in response to regime changes — not just execute fixed rules, but recognize when the environment has shifted and adjust accordingly.

---

## Required Links

| Item | Link |
|---|---|
| **Live Strategy (GetAgent Studio)** | [getagent.studio/strategy/6630a7e7-88fd-4221-b794-e5fe2aa474ab](https://getagent.studio/strategy/6630a7e7-88fd-4221-b794-e5fe2aa474ab) |
| **Bitget Campaign Registration** | [bitget.com/campaigns/d8a2…](https://bitget.com/campaigns/d8a2) |
| **GitHub Repo / Execution Logs** | *(add your GitHub link here)* |
| **Project Post (with #BitgetHackathon + @BitgetAI)** | [x.com/princesschi99/status/2070089910535454890](https://x.com/princesschi99/status/2070089910535454890) |
| **Repost of Official Campaign Post** | [x.com/princesschi99/status/2070090808703733967](https://x.com/princesschi99/status/2070090808703733967) |
| **Demo Video (if required)** | *(add YouTube or public X video link here)* |

---

## Bitget AI Hackathon S1

Built for the **Bitget AI Hackathon S1** — a competition where traders describe their strategy ideas in plain English and Bitget AI brings them to life.

**$50,000 USDT in prizes. No coding required. Just a thesis.**

`#BitgetHackathon` `@BitgetAI`

---

*Paper trading since Jun 22, 2026 · Strategy by Tony · BTCUSDT Perpetual Futures · Bitget Playbook v1*
