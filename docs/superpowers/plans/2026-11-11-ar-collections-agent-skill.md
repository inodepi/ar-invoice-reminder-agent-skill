# AR Collections Agent Skill Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish `ar-collections-agent`, a SKILL.md package where a buyer's own agent runs their AR collections with graduated autonomy, and mirror it in a public marketing repo.

**Architecture:** The skill is a self-contained folder (`ar-collections-agent/`) with SKILL.md, one reference file, four email templates, a worked example, and a sanitized n8n workflow as a bonus asset. The repo README and LISTING.md carry the storefront copy. No runtime code — the agent executes the instructions using the buyer's own spreadsheet and email tools.

**Tech Stack:** Markdown + YAML frontmatter (SKILL.md open standard), Git, GitHub CLI for publishing.

**Spec:** Design agreed in conversation 2026-11-11: graduated autonomy (auto-send under $5k and ≤30 days; everything else queued), launch free then $9, Finance & Accounting category.

## Global Constraints

- Frontmatter `name` must equal the skill folder name: `ar-collections-agent`.
- Only portable frontmatter fields: `name`, `description`, `when_to_use`. No `allowed-tools`, no hooks.
- No credentials, API keys, or real client data anywhere in the repo.
- No `[bracket]` placeholders in rendered emails except the signature `[Billing Team]`.
- Tone ladder is fixed: 1–14 friendly, 15–30 firm, 31–60 urgent/solution, 61+ final notice.
- Defaults copied verbatim: auto-send limit `5000`, max auto-send days `30`, cooldown `7` days.
- Every email uses only supplied data; payment link sentence omitted when blank.

## Review Focus

- A row with a paid/void/disputed status must never be emailed — skipped and reported instead.
- A row with a broken email, amount, or due date must be skipped, named in the report, never guessed.
- Final-notice tier (61+ days) must always require approval, even if settings would auto-send.
- A second run within 7 days must not re-email the same invoice.
- Missing sheet/email capability must stop the run with a connect-instructions message, never a simulated send.

---

### Task 1: Scaffold repo and skill folder

**Files:**
- Create: `ar-collections-agent/SKILL.md`
- Create: `ar-collections-agent/references/aging-policy.md`
- Create: `ar-collections-agent/templates/{friendly-nudge,firm-reminder,urgent-solution,final-notice}.md`
- Create: `ar-collections-agent/examples/worked-example.md`
- Create: `ar-collections-agent/assets/ar-invoice-reminder-agent.n8n.json`

**Interfaces:**
- Produces: folder layout consumed by the Agensi submission zip; skill name `ar-collections-agent`.

- [x] **Step 1:** Create folder tree.
- [x] **Step 2:** Copy sanitized workflow JSON, replacing the spreadsheet ID with `YOUR_SPREADSHEET_ID`.
- [x] **Step 3:** Write SKILL.md with the 8-step run method.
- [x] **Step 4:** Write reference, templates, and worked example.
- [x] **Step 5:** Commit.

### Task 2: Storefront and listing metadata

**Files:**
- Create: `README.md`
- Create: `LISTING.md`
- Create: `LICENSE`

**Interfaces:**
- Consumes: skill folder from Task 1.
- Produces: submission-ready listing copy (title, short/long description, category, price plan).

- [x] **Step 1:** Write README with story, contents, install, requirements.
- [x] **Step 2:** Write LISTING.md with Agensi fields and launch-free → $9 plan.
- [x] **Step 3:** Add MIT license.
- [x] **Step 4:** Commit.

### Task 3: Validate and publish

**Files:**
- Verify: all files above.

- [x] **Step 1:** Confirm frontmatter name matches folder name.
- [x] **Step 2:** Confirm no credentials/sheet IDs/real data remain (`grep`).
- [x] **Step 3:** Confirm templates contain no bracket placeholders besides the signature.
- [x] **Step 4:** Create `inodepi/ar-invoice-reminder-agent-skill` on GitHub and push.

**Verification:** grep for the original spreadsheet ID prefix returns nothing outside this sentence; YAML check of SKILL.md name/description; `git status` clean after push.
