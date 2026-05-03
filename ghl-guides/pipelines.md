# GHL Guide — Pipelines & Opportunities

---

## What Pipelines Are

A pipeline is a visual, stage-based tracking system for contacts. Each contact in a pipeline becomes an "opportunity" — a record that tracks where that contact is in a specific journey. A contact can exist in multiple pipelines simultaneously with separate opportunity records in each.

Pipelines are not automation — they are visibility. Automation (workflows) moves contacts through pipeline stages. The pipeline shows you where everything is at a glance.

**Where in GHL:** Opportunities → Pipelines → + Add Pipeline (to create); Opportunities → (select pipeline) (to view)

---

## How Pipelines Work

**Pipeline → Stages → Opportunities**

- A pipeline contains stages in a fixed left-to-right order
- Each stage contains opportunities (contacts at that point in the journey)
- An opportunity is created when a contact enters the pipeline for the first time
- An opportunity is moved when a workflow action fires "Move Opportunity to Stage" OR a team member drags it manually

**Opportunity record contains:**
- Contact it belongs to
- Current stage
- Stage history (which stages it passed through, with timestamps)
- Opportunity value (dollar amount — useful for revenue forecasting)
- Assigned owner (team member)
- Notes and activity log
- Any custom opportunity fields

---

## Creating a Pipeline

1. Opportunities → Pipelines → + Add Pipeline
2. Name the pipeline — use naming convention `PL-##: Name`
3. Add stages in left-to-right order
4. Each stage has:
   - Name (this exact text is what workflows reference — get it right now)
   - Color (visual only)
   - Rotting days (optional — highlights opportunities that have been in this stage too long)

**Stage names are permanent contracts.** Once a workflow is built referencing a stage name, changing the stage name breaks every workflow action pointing to it. Name stages carefully before building workflows.

---

## Opportunity Value

Every opportunity can have a monetary value assigned. This feeds the pipeline revenue view.

- Set a value in the "Create Opportunity" or "Update Opportunity" workflow action
- Can be a fixed amount or reference a custom field (e.g., `{{contact.dental_treatment_value}}`)
- Pipeline view shows total value per stage and total pipeline value
- Useful for tracking: lead pipeline value, treatment plan value, active patient revenue at risk

---

## Pipeline Stage Design Principles

**Each stage should represent a meaningful point in the journey** — not every micro-action, but the states where a human might need to take action or where the journey branches.

**A stage should answer the question: "What is the business waiting for at this point?"**
- Waiting for contact to book → "Nurture / Contacted"
- Waiting for patient to arrive → "Appointment Scheduled"
- Waiting for treatment decision → "Treatment Plan Presented"

**Terminal stages:** Every pipeline needs clear terminal stages:
- Won / Converted — the positive outcome
- Lost / Unrecoverable — the contact is no longer in active play
- These should be the rightmost stages

**Dead-end trap:** Do not create stages with no exit path. Every stage should have a workflow that eventually moves the opportunity out — either forward or to a terminal stage.

---

## Multiple Pipelines Per Contact

A contact can have multiple simultaneous opportunities across different pipelines. This is intentional — the same person can be:
- A lead being nurtured in a Lead Acquisition pipeline
- An active patient in a Patient Lifecycle pipeline
- A treatment plan prospect in a Treatment Plan pipeline

Each pipeline tracks a different dimension of the relationship. Workflows that fire on a contact check all active pipeline records. When a workflow says "Move to Stage X in Pipeline Y," it only affects that specific pipeline record.

---

## How Workflows Interact with Pipelines

**Create Opportunity:**
- Creates a new opportunity record for the contact in the specified pipeline
- Sets initial stage, value, owner
- Use this when a contact enters a pipeline for the first time

**Move Opportunity:**
- Moves the existing opportunity to a new stage within the pipeline
- If no opportunity exists, this action may fail silently — always create before moving
- Specify: Pipeline name + Stage name (exact text match required)

**Update Opportunity:**
- Updates values on an existing opportunity (value, owner, name) without moving stage

**Opportunity Trigger (workflow trigger):**
- Trigger: Opportunity Stage Changed
- Filter by: specific pipeline, specific stage
- Fires when any opportunity moves into the specified stage
- Use this for stage-specific automations (e.g., "when moved to Treatment Plan Presented, send follow-up email")

---

## Technical Constraints

- A pipeline can have unlimited stages
- A contact can have multiple opportunities in the same pipeline (e.g., if they come back as a new lead) — GHL creates a new opportunity record rather than overwriting the old one
- Pipeline stage history is stored and viewable — you can see every stage transition with timestamps
- Opportunities can be filtered and searched; smart lists can filter by pipeline stage
- Stage names have a character limit (~50 characters) — keep them concise
- Pipelines cannot be deleted if they have open opportunities — archive or close opportunities first
- No built-in SLA enforcement — use "rotting days" for visual alerts, or build a workflow that triggers if an opportunity stays in a stage too long

---

## Connection to the Rest of the System

**Pipelines depend on:**
- Nothing — pipelines are the first structural thing to build before workflows

**What depends on pipelines:**
- Workflows (every action that moves an opportunity references a pipeline + stage name)
- Smart lists (can filter by pipeline stage)
- Reporting views (pipeline value, stage conversion rates)
- AI agents that update opportunity stages via workflow actions

**Build order:** Pipelines must be built before workflows. Stage names must be final before any workflow that references them is created.
