# AI-Native User Flow · Juno

> Module 4 · AI-Native UX. The end-to-end user flow, designed with the **M4 · AI User Flow Architect**. Paste the tool's markdown over this file.

## Entry point

**Signal type:** Specific user action

Loan scenario fields reach a priceable threshold in DESK — property address, loan amount, FICO, LTV, occupancy, and loan purpose populated from Encompass. The moment the last required field validates, the pricing intent exists. Juno fires on that field-completion event, not on a "Get Pricing" button.

**What they see instantly**

A status badge appears inline on the scenario card — "Juno is pricing this scenario…" — before any product results return.

## The flow

1. Normalize scenario → build the OB pricing request payload (loan attributes, borrower, property).
Eligibility pass → run product/eligibility rules engine to filter ineligible products (AMI, HomeReady/Home Possible, Bond/HFA, HELOC/CES paths).
Pricing call → Optimal Blue for rate/price grids on surviving products; apply fees-in-price and margin/markup overrides.
Rank → score by rate, cost, and eligibility confidence.
2. "Checking eligibility across products…" → "Pulling live pricing from Optimal Blue…" → "Applying fees & margin…" → "Ranking your best options." Each under ~2s.
3. Single eligible product path → return priced options directly. Bond/HFA or HELOC/CES detected → route through the specialized eligibility sub-flow first. Eligibility confidence < 70% (e.g., AMI boundary, missing income) → route to a clarification step instead of pricing.

## AI moments

**Placement:** Hybrid (multiple placements)

Ranked rate/price cards (best-fit first) with rate, points, monthly payment, and lock eligibility. Each card carries an eligibility-rationale line ("HomeReady — AMI 78%, qualifies") and a citation to the governing rule or OB product code. A one-click "Send to Lock Desk" on each.

Value = augmentation. The LO reviews and selects; Juno doesn't create a lock from a blank slate. Inline keeps the LO in the scenario, not bouncing to OB's UI.

## Fallbacks

**Kill switch**

"Override" on every card lets the LO manually adjust margin, force-surface a filtered product, or push a different rate — plus "Talk to Pricing Desk" to escalate to a human.

**Training signal**

LO overrides a filtered-out product → logged as eligibility_correction. LO consistently demotes Juno's top-ranked card → logged as ranking_mismatch → tightens future scoring weights. Repeated corrections on one rule → flags that rule for review.

**Fail-safe**

OB call fails or returns no eligible product → Juno drops into cautious mode: no invented rates, confidence set to N/A, message "I couldn't return live pricing for this scenario. Want me to retry, or send it to the Pricing Desk?" Never fabricates a rate or eligibility result.

## Self-review

- [ ] Trigger fires on the earliest possible signal, no manual “Start AI” click.
- [ ] At least one breadcrumb message turns latency into transparency.
- [ ] Maneuver matches the M2 value prop (Automation / Augmentation / Insights / Personalization).
- [ ] Every automated decision has a working kill switch.
- [ ] Fail-safe path is explicit. No dead end with a bad AI result.
- [ ] Hidden logic references M3 PRD specs (Top-K, latency target, knowledge base).






