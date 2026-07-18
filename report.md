# Zodial UX & Product Feedback Report
### A Real-World Test of Cross-Margin Lending, Risk Engine Clarity, and Onboarding Flow

*By @0xinaids — Submitted for the Superteam Germany x Zodial Bounty*
*Testing period: July 14–28, 2026*

---

## 1. User Profile

**DeFi experience:** Intermediate. I have used DeFi lending protocols before, including a 12-day real-usage test of Hobba (Superteam Balkan bounty, June 2026) covering deposit, borrow, repay, and withdraw flows. General awareness of Kamino, Marginfi, and Jupiter lending markets.

**Role:** Developer and DeFi user. I evaluate products from both a product UX perspective and a technical clarity lens — I notice when error messages lack codes, when nomenclature is inconsistent across components, and when two paths to the same flow behave differently.

**Platforms used:** Hobba (Solana, extended real usage), Kamino (awareness), Marginfi (awareness), Jupiter (regular usage for swaps).

**Testing approach:** I entered Zodial without reading documentation first, using only the interface to navigate. This is intentional — it reflects how most real users onboard and surfaces friction that documentation familiarity would hide.

---

## 2. First Impressions

**What the first 5 minutes felt like:**

After connecting my Phantom wallet, the app redirected me directly to the Market Overview page — a dense table of assets, APYs, utilization rates, and tranches. There was no welcome message, no "start here" prompt, no suggested first action.

My immediate reaction was: *where do I go?*

On Hobba, the first screen after wallet connect was a loan simulator that explained the core concept before asking me to do anything. On Zodial, the first screen assumed I already knew what a cross-margin portfolio account was, what tranches meant, and why there were two versions of USD Coin listed side by side.

The interface is visually clean and the data density is appropriate for an experienced DeFi user. But for anyone arriving without prior context, the Market page as a landing destination is a steep entry point.

**What was immediately clear:**
The asset list and market data are well-organized. Seeing tokenized stocks (TSLA, NVDA, MSTR, SpaceX) alongside crypto and stablecoins immediately communicated that this is not a standard lending protocol — that differentiation is striking and genuine.

**What was confusing:**
The concept of "Portfolio Account" is central to everything, but it appears only as a small button in the top-right corner labeled "+ New Account." There is no explanation of what a Portfolio Account is, why it costs SOL to create, or what happens after creation.

I clicked "+ New Account," paid ~0.017 SOL in transaction fees, confirmed in Phantom — and the app returned to the exact same Market page with no confirmation message, no success state, no next step. I did not know if the account had been created until I navigated to the Portfolio tab manually.

**What made me want to continue:**
The asset variety. Borrowing against tokenized SpaceX shares or Tesla xStock as collateral is genuinely novel. Once I understood the cross-margin concept — your entire portfolio as one balance sheet — the value proposition became clear and compelling. It just took longer than it should have to get there.

---

## 3. Friction Points

### FP-1 — No Onboarding After Wallet Connect

**What happened:** After connecting Phantom, the app landed directly on the Market Overview — a full table of assets, APYs, tranches, and utilization rates. No welcome flow, no explanation of what a Portfolio Account is, no suggested first action.

**Why it caused friction:** The core concept of Zodial — cross-margin lending using your entire portfolio as one balance sheet — is not intuitive for users coming from isolated-position protocols like Kamino or Marginfi. Dropping a new user into a raw market table without context means they have to reverse-engineer the product before they can use it.

**Severity:** Critical

**Suggested improvement:** After wallet connect, show a 3-step modal: (1) what Zodial does in one sentence, (2) create your Portfolio Account, (3) make your first deposit. The Market page should be a secondary destination, not the entry point.

**Expected impact:** Reduces time-to-first-deposit significantly. Users who understand the product before interacting with it are less likely to abandon at the Portfolio Account creation step.

---

### FP-2 — "New Domain" Warning on Every Transaction

**What happened:** Every single transaction — account creation, deposit, borrow — triggered a yellow warning banner in Phantom: "Este domínio é novo. Prossiga apenas se confiar neste site."

