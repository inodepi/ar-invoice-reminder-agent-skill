# Final Notice — 61+ days past due

Use only at the top of the ladder. Never auto-sent, whatever the settings say.

**Subject pattern:** `Final notice: invoice {{invoice_number}} — {{amount}}, {{days_past_due}} days overdue`

```text
Hi {{client_first_name}},

This is a final notice that invoice {{invoice_number}} for {{amount}} remains unpaid {{days_past_due}} days after its {{due_date}} due date. Please reply today with a payment date or a plan proposal so we can avoid escalating the account.{{payment_link_sentence}}

Regards,
[Billing Team]
```

Fill rules:

- "Escalating the account" is the furthest the language goes. Do not name legal action, collections agencies, or fees unless the user supplied those words.
- If the user has a policy sentence for this tier, use theirs instead of the generic line.
- `{{payment_link_sentence}}` — ` You can settle it here: {{payment_link}}.` when a link exists, otherwise empty.
- Always queued for approval. If the user approves, send once and log it. Do not follow up again within 7 days.
- For invoices older than 180 days, recommend a human review instead of another automated notice.
