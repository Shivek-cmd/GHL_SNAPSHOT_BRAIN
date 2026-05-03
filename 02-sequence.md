# 02 — Build Sequence

> **Pre-condition:** `01-system-design.md` must be approved before Step 1.
> **How this works:** Work through phases in order. Each step tells you the GHL location and what the system design specifies to build there. Mark `[x]` when done. Mark `[SKIP]` with a reason if skipping. After each step, AI will confirm what's next and what's now unlocked.

---

## Build Status

```
Snapshot Name:    [from system design]
Industry:         [from system design]
Complexity:       [Simple / Medium / Full]
Snapshot Folder:  snapshots/[name]/
Started:          [date]
Last Updated:     [date]
```

---

## Phase 1 — Data Layer
*Build first. Everything else references these.*

**[ ] Step 1 — Custom Values**
GHL: Settings → Custom Values
Guide: `ghl-guides/custom-data.md`
Build what system design specifies. These are the practice-wide variables.
→ Done when: all values created and named per convention

**[ ] Step 2 — Custom Fields**
GHL: Settings → Custom Fields → Contact
Guide: `ghl-guides/custom-data.md`
Build what system design specifies. Prefix all fields with `[industry]_`.
→ Done when: all fields created with correct types and keys

**[ ] Step 3 — Tags**
GHL: Applied via workflows / managed under Contacts
Guide: `ghl-guides/custom-data.md`
Create the tag list from system design. Confirm naming is kebab-case.
→ Done when: tag list documented; tags will auto-create when workflows use them

**[ ] Step 4 — Smart Lists**
GHL: Contacts → Filters → Save as Smart List
Guide: `ghl-guides/custom-data.md`
Build the operational lists from system design. Return here after Step 10 to finalise.
→ Done when: core smart lists live; flagged for review after workflows are built

---

## Phase 2 — Communications
*Write all message content before building workflows.*

**[ ] Step 5 — Email Templates**
GHL: Marketing → Emails → Templates
Guide: `ghl-guides/communications.md`
Build what system design specifies. No content inside workflows — templates only.
→ Done when: all templates created and numbered ET-01 onward

**[ ] Step 6 — SMS Templates**
GHL: Marketing → SMS / referenced in workflows
Guide: `ghl-guides/communications.md`
Skip if SMS = No in intake.
→ Done when: all templates created and numbered ST-01 onward

**[ ] Step 7 — WhatsApp Templates**
GHL: Settings → WhatsApp → Message Templates
Guide: `ghl-guides/communications.md`
Skip if WhatsApp = No in intake. Submit for Meta approval — build continues while waiting.
→ Done when: all templates submitted and numbered WA-01 onward

---

## Phase 3 — Booking
*Calendars and forms must exist before funnels and AI agents can reference them.*

**[ ] Step 8 — Calendars**
GHL: Calendars → Calendar Settings → + New Calendar
Guide: `ghl-guides/calendars-forms.md`
Build what system design specifies. Choose correct type per use case.
→ Done when: all calendars live, team assigned, confirmation workflow confirmed

**[ ] Step 9 — Forms**
GHL: Sites → Forms → + New Form
Guide: `ghl-guides/calendars-forms.md`
Build what system design specifies. Every field must map to a custom field.
→ Done when: all forms built, fields mapped, submission triggers confirmed

---

## Phase 4 — Acquisition
*Funnels embed forms and link to calendars — both must exist.*

**[ ] Step 10 — Funnels**
GHL: Sites → Funnels → + New Funnel
Guide: `ghl-guides/funnels-website.md`
Skip if funnels = No in intake.
→ Done when: all funnel pages live, forms embedded, CTAs linked to trigger links

**[ ] Step 11 — Website**
GHL: Sites → Websites
Guide: `ghl-guides/funnels-website.md`
Skip if website = No in intake.
→ Done when: all pages built, chat widget installed, tracking codes added

**[ ] Step 12 — Chat Widget**
GHL: Settings → Chat Widget
Guide: `ghl-guides/funnels-website.md`
Connect to Conversation AI after Step 13 is done. Configure first, connect later.
→ Done when: widget live on site, greeting set, AI connected (after Step 13)

