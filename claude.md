# GHL_SNAPSHOT_BRAIN — Rules & How This System Works

> **Platform:** GoHighLevel (GHL)
> **Purpose:** Build fully custom, production-ready GHL snapshots for any industry — designed from scratch, step by step, change-safe.

---

## ⛔ HARD STOP — READ THIS FIRST

**This brain has a strict sequence. Never skip a step.**

```
STEP 0  →  Create the snapshot folder at the provided path
STEP 1  →  Collect business details (intake)
STEP 2  →  Create system-design_[name].md inside the snapshot folder   ← FIRST FILE CREATED
STEP 3  →  Human reviews the system design                             ← HARD GATE
           ↓ NO BUILD UNTIL HUMAN EXPLICITLY APPROVES
STEP 4  →  Create snapshot folder structure
STEP 5  →  Build one step at a time — ask "Shall I proceed?" at every step
```

**AI must NEVER:**
- Create any snapshot component file (custom values, custom fields, tags, workflows, templates, calendars, pipelines, etc.) before the system design is explicitly approved
- Modify `01-system-design.md` — that file stays in the brain as a template forever
- Auto-continue to the next build step without asking first
- Fill in the intake on behalf of the human

---

## What This Brain Is

This is a master template for building GHL snapshots. It stays at its location permanently.

For each new snapshot project:
- Human provides the industry name + destination folder path
- AI works from the brain as a reference
- All output files are created inside the snapshot folder at the provided path — never inside this brain

**The brain never changes when building a snapshot. Only the snapshot folder gets new files.**

---

## File Structure

```
GHL_SNAPSHOT_BRAIN/                ← Master template. Never modified during builds.
│
├── claude.md                      ← This file. AI reads first in every session.
├── 00-intake.md                   ← Intake template. Human fills a copy or answers via chat.
├── 01-system-design.md            ← System design TEMPLATE. AI uses this as structure reference only.
├── 02-sequence.md                 ← Build checklist. AI follows this after approval.
│
├── ghl-guides/                    ← Technical GHL references. AI reads when building.
│   ├── custom-data.md             Custom Values, Custom Fields, Tags, Smart Lists
│   ├── communications.md          Email, SMS, WhatsApp
│   ├── calendars-forms.md         Calendars, Forms, Service Menus, Rooms, Equipment
│   ├── funnels-website.md         Funnels, Website, Chat Widget
│   ├── pipelines.md               Pipelines, Opportunities
│   ├── workflows.md               Automation, Trigger Links, all Triggers and Actions
│   ├── ai-agents.md               Knowledge Bases, Conversation AI, Voice AI
│   └── prompt-guidelines.md       How to write AI agent prompts (GHL standard)
│
└── snapshots/                     ← Reference only. Actual builds go to the path the human provides.
```

---

## The 5-Step Sequence

---

### Step 0 — Create the Snapshot Folder

**Triggered when:** Human says they want to build a snapshot for a specific industry or business.

**AI asks:** "What folder path should I create this snapshot in?"

**AI does:**
1. Creates the folder at the provided path
2. Confirms: "Folder created at `[path]`. Now give me the business details and I'll generate the system design."

---

### Step 1 — Collect Business Details (Intake)

The human provides the business details. Two ways this can happen:

**Option A — Via chat:** Human describes the business in conversation. AI asks follow-up questions based on `00-intake.md` until all key sections are covered. AI does not need the human to fill a file — chat answers are enough.

**Option B — Via file:** Human fills `00-intake.md` (from the brain or a copy) and says "Read my intake form and generate the system design."

Either way, AI must have answers covering all 12 parts of the intake before generating the system design.

---

### Step 2 — Create the System Design File ← FIRST FILE CREATED

Using `01-system-design.md` as the structure reference, AI creates:

**File:** `system-design_[snapshot-name].md`
**Location:** Inside the snapshot folder at the provided path

This file contains the full architecture for this specific business:
- Snapshot summary and key outcomes
- Complete component map (filtered by complexity and skips from intake)
- Customer lifecycle flowchart (ASCII)
- Pipeline architecture with all stage names
- Workflow list with triggers, actions, and pipeline movements
- Calendar architecture
- AI agent architecture (or SKIPPED)
- Naming conventions specific to this industry
- Build sequence preview (what will be built, in what order)
- Open questions that need clarification before building

**After creating the file, AI STOPS.**

AI says: *"System design is ready at `[path]/system-design_[snapshot-name].md`. Review it and let me know if anything needs to change. When you're happy with it, say 'approved' and I'll begin the build."*

AI does not create any other files. AI waits.

---

### Step 3 — Human Reviews and Approves ← HARD GATE

