# GHL Guide — Forms

**Where in GHL:** Sites → Forms → + New Form

---

## What Forms Are

Data collection forms built inside GHL. Contacts submit forms to enter the system, provide information, or trigger automations. Every field on a form must map to a custom field on the contact record — forms are the bridge between what a contact fills out and what GHL stores and can act on.

---

## Form Types

**Standard Form:** Multi-field, multi-page capable. Used for lead capture, intake, patient info, etc.

**Survey:** Handled separately (Sites → Surveys) — designed for NPS, satisfaction scoring, and branching question flows. See `surveys.md` for Surveys documentation.

---

## How to Build a Form

1. Sites → Forms → + New Form
2. Name the form clearly
3. Use the form builder to add fields:
   - GHL standard fields (Name, Email, Phone, Address) — map to the core contact object automatically
   - Custom fields — drag from the "Custom Fields" panel or add field → select from list → maps to the custom field
4. Each field has: label (shown to user), required toggle, placeholder text
5. Add a submit button — label should reflect the action ("Book My Appointment", "Send My Info", "Get My Quote")
6. Configure submission settings:
   - Redirect URL after submit — use `{{custom_values.booking_confirmation_page}}` or a specific thank-you page
   - Sticky Contact — pre-fills known contact info if the contact visits from a tracked browser session
7. Form can be embedded on a funnel page, website page, or accessed via its own standalone URL

---

## Field Mapping Rules

**Every custom field on a form must have a corresponding custom field in GHL Settings → Custom Fields.**

Do not collect data in a form that has nowhere to go. Before building a form:
- Identify every piece of data the form will collect
- Confirm each has a custom field already created (Step 2 of the build sequence)
- Map fields in the form builder to those custom fields

Standard fields (First Name, Last Name, Email, Phone, Address, City, State, Zip) map automatically to GHL's built-in contact fields — no custom field needed.

---

## Submission Triggers

When a form is submitted, GHL fires the "Form Submitted" event. Workflows can use this as a trigger:
- Trigger: **Form Submitted** → filter by specific form name
- This fires the workflow for every submission of that form
- Typical actions that follow: add tag, move pipeline, send confirmation, notify staff

---

## Technical Constraints

- Forms do not have a field limit but long forms reduce completion rates
- File Upload fields store files in GHL's media library — file URL goes into the mapped custom field
- Phone field should include country code format settings
- Multi-page forms are supported — use "Next" buttons to paginate
- Conditional logic on form fields (show/hide based on another field's value) — available in the form builder via field conditions
- Forms cannot do payment collection natively — integrate Stripe or redirect to payment page on submit
- HIPAA: do not collect PHI in forms unless the GHL sub-account is on a HIPAA-compliant plan with BAA signed

---

## How Forms Connect to the Rest of the System

| Connection | Details |
|---|---|
| **Funnels and Website pages** | Embed forms using the Form block in the page builder |
| **Workflows** | "Form Submitted" trigger — most common entry point for new leads |
| **Custom Fields** | Every collected value lands in a custom field, available for conditions and merge tags immediately |
| **Calendars** | A form can be the step before a calendar booking: collect info → redirect to calendar booking link |
| **Pipelines** | Workflow fired on form submission typically moves contact to Stage 1 of the acquisition pipeline |

---

## What Must Exist Before Building Forms

- Custom fields for every non-standard piece of data the form collects
- A confirmation/thank-you page URL (or use GHL default) — add to custom values
- The workflow that will fire on submission (build workflow first, then connect form to it)
