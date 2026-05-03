# GHL Guide — Calendars & Forms

---

## Calendars

**What they are:** Booking systems inside GHL that allow contacts to self-book appointments. Each calendar has its own settings, availability, team routing, and confirmation flow. Workflows are triggered when appointments are booked, confirmed, cancelled, or completed.

**Where in GHL:** Calendars → Calendar Settings → + New Calendar

---

### Calendar Types

Choose the type when creating the calendar — it cannot be changed after creation.

**Round Robin**
- Multiple team members share one calendar
- GHL distributes incoming bookings among available staff
- Distribution options: Even distribution (rotate equally), Weighted (by percentage), Check conflicts (assign to whoever has availability)
- Use when: multiple staff members offer the same appointment type and availability should be pooled

**Personal Booking**
- One specific team member owns the calendar
- Bookings always go to that person
- Use when: a specific doctor, consultant, or specialist must handle this appointment type

**Service Booking (or Service Calendar)**
- Used for business-level service offerings, not tied to a specific individual
- Allows booking by service type across staff
- Use when: offering a menu of services where different staff may handle different services

**Class / Group Booking**
- Multiple contacts can book the same time slot
- Capacity limit controls maximum attendees
- Use when: group events, group classes, webinars, info sessions

**Collective Booking (or Team Calendar)**
- All selected team members must be available for the slot to show
- Use when: booking requires multiple people present (e.g., consultation requiring doctor + coordinator)

**Event**
- Fixed date/time slots — not recurring availability windows
- Contacts register for specific events
- Use when: one-time or recurring events where time slots are predetermined

---

### Calendar Settings — All Options

**When creating or editing a calendar:**

**Basic Settings:**
- Calendar Name — use naming convention `CAL-##: Name`
- Calendar Type — set at creation, cannot change
- Description — internal note, not shown to bookers unless added to page
- Color — visual only, shown in GHL calendar view

**Availability:**
- Days of week available
- Hours per day (can vary by day)
- Timezone — set to sub-account default unless this calendar serves a different timezone
- Date range — how far ahead contacts can book (e.g., 60 days)
- Minimum scheduling notice — how far in advance a contact must book (e.g., 24 hours)

**Appointment Settings:**
- Duration — length of each appointment slot
- Buffer time — gap after each appointment before the next slot opens
- Slot interval — how frequently slots appear (e.g., every 30 min, every 60 min)
- Daily appointment limit — max bookings per day across the calendar

**Confirmation Settings:**
- Confirmation page — custom URL or GHL default thank-you page
- Confirmation email — sent from GHL automatically OR managed by a workflow (do not double-send)
- Allow reschedule — Yes/No
- Allow cancellation — Yes/No
- Cancellation notice required — minimum hours before appointment for cancellation to be allowed

**Team Settings (Round Robin / Collective):**
- Add team members
- Set distribution rules
- Each team member must have their own GHL user account and their availability set in their calendar settings

**Meeting Location:**
- In-person (show address — use `{{custom_values.business_address}}`)
- Phone call
- Zoom / Google Meet (requires integration)
- Custom location

**Notifications:**
- Staff notification on booking — email/SMS to the assigned team member
- Contact confirmation — managed via workflow to avoid duplicate sends

**Custom Questions:**
- Additional fields collected at booking time
- These should map to custom fields on the contact record, not store data in isolation

---

### What Must Exist Before Building Calendars

- Team members must have GHL user accounts
- Custom values for durations, addresses, confirmation pages must be created first
- If a calendar will be linked from a trigger link — create the trigger link after the calendar exists

---

### How Calendars Connect to the Rest of the System

**Workflows that fire on calendar events:**
- Appointment Booked → trigger a workflow (confirmation sequence, pipeline movement)
- Appointment Confirmed → trigger a workflow
- Appointment Cancelled → trigger a workflow (re-engagement)
- Appointment No-Showed → trigger a workflow (recovery)
- Appointment Completed → trigger a workflow (post-visit follow-up)

Each calendar can have its own workflow connection — configure this in the calendar's notification/workflow settings OR use the workflow trigger "Appointment Status" filtered by calendar.

**AI Agents booking into calendars:**
- Conversation AI booking action: select calendar → agent books into it when conversation leads to booking intent
- Voice AI booking action: same — each agent must specify exactly one calendar per booking action

**Trigger Links pointing to calendars:**
- A trigger link can have the destination set to a calendar booking URL
- The calendar booking URL is found in: Calendar Settings → Calendar → Share / Embed → Direct Link

---

## Forms

**What they are:** Data collection forms built inside GHL. Contacts submit forms to enter the system, provide information, or trigger automations. Every field on a form must map to a custom field on the contact record — forms are the bridge between what a contact fills out and what GHL stores and can act on.

**Where in GHL:** Sites → Forms → + New Form

---

### Form Types

**Standard Form:** Multi-field, multi-page capable. Used for lead capture, intake, patient info, etc.

**Survey:** Handled separately (Sites → Surveys) — designed for NPS, satisfaction scoring, and branching question flows. Not covered in this guide.

---

### How to Build a Form

1. Sites → Forms → + New Form
2. Name the form clearly
3. Use the form builder to add fields:
   - GHL standard fields (Name, Email, Phone, Address) — these map to the core contact object automatically
   - Custom fields — drag from the "Custom Fields" panel or add field → select from list → maps to the custom field
4. Each field has: label (shown to user), required toggle, placeholder text
5. Add a submit button — label should reflect the action ("Book My Appointment", "Send My Info", "Get My Quote")
6. Configure submission settings:
   - Redirect URL after submit — use `{{custom_values.booking_confirmation_page}}` or a specific thank-you page
   - Sticky Contact — pre-fills known contact info if the contact visits from a tracked browser session
7. Form can be embedded on a funnel page, website page, or accessed via its own standalone URL

---

### Field Mapping Rules

**Every custom field on a form must have a corresponding custom field in GHL Settings → Custom Fields.**

Do not collect data in a form that has nowhere to go. Before building a form:
- Identify every piece of data the form will collect
- Confirm each has a custom field already created (Step 2 of the build sequence)
- Map fields in the form builder to those custom fields

Standard fields (First Name, Last Name, Email, Phone, Address, City, State, Zip) map automatically to GHL's built-in contact fields — no custom field needed.

---

### Submission Triggers

When a form is submitted, GHL fires the "Form Submitted" event. Workflows can use this as a trigger:
- Trigger: Form Submitted → filter by specific form name
- This fires the workflow for every submission of that form
- Typical actions that follow: add tag, move pipeline, send confirmation, notify staff

---

### Technical Constraints

- Forms do not have a field limit but long forms reduce completion rates
- File Upload fields store files in GHL's media library — file URL goes into the mapped custom field
- Phone field should include country code format settings
- Multi-page forms are supported — use "Next" buttons to paginate
- Conditional logic on form fields (show/hide based on another field's value) — available in the form builder via field conditions
- Forms cannot do payment collection natively — integrate Stripe or redirect to payment page on submit
- HIPAA: do not collect PHI in forms unless the GHL sub-account is on a HIPAA-compliant plan with BAA signed

---

### How Forms Connect to the Rest of the System

- **Funnels and Website pages:** Embed forms using the Form block in the page builder
- **Workflows:** "Form Submitted" trigger — the most common entry point for new leads
- **Custom Fields:** Every collected value lands in a custom field, available for conditions and merge tags immediately
- **Calendars:** A form can be the step before a calendar booking (collect info → redirect to calendar booking link)
- **Pipelines:** Workflow fired on form submission typically moves contact to Stage 1 of the acquisition pipeline
