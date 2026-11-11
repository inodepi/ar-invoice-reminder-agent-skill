# Friendly Nudge — 1 to 14 days past due

Use for the first nudge. Assume the client simply forgot. Warm, short, no pressure.

**Subject pattern:** `Friendly reminder: invoice {{invoice_number}} for {{amount}}`

```text
Hi {{client_first_name}},

Just a gentle nudge that invoice {{invoice_number}} for {{amount}} was due on {{due_date}}. If it is already on its way, please disregard this note.{{payment_link_sentence}}

Regards,
[Billing Team]
```

Fill rules:

- `{{client_first_name}}` — first word of `Client Name`.
- `{{payment_link_sentence}}` — ` You can settle it here: {{payment_link}}.` when a link exists, otherwise empty.
- Do not add a second nudge, a deadline, or a threat. Tier 1 has none.
