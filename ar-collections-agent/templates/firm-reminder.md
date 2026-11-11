# Firm Reminder — 15 to 30 days past due

Use when a friendly nudge would understate the situation. State the invoice and the amount clearly, then ask for a date.

**Subject pattern:** `Invoice {{invoice_number}} — {{amount}} now {{days_past_due}} days past due`

```text
Hi {{client_first_name}},

Invoice {{invoice_number}} for {{amount}} was due on {{due_date}} and is now {{days_past_due}} days past due. Could you confirm the payment date today?{{payment_link_sentence}}

Regards,
[Billing Team]
```

Fill rules:

- Keep the invoice number and the amount exact — no rounding, no "about".
- The ask is a date, not an apology or an explanation.
- `{{payment_link_sentence}}` — ` You can settle the balance here: {{payment_link}}.` when a link exists, otherwise empty.
- Still no threats. Escalation language belongs to tier 2.
