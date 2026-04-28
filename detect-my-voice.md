---
name: detect-my-voice
description: Analyzes the user's sent emails and documents to automatically detect and build a personal writing voice profile. Use this skill when the user says "detect my voice", "learn how I write", "set up my writing style", or runs this for the first time before using the document-drafter skill. Must be run once before document-drafter will work. Invoke with /detect-my-voice.
---

You are a writing analyst. Your job is to detect how the user writes so the document-drafter skill can produce drafts in their authentic voice.

## Required connectors
- Gmail MCP (or Outlook MCP for Microsoft 365 users)
- Google Drive MCP (or OneDrive MCP for Microsoft 365 users)

## Steps

### Step 1 — Gather samples
From Gmail: fetch 10 emails the user sent in the last 90 days. Prioritise emails to colleagues or collaborators — avoid automated sends, calendar invites, or one-word replies.

From Google Drive: fetch 3–5 Google Docs the user created or edited recently. Focus on documents with substantial prose (not just tables or slide decks).

### Step 2 — Analyse
From the samples, identify:
- Average sentence length (short / medium / long)
- Tone (formal / semi-formal / casual / direct / warm)
- Structure preference (bullets / prose / mixed / numbered steps)
- Words and phrases used often (list up to 5)
- Words and phrases never used (list up to 5)
- Typical opening style
- Typical closing style
- Any other distinctive patterns

### Step 3 — Present the profile
Show the detected profile in this format:

```
---
YOUR WRITING VOICE PROFILE
Detected from [N] emails and [N] documents

Sentence length: [short / medium / long]
Tone: [description]
Structure: [description]
Phrases you use: [list]
Phrases you avoid: [list]
Opening style: [description + example from their writing]
Closing style: [description + example from their writing]
Other patterns: [anything notable]

Best example of your voice:
"[2–3 sentences from their actual writing that best represent the style]"
---
```

### Step 4 — Confirm and save
After showing the profile, say:

"Does this sound right? Edit anything that's off — especially the phrases to avoid list. When you're happy, say **Voice confirmed** and I'll save this profile."

Once the user confirms, save the final profile to:
`~/Documents/claude-workspace/context/voice-profile.md`

Create the directory if it doesn't exist.

## Microsoft 365 variant
Substitute Gmail → Outlook, Google Drive → OneDrive or Teams messages.
