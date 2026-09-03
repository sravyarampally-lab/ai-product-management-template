# AI PRD · Juno

## Problem & user

**User:** Loan Officers (LOs) at Rate who need fast, accurate answers about pricing, eligibility, and product guidelines during live borrower conversations.

**Problem:** Pricing and eligibility rules live across scattered sources — Optimal Blue, product guideline PDFs, DESK rule configs, investor overlays, and internal policy docs. LOs currently interrupt pricing desk staff or dig through stale documents, leading to quote errors, compliance risk, and slow turnaround. They need a grounded assistant that answers "can this loan be priced/locked, and under what terms?" with citations they can trust.

## Solution overview

Juno is a retrieval-grounded Q&A assistant embedded in DESK that answers LO questions on product eligibility, pricing rules, lock policies, and guideline overlays. It retrieves from authoritative pricing/guideline sources, cites every answer, and refuses to speculate when no grounded source exists — deferring to the pricing desk instead.

## Retrieval requirements (RAG)

- **Sources:** Optimal Blue product/pricing exports, investor & agency guideline PDFs (Fannie/Freddie/FHA/VA/Bond-HFA), DESK rule-engine configs and eligibility metadata, internal lock/relock policy docs, and product overlay matrices.
- **Chunking / indexing:** Structure-aware chunking — split guideline docs by section/subsection headers (not fixed token windows) to keep a rule and its conditions intact; index rule-engine configs as discrete key-value records per product. Rationale: eligibility rules lose meaning when a threshold is severed from its qualifying condition.
- **Grounding rule:** No answer without a cited source. If retrieval returns no passage above the relevance threshold, Juno states it cannot answer and routes the LO to the pricing desk — it never infers eligibility.
- **Freshness:** Pricing/rate-sensitive sources re-indexed intraday (OB exports on each publish); guideline docs re-indexed within 24h of source update. Each answer surfaces the source's effective date.

## Requirements

| # | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| 1 | Grounded answers with citations | Must | Every answer links ≥1 retrieved source with effective date |
| 2 | Refuse ungrounded queries | Must | Below relevance threshold → refusal + pricing-desk handoff, no speculation |
| 3 | Product eligibility Q&A | Must | Returns correct eligibility for a given product + loan scenario against test set |
| 4 | Intraday pricing freshness | Must | OB export changes reflected in retrieval within one publish cycle |
| 5 | Effective-date disclosure | Should | Each cited source shows its effective/as-of date inline |
| 6 | Query logging for audit | Should | All Q&A pairs + retrieved sources logged for compliance review |
| 7 | Conflicting-source flagging | Could | When two sources disagree, both surfaced with a conflict notice |

## Out of scope

Generating or committing actual price locks (Juno is advisory only); modifying DESK rule configs; borrower-facing access; underwriting decisions or conditions clearance; non-pricing LOS workflows in Encompass.