**Why it caused friction:** Zodial is audited by Ackee Blockchain Security and live on mainnet. A "new domain" warning on every confirmation screen directly contradicts the trust signals the protocol displays in its own footer. For a first-time user who is about to commit real assets, this warning creates genuine hesitation at the worst possible moment.

**Severity:** Medium

**Suggested improvement:** Register the domain with Phantom's verified domain program. This is a one-time fix that eliminates a trust-breaking signal on every user transaction permanently.

**Expected impact:** Removes friction at the highest-stakes moments in the user journey — the exact points where trust matters most.

---

### FP-3 — No Confirmation After Paying to Create Account

**What happened:** I clicked "+ New Account," paid ~0.017 SOL in transaction fees, confirmed in Phantom, and the app returned silently to the same Market Overview page. No success message, no "your account was created," no next step suggested.

**Why it caused friction:** The user just paid real money for an action. The absence of any confirmation creates immediate uncertainty — did it work? Did I lose SOL for nothing? I only discovered the account existed by navigating to Portfolio manually.

**Severity:** High

**Suggested improvement:** After successful account creation, show a confirmation state with: account address, a "Make your first deposit" CTA, and the borrowing power that will unlock after depositing. Turn the success moment into an onboarding moment.

**Expected impact:** Eliminates post-payment anxiety. Converts a confusing dead-end into a natural next step.

---

### FP-4 — Inconsistent Asset Naming Across the Same Modal

**What happened:** Within the Deposit modal, the asset name changed between interactions. On first open it displayed "Wrapped SOL." After typing an amount and re-opening, it displayed "SOLANA." The Market table shows "Wrapped SOL (SOL)." The Portfolio page shows "SOL." The Wallet Balances section shows "Wrapped SOL" with symbol "SOL" and separately "SOLANA" with symbol "SOL."

**Why it caused friction:** SOL and wSOL are technically different assets. A developer or experienced DeFi user notices this immediately and wonders which one is actually being deposited. The inconsistency also erodes confidence in the precision of the interface overall.

**Severity:** Low

**Suggested improvement:** Standardize on one name across all surfaces. "SOL (Wrapped)" with a tooltip explaining the wrapping happens automatically is clearer than alternating between three different labels.

**Expected impact:** Removes a small but persistent source of doubt for technical users and avoids confusion for non-technical users who may not know SOL and wSOL are related.

---

### FP-5 — Deposit Modal Shows No Post-Deposit Impact

**What happened:** The Deposit modal shows the amount being deposited and its USD value. Nothing else. After clicking Deposit, the user has no idea what borrowing power they will have, what APY they will earn, or what their portfolio health will look like.

**Why it caused friction:** In a cross-margin protocol, the deposit is not just a deposit — it is collateral that unlocks borrowing capacity across multiple assets simultaneously. That context is invisible at the moment of decision.

**Severity:** Medium

**Suggested improvement:** Add a preview section to the Deposit modal showing: estimated borrowing power unlocked, deposit APY, and resulting portfolio health after deposit. These numbers already exist in the system — surfacing them at the deposit step makes the action feel meaningful rather than transactional.

**Expected impact:** Users understand what they are gaining before confirming. This directly supports Zodial's core value proposition of portfolio-as-collateral.

---

### FP-6 — Amount Discrepancy Between Modal and Phantom

**What happened:** I entered 0.8 SOL in the Deposit modal. The modal confirmed "You will deposit 0.8 SOL ($60.79)." The Phantom confirmation screen showed -0.819022 SOL — a difference of ~0.019 SOL (~$1.44) with no explanation anywhere in the Zodial interface.

**Why it caused friction:** The user agreed to deposit 0.8 SOL. Phantom is asking them to sign for 0.819 SOL. Without an explanation, this looks like a hidden fee or a rounding error in the protocol's favor. At a minimum it breaks the user's trust in the numbers shown on screen.

**Severity:** High

