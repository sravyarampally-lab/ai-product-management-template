# Trust-Gap Mitigations · Juno
> Module 4 · AI-Native UX. Trust gaps surfaced with the **M4 · AI-UX Trust Gap Checker**, and how each is mitigated.

## Trust gaps

| Gap | Where it shows up | User cost | Mitigation |
|---|---|---|---|
| Hallucination | LO asks "why is this rate X?" and the assistant fabricates a pricing adjustment or eligibility reason not present in the OB/rules-engine response | LO quotes a borrower a rate/fee that doesn't hold at lock; broken trust and potential compliance exposure | Ground every pricing/eligibility claim in the actual DESK rules-engine + OB payload; render only fields returned by the pricing call, and show "not available" rather than inferring an adjustment |
| Opacity (no "why") | Eligibility result or price shows a number with no breakdown of the LLPAs, margin, or rule hits that produced it | LO can't defend the price to the borrower or catch a bad input; escalates to Pricing Tech Team / Tavant | Surface the adjustment stack (base + each LLPA + margin/markup) and the specific eligibility rules that fired, linked to their source (OB, DESK rule ID) |
| No user control | Assistant auto-selects a product/lock scenario the LO didn't intend, with no way to adjust inputs or override | LO locks the wrong scenario or abandons the tool for manual OB; loss of confidence | Let the LO edit inputs (loan amount, LTV, product, lock period) and re-run, with an explicit confirm step before any lock/reprice action |

## Highest-priority fix

Opacity. In mortgage pricing the number is only trustworthy if the LO can see and defend how it was built — the LLPA stack, margin, and eligibility rule hits. Closing this also mitigates hallucination (an itemized breakdown has nowhere to invent adjustments) and gives the LO the footing to know when to exercise control. A confident-looking price with no "why" is the fastest way to lose LO trust and the hardest gap to recover from at lock.

**Example — DESK:** An LO sees a 6.875% rate on a HomeReady loan. The gap-closed view itemizes: base 6.500%, +0.250 LTV/FICO LLPA, +0.125 product LLPA, −0.000 AMI waiver (HomeReady eligibility rule hit, tied to the census-tract AMI check), plus margin — each line traceable to the OB payload or DESK rule ID. The LO can now defend the quote, and spot immediately if the AMI waiver failed to apply because of a bad input.
