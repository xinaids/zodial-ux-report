# Zodial UX & Product Feedback Report
### A Real-World Test of Cross-Margin Lending, Risk Engine Clarity, and Onboarding Flow

*By [@0xinaids](https://x.com/0xinaids) — Submitted for the [Superteam Germany x Zodial Bounty](https://earn.superteam.fun/)*
*Testing period: July 14–28, 2026 | 10 days of real usage*

---
## Executive Summary

**15 friction points found. 3 Critical, 5 High, 5 Medium, 2 Low.**

The onboarding funnel breaks at 3 consecutive points before any successful action: the user pays SOL to create an account with no confirmation (FP-3), tries to borrow from the most visible entry point and is silently blocked (FP-8), and hits an unexplained error during deposit with no recovery path (FP-7). A new user following the default path encounters three failures in a row before completing a single successful transaction.

The strongest differentiator Zodial has — tokenized stocks, RWAs, and Tether Gold as collateral alongside crypto — is buried behind an onboarding experience that most users will not survive long enough to discover.

**Three fixes that would immediately move the needle:** fix the Market borrow flow, add tooltips to the risk engine, register with Phantom's verified domain program.

---

## 1. User Profile

**DeFi experience:** Intermediate. I have used DeFi lending protocols before, including a 12-day real-usage test of Hobba (Superteam Balkan bounty, June 2026) covering deposit, borrow, repay, and withdraw flows. General awareness of Kamino, Marginfi, and Jupiter lending markets.

**Role:** Developer and DeFi user. I evaluate products from both a product UX perspective and a technical clarity lens — I notice when error messages lack codes, when nomenclature is inconsistent across components, and when two paths to the same flow behave differently.

**Platforms used:** Hobba (Solana, extended real usage), Kamino (awareness), Marginfi (awareness), Jupiter (regular usage for swaps).

**Testing approach:** I entered Zodial without reading documentation first, using only the interface to navigate. This is intentional — it reflects how most real users onboard and surfaces friction that documentation familiarity would hide.

---

## Landing Page Analysis

**zodial.xyz vs app.zodial.xyz**

The marketing landing page and the application feel like two separate products with no connection between them.

![Zodial landing page — hero section](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/13-landing-page.png)

**What the landing page communicates:**
- "Perfect Portfolio." — a headline with no explanation of what that means in practice
- "DeFi's first direct lending protocol on Solana." — potentially misleading, as Marginfi and Kamino predate Zodial on Solana
- A single "Launch App" CTA
- An email subscription form labeled "Early Access" — which contradicts the fact that the app is already live on mainnet and audited by Ackee

**What is missing:**
- No mention of cross-margin lending — the core differentiator
- No mention of tokenized stocks, RWAs, or Tether Gold as collateral options
- No APY ranges, no TVL, no social proof, no audit badge
- No explanation of what a Portfolio Account is or why creating one costs SOL
- No screenshots or demo of the actual app

**The disconnect:** A user who reads "DeFi's first direct lending protocol on Solana" and clicks Launch App arrives at a raw market table with no continuity from what they just read. The landing page does not prepare the user for the app, and the app does not reference the landing page.

**Suggested improvement:** Before the CTA, the landing page should show:
1. What cross-margin means vs isolated positions — one sentence and a visual
2. Which assets are available as collateral (TSLA, NVDA, SpaceX, SOL, BTC, XAUT)
3. Current APY ranges and TVL as trust signals
4. The Ackee audit badge — currently only visible in the app footer

---

## 2. First Impressions

**What the first 5 minutes felt like:**

After connecting my Phantom wallet, the app redirected me directly to the Market Overview page — a dense table of assets, APYs, utilization rates, and tranches. There was no welcome message, no "start here" prompt, no suggested first action.

My immediate reaction was: *where do I go?*

![First screen after wallet connect — raw market table with no onboarding](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/01-market-no-onboarding.png)

On Hobba, the first screen after wallet connect was a loan simulator that explained the core concept before asking me to do anything. On Zodial, the first screen assumed I already knew what a cross-margin portfolio account was, what tranches meant, and why there were two versions of USD Coin listed side by side.

**What was immediately clear:**
The asset list and market data are well-organized. Seeing tokenized stocks (TSLA, NVDA, MSTR, SpaceX) alongside crypto and stablecoins immediately communicated that this is not a standard lending protocol — that differentiation is striking and genuine.

**What was confusing:**
The concept of "Portfolio Account" is central to everything, but it appears only as a small button in the top-right corner labeled "+ New Account." There is no explanation of what a Portfolio Account is, why it costs SOL to create, or what happens after creation.

I clicked "+ New Account," paid ~0.017 SOL in transaction fees, confirmed in Phantom — and the app returned to the exact same Market page with no confirmation message, no success state, no next step.

**What made me want to continue:**
The asset variety. Borrowing against tokenized SpaceX shares or Tesla xStock as collateral is genuinely novel. Once I understood the cross-margin concept — your entire portfolio as one balance sheet — the value proposition became clear and compelling. It just took longer than it should have to get there.

---

## 3. Friction Points

### FP-1 — No Onboarding After Wallet Connect

**What happened:** After connecting Phantom, the app landed directly on the Market Overview — a full table of assets, APYs, tranches, and utilization rates. No welcome flow, no explanation of what a Portfolio Account is, no suggested first action.

![Market Overview as landing screen — no onboarding flow](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/01-market-no-onboarding.png)

**Why it caused friction:** The core concept of Zodial — cross-margin lending using your entire portfolio as one balance sheet — is not intuitive for users coming from isolated-position protocols like Kamino or Marginfi. Dropping a new user into a raw market table without context means they have to reverse-engineer the product before they can use it.

**Severity:** Critical

**Suggested improvement:** After wallet connect, show a 3-step modal: (1) what Zodial does in one sentence, (2) create your Portfolio Account, (3) make your first deposit. The Market page should be a secondary destination, not the entry point.

**Expected impact:** Reduces time-to-first-deposit significantly. Users who understand the product before interacting with it are less likely to abandon at the Portfolio Account creation step.

---

### FP-2 — "New Domain" Warning on Every Transaction

**What happened:** Every single transaction — account creation, deposit, borrow — triggered a yellow warning banner in Phantom: "Este domínio é novo. Prossiga apenas se confiar neste site."

![Phantom showing "new domain" warning on every transaction](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/02-phantom-new-domain-warning.png)

**Why it caused friction:** Zodial is audited by Ackee Blockchain Security and live on mainnet. A "new domain" warning on every confirmation screen directly contradicts the trust signals the protocol displays in its own footer. This affects every transaction, for every user, permanently — until the domain is registered with Phantom's verified program.

**Severity:** High

**Suggested improvement:** Register the domain with Phantom's verified domain program. This is a one-time fix that eliminates a trust-breaking signal on every user transaction permanently.

**Expected impact:** Removes friction at the highest-stakes moments in the user journey.

---

### FP-3 — No Confirmation After Paying to Create Account

**What happened:** I clicked "+ New Account," paid ~0.017 SOL in transaction fees, confirmed in Phantom, and the app returned silently to the same Market Overview page. No success message, no "your account was created," no next step suggested.

![App returned to same screen after account creation — no confirmation](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/03-no-confirmation-after-account.png)

**Why it caused friction:** The user just paid real money for an action. The absence of any confirmation creates immediate uncertainty — did it work? Did I lose SOL for nothing? I only discovered the account existed by navigating to Portfolio manually.

**Severity:** High

**Suggested improvement:** After successful account creation, show a confirmation state with: account address, a "Make your first deposit" CTA, and the borrowing power that will unlock after depositing.

**Expected impact:** Eliminates post-payment anxiety. Converts a confusing dead-end into a natural next step.

---

### FP-4 — Inconsistent Asset Naming Across the Same Modal

**What happened:** Within the Deposit modal, the asset name changed between interactions. On first open it displayed "Wrapped SOL." After typing an amount and re-opening, it displayed "SOLANA." The Market table shows "Wrapped SOL (SOL)." The Portfolio page shows "SOL."

**Why it caused friction:** SOL and wSOL are technically different assets. A developer or experienced DeFi user notices this immediately and wonders which one is actually being deposited.

**Severity:** Low

**Suggested improvement:** Standardize on one name across all surfaces. "SOL (Wrapped)" with a tooltip explaining the wrapping happens automatically.

**Expected impact:** Removes a small but persistent source of doubt for technical users.

---

### FP-5 — Deposit Modal Shows No Post-Deposit Impact

**What happened:** The Deposit modal shows the amount being deposited and its USD value. Nothing else. After clicking Deposit, the user has no idea what borrowing power they will have, what APY they will earn, or what their portfolio health will look like.

**Why it caused friction:** In a cross-margin protocol, the deposit is not just a deposit — it is collateral that unlocks borrowing capacity across multiple assets simultaneously. That context is invisible at the moment of decision.

**Severity:** Medium

**Suggested improvement:** Add a preview section to the Deposit modal showing: estimated borrowing power unlocked, deposit APY, and resulting portfolio health after deposit.

**Expected impact:** Users understand what they are gaining before confirming.

---

### FP-6 — Amount Discrepancy Between Modal and Phantom

**What happened:** I entered 0.8 SOL in the Deposit modal. The modal confirmed "You will deposit 0.8 SOL ($60.79)." The Phantom confirmation screen showed -0.819022 SOL — a difference of ~0.019 SOL (~$1.44) with no explanation anywhere in the Zodial interface.

| Zodial modal | Phantom confirmation |
|---|---|
| ![Deposit modal showing 0.8 SOL](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/08-deposit-modal-08sol.png) | ![Phantom asking for 0.819 SOL](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/09-phantom-0819sol.png) |

**Why it caused friction:** The user agreed to deposit 0.8 SOL. Phantom is asking them to sign for 0.819 SOL. Without an explanation, this looks like a hidden fee or a rounding error in the protocol's favor.

**Severity:** High

**Suggested improvement:** Before the wallet confirmation, show a transaction breakdown: deposit amount, estimated network fee, wSOL wrapping cost, and total SOL leaving the wallet. *A number users cannot verify is a number users will not trust.*

**Expected impact:** Users confirm transactions with full information.

---

### FP-7 — "Unexpected Error" With No Code, No Cause, No Recovery Path

**What happened:** Multiple deposit attempts returned a red "Unexpected error" message at the bottom of the Deposit modal. The error persisted across retries with different amounts (0.8 SOL, 0.79 SOL, 0.7 SOL) and across both the Market and Portfolio entry points. No error code, no explanation of what failed, no suggestion of what to try next.

![Unexpected error with no code or recovery path](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/04-unexpected-error.png)

![Error persisting on retry with different amount](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/05-unexpected-error-retry.png)

> **Reproduction note:** This error was reproduced across multiple attempts on July 14, 2026 with amounts of 0.8, 0.79, and 0.7 SOL. The deposit eventually succeeded on a later retry with no explanation of what changed. Screenshots: assets/screenshots/04-unexpected-error.png and 05-unexpected-error-retry.png.

**Why it caused friction:** The user has already confirmed a transaction in Phantom and is now staring at a two-word error message with no path forward.

**Severity:** Critical

**Suggested improvement:** Every error state should include: a short description of what failed, an error code for support reference, and at least one suggested next action.

**Expected impact:** Users who hit errors do not abandon — they have a clear path to resolution.

> **Root cause confirmed:** On July 15, 2026, the Zodial team disclosed 
> in their official Telegram support channel that a new frontend safety 
> feature introduced around July 14 had not been tested with Phantom wallet, 
> causing transaction failures. This confirms the "Unexpected error" was a 
> real protocol-level bug, not user error. The team deployed a hotfix within 
> hours after community reports.

---

### FP-8 — Borrow From Market Page Silently Fails; Portfolio Page Works

**What happened:** Clicking "Borrow" on any asset in the Market Overview table produced "Unable to borrow right now." with no explanation. Clicking "New Borrow" from the Portfolio page with the same amount on the same asset succeeded immediately.

| Market page — fails silently | Portfolio page — works |
|---|---|
| ![Unable to borrow from Market](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/06-unable-to-borrow-market.png) | ![Borrow success from Portfolio](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/07-borrow-portfolio-success.png) |

**Why it caused friction:** Two entry points exist for the same action. One works. One does not. The broken one is the more prominent one — visible to every user browsing the market table.

**Severity:** Critical

**Suggested improvement:** Either fix the Market borrow flow to respect the selected Portfolio Account, or remove the Borrow buttons from the Market table entirely and route all borrow actions through the Portfolio page.

**Expected impact:** Eliminates the most common conversion failure in the product.

---

### FP-9 — Cross-Margin Terminology Has No Tooltips

**What happened:** After my first deposit, the Portfolio page displayed: "Portfolio Coverage Flow," "LTV mode vs LT liquidation buffer," "Collateral support Impact 0/100," "Borrow fit Efficient 100/100," "Pressure 100/100." None of these terms have tooltips or explanations.

**Why it caused friction:** This is the risk engine — the core technical differentiator of Zodial. It is completely opaque to any user who is not already fluent in cross-margin lending mechanics.

**Severity:** High

**Suggested improvement:** Add tooltips to every metric on the Portfolio Coverage Flow panel. A one-sentence plain-language explanation per metric is sufficient.

**Expected impact:** Users understand their risk position without leaving the app.

---

### FP-10 — Borrow Error Message Inconsistent By Value

**What happened:** When attempting a second borrow of $15, the modal showed a useful yellow warning explaining the 1.5x safety goal. When attempting $20 or $30, the same tranche showed only: "Unable to borrow right now."

**Why it caused friction:** The same underlying condition produces two completely different levels of information depending on the amount entered.

**Severity:** High

**Suggested improvement:** The informative yellow warning should appear for all values that exceed safe borrowing capacity — not just values below a certain threshold.

**Expected impact:** Users understand why they cannot borrow more and what to do next.

---

### FP-11 — P&L Shows Negative After Repay

**What happened:** After repaying $25 USDC, the Account P&L displayed -$24.99 (-224.8%). The number persisted briefly before resetting to $0.

**Why it caused friction:** Repaying debt is a healthy action. Seeing -224.8% P&L immediately after makes the user think they lost money.

**Severity:** Medium

**Suggested improvement:** P&L should separate unrealized asset gains/losses from debt repayment activity. Repaying a borrow should never appear as a negative P&L event.

**Expected impact:** Users feel confident repaying debt.

---

### FP-12 — Rewards Eligibility Hidden Until You Navigate There

**What happened:** The Rewards page shows "Not eligible (< $1.000)" as the first thing after navigating there. The $1,000 minimum net position requirement is not communicated anywhere before the user lands on the page.

**Why it caused friction:** Discovery-by-failure pattern — the requirement should be visible at the point where it is relevant.

**Severity:** Medium

**Suggested improvement:** Show an inline indicator on the Portfolio page: *"Rewards eligibility: $X of $1,000 minimum net position required."*

**Expected impact:** Removes a frustrating gate that currently feels like a trap.

---

### FP-13 — Loop Tab Has No Entry Guidance

**What happened:** The Loop tab opens with all fields empty and no instruction on what to do first.

**Why it caused friction:** Loop is the most complex flow in the product and the one with the least guidance.

**Severity:** Medium

**Suggested improvement:** Add a one-line instruction with a worked example: *"Example: Deposit SOL, borrow USDC, loop up to 3x."*

**Expected impact:** Loop adoption increases.

---

### FP-14 — No Alert When LTV Rises Due to Price Movement

**What happened:** Over 9 days of monitoring, SOL dropped ~2% and LTV rose from 50.8% to 51.9% silently. No notification, no banner, no email.

![10-day P&L chart showing position evolution](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/12-pnl-chart-10days.png)

**Why it caused friction:** A user who deposited and stepped away has no way to know their LTV changed without manually checking the app.

**Severity:** High

**Suggested improvement:** Add configurable health alerts when LTV crosses user-defined thresholds (60%, 70%, 80%). Kamino and Marginfi both offer health alerts. This is standard in mature lending protocols.

**Expected impact:** Users manage risk proactively instead of reactively.

---

### FP-15 — Critical Performance Issues Across Desktop and Mobile

**What happened:** I ran Lighthouse audits on Zodial, Kamino, and Marginfi/P0 on July 24, 2026. The results reveal that all three protocols fail Core Web Vitals — but Zodial has a specific mobile LCP issue that represents a safety risk.

**Desktop Lighthouse Comparison:**

| Metric | Zodial | Kamino | Marginfi/P0 |
|---|---|---|---|
| Performance Score | 38/100 🔴 | 1/100 🔴 | 57/100 🟡 |
| LCP | 4.3s 🔴 | 8.9s 🔴 | **1.3s** 🟢 |
| TBT | 2,610ms 🔴 | 4,450ms 🔴 | 14,120ms 🔴 |
| Accessibility | **90/100** 🟢 | 74/100 🟡 | 96/100 🟢 |
| Best Practices | 92/100 🟢 | 54/100 🔴 | **100/100** 🟢 |
| Total Payload | 3,851 KiB | **23,354 KiB** 🔴 | 4,915 KiB |

**Mobile Lighthouse Comparison (Slow 4G):**

| Metric | Zodial | Kamino | Marginfi/P0 |
|---|---|---|---|
| Performance Score | 43/100 🔴 | **Crashed** ❌ | 37/100 🔴 |
| LCP | 13.1s 🔴 | Page stopped responding ❌ | 13.6s 🔴 |
| TBT | 900ms 🔴 | Error ❌ | 2,350ms 🔴 |
| Accessibility | 83/100 🟡 | Error ❌ | **96/100** 🟢 |

*Note: Kamino's mobile Lighthouse audit failed completely — the page stopped responding during the test.*

**WebPageTest Results (Jul 25, 2026 — Desktop, WiFi, Milan):**

| Metric | Score | Status |
|---|---|---|
| Time To First Byte | 0.114s | 🟢 Excellent |
| Start Render | 0.7s | 🟢 Fast |
| First Contentful Paint | 2.181s | 🟡 Acceptable |
| Largest Contentful Paint | 2.349s | 🟢 Passes threshold |
| Cumulative Layout Shift | 0.101 | 🟡 Minor issues |
| Total Blocking Time | 0.906s | 🟡 Needs improvement |
| Total Requests | 205 | 🔴 Very high |
| Page Weight | 4MB | 🔴 Heavy |
| Total Load Time | 4.995s | 🟡 Needs improvement |

**Key finding:** Under ideal conditions (WiFi, low latency), LCP passes at 2.349s — 
within the 2.5s threshold. This contrasts with Lighthouse's 4.3s LCP, which simulates 
throttled conditions. The real-world performance on good connections is acceptable; 
the problem is specifically mobile and slow connections.

**2 serious accessibility issues** were flagged — consistent with the Lighthouse 
mobile accessibility drop from 90 to 83.

**205 total requests and 4MB page weight** explain the slow mobile experience. 
For reference, a well-optimized DeFi app should be under 100 requests and 2MB.

**Why it caused friction:** A mobile LCP of 13.1s means the largest visible content takes 13 seconds to render on a standard 4G connection. For a lending protocol where users may need to act quickly on liquidation risk, this is a safety concern. The mobile Accessibility score dropped from 90 to 83 with specific issues: buttons without accessible names, prohibited ARIA attributes, and insufficient color contrast.

**Severity:** High

**Context:** Performance issues are not unique to Zodial — Kamino scores 1/100 on desktop and crashes on mobile. However, this makes the opportunity clear: **Zodial could be the first cross-margin DeFi protocol on Solana to pass Core Web Vitals.** None of the three do today.

**Suggested improvements:**
1. Reduce unused JavaScript — 1,292 KiB of savings available on desktop
2. Optimize image delivery — 411 KiB savings available
3. Code-split the Trade page — TradingView is the likely source of the bloated payload
4. Prioritize Time to Interactive on Portfolio — the page users need fastest when managing risk

**Expected impact:** Bringing LCP under 2.5s and TBT under 200ms on mobile would meaningfully reduce bounce rate and improve trust for new users.

---

## Mobile Experience

![Mobile view — Market Overview](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/14-mobile-market-view.png)

The mobile layout reorganizes into vertical cards, which is functional, but the data density is significantly reduced — requiring more scrolling to see the same information available on desktop. The Portfolio Coverage Flow panel, which is already under-explained on desktop, is harder to parse on mobile due to limited screen space.

---

## 4. UI/UX and Product Suggestions

### Suggestion 1 — Add Transaction Breakdown Before Wallet Confirmation ⭐ MAIN SUGGESTION

**Problem:** The Deposit modal says "You will deposit 0.8 SOL ($60.79)." Phantom asks the user to sign for -0.819022 SOL. The difference (~0.019 SOL, ~$1.44) is never explained anywhere in the Zodial interface.

This is not a fee transparency issue — it is a trust issue. When the number on screen does not match the number in the wallet, the user's first instinct is that something is wrong with the protocol.

**Proposed solution:**

```
Deposit summary
--------------------------------------
Deposit amount        0.800000 SOL   ($61.72)
wSOL wrapping cost    0.009000 SOL   ($0.69)
Network fee (est.)    0.010022 SOL   ($0.77)
--------------------------------------
Total leaving wallet  0.819022 SOL   ($63.18)
```

**Visual mockup:**

![Deposit Breakdown Mockup — Current vs Proposed](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/10-mockup-breakdown.png)

**Why it matters:** A number users cannot verify is a number users will not trust. This fix costs one UI component and recovers every user who currently abandons at the Phantom confirmation screen.

---

### Suggestion 2 — Fix the Silent Failure on Market Borrow

**Problem:** The Borrow button in the Market Overview table produces "Unable to borrow right now." The Portfolio page borrow flow works correctly. Two entry points, one broken, no indication of which to use.

**Proposed solution:** Either fix the Market borrow flow to respect the selected Portfolio Account, or replace the Market Borrow buttons with a tooltip: *"To borrow, go to your Portfolio page and click New Borrow."*

**Why it matters:** Every user who successfully deposits and then tries to borrow from the Market table is currently being blocked silently.

---

### Suggestion 3 — Add Tooltips to Every Risk Metric

**Problem:** "LTV mode vs LT liquidation buffer," "Portfolio Coverage Flow," "Impact 100/100," "Pressure 100/100" — none of these have explanations.

**Proposed solution:**
- **LTV vs LT:** *"LTV shows how much you can still borrow. LT shows how close you are to liquidation. Always watch LT."*
- **Impact 100/100:** *"Your collateral is fully supporting your current debt."*
- **Pressure 100/100:** *"Adding debt or reducing collateral increases liquidation risk."*

---

### Suggestion 4 — Unify Asset Naming Across All Surfaces

**Problem:** The same asset appears as "SOLANA," "Wrapped SOL," "SOL," and "Wrapped SOL (SOL)" across the Market table, Deposit modal, Portfolio page, and Wallet Balances within the same session.

**Proposed solution:** One canonical name per asset. Suggested: "SOL" with subtitle "Wrapped automatically on deposit."

---

## 5. What Works

**The asset universe is genuinely novel.**
Seeing SpaceX, Tesla, NVIDIA, and Tether Gold alongside SOL and USDC in a single lending market is unlike anything available on Kamino or Marginfi.

**The Portfolio Coverage Flow panel is conceptually strong.**
The "Current Flow Allocation" section showing which asset covers which debt at what effective LTV is a level of transparency that Kamino's isolated markets cannot offer.

**The Trade terminal is unexpectedly sophisticated.**

![Trade terminal with TradingView integration](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/11-trade-terminal.png)

The Trade page combines a full TradingView chart with Auto / Lend / Loop / Swap tabs and a real-time portfolio health panel. For a lending protocol, this is closer to a trading terminal than anything on Kamino or Marginfi.

**The Deleverage flow is genuinely well-designed.**
Executes withdrawal, swap, and repay in a single bundled transaction. Most protocols force the user to do this in 3-4 separate steps.

**The Repay modal offers Wallet vs Collateral funding choice.**
Most lending protocols on Solana do not offer this choice.

**The P&L chart shows position history as visual events.**

![10-day P&L chart](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/12-pnl-chart-10days.png)

Every action — deposit, borrow, repay — appears as a visual event on the timeline. Position history without needing a block explorer.

**The Leaderboard is fully transparent.**
Real-time Net Position, Deposits, Borrows, and 30-day PnL for every user. Kamino and Marginfi have no equivalent.

---

## 6. One-Sentence Test

*Zodial lets you deposit crypto or tokenized stocks, borrow against all of them together as one portfolio, and manage your risk with a live engine that shows exactly how each asset supports your debt — so you never need to lock assets into separate isolated positions like on Kamino or Marginfi.*

---

## Comparison With Other Lending Protocols

| Feature | Zodial | Kamino | Marginfi/P0 |
|---|---|---|---|
| Cross-margin (portfolio as one balance sheet) | ✅ | ❌ | ❌ |
| Tokenized stocks as collateral | ✅ | ❌ | ❌ |
| RWAs / Tether Gold as collateral | ✅ | ❌ | ❌ |
| Health factor alerts | ❌ | ✅ | ✅ |
| Guided onboarding flow | ❌ | ✅ | ✅ |
| Informative error messages | ❌ | ✅ | ✅ |
| Deleverage in single transaction | ✅ | ❌ | ❌ |
| Repay directly from collateral | ✅ | ❌ | ❌ |
| Public leaderboard with real PnL | ✅ | ❌ | ❌ |
| Phantom verified domain | ❌ | ✅ | ✅ |
| Desktop Lighthouse Performance | 38/100 🔴 | 1/100 🔴 | 57/100 🟡 |
| Mobile LCP (Slow 4G) | 13.1s 🔴 | Crashed ❌ | 13.6s 🔴 |
| Core Web Vitals passing | ❌ | ❌ | ❌ |

**Where Zodial is better than Kamino:**
Cross-margin model eliminates isolated positions. One health factor for the entire portfolio vs three separate ones. Kamino's desktop Lighthouse score of 1/100 and complete mobile crash shows Zodial is not uniquely behind on performance.

**Where Zodial is better than Marginfi/P0:**
Tokenized RWAs (stocks, gold) as collateral have no equivalent in Marginfi. Portfolio-level risk visualization is more sophisticated.

**Where Kamino feels better today:**
Onboarding is cleaner. First action is obvious, confirmation flow is consistent, error messages explain what went wrong.

**Where Marginfi/P0 feels better today:**
Error states are more informative. Accessibility score of 96/100 vs Zodial's 83/100 on mobile.

**One feature Zodial has that no competitor offers:**
A public Leaderboard with real-time Net Position, Deposits, Borrows, and 30-day PnL for every user.

**The opportunity:** None of the three protocols pass Core Web Vitals today. Zodial could be the first cross-margin DeFi protocol on Solana to achieve this — a meaningful trust signal for users managing real capital.

---

## Senior Analysis — What Would Make Zodial Unbeatable

**1. The onboarding funnel is broken at every step.**
Account creation costs SOL with no confirmation. Deposit has an unexplained fee discrepancy. Borrow fails from the most prominent entry point. A new user hitting all three in sequence has three consecutive moments of confusion or failure before a single successful action.

**2. The risk engine is the core product but the least legible part of the UI.**
Zodial's entire value proposition is that cross-margin is better than isolated positions. But to feel that benefit, the user needs to understand what the risk engine is showing them. Right now, the most important panel in the app requires the most prior knowledge to read. This is backwards.

**3. There is no notification layer.**
No alerts when LTV rises. No confirmation when account creation succeeds. No email or Telegram alerts. A lending protocol in 2026 with no notification system is a significant trust and safety gap.

**4. Error states are not a product.**
"Unexpected error" and "Unable to borrow right now" are placeholders. Every error should be a designed moment: what happened, why, what to do next.

**5. Performance is a safety issue, not just a UX issue.**
A mobile LCP of 13.1s means users cannot see the most important content for 13 seconds on 4G. For a protocol where users need to act quickly on liquidation risk, this is dangerous. The good news: no competitor passes Core Web Vitals either, making this a genuine opportunity to differentiate.

**6. The landing page and the app are disconnected.**
A user who reads "Perfect Portfolio" on zodial.xyz and clicks Launch App arrives at a raw market table with no continuity. The landing page mentions none of Zodial's actual differentiators — cross-margin, tokenized stocks, RWAs, trade terminal.

**7. The Trade terminal is underexposed.**
The most sophisticated part of Zodial is the least discoverable. A new user going through the default flow will never reach it.

**The three changes that would immediately move the needle:**
1. Fix the Market borrow flow — eliminates the most common conversion failure
2. Add tooltips to every risk metric — makes the core product legible
3. Fix page performance (LCP + TBT) — opportunity to lead the category

---

## Proof of Usage

**Deposit transaction (0.8 SOL):**
`MhTsrTUMdSF6ffbpAvfFPqAk4jfXrDL3igdcqdoDvpKe529YmPgnt98aEu8QHrAWHbVbjjYiWE2Q66779LDGUFP`
https://solscan.io/tx/MhTsrTUMdSF6ffbpAvfFPqAk4jfXrDL3igdcqdoDvpKe529YmPgnt98aEu8QHrAWHbVbjjYiWE2Q66779LDGUFP

**Borrow transaction 1 ($30 USDC):**
`5weQgugN5cWjhvDRirRDXSb45noj7siYEGngVELyGynNUGZnqwR4MwtBhcLrdNFi2DFVUvBVDnrxgbDufNmmTxpT`
https://solscan.io/tx/5weQgugN5cWjhvDRirRDXSb45noj7siYEGngVELyGynNUGZnqwR4MwtBhcLrdNFi2DFVUvBVDnrxgbDufNmmTxpT

**Borrow transaction 2 ($4.37 USDC):**
`2jBhvMeGoDKGQQwAWL4Nn9gupdpPYygX5XfVw6vMZ15kL5uhMQfRhuPQuT1r2EjtZ75zg8jhhidMa1sKCRNbd8fF`
https://solscan.io/tx/2jBhvMeGoDKGQQwAWL4Nn9gupdpPYygX5XfVw6vMZ15kL5uhMQfRhuPQuT1r2EjtZ75zg8jhhidMa1sKCRNbd8fF

**Borrow transaction 3 ($17.04 USDC — total $51.41):**
`2Jdw7V1XFo1UxrPQKKDZnqbcxCWKo5ie8N1AhfXYN8XtNzanrqsXCjyeXSzjZ4p7ESw4tH9sS32FhKFPxPSBfiEV`
https://solscan.io/tx/2Jdw7V1XFo1UxrPQKKDZnqbcxCWKo5ie8N1AhfXYN8XtNzanrqsXCjyeXSzjZ4p7ESw4tH9sS32FhKFPxPSBfiEV

**Repay transaction ($25 USDC):**
`2EDeYT3RsuWFWz2F8BxnfVEhQEJVPfprecB3f9CDtjseTQR6XGLnfd1jEmrUMjCZg6YnWbYb8bWh9g6Vf58gNjv5`
https://solscan.io/tx/2EDeYT3RsuWFWz2F8BxnfVEhQEJVPfprecB3f9CDtjseTQR6XGLnfd1jEmrUMjCZg6YnWbYb8bWh9g6Vf58gNjv5

**Wallet:** `DHG4p1tKiXuQS2oYUMAnxR1P4YDgzGdkQfzJZfYoRnNV`
**Testing period:** July 14–28, 2026

**Position status (Jul 27, 2026 — 24h before deadline):**
- Deposits: 0.8002 SOL ($60.30) — active
- Borrows: 26.41 USDC ($26.41) — active
- Net position: $33.88
- LTV: 52.5% — healthy
- Account P&L: -$0.86 (SOL price movement, position maintained throughout)
- Testing period: 13 days continuous

The 30D chart confirms the full position lifecycle — deposit Jul 14,
peak borrow Jul 14, repay Jul 15, stable monitoring Jul 15–27.

---

## Bonus

**Screen recording:** https://youtu.be/zDwjqCe1wjg

**X thread:** https://x.com/0xinaids/status/2077124328160698826

**Visual mockup (Suggestion 1):**
https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/screenshots/10-mockup-breakdown.png