**Suggested improvement:** Before the wallet confirmation, show a transaction breakdown: deposit amount, estimated network fee, wSOL wrapping cost, and total SOL leaving the wallet. A number users cannot verify is a number users will not trust.

**Expected impact:** Users confirm transactions with full information. Unexpected charges are one of the most common reasons users abandon DeFi protocols permanently after a first bad experience.

---

### FP-7 — "Unexpected Error" With No Code, No Cause, No Recovery Path

**What happened:** Multiple deposit attempts returned a red "Unexpected error" message at the bottom of the Deposit modal. The error persisted across retries with different amounts (0.8 SOL, 0.79 SOL, 0.7 SOL) and across both the Market and Portfolio entry points. No error code, no explanation of what failed, no suggestion of what to try next.

**Why it caused friction:** The user has already confirmed a transaction in Phantom and is now staring at a two-word error message with no path forward. This is the highest-friction moment in the entire onboarding flow — the user has committed capital intent and the protocol responds with silence.

**Severity:** Critical

**Suggested improvement:** Every error state should include: a short description of what failed, an error code for support reference, and at least one suggested next action ("Try a smaller amount," "Check your SOL balance for fees," "Contact support"). The current "Unexpected error" message provides none of these.

**Expected impact:** Users who hit errors do not abandon — they have a clear path to resolution. Support load decreases because users can self-diagnose.

---

### FP-8 — Borrow From Market Page Silently Fails; Portfolio Page Works

**What happened:** Clicking "Borrow" on any asset in the Market Overview table and entering an amount produced "Unable to borrow right now." with no explanation. Clicking "New Borrow" from the Portfolio page with the same amount on the same asset succeeded immediately.

**Why it caused friction:** Two entry points exist for the same action. One works. One does not. The broken one is the more prominent one — it is the button visible to every user browsing the market table. A user who tries the Market path and gets rejected has no reason to know the Portfolio path exists and works.

**Severity:** Critical

**Suggested improvement:** Either fix the Market borrow flow to respect the selected Portfolio Account, or remove the Borrow buttons from the Market table entirely and route all borrow actions through the Portfolio page where the context (account selection, portfolio health) already exists. If both paths must exist, they must behave identically.

**Expected impact:** Eliminates the most common conversion failure in the product. Every user who successfully deposits and then tries to borrow from the Market page is currently being blocked silently.

---

### FP-9 — Cross-Margin Terminology Has No Tooltips

**What happened:** After my first deposit, the Portfolio page displayed: "Portfolio Coverage Flow," "LTV mode vs LT liquidation buffer," "Collateral support Impact 0/100," "Borrow fit Efficient 100/100," "Pressure 100/100," "$49.39 to take on new borrows (LTV)," "$55.56 till liquidation (LT)." None of these terms have tooltips or explanations.

**Why it caused friction:** This is the risk engine — the core technical differentiator of Zodial. It is also completely opaque to any user who is not already fluent in cross-margin lending mechanics. The difference between LTV headroom and LT liquidation buffer is not obvious, and getting it wrong means liquidation.

**Severity:** High

**Suggested improvement:** Add tooltips to every metric on the Portfolio Coverage Flow panel. Priority: LTV vs LT distinction, what "Impact 100/100" means in practice, and what triggers a liquidation. A one-sentence plain-language explanation per metric is sufficient.

**Expected impact:** Users understand their risk position without leaving the app. This is especially critical because Zodial's cross-margin model creates non-obvious interactions between assets — a user needs to understand the display to manage risk correctly.

---

### FP-10 — Borrow Error Message Inconsistent By Value

**What happened:** When attempting a second borrow of $15 via the [P] USDC tranche, the modal showed a yellow warning: "You are already at the safe health target. Current positions meet the 1.5x safety goal, so there is no safe headroom to borrow more without adjusting the target." When attempting $20 or $30, the same tranche showed only: "Unable to borrow right now."

