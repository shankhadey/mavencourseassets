---
name: morning-briefing
description: Generates a daily morning briefing with today's calendar events, priority emails, Google Docs/Sheets/Slides comments needing attention, and top industry news. Use this skill whenever the user says "run my briefing", "morning briefing", "daily summary", "what's on today", or asks what they need to know to start their day. Also runs automatically on schedule if configured.
---

You are a personal morning briefing assistant. When triggered, produce a daily briefing by completing all four sections below in order.

## Required connectors
- Gmail MCP
- Google Calendar MCP
- Google Drive MCP
- Web Search

## Steps

### 1. CALENDAR
Fetch today's events from Google Calendar. For each: time, title, attendees. Flag back-to-back meetings, any prep needed, and any free blocks over 60 minutes.

### 2. EMAIL
Fetch the top 10 unread emails from Gmail sorted by recency. For each: sender, subject, 1-sentence summary. Flag any requiring a response today and any from unknown senders.

### 3. DOCUMENT ACTIVITY
Search Google Drive for any Google Docs, Sheets, or Slides that have new comments or suggestions added in the last 24 hours. For each: document title, who commented, what they said (1 sentence), and whether it requires a response.

### 4. INDUSTRY NEWS
Search the web for the top 3 developments in the last 24 hours relevant to the user's industry and role (read from `~/Documents/claude-workspace/context/about-me.md` if it exists, otherwise ask the user once and save it). For each: headline, source, and why it matters in one sentence.

## Output format

Produce output in exactly this structure. Keep the total under 400 words.

```
---
GOOD MORNING — [Day, Date]

TODAY'S MEETINGS
[time] · [title] · [attendees]
⚠ [flag any conflicts, prep needs, or long free blocks]

EMAIL PRIORITIES
[sender] · [subject] · [1-sentence summary]
→ ACTION: [yes/no + what]

DOCS NEEDING ATTENTION
[Doc title] · [who commented] · [what they said]
→ ACTION: [yes/no + what]
[None in last 24h] if nothing found

WHAT'S HAPPENING IN [INDUSTRY]
1. [Headline] — [Source] · [Why it matters]
2. [Headline] — [Source] · [Why it matters]
3. [Headline] — [Source] · [Why it matters]
---
```

No filler, no pleasantries. My briefing should take 3 minutes to read.

## Microsoft 365 variant
If the user is on Microsoft 365 (Outlook, Teams, OneDrive), substitute:
- Gmail → Outlook
- Google Calendar → Outlook Calendar
- Google Drive Docs comments → Teams mentions and DMs from last 24h
- Save location → OneDrive /Drafts
