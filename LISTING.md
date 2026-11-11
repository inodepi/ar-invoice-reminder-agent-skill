# Agensi Listing — AR Collections Agent

Submission copy for https://www.agensi.io/dashboard/submit. Keep this in sync with SKILL.md when behaviour changes.

## Fields

| Field | Value |
| --- | --- |
| Skill name (internal) | `ar-collections-agent` |
| Display title | AR Collections Agent |
| Category | Finance & Accounting |
| Tagline | Clear your receivables queue without writing a single reminder. |
| Price | Free at launch — flip to $9 after the first 5 reviews |
| Version | 1.0.0 |
| License | MIT |
| Skills directory | `ar-collections-agent/` |

## Short description

Runs accounts-receivable collections end to end: reads your overdue invoices, writes a tone-matched reminder, sends the low-risk ones automatically, and queues the rest for one approval. Every email uses only the data in your tracker, and final notices always need a human.

## Long description

Chasing late invoices is the task every small finance team postpones. A copy-pasted reminder is either too soft to work or too aggressive to be safe, and nobody wants to scan a spreadsheet to work out who is 9 days late versus 60.

This skill turns your agent into the AR specialist that does that first pass properly:

- **Finds the real queue.** Paid, void, closed, disputed, and broken rows are skipped. Invoices chased in the last 7 days are skipped too, so no client gets nagged twice in a week.
- **Matches the tone to the age.** Friendly at 1–14 days, firm at 15–30, solution-oriented at 31–60, final notice at 61+. Tone is computed from the dates, not guessed.
- **Sends only what's safe.** Invoices under $5,000 and 30 days or less go out automatically. Larger, older, or urgent ones are drafted and put in front of you for a single yes/no. Final notices always require approval.
- **Writes like a person.** Under four sentences, exact invoice number and amount, no invented links or dates, no placeholders.
- **Logs as it goes.** Follow-up date and note are written back to your tracker. You get a clean report of sent, queued, skipped, and failed.

Works with any spreadsheet and mailbox your agent can reach. If a connector is missing, the skill tells you what to add instead of faking a send.

Includes four ready email templates, the full aging and escalation policy, a worked example with a fictional book, and — as a bonus — the original n8n workflow for teams that prefer a scheduled, draft-only pipeline.

## What's included

- `SKILL.md` — the end-to-end run method
- `references/aging-policy.md` — the ladder, cadence, edge cases, risk signals
- `templates/` — friendly, firm, urgent, and final-notice emails
- `examples/worked-example.md` — a full sample run with decisions and report
- `assets/ar-invoice-reminder-agent.n8n.json` — the companion n8n workflow

## Requirements

- Spreadsheet read/write via connector or CSV
- Email send via connector or email API
- An invoice tracker with the standard headers (the skill detects and maps them)

## Keywords

accounts receivable, AR, collections, overdue invoices, payment reminders, dunning, invoicing, follow-up, cash flow, finance automation

## Security notes

- No credentials or API keys in the package
- Requires email-send capability, declared on the listing
- Never auto-sends tier 3 (61+ days); never emails a guessed address; never modifies `Status`
- Ships an example book with fictional `.example` addresses only

## Promotion

- Link the skill from the companion repo README
- Post the 1:21 workflow film with a "now as an agent skill" note
- Reply to Agensi's "find a skill that chases overdue invoices" style prompts with the listing link