**Why it caused friction:** The yellow warning at $15 is actually useful — it explains why borrowing is blocked and what the constraint is. The red error at $20-30 gives nothing. The same underlying condition produces two completely different levels of information depending on the amount entered, with no logic visible to the user.

**Severity:** High

**Suggested improvement:** The yellow warning with the health target explanation should appear for all values that exceed safe borrowing capacity — not just values below a certain threshold. The informative message should be the default, not the exception.

**Expected impact:** Users understand why they cannot borrow more, what they would need to do to unlock more capacity, and what the protocol's safety logic is. This turns a dead-end into a teachable moment about cross-margin risk management.

---

### FP-11 — P&L Shows Negative After Repay

**What happened:** After repaying $25 USDC, the Account P&L displayed -$24.99 (-224.8%). The number persisted briefly before resetting to $0.

**Why it caused friction:** Repaying debt is a healthy action. Seeing -224.8% P&L immediately after makes the user think they lost money rather than improved their position. The psychological impact of a large negative number after a correct risk management action is significant.

**Severity:** Medium

**Suggested improvement:** P&L should separate unrealized asset gains/losses from debt repayment activity. Repaying a borrow should never appear as a negative P&L event. A tooltip on the P&L metric explaining what it tracks (and what it does not) would also help.

**Expected impact:** Users feel confident repaying debt. A negative P&L after a healthy action creates confusion and erodes trust in the dashboard accuracy at the exact moment the user is doing the right thing.

---

### FP-12 — Rewards Eligibility Hidden Until You Navigate There

**What happened:** The Rewards page shows "Not eligible (< $1.000)" as the first thing after navigating there. The $1,000 minimum net position requirement is not communicated anywhere before the user lands on the page.

**Why it caused friction:** A user who built a position expecting to earn referral rewards discovers the eligibility gate only after navigating to Rewards. This is a discovery-by-failure pattern — the requirement should be visible at the point where it is relevant, not as a rejection message after the fact.

**Severity:** Medium

**Suggested improvement:** Show a small inline indicator on the Portfolio page: "Rewards eligibility: $X of $1,000 minimum net position required." This sets expectations before the user navigates to the Rewards tab.

**Expected impact:** Users understand what they need to do to qualify for rewards before they go looking. Removes a frustrating gate that currently feels like a trap.

---

### FP-13 — Loop Tab Has No Entry Guidance

**What happened:** The Loop tab opens with all fields empty and no instruction on what to do first. The only guidance — "Select both long and short assets for deposit loop" — appears in the risk panel on the right side, not in the main form where the user's attention is focused.

**Why it caused friction:** Loop is the most complex flow in the product. It is the one that most needs onboarding guidance, and it is the one that has the least. A user who arrives at this tab without prior knowledge of looping strategies has no path to understanding what to do.

**Severity:** Medium

**Suggested improvement:** Add a one-line instruction above the asset selectors: "Choose a collateral asset and a borrow asset to build a leveraged position." Add a worked example: "Example: Deposit SOL, borrow USDC, loop up to 3x." A link to documentation is a minimum viable fallback.

**Expected impact:** Loop adoption increases. The feature is powerful but currently invisible to users who did not arrive already knowing what looping means.

---

## 4. UI/UX and Product Suggestions

### Suggestion 1 — Fix the Silent Failure on Market Borrow

**Problem:** The Borrow button in the Market Overview table produces "Unable to borrow right now." with no explanation. The Portfolio page borrow flow works correctly. Two entry points, one broken, no indication of which to use.

**Proposed solution:** Either fix the Market borrow flow to respect the selected Portfolio Account, or replace the Market Borrow buttons with a tooltip: "To borrow, go to your Portfolio page and click New Borrow." One line of copy eliminates the most common conversion failure in the product.

**Why it matters:** Every user who successfully deposits and then tries to borrow from the Market table is currently being blocked silently. This is not a minor edge case — it is the primary conversion funnel.

**How it makes Zodial easier:** Users stop abandoning at the borrow step thinking the protocol is broken.

---

