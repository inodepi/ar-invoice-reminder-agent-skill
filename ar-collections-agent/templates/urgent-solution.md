# Urgent / Solution-Oriented — 31 to 60 days past due

Use when the balance needs a plan. Firm on the fact, generous on the route to payment.

**Subject pattern:** `Overdue: invoice {{invoice_number}} — {{amount}}, {{days_past_due}} days late`

```text
Hi {{client_first_name}},

Invoice {{invoice_number}} for {{amount}} is now {{days_past_due}} days past due and I would like to get this resolved. If paying in full is not possible right now, reply with a date and amount that works and we can set up a payment plan.{{payment_link_sentence}}

Regards,
[Billing Team]
```

Fill rules:

- Offer the plan; never shame the client or speculate about their finances.
- Do not promise terms you were not given. "We can set up a plan" is the limit.
- `{{payment_link_sentence}}` — ` You can also pay here: {{payment_link}}.` when a link exists, otherwise empty.
- This tier is queued for approval by default, because large or older balances are relationship-sensitive.
