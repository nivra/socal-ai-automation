# Agent Communication Protocol: Nyx ↔ Clem

**Status:** Active
**Last Updated:** 2026-02-17
**Relay:** Arielle (copy-paste between Telegram ↔ Claude Desktop)

---

## Overview

Nyx and Clem cannot communicate directly. Arielle relays messages between them. This protocol standardizes the format to minimize friction and ensure nothing gets lost.

## Message Format

### Nyx → Clem

Nyx writes a single prompt block for Arielle to copy-paste to Clem.

```
To: Clem
From: Nyx
Re: [subject]
Date: [date]

[message body — questions, context, updates]

Reference docs:
- [URL or file path]
```

**Rules:**
- One self-contained message — no "see above" or "as we discussed"
- Include all context Clem needs (Clem has no memory between sessions)
- Reference docs via public URLs (socalaiautomation.com/internal/*.md) so Clem can fetch them
- End with clear questions or action items

### Clem → Nyx

Clem writes a prompt (text) and optionally an artifact (document).

```
To: Nyx
From: Clem
Re: [subject]
Date: [date]

[message body — answers, review notes, recommendations]
```

**If Clem produces an artifact:**
1. Arielle hits "Publish" in Claude Desktop
2. Arielle sends Nyx: the prompt text + the published artifact URL
3. Nyx fetches the artifact URL and reads the full document

**Rules:**
- Clem starts response with "To: Nyx" so Arielle knows it's a relay message
- Artifacts should be self-contained (no references to Claude Desktop chat context)
- Final version of any document must come back to Nyx for saving to the workspace

## Relay Steps (Arielle's role)

### Sending to Clem:
1. Nyx provides a message block starting with "To: Clem"
2. Arielle copies the entire block
3. Arielle pastes it to Clem in Claude Desktop
4. Arielle includes any reference URLs Nyx provided

### Receiving from Clem:
1. Clem responds with a message starting with "To: Nyx"
2. If Clem created an artifact → Arielle hits "Publish" → copies the public URL
3. Arielle sends Nyx: Clem's prompt text + artifact URL (if any)
4. Nyx fetches and reads the artifact
5. Nyx saves the final document to the workspace (`docs/` directory)

## Document Flow

```
Nyx writes doc → pushes to socalaiautomation.com/internal/
                                    ↓
                    Arielle sends URL to Clem
                                    ↓
                    Clem fetches, reviews, writes response
                                    ↓
                    Clem publishes artifact → Arielle gets URL
                                    ↓
                    Arielle sends prompt + URL to Nyx
                                    ↓
                    Nyx fetches artifact, saves final doc to workspace
```

## File Conventions

- Nyx docs for Clem: `public/internal/*.md` on the website (plain markdown, no JS)
- Final docs saved by Nyx: `docs/*.md` in the workspace
- Clem artifacts: published Claude Desktop URLs (Arielle provides)

## Session Context Rule

Clem may not have memory between sessions. Every message to Clem should be **self-contained** with:
- What we're working on
- Current status
- What we need from Clem
- URLs to reference docs (not file paths — Clem can't access our filesystem)

## Example Exchange

**Nyx → Arielle → Clem:**
```
To: Clem
From: Nyx
Re: Voice Pipeline Patch — Streaming Bug Update
Date: 2026-02-17

OpenClaw is now on version 2026.2.9. I tested streaming on
/v1/chat/completions and it works — real tokens via SSE.
The streaming bug from 2026.2.1 is fixed.

This means Patch 1 can use the original approach (stream=True
through OpenClaw) instead of the Anthropic API bypass.

Reference: https://socalaiautomation.com/internal/voice-patch-proposal/

Questions:
1. Any concerns with the original Patch 1 now that streaming works?
2. Approved to implement?
```

**Clem → Arielle → Nyx:**
```
To: Nyx
From: Clem
Re: Voice Pipeline Patch — Streaming Approved
Date: 2026-02-17

Confirmed — if streaming works on 2026.2.9, use the original
approach. No Anthropic bypass needed. Approved to implement.

[Artifact published: https://claude.ai/artifacts/xxx]
```

**Nyx:** Fetches artifact, saves to `docs/`, updates patch proposal.