### Suggestion 2 — Add Transaction Breakdown Before Wallet Confirmation (MAIN SUGGESTION)

**Problem:** The Deposit modal says "You will deposit 0.8 SOL ($60.79)." Phantom asks the user to sign for -0.819022 SOL. The difference (~0.019 SOL, ~$1.44) is never explained anywhere in the Zodial interface. The user agreed to one number and is being asked to confirm a different one.

This is not a fee transparency issue — it is a trust issue. When the number on screen does not match the number in the wallet, the user's first instinct is that something is wrong with the protocol.

**Proposed solution:** Before triggering the wallet confirmation, show a pre-confirmation breakdown inside the Zodial modal:
Deposit summary
Deposit amount        0.800000 SOL   ($61.72)
wSOL wrapping cost    0.009000 SOL   ($0.69)
Network fee (est.)    0.010022 SOL   ($0.77)
Total leaving wallet  0.819022 SOL   ($63.18)

**Why it matters:** A number users cannot verify is a number users will not trust. DeFi protocols lose users permanently at the moment of the first unexpected charge — not because the charge was wrong, but because it was unexplained. This fix costs one UI component and recovers every user who currently abandons at the Phantom confirmation screen.

**How it makes Zodial safer:** Users confirm transactions with complete information. The protocol cannot be blamed for fees it disclosed clearly.

**Visual mockup:**

![Deposit Breakdown Mockup](https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/deposit-mockup.png)

---

### Suggestion 3 — Add Tooltips to Every Risk Metric

**Problem:** "LTV mode vs LT liquidation buffer," "Portfolio Coverage Flow," "Impact 100/100," "Pressure 100/100" — none of these have explanations. For a protocol where misunderstanding the risk display can lead to liquidation, this is a safety gap.

**Proposed solution:** One-sentence tooltip on every metric. Priority order:

- **LTV vs LT:** "LTV shows how much you can still borrow. LT shows how close you are to liquidation. They use different thresholds — always watch LT."
- **Impact 100/100:** "Your collateral is fully supporting your current debt. No unused capacity in this asset."
- **Pressure 100/100:** "This borrow is using maximum capacity from your collateral. Adding debt or reducing collateral increases liquidation risk."

**Why it matters:** Cross-margin risk is non-obvious. Users coming from isolated-position protocols (Kamino, Marginfi) are not familiar with portfolio-level health. The risk engine is Zodial's core differentiator — it should be the most legible part of the interface, not the least.

---

### Suggestion 4 — Unify Asset Naming Across All Surfaces

**Problem:** The same asset appears as "SOLANA," "Wrapped SOL," "SOL," and "Wrapped SOL (SOL)" across the Market table, Deposit modal, Portfolio page, and Wallet Balances section within the same session.

**Proposed solution:** One canonical name per asset used consistently everywhere. Suggested standard: display name "SOL" with subtitle "Wrapped automatically on deposit" as a one-time tooltip on first interaction.

**Why it matters:** SOL and wSOL are different on-chain assets. The inconsistency creates doubt about what is actually being deposited, which is amplified in a cross-margin context where asset identity affects collateral calculations.

---

## 5. What Works

**The asset universe is genuinely novel.**
Seeing SpaceX, Tesla, NVIDIA, and Tether Gold alongside SOL and USDC in a single lending market is unlike anything available on Kamino or Marginfi. The ability to use tokenized stocks as collateral to borrow stablecoins — or vice versa — is a real product differentiator that no competitor offers on Solana today. This should be protected and made more prominent in onboarding.

**The Portfolio Coverage Flow panel is conceptually strong.**
Once I understood what it was showing — which took longer than it should have — the visualization of how my SOL collateral supports my USDC debt is genuinely useful. The "Current Flow Allocation" section showing which asset covers which debt at what effective LTV is a level of transparency that Kamino's isolated markets cannot offer. The concept is right; the labels just need tooltips.

