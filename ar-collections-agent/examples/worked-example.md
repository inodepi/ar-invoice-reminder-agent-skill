# Worked Example

A fictional book, one run, on **2026-11-11**. Settings tab: `Auto-Send Limit` = `5000`, `Auto-Send Max Days` = `30`.

## Input: `Invoices` tab

| Invoice ID | Client Name | Client Email | Amount (in USD) | Due Date | Status | Last Follow-Up Date | Payment Link |
| --- | --- | --- | --- | --- | --- | --- | --- |
| INV-1041 | Maya Chen | maya@blueharbor.example | 820.00 | 2026-10-28 | Sent | | https://pay.example.com/inv-1041 |
| INV-1038 | Daniel Okafor | daniel@northline.example | 4200.00 | 2026-10-12 | Sent | | |
| INV-1027 | Sofia Ramos | sofia@meridian.example | 7800.00 | 2026-10-01 | Sent | | https://pay.example.com/inv-1027 |
| INV-0995 | Ace Facilities | billing@acefacilities.example | 1250.00 | 2026-08-15 | Sent | | |
| INV-1042 | Priya Nair | priya@kestrel.example | 950.00 | 2026-11-05 | Sent | 2026-11-08 | |
| INV-1030 | Jonas Feld | | 2400.00 | 2026-10-20 | Sent | | |
| INV-1033 | Ines Duarte | ines@lumen.example | 600.00 | 2026-09-30 | Paid | | |
| INV-1036 | Theo Marsh | theo@cobalt.example | TBD | 2026-10-05 | Sent | | |

## Decisions the policy produces

| Invoice | Days | Amount | Tier | Decision | Why |
| --- | --- | --- | --- | --- | --- |
| INV-1041 | 14 | $820.00 | 1 friendly | **Send** | Under $5,000, at 30 days or less, tier 1 |
| INV-1038 | 30 | $4,200.00 | 1 firm | **Send** | Under $5,000, exactly at the day limit, tier 1 |
| INV-1027 | 41 | $7,800.00 | 2 urgent | **Queue** | Above the auto-send limit |
| INV-0995 | 88 | $1,250.00 | 3 final notice | **Queue** | Tier 3 always needs approval |
| INV-1042 | 6 | $950.00 | 1 | **Skip** | Followed up 3 days ago — inside the 7-day cooldown |
| INV-1030 | 22 | $2,400.00 | — | **Skip** | No valid client email |
| INV-1033 | 42 | $600.00 | — | **Skip** | Status is Paid |
| INV-1036 | 37 | TBD | — | **Skip** | Amount is not parseable |

## Rendered email for INV-1041

```text
Subject: Friendly reminder: invoice INV-1041 for $820.00

Hi Maya,

Just a gentle nudge that invoice INV-1041 for $820.00 was due on 2026-10-28. If it is already on its way, please disregard this note. You can settle it here: https://pay.example.com/inv-1041.

Regards,
[Billing Team]
```

Three sentences before the signature, only supplied data, no placeholder left.

## Run report

| Invoice | Client | Amount | Days | Tone | Action |
| --- | --- | --- | --- | --- | --- |
| INV-1041 | Maya Chen | $820.00 | 14 | Friendly Reminder | sent |
| INV-1038 | Daniel Okafor | $4,200.00 | 30 | Firm & Direct | sent |
| INV-1027 | Sofia Ramos | $7,800.00 | 41 | Urgent / Solution-Oriented | queued |
| INV-0995 | Ace Facilities | $1,250.00 | 88 | Final Notice | queued |
| INV-1042 | Priya Nair | $950.00 | 6 | — | skipped (cooldown) |
| INV-1030 | Jonas Feld | $2,400.00 | 22 | — | skipped (no email) |
| INV-1033 | Ines Duarte | $600.00 | 42 | — | skipped (paid) |
| INV-1036 | Theo Marsh | TBD | 37 | — | skipped (amount unparseable) |

```text
Sent: 2 · Queued: 2 · Skipped: 4 · Failed: 0
```

Broken rows to fix: INV-1030 (missing email), INV-1036 (amount written as text instead of a number).
