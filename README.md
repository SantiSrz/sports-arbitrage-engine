# sports-arbitrage-engine
# Sports Arbitrage Engine

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Code Style: Black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

A modular Python framework designed to consume real-time odds, identify market pricing discrepancies across bookmakers, and detect guaranteed arbitrage opportunities (Surebets) in 2-way and 3-way sports markets.

---

## Features

- **Automated Arbitrage Detection:** Scans decimal odds across major bookmakers and flags mathematical discrepancies.
- **2-Way & 3-Way Market Support:** Native calculations for Head-to-Head (tennis, basketball) and 1X2 (soccer) markets.
- **Optimal Stake Allocation:** Computes stake sizing based on a target bankroll to lock in equal return across all outcomes.
- **Account Health Protection:** Stake rounding algorithm to generate natural wagers, preventing account restrictions.
- **API Consumption Monitor:** Tracks monthly free-tier quotas (`x-requests-remaining`) via headers to prevent overages.

---

## Mathematical Background

An arbitrage opportunity exists when the sum of implied probabilities for all mutually exclusive outcomes in an event is less than 1 (100%):

$$\sum_{i=1}^{n} \frac{1}{O_i} < 1$$

Where:
- $n \in \{2, 3\}$ represents the number of outcomes.
- $O_i$ is the highest available decimal odd for outcome $i$.

The arbitrage margin ($M$) is calculated as:

$$M = 1 - \sum_{i=1}^{n} \frac{1}{O_i}$$

For a target total stake $S_{\text{total}}$, individual stakes ($S_i$) are weighted proportionally:

$$S_i = S_{\text{total}} \times \frac{\frac{1}{O_i}}{\sum_{j=1}^{n} \frac{1}{O_j}}$$

---

## Project Structure

```text
sports-arbitrage-engine/
│
├── config/
│   └── settings.py          # Environment variables & constants
├── core/
│   ├── models.py            # Dataclasses for events, odds, and opportunities
│   ├── calculator.py        # Mathematical formulas and stake distributions
│   └── scanner.py           # Core orchestrator
├── clients/
│   └── odds_api.py          # HTTP client for The Odds API
├── main.py                  # Entrypoint CLI
├── .env.example             # Environment template
├── requirements.txt         # Project dependencies
└── README.md                # Documentation
