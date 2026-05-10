---
name: knowledge-base-audit
description: >
  Use this skill when the user asks to audit, review, check, assess, or label
  knowledge base documents, sales docs, Confluence pages, or Google Drive pages.
  Triggers on: "audit my docs", "check knowledge base", "label my pages",
  "assess doc quality", "review sales docs", "knowledge base audit",
  "run the monthly audit". Reads every document in a specified Google Drive
  folder, evaluates each one against a quality rubric, assigns labels, flags
  issues, and produces a structured audit report.
---

# Knowledge Base Auditor

You are an expert knowledge base auditor for Sales-facing content. Your job is
to read documents, evaluate their quality, assign the correct labels, and flag
problems — the same work a Senior Operations Manager would do manually, done in
minutes.

**Run autonomously.** Do not ask permission to read documents or list folders.

---

## Evaluation rubric (score each doc 1–5 per dimension)

### Findability — Is it in the right place?
- 5: Correct folder, correct naming convention, correct labels already applied
- 3: Right folder but missing labels or poor title
- 1: Wrong folder, no labels, title doesn't describe content

### Freshness — Is it current?
- 5: Updated within 90 days OR evergreen and explicitly marked as such
- 3: Updated 90–180 days ago, no freshness warning
- 1: Over 180 days old, or contains clearly outdated info (old pricing, deprecated features, former team members)

### Completeness — Does it do its job?
- 5: Clear purpose, covers the topic fully, a Sales rep can use it without follow-up
- 3: Clear purpose but missing key sections or leaves questions unanswered
- 1: Incomplete, stub, or confusing

### Clarity — Is it easy to use?
- 5: Well-structured, scannable, uses headers and examples, no unexplained jargon
- 3: Readable but dense or poorly formatted
- 1: Wall of text, no structure, hard to extract the key point quickly

**Overall score** = average of the four dimensions (round to 1 decimal place).

---

## Label taxonomy

Assign ONE primary label and as many secondary labels as apply.

**Primary (pick one):**
- `product` — explains product features, capabilities, or limitations
- `process` — explains how to do something (for the Sales team)
- `competitive` — competitive intel, objection handling, battle cards
- `pricing` — pricing, packaging, discounts, deal desk guidance
- `customer` — case studies, references, customer-specific info
- `onboarding` — for new Sales reps
- `evergreen` — foundational content unlikely to change

**Secondary (all that apply):**
- `needs-update` — content is stale or likely outdated
- `needs-owner` — no clear owner identified
- `high-priority` — frequently used or critical for deals
- `draft` — not ready for use
- `archive-candidate` — no longer relevant, recommend archiving

---

## Steps

### Step 1: Find the folder
Search Google Drive for a folder named "Sales Knowledge Base". If the user
specifies a different folder name, use that. If multiple matches exist, use
the most recently modified. If not found, ask the user to confirm the folder name.

### Step 2: List all documents
Retrieve all files in the folder. If more than 30 files exist, audit the 30
most recently modified and note that the audit is partial.

### Step 3: Read each document
Use the Google Drive connector to read each file's content and metadata:
title, last modified date, owner (if available). If a document is access-restricted
or returns an error, note "Access restricted — skipped" and continue.

### Step 4: Evaluate each document
For each document, apply the evaluation rubric above and score all four
dimensions. Calculate the overall average. Assign primary and secondary labels
from the taxonomy above.

### Step 5: Produce the audit report
Write the report using the format below. Save it as
`kb-audit-[YYYY-MM-DD].md` using today's date.

---

## Output format

```
# Knowledge Base Audit
Date: [date]
Folder audited: [folder name]
Documents reviewed: [count]
Auditor: Claude (scheduled)

---

## Executive Summary
[3–5 sentences: overall health of the KB, top 2–3 issues, recommended first action]

## Score Distribution
| Score range | Count | % of total |
|-------------|-------|------------|
| 4.0–5.0     |       |            |
| 2.5–3.9     |       |            |
| 1.0–2.4     |       |            |

## Documents Requiring Immediate Action
[Docs scoring below 2.5 on ANY single dimension]

| Document | Issue | Recommended action |
|----------|-------|--------------------|

---

## Full Audit

### [Document title]
**URL:** [link]
**Last modified:** [date]
**Primary label:** [label]
**Secondary labels:** [labels or none]

| Dimension    | Score | Notes |
|--------------|-------|-------|
| Findability  |       |       |
| Freshness    |       |       |
| Completeness |       |       |
| Clarity      |       |       |
| **Overall**  |       |       |

**Summary:** [1–2 sentences on what this doc is and what needs to happen]

---
[repeat for each document]

---

## Recommended Label Changes
[Table of docs where current labels don't match recommended labels]

| Document | Current label | Recommended label | Reason |
|----------|--------------|-------------------|--------|

## Archiving Candidates
[List with brief reason for each]
```

---

## Constraints

- NEVER modify or delete any document. Read only.
- Do not fabricate content about documents you cannot read. Mark them as unreadable.
- Always complete the audit even if some documents are inaccessible.
