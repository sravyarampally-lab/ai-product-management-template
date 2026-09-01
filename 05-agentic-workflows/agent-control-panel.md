# Agent Control Panel · Juno
## Autonomy level

Agent may draft and price a quote; it cannot execute a lock or send borrower-facing output. Lock action requires LO click.

## Controls

- **Kill switch:** Agent aborts when any fires: max_steps = 12, wall-clock timeout = 90s, or 3 consecutive tool errors. On abort → return last valid pricing snapshot + status: incomplete, never a partial lock.
- **Rate / cost caps:** Every tool returns typed JSON: { data, source, timestamp, confidence }. OB pricing call returns { rate, price, lockEligible, confidence: 0.0–1.0 }; Encompass reads return { field, value, retrievedAt }. No free-text observations — engineering enforces the contract at the API boundary.
- **Escalate-on-stuck:** On loop break or gate trigger → surface last valid snapshot with status: incomplete, route to LO queue, log the abort reason. No silent failures.

## Monitoring

**Confidence thresholds (map to actions):**

≥ 0.90 → agent proceeds autonomously. 0.70–0.89 → proceed but flag for LO review. < 0.70 → halt, escalate to human. Eligibility ambiguity (Bond/HFA, AMI edge cases) always drops below threshold by rule.

**Checkpoints:**

Human intervention required when: loan amount > $2M, confidence < 0.70, non-standard product (Bond/HFA, HELOC/CES), or eligibility flags conflict.

**North Star (re-read every loop):**

Re-read every loop: "Produce an accurate, lock-eligible price for this loan scenario using only verified OB and Encompass data. Never fabricate rates. Never advance a lock without eligibility confirmation."

## Permissions

Read: OB pricing, Encompass loan fields, DESK eligibility rules. Write: DESK scratchpad only. No writes to Encompass or OB.

## Self-review

- [ ] Stop conditions include max_steps + wall-clock timeout.
- [ ] Tool outputs include a confidence/score field per retrieval tool.
- [ ] Confidence thresholds map to actions, not just labels.
- [ ] North Star is one sentence, re-read every loop.
- [ ] Each rule of engagement names something the agent CANNOT do.