---

## Phase 5 — Pipelines
*Must exist before workflows. Workflows reference stage names by exact text.*

**[ ] Step 13 — Pipelines**
GHL: Opportunities → Pipelines → + Add Pipeline
Guide: `ghl-guides/pipelines.md`
Build every pipeline from system design. Stage names must match exactly what workflows will reference.
→ Done when: all pipelines and stages created, test-moved a dummy contact through each

---

## Phase 6 — Automation
*Trigger links before workflows. Workflows reference TL IDs.*

**[ ] Step 14 — Trigger Links**
GHL: Marketing → Trigger Links → + New Trigger Link
Guide: `ghl-guides/workflows.md`
Build every trigger link from system design. Destinations use custom values — no hardcoded URLs.
→ Done when: all links created, actions confirmed, TL-## IDs documented

**[ ] Step 15 — Workflows**
GHL: Automation → Workflows → + New Workflow
Guide: `ghl-guides/workflows.md`
Build in dependency order from system design. Test each workflow before activating.
→ Done when: all workflows live, tested with dummy contact, pipelines moving correctly

---

## Phase 7 — AI Agents
*Knowledge bases before AI agents. Workflows and calendars must exist.*

**[ ] Step 16 — Knowledge Bases**
GHL: Settings → Knowledge Base → + New
Guide: `ghl-guides/ai-agents.md`
Skip if all AI = No in intake. Max 4 KBs per Conversation AI. Max 1 per Voice AI.
→ Done when: KBs built, FAQs populated, web crawler URLs added

**[ ] Step 17 — Conversation AI**
GHL: Settings → Conversation AI
Guide: `ghl-guides/ai-agents.md`
Skip if Chat AI = No in intake.
→ Done when: bot configured, KBs attached with trigger instructions, all actions set, 10 test conversations passed

**[ ] Step 18 — Voice AI Agent**
GHL: Settings → Voice AI
Guide: `ghl-guides/ai-agents.md`
Skip if Voice AI = No in intake. One agent handles both inbound and outbound. Write the inbound welcome message and outbound welcome message separately — everything else (KB, instructions, actions) is configured once.
→ Done when: both welcome messages written, KB attached, all actions set, inbound test call placed, outbound test call triggered via workflow

---

## Phase 8 — Final

**[ ] Step 20 — Surveys**
GHL: Sites → Surveys → + New Survey
Guide: (standard GHL survey builder)
Skip if surveys = No in intake.
→ Done when: surveys built, NPS field connected, routing logic confirmed

**[ ] Step 21 — Smart Lists (Final)**
Return to smart lists built in Step 4. Add any workflow-specific or pipeline-specific lists that now make sense after everything is built.
→ Done when: all operational lists tested and showing correct contacts

**[ ] Step 22 — End-to-End Test**
Run a dummy contact through every path in the system design:
- Lead enters → nurture sequence → books → confirms → attends → review requested
- No-show path
- Emergency path (if built)
- AI agent booking path (if built)
→ Done when: all paths tested, pipelines moving, templates sending, no broken links

**[ ] Step 23 — Snapshot Export**
GHL: Agency View → Sub-Accounts → [this sub-account] → Export Snapshot
- Confirm all custom values are blank (not pre-filled with client data)
- Document any manual setup steps in a handoff note inside the snapshot folder
→ Done when: snapshot exported and test-imported in a blank sub-account

---

## Change Impact Check

Run this whenever you make a change mid-build:

| Changed | Must review |
|---------|------------|
| Custom Value | All email / SMS / WA templates, funnel pages, website, AI agent scripts, calendar settings |
| Custom Field | Workflow conditions using that field, smart list filters, form mappings |
| Tag name | Workflow triggers, workflow conditions, smart list filters |
| Pipeline stage name | Every workflow action that moves a contact to that stage |
| Calendar settings | Trigger links pointing to it, AI agent booking actions, confirmation workflows |
| Template content/ID | Every workflow that references that template |
| Workflow trigger/exit | Connected workflows, pipeline stages that depend on this workflow |
| AI Agent action | Workflows it triggers, calendars it books into, fields it updates |
| Form field | Custom field it maps to, workflow that fires on submission |
