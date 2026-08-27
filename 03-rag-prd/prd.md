# AI PRD · Juno

> Module 3 · RAG / AI PRD. The AI product requirements doc with retrieval requirements, built with the **M3 · AI PRD Builder** (RAG design from the **M3 · RAG Architecture Decider**). Paste the tool's markdown over this file.
_

## Problem & user

RocketShip PMs need evidence-based prioritization. Juno turns noisy Slack, tickets, and strategy docs into a ranked, cited backlog they can defend.

## Solution overview

**Retrieval strategy:** Hybrid

Exact eligibility lookups need keyword precision against guideline tables; pricing-movement and "why" questions need semantic retrieval across rate history and lock notes. Where = inside DESK at point of pricing; Scale = ~1,200 docs with intraday rate churn, so modular retrieval keeps the current rate sheet authoritative without re-embedding the whole corpus.

## Retrieval requirements (RAG)

- **Sources:** Sources: Optimal Blue rate sheets (current + trailing 30 days), agency/investor guideline docs (Fannie, Freddie, FHA, VA, plus HFA/Bond overlays), internal DESK eligibility rules + margin/markup config, and lock desk policy (extensions, relocks, reprices). Quantity: ~1,200 documents. Investor guidelines are the authority for eligibility; rate sheets are the authority for price; internal config is the tiebreaker for what Rate actually offers.
- **Chunking / indexing:** Hybrid (Semantic + Keyword)
- **Grounding rule:** Every pricing or eligibility answer cites at least one guideline clause (doc + section) AND the specific rate sheet (investor, product, effective timestamp). Eligibility verdicts additionally cite the DESK rule ID applied. Citations render inline so the LO can click through and defend the number to a borrower or auditor.
- **Freshness:** Rate sheets: sync on publish (multiple intraday reprices — stale price is wrong price). Guidelines + HFA/Bond overlays: daily at 05:00 CT. Lock policy + margin/markup config: sync on commit (lives in DESK config/git). Eligibility rules: sync on commit.

## Requirements

| # | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| 1 | Retrieval quality and latency | Must | Top-K = 6 segments per pricing query. p95 latency < 2.5s end-to-end (from LO query to cited answer). At $0.03/1k blended token cost, ~$0.05 per query — acceptable for high-frequency LO use at the pricing screen. |
| 2 | Fail-safe on empty retrieval | Must | If retrieval returns < 2 relevant segments, OR the rate sheet is older than the last known reprice, OR guideline and internal config conflict, the Copilot does NOT quote a price or clear eligibility. It returns: "Can't confirm pricing from current sources — rate sheet may be stale or guidelines conflict. Re-run pricing in DESK or confirm with the lock desk." A wrong price that gets locked is a financial liability, so cautious beats confident. |
| 3 | Grounded trust | Must | Every pricing or eligibility answer cites at least one guideline clause (doc + section) AND the specific rate sheet (investor, product, effective timestamp). Eligibility verdicts additionally cite the DESK rule ID applied. Citations render inline so the LO can click through and defend the number to a borrower or auditor. |

## Out of scope

Decisions that cannot be cited to a source in the knowledge base. Anything Juno is not allowed to retrieve or act on without a human.
