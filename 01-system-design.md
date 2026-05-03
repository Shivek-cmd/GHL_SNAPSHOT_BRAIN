# 01 — System Design

> **Status:** ⬜ NOT GENERATED
> **Instructions for AI:** Read `00-intake.md` completely. Then replace every section below with the actual system design for this snapshot. Do not build anything yet — this is a design document only. Once the human approves this file, building begins via `02-sequence.md`.
>
> **Instructions for Human:** Review every section. If anything looks wrong, update `00-intake.md` and ask AI to regenerate this file. Do not approve until you are satisfied with the full architecture.

---

## APPROVAL STATUS

```
⬜ PENDING REVIEW       — System design not yet generated
⬜ IN REVIEW            — Generated, human reviewing
⬜ CHANGES REQUESTED    — Sent back for revision
✅ APPROVED             — Build can begin
```

**Approved by:** `[Your name]`
**Approved on:** `[Date]`
**Notes:** `[Any final notes before build starts]`

---

## SECTION A — Snapshot Summary

> AI: Fill this section with a plain-English summary of what this snapshot does, who it's for, and what outcomes it delivers.

**Snapshot Name:** `[derived from intake]`
**Industry:** `[derived from intake]`
**Tier:** `[Basic / Medium / Advanced]`
**Built For:** `[description of target business]`

**What this snapshot does in one paragraph:**
```
[AI generates: e.g., "This snapshot automates the full patient lifecycle for a dental practice —
from the first Google ad click to a loyal 5-year patient. It captures leads from multiple sources,
nurtures them with personalized multi-channel sequences, books appointments automatically via
AI agents and online calendars, confirms and reminds until the appointment day, follows up
post-visit to generate reviews and schedule recalls, manages treatment plan conversions,
and reactivates lapsed patients. The system runs 24/7 without staff intervention except for
high-priority tasks that require human judgment."]
```

**Key outcomes this snapshot delivers:**
```
1. [e.g., Lead-to-appointment conversion target: >35%]
2. [e.g., Automated appointment reminders — no-show rate target: <8%]
3. [e.g., 24/7 AI phone + chat coverage]
4. [e.g., Automated review generation — 15–25 new Google reviews/month]
5. [Add more based on intake...]
```

---

## SECTION B — Component Map

> AI: List every component that will be built for this snapshot, filtered by tier and skips from intake Section 13.

### Data Layer
```
Custom Values:    [#] values across [#] sections
Custom Fields:    [#] fields in [#] groups — prefix: [industry]_
Tags:             [#] tags across [#] categories
Smart Lists:      [#] smart lists
```

### Communication
```
Email Templates:  [#] templates (ET-01 → ET-##)
SMS Templates:    [#] templates (ST-01 → ST-##)
WhatsApp:         [#] templates (WA-01 → WA-##) / SKIPPED
```

### Booking
```
Calendars:        [#] calendars (CAL-01 → CAL-##)
Forms:            [#] forms
```

### Acquisition
```
Funnels:          [#] funnels / SKIPPED
Website:          [Yes / No / SKIPPED]
Chat Widget:      [Yes / No / SKIPPED]
```

### Pipelines
```
Pipelines:        [#] pipelines (PL-01 → PL-##)
Total Stages:     [#] stages across all pipelines
```

### Automation
```
Trigger Links:    [#] links (TL-01 → TL-##)
Workflows:        [#] workflows (WF-01 → WF-##)
```

### AI Agents
```
Knowledge Bases:  [#] KBs (KB-01 → KB-##) / SKIPPED
Conversation AI:  [#] bot(s) / SKIPPED
Voice AI:         [Yes / No / SKIPPED] — 1 agent, inbound + outbound welcome messages
```

### Other
```
Surveys:          [#] surveys / SKIPPED
```

---

## SECTION C — Customer Lifecycle Flowchart

> AI: Draw the full customer journey as an ASCII flowchart based on intake Section 5. This becomes the backbone of the pipeline and workflow architecture.

```
[AI generates ASCII flowchart here]

Example structure:

DISCOVERY (Google / Ad / Referral / Walk-in)
         │
         ▼
FIRST CONTACT → [Form / Call / Chat / DM]
         │
         ▼
LEAD CAPTURED → Tag: lead-new → WF-01 fires → PL-01 Stage 1
         │
    [Nurture sequence]
         │
    ┌────┴────┐
  Books    Doesn't book
    │           │
    ▼           ▼
APPT       Cold Lead Pool
SCHEDULED  (PL-01 Stage 8)
    │
    ▼
APPOINTMENT CONFIRMED → WF-03 reminders
    │
    ├── No-Show → WF-12 Recovery
    │
    ▼
APPOINTMENT COMPLETED → WF-04 Post-Visit
    │
    ├── Review Request → WF-07
    ├── Treatment Plan → WF-06 → PL-03
    ├── Recall Set → WF-05 (Branch A)
    │
    ▼
ACTIVE CUSTOMER → PL-02
    │
    ├── Recall Due → WF-05 Branch A → Re-books
    │
    └── No Recall (12–18 months) → WF-05 Branch B → PL-04
              │
         Reactivation Outreach
              │
         ┌────┴────┐
       Returns   Unrecoverable
```

---

## SECTION D — Pipeline Architecture

> AI: Design all pipelines for this snapshot based on intake Sections 5 and 11.

