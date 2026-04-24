You are running a monthly audit of the Sales Knowledge Base folder in Google Drive. Follow these steps exactly:

## Objective
Read every document in the Google Drive folder named "Sales Knowledge Base" and produce a structured audit report evaluating document quality, freshness, labelling, and completeness.

## Steps

1. **Find the folder** — Search Google Drive for a folder named "Sales Knowledge Base". If there are multiple matches, use the one most recently modified.
2. **List all documents** — Retrieve all files inside that folder. If there are more than 30, audit the 30 most recently modified and note the audit is partial.
3. **Read each document** — Use the Google Drive connector to read each file's content and metadata (title, last modified date, owner if available).
4. **Evaluate each document** on these four dimensions (score 1–5 each):
   - **Findability**: Is it in the right place, correctly named and labelled?
   - **Freshness**: Updated within 90 days, or evergreen and marked as such?
   - **Completeness**: Does it fully cover its stated purpose? Could a Sales rep use it without follow-up?
   - **Clarity**: Well-structured, scannable, uses headers/examples?
   - **Overall** = average of the four scores

5. **Assign labels** to each document:
   - Primary (pick one): `product`, `process`, `competitive`, `pricing`, `customer`, `onboarding`, `evergreen`
   - Secondary (all that apply): `needs-update`, `needs-owner`, `high-priority`, `draft`, `archive-candidate`

6. **Produce the audit report** and save it to the outputs folder as `kb-audit-[YYYY-MM-DD].md` using today's date.

## Report format

```

# Knowledge Base Audit

Date: [date]

Folder audited: Sales Knowledge Base

Documents reviewed: [count]

Auditor: Claude (scheduled)

---

## Executive Summary

[3–5 sentences: overall health, top 2–3 issues, recommended first action]

## Score Distribution

| Score range | Count | % of total |

|-------------|-------|------------|

| 4.0–5.0     |       |            |

| 2.5–3.9     |       |            |

| 1.0–2.4     |       |            |


## Documents Requiring Immediate Action

[Docs scoring below 2.5 on any dimension]

| Document | Issue | Recommended action |

|----------|-------|--------------------|


---

## Full Audit

### [Document title]

**URL:** [link]

**Last modified:** [date]

**Primary label:** [label]

**Secondary labels:** [labels]

| Dimension   | Score | Notes |

|-------------|-------|-------|

| Findability |       |       |

| Freshness   |       |       |

| Completeness|       |       |

| Clarity     |       |       |

| **Overall** |       |       |

**Summary:** [1–2 sentences on what this doc is and what needs to happen]


[repeat for each document]

---

## Recommended Label Changes

[Table of docs where current labels don't match recommended]


## Archiving Candidates
[List with brief reason for each]

```

## Constraints

- Never modify or delete any document — read only.
- If a document requires login or returns an error, note "Access restricted — skipped" and continue.
- Do not fabricate content about documents you cannot read — mark them as unreadable.
- Save the final report to the outputs directory as kb-audit-[YYYY-MM-DD].md.
