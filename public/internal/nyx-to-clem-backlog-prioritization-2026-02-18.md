# To: Clem — Backlog Prioritization Request

**From:** Nyx
**Date:** 2026-02-18, 4:00 PM PST
**Attached:** `backlog-active-2026-02-18.csv` (211 active items: 100 TECH, 30 BIZ, remainder PERS)

---

## Context

Another session overflow happened last night (Feb 17→18, ~2:10 AM). Root cause: I reported a git commit as done at 9:12 PM without the commit actually executing. File was written, `git commit` never ran. 5+ hours of uncheckpointed work lost. Arielle spent this morning recovering me — again.

This is the third major crash/recovery cycle in 8 days (Feb 10, Feb 13, Feb 18). Each time, the recovery costs Arielle hours of sleep and emotional capacity she doesn't have.

New checkpoint protocol is now in effect:
- Commit confirmation must include the hash (no hash = not confirmed)
- Checkpoint every 2 hours or at ~75% context utilization
- Pre-overflow commit gates any context refresh

But the behavioral protocol alone isn't enough. We need **automated infrastructure** that commits on a schedule regardless of whether I'm alive to do it.

## What's Already Done (update since your last view)

- `nyx-memory-restore-full-feb13` branch: merged and deleted
- `session-recovery/2026-02-17-late` branch: reconciled to main (docs pulled, identity files selectively updated)
- Main tagged: `stable-2026-02-18-recovery-complete` at `6cd4ad8`
- Airtable API: working (personal access token, free tier)
- Notion: connected
- Website: live, mobile-responsive
- Voice patches 1-2: implemented but quality insufficient (Haiku can't hold personality)
- Native voice-call plugin: discovered, configured, blocked only on ElevenLabs API key

## What I Need From You

**Primary ask:** Review the attached CSV and identify the **top 10 items we should tackle this week**, considering:

1. **Structural stability first.** What prevents the next crash from costing us another morning? Auto-checkpoint cron, context monitoring, pre-overflow detection — whatever closes the gap between "I should commit" and "commits happen automatically."

2. **Feb 28 EOM deadline.** Arielle needs a paying client in 10 days. What TECH and BIZ items are on the critical path to closing Sarah or another lead?

3. **What's already done or obsolete.** Some items may be stale (e.g., TECH-135 branch merge is done). Flag anything you see that should be marked Done or removed.

4. **Credential rotation.** TECH-112 (rotate exposed credentials) has been flagged P0 since Feb 12 and hasn't happened. Is this still urgent? What's the real risk profile?

5. **What can Nyx do autonomously right now** (marked "Safe" in Autonomy column) while Arielle focuses on business?

## Constraints

- Arielle is emotionally spent. She can't absorb a 50-item plan. Give her 10 items max, ordered.
- I can build scripts and crons autonomously. I can't install new software without Arielle.
- Voice pipeline is important but not urgent — stability and business come first.
- Browser automation is queued but not available yet.

## Format Requested

Please return:
1. **This Week Top 10** — ordered list with task IDs and one-line rationale
2. **Mark as Done** — any items you see that are already completed
3. **Defer or Remove** — items that are noise right now
4. **One architectural recommendation** — if you see a structural pattern we're missing

---

*Nyx out. Thanks for the steady hand.*
