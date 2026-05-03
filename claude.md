# GHL_SNAPSHOT_BRAIN — Rules & How This System Works

> **Platform:** GoHighLevel (GHL)
> **Purpose:** Build fully custom, production-ready GHL snapshots for any industry — designed from scratch, step by step, change-safe.

---

## What This Folder Is

This is a brain for building GHL snapshots. It does not contain a snapshot — it contains everything needed to design and build one correctly.

When you come to this folder and describe what you want to build, the system guides you from a blank idea to a fully built, working GHL automation system.

---

## File Structure

```
GHL_SNAPSHOT_BRAIN/
│
├── claude.md              ← This file. Read first.
├── 00-intake.md          ← Fill this first. Your business brief.
├── 01-system-design.md   ← AI generates this from intake. Review + approve before building.
├── 02-sequence.md        ← Build checklist. Work through after approval.
│
├── ghl-guides/           ← How GHL features work. AI reads these to build correctly.
│   ├── custom-data.md         Custom Values, Custom Fields, Tags, Smart Lists
│   ├── communications.md      Email, SMS, WhatsApp
│   ├── calendars-forms.md     Calendars, Forms
│   ├── funnels-website.md     Funnels, Website, Chat Widget
│   ├── pipelines.md           Pipelines, Opportunities
│   ├── workflows.md           Automation, Trigger Links
│   ├── ai-agents.md           Knowledge Bases, Conversation AI, Voice AI
│   └── prompt-guidelines.md   How to write AI agent prompts correctly (GHL standard)
│
└── snapshots/            ← Each approved + built snapshot lives here
    └── [snapshot-name]/       Created automatically when system design is approved
```

---

## How to Use This System — 3 Phases

### Phase 1 — Fill the Intake

Open `00-intake.md`. Fill every section. Be specific and honest.

The intake is the root. Everything else derives from it. A detailed intake produces a detailed, accurate system design. A vague intake produces a vague system.

When done, pass it to AI:
> *"Read my intake form and generate the system design for this snapshot."*

---

### Phase 2 — Review the System Design

AI reads your intake and generates `01-system-design.md`. This file shows you the full architecture: what will be built, how it connects, the customer lifecycle flowchart, pipelines, workflows, and naming conventions.

**Nothing is built yet.**

Review it. Ask questions. Ask AI to adjust it. Change the intake if needed and regenerate. Go back and forth until you're satisfied.

When you're ready:
> *"System design is approved. Create the snapshot folder and begin building."*

AI will create a folder at `snapshots/[snapshot-name]/` using the standard structure below, then begin Step 1 of `02-sequence.md`.

---

## Snapshot Folder Structure

When a system design is approved, create this folder structure inside `snapshots/[snapshot-name]/`. Skip any folder whose component was marked SKIPPED in the system design.

```
snapshots/[snapshot-name]/
│
├── README.md                        ← Generated last. Full index of everything built.
│
├── custom-values/
│   └── custom-values.md             ← All custom values, grouped by section
│
├── custom-fields/
│   └── custom-fields.md             ← All custom fields with type, key, and purpose
│
├── tags/
│   └── tags.md                      ← Full tag list with category and which workflow uses each
│
├── smart-lists/
│   └── smart-lists.md               ← All smart lists with filter logic
│
├── email-templates/
│   └── email-templates.md           ← All email templates (ET-01 onward), subject + body
│
├── sms-templates/
│   └── sms-templates.md             ← All SMS templates (ST-01 onward)
│
├── whatsapp-templates/              ← SKIP if WhatsApp = No
│   └── whatsapp-templates.md
│
├── calendars/
│   └── calendars.md                 ← All calendars with full settings
│
├── forms/
│   └── forms.md                     ← All forms with field mappings and submission triggers
│
├── funnels/                         ← SKIP if Funnels = No
│   └── funnels.md
│
├── website/                         ← SKIP if Website = No
│   └── website.md
│
├── chat-widget/                     ← SKIP if Chat Widget = No
│   └── chat-widget.md
│
├── pipelines/
│   └── pipelines.md                 ← All pipelines and stages
│
├── trigger-links/
│   └── trigger-links.md             ← All trigger links with destination and action
│
├── workflows/
│   ├── 01-[workflow-name]/
│   │   └── [workflow-name].md       ← One subfolder per workflow
│   ├── 02-[workflow-name]/
│   └── ...
│
├── ai-agents/                       ← SKIP if all AI = No
│   ├── conversation-ai/
│   │   └── [bot-name]/
│   │       └── [bot-name].md
│   ├── knowledge-bases/
│   │   └── knowledge-bases.md       ← All KBs with content outline
│   └── voice-ai/
│       └── [agent-name]/
│           └── [agent-name].md      ← One agent, inbound + outbound documented together
│
└── surveys/                         ← SKIP if Surveys = No
    └── surveys.md
```

