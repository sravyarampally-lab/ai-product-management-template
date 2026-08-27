# AI Strategy One-Pager · Juno

> Module 2 · Strategy. Built with the **M2 · AI Strategy One-Pager Builder** (informed by the Three-Layer Model Mapper). Paste the tool's markdown over this file.
# AI Strategy One-Pager · Pre-Close Condition Risk-Checker

## The bet

_An AI copilot that cross-references every loan file's conditions against source docs and guidelines before clear-to-close will cut late-stage closing delays without adding compliance risk._

## Problem & Workflow

**The Problem:** Loan files often reach clear-to-close with missing or inconsistent conditions — income docs that don't match the application, appraisal gaps, unresolved title issues — that go unnoticed until underwriting or closing, causing last-minute delays, borrower frustration, and rework for the whole team.

**Prevention:** It explicitly prevents *late-stage condition surprises* — a loan moving toward clear-to-close on the assumption that all conditions are satisfied, when in fact a document mismatch or gap was never caught, because it wasn't cross-referenced against the full file until the underwriter or closer stumbled on it manually.

## Target Metrics

**Cycle time:** Reduction in average days from "conditions submitted" to "clear-to-close," by catching gaps upfront instead of in a late review cycle.

**Leadership proof:** Number of closings delayed due to missed/incorrect conditions, tracked monthly — the metric that makes leadership say "don't touch it" is a visible drop in condition-related closing delays without an increase in loan officer overrides.

## Autonomy Level

**Choice:** Copilot. It surfaces flagged conditions, mismatches, and gaps directly to the processor or underwriter, alongside the evidence (which doc, what's missing or inconsistent), so a human makes the final call on every file.

**Explicitly avoiding:** Agent. I'm not letting the system auto-clear conditions or auto-approve a file to move to clear-to-close on its own. In lending, an autonomous agent that quietly waives or resolves a condition without a human sign-off creates an unreviewable compliance and repurchase risk — the whole point is to make risk visible, not to make decisions in the dark.

## Data & Model Approach

**Approach:** Ground (RAG). The system retrieves from the actual loan file — income docs, appraisal, title report, underwriting guidelines — and cross-references them against each other and against investor/agency requirements before flagging a gap.

**Explicitly avoiding:** Fine-tuning a model on historical loan data. Guidelines, investor overlays, and compliance requirements change often, and a fine-tuned model would bake in stale rules that are expensive to retrain. Grounding in current source documents and live guideline references means the system stays accurate as policy changes, without a retraining cycle.

## Risks & Mitigations

**Risk:** The system misses a genuine condition gap (false negative) and the file proceeds to clear-to-close, giving processors false confidence that a human check is no longer needed — this is the one-way door: erosion of the manual review habit that catches what the AI doesn't.

**Mitigation:** Every file still requires a human sign-off before clear-to-close, and the tool logs its own confidence and coverage (what it checked vs. what it couldn't verify) on each file, so processors can see when a review was thin rather than assuming silence means "all clear."

## V1 Scope

**In:** Flags missing, mismatched, or inconsistent conditions on purchase and refi conventional loan files (income docs, appraisal, title) before the file moves to clear-to-close, and surfaces the specific evidence behind each flag for processor/underwriter review.

**Out:** (1) It does not clear or waive any condition automatically — every flag requires human sign-off, no auto-approval. (2) It does not cover non-conventional loan types (jumbo, non-QM, government/FHA-VA) in V1 — those have enough guideline variance that they're out of scope until the core model is validated on conventional volume.