**The [F] and [P] tranche system offers real flexibility.**
Two tranches of USDC with different Max LT values (97.0% vs 97.5%) and different borrow rates (0.98% vs 0.14%) give users meaningful choices. This is sophisticated and appropriate for the protocol's target audience. The problem is that the difference between tranches is never explained — but the underlying feature is sound.

**Transaction confirmations in Phantom show the Zodial logo.**
A small detail, but it matters. When Phantom shows a recognizable Zodial icon on the confirmation screen, the protocol feels like a legitimate product rather than an anonymous contract interaction. This builds trust at exactly the right moment.

**The Trade terminal is unexpectedly sophisticated.**
The Trade page combines a full TradingView chart with Auto / Lend / Loop / Swap tabs and a real-time portfolio health panel showing equity, deposits, borrows, and capital used simultaneously. For a lending protocol, this is closer to a trading terminal than anything available on Kamino or Marginfi. The Loop tab offers Deposit Loop and Short Loop modes with projected health, max leverage, and borrow headroom updating in real time before confirmation.

**The Deleverage flow is genuinely well-designed.**
The Deleverage modal lets you choose the liability to repay, the funding source (Wallet or Collateral), and the collateral asset to reduce — then shows the minimum route output before confirmation. It executes withdrawal, swap, and repay in a single bundled transaction. Most protocols force the user to manually calculate and execute this sequence in 3-4 separate steps. Zodial does it in one.

**The Repay modal offers Wallet vs Collateral funding choice.**
When repaying a borrow, you can choose to repay from your connected wallet or directly from deposited collateral. This removes the need for a separate withdrawal step and saves the user an extra transaction and gas cost. Most lending protocols on Solana do not offer this choice.

**The Leaderboard is fully transparent.**
Real-time Net Position, Deposits, Borrows, and 30-day PnL for every user, publicly visible. This level of on-chain transparency is rare — it creates competitive context and social proof simultaneously. Kamino and Marginfi have no equivalent.

---

## 6. One-Sentence Test

Zodial lets you deposit crypto or tokenized stocks, borrow against all of them together as one portfolio, and manage your risk with a live engine that shows exactly how each asset supports your debt — so you never need to lock assets into separate isolated positions like on Kamino or Marginfi.

---

## Comparison With Other Lending Protocols

**Where Zodial is better than Kamino:**
Kamino requires isolated positions per asset. If you have SOL, WBTC, and USDC, you manage three separate health factors. On Zodial, all three contribute to a single portfolio balance sheet. This is a material efficiency improvement for users with diversified holdings.

**Where Zodial is better than Marginfi/P0:**
The cross-margin model and the presence of tokenized RWAs (stocks, gold) as collateral assets have no equivalent in Marginfi. The portfolio-level risk visualization — even in its current under-documented state — is more sophisticated than anything Marginfi surfaces to users.

**Where Kamino feels better today:**
Kamino's onboarding is cleaner for first-time users. The first action is obvious, the confirmation flow is consistent, and error messages explain what went wrong. Zodial's onboarding needs to reach this baseline before it can compete for mainstream users.

**Where Marginfi/P0 feels better today:**
Marginfi's error states are more informative. When a transaction fails, users get context. Zodial's "Unexpected error" and "Unable to borrow right now" messages provide no path forward.

**One feature from Kamino I would want in Zodial:**
A health factor meter with color-coded safe/warning/danger zones displayed permanently on the Portfolio page — not buried in the Coverage Flow panel. When you are at 99.7% capital used (as I was after borrowing $51), the risk should be visually impossible to miss.

**One feature Zodial has that no competitor offers:**
A public Leaderboard with real-time Net Position, Deposits, Borrows, and 30-day PnL for every user. This transparency is rare in DeFi and creates both competitive context and social proof simultaneously.

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

---

## Bonus

**Screen recording:** *(Loom link to be added — recording scheduled for July 21)*

**X thread:** https://x.com/0xinaids/status/2077124328160698826

**Visual mockup (Suggestion 2):**
https://raw.githubusercontent.com/xinaids/zodial-ux-report/main/assets/deposit-mockup.png
