# AR Collections Agent

A SKILL.md skill that turns your AI agent into an accounts-receivable specialist. Point it at your invoice tracker and it finds what's overdue, writes a reminder in the right tone, sends the safe ones on its own, and queues only the emails that deserve your eyes.

Built from the [AR Invoice Reminder Agent](https://github.com/potaterrr/ar-invoice-reminder-agent) n8n workflow — same tone ladder, same guardrails, but the agent does the sending instead of filing a draft for a human.

## What it does

1. Checks it actually has spreadsheet and email access — stops and tells you what to connect if not
2. Reads your overdue invoices and computes days past due
3. Skips paid, void, closed, disputed, broken, and recently-chased rows
4. Writes a reminder in the tier's tone: friendly, firm, urgent, or final notice
5. Sends tier-1 invoices under your threshold automatically
6. Queues everything risky for one approval, then sends
7. Logs the follow-up date and note back to the sheet
8. Reports sent, queued, skipped, and failed — with reasons

## Graduated autonomy

| Situation | What happens |
| --- | --- |
| Under $5,000, 30 days late or less, friendly or firm | Sent automatically |
| Larger, older, or urgent | Drafted, then one yes/no from you |
| 61+ days (final notice) | Always requires approval |
| First ever run | Full review, then hands-off |

Both thresholds live in an optional `Settings` tab, so "send everything" is one cell away.

## The tone ladder

| Days past due | Tone | Email asks for |
| --- | --- | --- |
| 1–14 | Friendly Reminder | A gentle nudge; "already on its way" is a fine reply |
| 15–30 | Firm & Direct | A payment date, with the exact invoice number and amount |
| 31–60 | Urgent / Solution-Oriented | A reply to set up a payment plan |
| 61+ | Final Notice | A payment date or plan today, always with your approval |

Every email stays under four sentences, uses only data from your sheet, omits the payment link when blank, and ends exactly:

```text
Regards,
[Billing Team]
```

## What's inside

```text
ar-collections-agent/
├── SKILL.md                     # the run method the agent follows
├── references/
│   └── aging-policy.md          # ladder, cadence, edge cases, risk signals
├── templates/
│   ├── friendly-nudge.md
│   ├── firm-reminder.md
│   ├── urgent-solution.md
│   └── final-notice.md
├── examples/
│   └── worked-example.md        # sample book, decisions, rendered email, report
└── assets/
    └── ar-invoice-reminder-agent.n8n.json   # bonus: the unattended n8n workflow
```

## Requirements

- A spreadsheet your agent can read and write — Google Sheets connector, or a CSV you hand it
- An email tool it can send from — Gmail/Outlook connector or email API
- Your invoice tracker with these headers: `Invoice ID`, `Client Name`, `Client Email`, `Amount (in USD)` or `Amount Due`, `Due Date`, `Status`, `Last Follow-Up Date`, `Notes`, optional `Payment Link`

No credentials live in this repo. Nothing is sent until your agent runs this skill.

## Get it

- **Agensi:** _listing link after publication_
- **Local:** copy the `ar-collections-agent/` folder into your agent's skills directory (for Claude Code: `~/.claude/skills/ar-collections-agent/`). The folder name must match `name` in the frontmatter.

## Prefer unattended automation instead?

The `assets/` folder carries the original n8n workflow: a daily schedule, Gemini drafting, Gmail drafts, and sheet logging. Import it into n8n and attach your own credentials. It drafts and never sends — the deliberate opposite of the skill, for teams that want a human send button.

Full workflow documentation lives in the [companion repo](https://github.com/potaterrr/ar-invoice-reminder-agent).

## Safety

- One reminder per invoice per 7 days
- Paid, void, cancelled, closed, disputed, and broken rows are never emailed
- Final notices are never auto-sent
- `Status` is never modified

## License

MIT