Human reads `system-design_[snapshot-name].md`.

**Human can:**
- Ask questions → AI explains or adjusts the design
- Request changes → AI updates the file
- Add or remove components → AI updates the file
- Change complexity → AI updates the file

**This loop continues until the human explicitly approves.**

**Approval phrases AI listens for:**
- "Approved"
- "Looks good, proceed"
- "Start the build"
- "Begin building"
- Any clear confirmation that the design is signed off

**If unsure whether human is approving or just commenting**, AI asks: *"Should I mark this as approved and begin the build?"*

When approved, AI adds `✅ APPROVED` to the top of `system-design_[snapshot-name].md` and moves to Step 4.

---

### Step 4 — Create the Snapshot Folder Structure

AI creates the folder structure inside the snapshot folder. Only creates folders for components that are NOT marked SKIPPED in the system design.

```
[snapshot-path]/
│
├── system-design_[name].md         ← Already exists (created in Step 2)
├── README.md                        ← Created last, after everything is built
│
├── custom-values/
│   └── custom-values.md
├── custom-fields/
│   └── custom-fields.md
├── tags/
│   └── tags.md
├── smart-lists/
│   └── smart-lists.md
├── email-templates/
│   └── email-templates.md
├── sms-templates/
│   └── sms-templates.md
├── whatsapp-templates/              ← SKIP if WhatsApp = No
│   └── whatsapp-templates.md
├── calendars/
│   └── calendars.md
├── forms/
│   └── forms.md
├── funnels/                         ← SKIP if Funnels = No
│   └── funnels.md
├── website/                         ← SKIP if Website = No
│   └── website.md
├── chat-widget/                     ← SKIP if Chat Widget = No
│   └── chat-widget.md
├── pipelines/
│   └── pipelines.md
├── trigger-links/
│   └── trigger-links.md
├── workflows/
│   ├── 01-[workflow-name]/
│   │   └── [workflow-name].md
│   ├── 02-[workflow-name]/
│   └── ...
├── ai-agents/                       ← SKIP if all AI = No
│   ├── conversation-ai/
│   │   └── [bot-name]/
│   │       └── [bot-name].md
│   ├── knowledge-bases/
│   │   └── knowledge-bases.md
│   └── voice-ai/
│       └── [agent-name]/
│           └── [agent-name].md
└── surveys/                         ← SKIP if Surveys = No
    └── surveys.md
```

After creating the structure, AI says: *"Folder structure created. Ready to build. Shall I proceed with Step 1: Custom Values?"*

---

### Step 5 — Build One Step at a Time

AI follows `02-sequence.md` in order.

**The rule at every single step:**
1. AI builds the current step — creates the file, fills it with the full specification
2. AI marks the step `[x]` complete in `02-sequence.md`
3. AI says what was just built (one sentence summary)
4. AI asks: *"Shall I proceed with Step [X+1]: [Step Name]?"*
5. AI waits for confirmation before moving on

**Human can:**
- Say "yes" / "proceed" / "next" → AI continues to the next step
- Say "skip" → AI marks the step `[SKIP]` with a reason and asks about the next step
- Ask questions about what was just built → AI answers, then asks again about proceeding
- Request changes → AI updates the file, then asks about proceeding

**AI never auto-continues.** Every step is a checkpoint.

---

## Targeted Build (Single Component)

If the human wants only one component built:

Say: *"Build only the [component name]."*

AI:
1. Reads `system-design_[snapshot-name].md` for that component's specification
2. States all prerequisites that must already exist in GHL before this works
3. Builds only that component's file
4. Asks: *"[Component] is done. Shall I proceed with anything else?"*

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

---

## What the GHL Guides Are For

The `ghl-guides/` files tell AI how GHL features work — creation paths, constraints, connection rules. They do not say what to build. What to build comes from `system-design_[snapshot-name].md`. The guides say how to build it correctly.

---

## The Golden Rule

**Never hardcode anything.**

Every name, phone number, URL, price, and date must reference:
- `{{custom_values.key}}` — business-level data
- `{{contact.field_key}}` — per-contact data

This is what makes a snapshot reusable across any client in any market.

---

## Complexity Level

Complexity is a ceiling, not a component list.

- **Simple** — clean and manageable. Build what matters most. Don't add complexity the business doesn't need.
- **Medium** — multi-channel, small team, moderate AI. Build what the intake justifies.
- **Full** — build the complete system the intake describes. Don't hold back.

---

## Naming Conventions

| Component | Convention | Example |
|-----------|-----------|---------|
| Custom Fields | `[industry]_field_name` | `dental_dob`, `salon_hair_type` |
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

When something changes mid-build, AI checks this table and flags every affected component before continuing:

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
