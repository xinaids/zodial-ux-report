# Zodial UX & Product Feedback Report

> **13-day real-usage test of cross-margin lending on Solana**
> Submitted for the [Superteam Germany x Zodial Bounty](https://earn.superteam.fun/listings/zodial-ux-bounty/)
> By [@0xinaids](https://x.com/0xinaids) — July 14–28, 2026

---

## Overview

This report documents a 9-day hands-on test of [Zodial](https://zodial.xyz) — a cross-margin DeFi lending protocol on Solana that lets users borrow against their entire portfolio as one balance sheet, including tokenized stocks and RWAs.

Testing was done with real assets, no documentation read upfront, and across all major flows: deposit, borrow, repay, deleverage, loop, swap, rewards, and leaderboard.

---

## Proof of Usage

| Action | Amount | Transaction |
|--------|--------|-------------|
| Deposit | 0.8 SOL | [Solscan ↗](https://solscan.io/tx/MhTsrTUMdSF6ffbpAvfFPqAk4jfXrDL3igdcqdoDvpKe529YmPgnt98aEu8QHrAWHbVbjjYiWE2Q66779LDGUFP) |
| Borrow 1 | $30 USDC | [Solscan ↗](https://solscan.io/tx/5weQgugN5cWjhvDRirRDXSb45noj7siYEGngVELyGynNUGZnqwR4MwtBhcLrdNFi2DFVUvBVDnrxgbDufNmmTxpT) |
| Borrow 2 | $4.37 USDC | [Solscan ↗](https://solscan.io/tx/2jBhvMeGoDKGQQwAWL4Nn9gupdpPYygX5XfVw6vMZ15kL5uhMQfRhuPQuT1r2EjtZ75zg8jhhidMa1sKCRNbd8fF) |
| Borrow 3 | $17.04 USDC | [Solscan ↗](https://solscan.io/tx/2Jdw7V1XFo1UxrPQKKDZnqbcxCWKo5ie8N1AhfXYN8XtNzanrqsXCjyeXSzjZ4p7ESw4tH9sS32FhKFPxPSBfiEV) |
| Repay | $25 USDC | [Solscan ↗](https://solscan.io/tx/2EDeYT3RsuWFWz2F8BxnfVEhQEJVPfprecB3f9CDtjseTQR6XGLnfd1jEmrUMjCZg6YnWbYb8bWh9g6Vf58gNjv5) |

**Total borrowed:** $51.41 USDC ✅
**Wallet:** `DHG4p1tKiXuQS2oYUMAnxR1P4YDgzGdkQfzJZfYoRnNV`

---

## Findings Summary

### Critical
| # | Finding |
|---|---------|
| FP-1 | No onboarding after wallet connect — Market table as landing destination |
| FP-7 | "Unexpected error" with no code, no cause, no recovery path |
| FP-8 | Borrow from Market page silently fails; Portfolio page works |

### High
| # | Finding |
|---|---------|
| FP-2 | "New domain" warning on every transaction despite Ackee audit |
| FP-3 | No confirmation after paying ~0.017 SOL to create account |
| FP-6 | Amount discrepancy between Zodial modal (0.8 SOL) and Phantom (-0.819 SOL) |
| FP-9 | Cross-margin terminology has no tooltips — risk engine is a black box |
| FP-10 | Borrow error message inconsistent by value |

### Medium
| # | Finding |
|---|---------|
| FP-5 | Deposit modal shows no post-deposit impact |
| FP-11 | P&L shows -224.8% after repaying debt |
| FP-12 | Rewards eligibility hidden until you navigate there |
| FP-13 | Loop tab has no entry guidance |

### Low
| # | Finding |
|---|---------|
| FP-4 | Inconsistent asset naming: SOLANA / Wrapped SOL / SOL across same session |

---

## Main Suggestion — Transaction Breakdown Before Wallet Confirmation

The deposit modal says "You will deposit 0.8 SOL." Phantom asks to sign for -0.819 SOL. The ~$1.44 difference is never explained.

**Proposed fix:**

![Deposit Breakdown Mockup](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/deposit-mockup.png)

---

## What Works

- Tokenized stocks (TSLA, NVDA, SpaceX) + Tether Gold as collateral — unique on Solana
- Portfolio Coverage Flow — cross-margin risk visualization not available on Kamino or Marginfi
- Trade terminal with TradingView + Loop + Swap tabs
- Deleverage in a single bundled transaction
- Repay from Wallet or Collateral — no extra step
- Public Leaderboard with real PnL for every user

---

## Links

- 📄 [Full Report](./report.md)
- 🐦 [X Thread](https://x.com/0xinaids/status/2077124328160698826)
- 🎨 [Visual Mockup](./assets/deposit-mockup.png)
- 🏆 [Bounty Listing](https://superteam.fun/earn/listing/learn-how-to-borrow-better-leave-product-feedback-and-earn-with-zodial)
- 🎥 [Video Review](https://youtu.be/zDwjqCe1wjg)