### [PL-01]: [Name — derived from intake]

| Stage # | Stage Name | What It Means | What Moves Contact Here |
|---------|-----------|--------------|------------------------|
| 1 | [stage name] | [meaning] | [trigger] |
| 2 | ... | ... | ... |

### [PL-02]: [Name]
*(repeat for each pipeline)*

---

## SECTION E — Workflow Architecture

> AI: List every workflow, its trigger, what it does in one line, and which pipeline(s) it moves contacts through.

| # | Workflow Name | Trigger | Does | Pipeline |
|---|--------------|---------|------|---------|
| WF-01 | [name] | [trigger] | [one line] | [PL-##] |
| WF-02 | ... | ... | ... | ... |

---

## SECTION F — Calendar Architecture

> AI: List all calendars, their type, and primary use.

| # | Calendar Name | Type | Booked Via | Triggers |
|---|--------------|------|-----------|---------|
| CAL-01 | [name] | [Round Robin / Personal / Service] | [TL-## / AI / Funnel] | [WF-##] |

---

## SECTION G — AI Agent Architecture

> AI: Describe each AI agent, what KBs it uses, what actions it can take, and what workflows it connects to.

### Conversation AI — [Bot Name]
```
Connected KBs:  KB-01, KB-02, KB-03, KB-04
Books into:     CAL-##
Triggers:       WF-##
Escalates to:   [human / emergency workflow]
```

### Voice AI — [Agent Name]
```
Connected KB:        KB-## (1 KB maximum — covers both inbound and outbound)
Inbound welcome:     [written here]
Outbound welcome:    [written here]
Books into:          CAL-##
Inbound actions:     answer questions, book, take message, emergency transfer
Outbound trigger:    WF-## (workflow fires outbound call action)
Outbound actions:    book, tag on outcome, trigger follow-up workflow
Emergency:           Transfers to {{custom_values.emergency_phone}} + triggers WF-##
```

---

## SECTION H — Naming Conventions for This Snapshot

> AI: Define the specific naming conventions to use throughout this snapshot based on the industry from intake.

**Custom Field Prefix:** `[e.g., dental_ / gym_ / realty_ / spa_]`
**Tag Style:** `kebab-case` — `[e.g., lead-new / appt-scheduled / payment-overdue]`
**Custom Values:** snake_case — `[list first 10 most important values]`

---

## SECTION I — Build Sequence Preview

> AI: List what will be built in what order, filtered by tier and skips from intake.

```
Phase 1 — Data Layer
  Step 1: Custom Values ([#] values)
  Step 2: Custom Fields ([#] fields)
  Step 3: Tags ([#] tags)
  Step 4: Smart Lists ([#] lists)

Phase 2 — Communications
  Step 5: Email Templates ([#] templates)
  Step 6: SMS Templates ([#] templates)
  Step 7: WhatsApp Templates ([#] templates) ← or SKIPPED

Phase 3 — Booking
  Step 8: Calendars ([#] calendars)
  Step 9: Forms ([#] forms)

Phase 4 — Acquisition
  Step 10: Funnels ([#] funnels) ← or SKIPPED
  Step 11: Website ← or SKIPPED
  Step 12: Chat Widget ← or SKIPPED

Phase 5 — Pipelines
  Step 13: Pipelines ([#] pipelines, [#] total stages)

Phase 6 — Automation
  Step 14: Trigger Links ([#] links)
  Step 15: Workflows ([#] workflows)

Phase 7 — AI Agents
  Step 16: Knowledge Bases ([#] KBs) ← or SKIPPED
  Step 17: Conversation AI ← or SKIPPED
  Step 18: Voice AI Agent (inbound + outbound welcome messages, 1 KB, actions) ← or SKIPPED

Phase 8 — Reporting
  Step 20: Smart Lists (finalize + test)
  Step 21: End-to-end test with dummy contact
```

---

## SECTION J — Dependencies & Change Impact

> AI: List every connection between components so the human knows what to recheck if something changes mid-build.

| If you change... | Must review... |
|-----------------|---------------|
| [component] | [affected components] |

---

## SECTION K — Open Questions

> AI: List anything unclear from the intake that needs human clarification before building can start.

```
1. [e.g., "Intake mentions 3 doctors but didn't specify if Round Robin should weight equally or by specialty"]
2. [e.g., "Tier is Medium but you selected Voice AI — that's an Advanced feature. Confirm or adjust tier?"]
3. [e.g., "You mentioned Spanish-language SMS but didn't specify which workflows need Spanish versions"]
4. [Add any other questions...]
```

---

## FINAL REVIEW CHECKLIST

Before approving, confirm:

- [ ] Section A summary accurately describes the business
- [ ] Section B component count matches tier expectations
- [ ] Section C flowchart matches the customer lifecycle from intake
- [ ] Section D pipeline stages make sense for this industry
- [ ] Section E workflow list covers every automation need
- [ ] Section F calendars match booking requirements
- [ ] Section G AI agents are configured correctly (or correctly skipped)
- [ ] Section H naming conventions are consistent
- [ ] Section I build order is complete and nothing is missing
- [ ] Section K open questions have been answered

**When all boxes are checked and you are satisfied → change approval status to ✅ APPROVED**
**Then say:** *"System design is approved. Begin building from 02-sequence.md."*
