# Aging Policy and Escalation Ladder

The reasoning behind the skill's fixed rules. Read this when the user asks why a tone was chosen, when a row is ambiguous, or when they want to change the send settings.

## The ladder

| Tier | Days past due | Tone | Intent | What the email asks for |
| --- | --- | --- | --- | --- |
| 1 | 1–14 | Friendly Reminder | Assume the client forgot. Warm and light, no pressure. | A quiet nudge; payment or a "already on its way" reply. |
| 1 | 15–30 | Firm & Direct | The invoice is no longer a surprise. | The exact invoice number and amount, plus a payment date. |
| 2 | 31–60 | Urgent / Solution-Oriented | The balance needs a plan, not a scolding. | A reply with a date and amount, or a payment split. |
| 3 | 61+ | Final Notice | Relationship is at risk and the account needs escalation. | A payment date or plan today, before escalation. |

The tone is computed from the number of days, never chosen by the model. This keeps two invoices at the same age worded the same way, and makes the behaviour predictable for the user.

## Cadence

- One reminder per invoice every **7 days** (cooldown). The cooldown is checked before drafting, so no tokens or time are spent on a row that was chased this week.
- Tone rises naturally as days accumulate: a weekly chaser walks from friendly to firm to urgent without any special scheduling.
- Never send two reminders for the same invoice in one day, even across separate runs.
- If the user asks for a different cooldown, ask what they want and use it for that run only. The default stays 7.

## Send policy

Defaults: `Auto-Send Limit` = 5000, `Auto-Send Max Days` = 30, read from the optional `Settings` tab.

| Amount | Days | Tier | Action |
| --- | --- | --- | --- |
| < limit | ≤ max days | 1 | Send automatically |
| < limit | ≤ max days | 2 | Queue |
| ≥ limit | any | 1–2 | Queue |
| any | > max days | 1–2 | Queue |
| any | any | 3 | Queue — always |

The graduated policy exists because the failure modes are asymmetric. A missed $800 nudge costs a few days of cash flow. An unprompted final notice to a key account costs the relationship, and possibly a refund under a marketplace guarantee.

The first run is always a review run: show every draft and the effective settings, get one confirmation, then go autonomous.

## Edge cases

**Partial payment.** Prefer an `Amount Due` column; the agent then chases the true balance. If only the original amount exists, do not compute the remainder yourself — ask the user to update the row and skip it this run.

**Dispute or on-hold.** Any status containing `disputed` or `on hold` is skipped. Report those rows explicitly so the user can handle them outside the collections queue.

**Broken data.** Missing email, unparseable amount or date, or a missing invoice number means skip and report. Never fill the gap with a guess.

**Several invoices for one client.** Draft one email per invoice. A combined email changes the amount being claimed, so it needs explicit approval even when each invoice individually would auto-send.

**Currency.** Default formatting is USD (`$1,234.56`). If the sheet carries another currency, ask before sending — do not relabel an amount as dollars.

**No payment link.** Omit the payment sentence entirely. Never invent a link.

**Very old invoices (180+ days).** Still tier 3. Recommend the user review the account or escalate to legal/collections instead of sending another automated notice.

**VIP or key accounts.** If the user names a client as sensitive, route that client to approval-only for the rest of the run.

**Replies.** Prefer replying in the existing invoice thread. Keep the subject stable; do not restate the whole history in one email.

## Risk signals that force a queue

Anything in this list overrides the auto-send table:

- amount at or above the auto-send limit
- days past due above the auto-send maximum
- tier 3 (61+ days)
- disputed, on-hold, or otherwise unusual status
- non-USD currency
- a client the user flagged as sensitive
- a thread that already contains a dispute or a promise to pay

## Reporting

Skip reasons are shown per row, not collapsed into a count. The user should be able to fix broken rows in one pass and re-run.
