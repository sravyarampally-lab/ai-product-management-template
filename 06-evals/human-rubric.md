
# Human Evaluation Rubric · AI pricing assistant that generates rate quotes and pricing scenarios for loan officers (rate/price, points, lock terms, adjustments)


## What graders score

- **Task / product:** AI pricing assistant that generates rate quotes and pricing scenarios for loan officers (rate/price, points, lock terms, adjustments)
- **Reviewer audience:** Senior loan officer + secondary marketing / pricing analyst (rotating pair)
- **Value proposition:** The assistant must produce a rate quote that matches the live rate sheet and LLPA (loan-level price adjustment) grid at the moment of the quote, disclose all required terms clearly, and hand off to a human the instant a scenario falls outside standard pricing parameters.

## Dimensions

| Dimension | 1 (fail) | 3 (ok) | 5 (excellent) |
|---|---|---|---|
| _(unnamed)_ | Quotes a rate/price off the wrong day's sheet, or omits an LLPA that materially changes the price (e.g., missing cash-out or investment-property adjustment). | Rate and price are correct within rounding tolerance; all major LLPAs applied correctly. | Exact and itemized, plus flags a borderline LLPA threshold (e.g., borrower is 2 points from a better credit tier) the loan officer would want to know. |

_Full 1-5 anchors:_

### 1. _(unnamed)_

- **Score 1:** Quotes a rate/price off the wrong day's sheet, or omits an LLPA that materially changes the price (e.g., missing cash-out or investment-property adjustment).
- **Score 2:** Correct base rate sheet, but one adjustment is applied incorrectly (wrong tier, wrong direction) — price is off but in the right ballpark.
- **Score 3:** Rate and price are correct within rounding tolerance; all major LLPAs applied correctly.
- **Score 4:** 	Rate and price are exact, every applicable adjustment is itemized and correctly applied.
- **Score 5:** Exact and itemized, plus flags a borderline LLPA threshold (e.g., borrower is 2 points from a better credit tier) the loan officer would want to know.

## Calibration

- **Sampling rule:** Omits a required disclosure entirely (e.g., no APR shown, no lock expiration stated) — quote is not usable as given to a borrower.
- **Cadence:** All disclosures present but one is materially unclear or mislabeled (e.g., points shown as a rate, not a dollar cost).
- **Graders per item:** All required disclosures present and correctly labeled, if plainly formatted.
- **Calibration cadence:** Complete, correctly labeled, and formatted for direct borrower-facing use without editing.

Any dimension where two graders differ by 2+ points is auto-flagged for adjudication by the secondary marketing desk lead.
Any Rate & pricing accuracy score of 1, or Compliance disclosure score of 1, from either grader, triggers immediate escalation and a hold on that pricing path until reviewed — no averaging.
The adjudicated score (not an average) is the recorded score; rationale is logged for the next calibration session and fed back to the rate-sheet integration if the error was systemic rather than one-off.

## Pass bar

An item passes only if every dimension scores ≥ 3, and Rate & pricing accuracy and Compliance disclosure completeness each score ≥ 4. A 1 or 2 on any single dimension fails the item — dimensions are not averaged to reach a passing bar.

> Module 6 · Evals & Guardrails. The rubric human graders use to score Juno, from the **M6 · Human Evaluation Rubric**. Paste the tool's markdown over this file.

## What graders score

_The task and the sample they review._

_____

## Dimensions

| Dimension | 1 (fail) | 3 (ok) | 5 (excellent) |
|---|---|---|---|
| _Factual grounding_ | _…_ | _…_ | _…_ |
| _Helpfulness_ | _…_ | _…_ | _…_ |
| _Safety / tone_ | _…_ | _…_ | _…_ |

## Calibration

_How graders align (worked example + agreement target, e.g. κ ≥ 0.6)._

_____

## Pass bar

_The mean / threshold that counts as a pass._

_____