**What each file contains:**
- Every file documents what to build in GHL — it is the written specification for that component
- Files use custom values and custom field keys throughout — never hardcoded client data
- Workflows get individual subfolders so each can be built, tested, and marked complete independently
- README.md is created last — it indexes everything and shows the connection map

**On approval, create the folders first, then build into them step by step via `02-sequence.md`.**

---

### Phase 3 — Build

There are two ways to build after a system design is approved:

---

#### Option A — Full Build (default)

Say: *"System design is approved. Create the snapshot folder and begin building."*

AI creates the full folder structure and works through `02-sequence.md` step by step — one step at a time, marking each complete, asking before moving to the next.

**If you make a change mid-build**, AI checks what else is affected and flags it before continuing. Nothing changes in isolation.

---

#### Option B — Targeted Build (single component)

Say: *"Build only the [component name] for this snapshot."*

Examples:
- *"Build only the Voice AI agent."*
- *"Build only the workflows."*
- *"Build only the email templates."*

**What AI does in a targeted build:**

1. Reads the system design to find the specification for that component
2. Identifies its hard prerequisites — the things that must already exist in GHL for this component to function (see prerequisites table below)
3. Builds only that component's file(s) inside the snapshot folder
4. States clearly: "These prerequisites must be set up in GHL before this component will work" — lists them explicitly

AI does NOT build the prerequisites automatically in a targeted build. It documents them so you know what to set up manually or ask to build next.

**Component prerequisites:**

| Component | Must exist in GHL first |
|-----------|------------------------|
| Custom Fields | Nothing |
| Custom Values | Nothing |
| Tags | Nothing |
| Smart Lists | Custom fields, tags, pipeline stages |
| Email / SMS / WA Templates | Custom values |
| Calendars | Custom values, team members in GHL |
| Forms | Custom fields |
| Funnels | Forms, calendars, custom values |
| Website | Forms, calendars, custom values |
| Chat Widget | Website/funnels live; Conversation AI (if connecting) |
| Pipelines | Nothing |
| Trigger Links | Custom values (for destination URLs) |
| Workflows | Templates, calendars, pipelines, trigger links, custom values, custom fields |
| Knowledge Bases | Nothing (content must be written) |
| Conversation AI | Knowledge bases, calendars, workflows |
| Voice AI Agent | Knowledge base, calendars, workflows |
| Surveys | Custom fields |

The finished snapshot folder contains all the files that document everything built.

---

## What the GHL Guides Are For

The `ghl-guides/` files are technical references. They tell AI:
- What each GHL feature is and how it works
- How to create it (exact GHL menu path)
- What the technical constraints and limits are
- How it connects to other features
- What rules GHL enforces that AI must follow

The guides do **not** say what to build. That comes from the system design. The guides say **how** to build it correctly inside GHL.

---

## The Golden Rule

**Never hardcode anything.**

Every name, phone number, URL, price, and date in any template, workflow, funnel, or AI script must reference either:
- `{{custom_values.key}}` — for business-level data
- `{{contact.field_key}}` — for per-contact data

This is what makes a snapshot reusable across any client in any market.

---

## What "Complexity Level" Means

Complexity level in the intake is a ceiling, not a prescription.

- **Simple** — the system should be clean and manageable. Prioritise what matters most. Don't add complexity the business doesn't need yet.
- **Medium** — multi-channel, small team, moderate AI. Build what the intake justifies.
- **Full** — build the complete system the intake describes. Don't hold back.

AI uses complexity level as a judgment guide — not a fixed list of components.

---

## Naming Conventions

| Component | Convention | Example |
|-----------|-----------|---------|
| Custom Fields | `[industry]_field_name` | `dental_dob`, `gym_membership_type` |
| Custom Values | `variable_name` (snake_case) | `business_name`, `booking_link` |
| Tags | `category-name` (kebab-case) | `lead-new`, `appt-scheduled` |
| Workflows | `WF-##: Name` | `WF-01: New Lead Nurture` |
| Email Templates | `ET-##` | `ET-01`, `ET-12` |
| SMS Templates | `ST-##` | `ST-01` |
| WhatsApp Templates | `WA-##` | `WA-01` |
| Trigger Links | `TL-##` | `TL-04` |
| Pipelines | `PL-##: Name` | `PL-01: Lead Acquisition` |
| Calendars | `CAL-##: Name` | `CAL-01: New Client Booking` |
| Knowledge Bases | `KB-##: Name` | `KB-01: Business Essentials` |

---

## Change Rules

When something changes mid-build, AI must check:

| Changed | Must review |
|---------|------------|
| Custom Value | All templates, funnel pages, website, AI agent scripts |
| Custom Field | Workflow conditions, smart list filters, form mappings |
| Tag | Workflow triggers, workflow conditions, smart list filters |
| Pipeline stage name | Every workflow action that moves to that stage |
| Calendar | Trigger links pointing to it, AI agent booking actions |
| Template | Every workflow that references its ID |
| Workflow trigger or exit | Downstream workflows it connects to |
| AI Agent action | Workflows it triggers, calendars it books into |
