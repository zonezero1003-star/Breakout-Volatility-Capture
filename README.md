# 🚀 Breakout Volatility Capture
### Bitget AI Hackathon S1 Submission

> An autonomous BTC breakout trading strategy built on **Bitget Playbook** — no code, just a thesis described in plain English.

---

## 📌 Overview

**Strategy Name:** Breakout Volatility Capture  
**Market:** BTCUSDT — Bitget USDT-Margined Perpetual Futures  
**Tool Used:** Bitget Playbook  
**Status:** Live Paper Trading (since Jun 22, 2026)  
**Leverage:** 5×  
**Margin Budget:** $200 per trade  
**🔗 Live Strategy:** [View on GetAgent Studio](https://getagent.studio/strategy/6630a7e7-88fd-4221-b794-e5fe2aa474ab)  

---

## 💡 Why I Built It

BTC perpetual futures markets follow a repeating pattern: extended periods of low-volatility consolidation, followed by sharp directional impulse moves. Most traders either miss these breakouts entirely or chase them too late.

I built this strategy to systematically identify the **compression phase before the move** — entering early and capturing the bulk of the impulse rather than the tail.

The entire strategy was described in natural language and deployed through **Bitget Playbook** with zero manual coding.

---

## 🧠 Core Thesis

> When price compresses into a tight range with declining volatility, it signals equilibrium between buyers and sellers — a coiled spring. The resolution of that tension tends to be fast and directional.

Markets alternate between consolidation and expansion. This strategy identifies consolidation, waits for confirmation, and enters in the direction of the breakout.

---

## 📡 Signals & Indicators

| Signal | Parameter | Role |
|---|---|---|
| **Highest High / Lowest Low** | `consolidation_period = 20` | Defines resistance/support range boundary |
| **Bollinger Bands** | `bb_period = 20`, `bb_std = 2.0` | Confirms volatility compression when bands narrow |
| **Volume vs Volume MA** | `volume_multiplier = 1.5×`, `volume_ma_period = 20` | Validates breakout is genuine, filters fakeouts |
| **ATR** | `atr_period = 14` | Sizes stop loss dynamically relative to volatility |

---

## ⚙️ Entry & Exit Logic

### Entry
- **Long:** Price closes *above* the 20-bar highest high + volume spike ≥ 1.5× average volume
- **Short:** Price closes *below* the 20-bar lowest low + volume spike ≥ 1.5× average volume

### Exit
- **Take Profit:** Entry ± full consolidation range height (measured move target)
- **Stop Loss:** Placed *inside* the broken range — if price re-enters the range, the breakout is invalidated

---

## 🛡️ Risk Management

- Fixed position size: **0.015 BTC** per trade
- Leverage: **5×**
- Margin budget: **$200**
- ATR-based dynamic stop placement prevents oversized losses in volatile conditions
- No pyramiding — one position at a time

---

## 📊 Performance (May – Jun 2026)

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

## 📋 Full Execution History

| Direction | Entry | Exit | P&L | Return | Hold Time |
|---|---|---|---|---|---|
| Long | Jun 20 @ 63,922 | Jun 22 @ 63,866 | −$1.79 | −0.09% | 1d 10h |
| Long | Jun 15 @ 67,245 | Jun 18 @ 62,340 | −$74.54 | −7.29% | 3d 0h |
| Long | Jun 14 @ 65,235 | Jun 15 @ 66,554 | +$18.79 | +2.02% | 15h |
| Long | Jun 7 @ 62,440 | Jun 14 @ 64,542 | +$30.57 | +3.37% | 6d 15h |
| Short | Jun 4 @ 64,464 | Jun 5 @ 61,628 | +$41.60 | +4.40% | 1d 13h |
| Short | Jun 2 @ 68,777 | Jun 3 @ 65,719 | +$44.87 | +4.45% | 14h |
| Short | Jun 1 @ 71,712 | Jun 2 @ 69,404 | +$33.55 | +3.22% | 20h |
| Short | May 31 @ 73,574 | Jun 1 @ 72,879 | +$9.34 | +0.94% | 17h |
| Short | May 29 @ 73,120 | May 31 @ 74,101 | −$15.81 | −1.34% | 1d 14h |
| Long | May 23 @ 77,232 | May 28 @ 73,232 | −$61.13 | −5.18% | 4d 7h |
| Short | May 16 @ 78,350 | May 22 @ 75,819 | +$36.80 | +3.23% | 6d 12h |
| Long | May 14 @ 80,908 | May 16 @ 78,624 | −$35.46 | −2.82% | 1d 16h |

---

## 🔍 Key Observations

- **Short trades significantly outperformed longs** during the May–June BTC downtrend, highlighting the strategy's ability to adapt to both directions
- **Best trade:** Short Jun 2 → Jun 3, +4.45% (caught the BTC drop from ~$68.7K to $65.7K)
- **Worst trade:** Long Jun 15 → Jun 18, −7.29% (entered before a sharp leg down to ~$62K)
- The −9.3% max drawdown occurred during a period of choppy price action where multiple long breakouts failed — the primary known weakness

---

## ⚠️ Known Risks & Weaknesses

- **Choppy, range-bound markets** — repeated failed breakouts generate a series of small losses
- **Low-volume fakeouts** — volume filter helps but doesn't eliminate all false signals
- **Counter-trend longs in downtrends** — strategy has no higher timeframe trend filter, so it can take longs during sustained bearish macro conditions

---

## ✅ Completed Features

- [x] Rule-based breakout entry/exit logic
- [x] Bollinger Band volatility compression detection
- [x] Volume confirmation filter (1.5× MA threshold)
- [x] ATR-based dynamic stop loss
- [x] Measured move take profit
- [x] Live paper trading on Bitget Playbook
- [x] Full execution history logged (12 round trips)

## 🔲 Next Steps

- [ ] Higher timeframe trend filter (avoid longs in macro downtrends)
- [ ] Dynamic leverage scaling based on volatility regime
- [ ] Multi-asset expansion: ETHUSDT, SOLUSDT
- [ ] Funding rate awareness (avoid longs when funding is deeply negative)
- [ ] Bitget Skill Hub integration for additional signal enrichment

---

## 🛠️ Tools & Frameworks

| Tool | Usage |
|---|---|
| **Bitget Playbook** | Strategy deployment & paper trading |
| **GetAgent Studio** | Strategy hosting & live demo ([View here](https://getagent.studio/strategy/6630a7e7-88fd-4221-b794-e5fe2aa474ab)) |
| **Bitget Agent Hub** | Planned integration for signal layer |
| Bollinger Bands, ATR, Volume MA | Technical indicators (native Playbook config) |

---

## 🏆 Bitget Hackathon S1

This project was built for **Bitget AI Hackathon S1** — a competition where traders describe their strategy ideas in plain English and Bitget AI brings them to life.

**$50,000 USDT in prizes.**  
No coding required. Just a thesis.

🔗 **Live Demo:** [getagent.studio/strategy/6630a7e7-88fd-4221-b794-e5fe2aa474ab](https://getagent.studio/strategy/6630a7e7-88fd-4221-b794-e5fe2aa474ab)  
Register: [bitget.com/campaigns/d8a2…](https://bitget.com/campaigns/d8a2)

`#BitgetHackathon` `@BitgetAI`

---

*Paper trading since Jun 22, 2026 · Strategy by Tony · BTCUSDT · Bitget Playbook v1*
