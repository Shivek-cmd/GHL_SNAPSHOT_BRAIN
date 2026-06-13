# GHL Guide — Booking & Managing Appointments

**Where in GHL:** Calendars → Calendar View | Calendars → Appointment List View | Contacts → open contact → Appointments tab

---

## Manual Appointment Booking

Staff can book appointments on behalf of contacts without the contact self-booking.

### Access Points for Manual Booking

| Location | Path |
|---|---|
| Conversations | Conversations → select contact → Calendar icon → Book Appointment |
| Contacts | Contacts → open contact → Appointments tab → + Add |
| Calendar View | Calendars → Calendar View → click "New" or select a time slot |
| Opportunities | Open opportunity → Book/Update Appointment section |

### Booking Steps

**Step 1 — Select Calendar & Contact**
Choose the destination calendar and assign the booking to the appropriate contact.

**Step 2 — Fill in Appointment Details**
| Field | Notes |
|---|---|
| Title | Descriptive subject line for the appointment |
| Date & Time | Start/end with automatic timezone detection based on contact location |
| Location | Default (from calendar settings), custom, or video meeting link |
| Recurrence | Optional recurring pattern (daily, weekly, monthly) + end date |
| Notes | Internal notes about the appointment |

**Step 3 — Block Off Time (Optional)**
Use the "Blocked Off Time" tab instead of booking to mark a time as unavailable without creating a real appointment.

- Blocked time prevents new bookings during that window
- Does NOT affect or remove existing appointments in that period
- Use for: staff vacation, lunch breaks, equipment maintenance

### Timezone Handling
- GHL auto-detects and displays time based on the contact's timezone
- Staff booking on behalf of a contact: times adjust to the contact's timezone
- Can override timezone per booking if needed

### Recurring Appointments via Manual Booking
- Enable Recurrence toggle in the booking modal
- Set: frequency (daily/weekly/monthly), interval, end date
- **Limitation:** Recurring appointments are manual-booking only — the public self-booking widget does NOT support recurring bookings. The Book Appointment workflow action also does NOT support recurring calendars.

---

## Appointment List View

A list-based workspace for managing appointments at scale across multiple calendars.

**Path:** Calendars → Appointment List View

### Appointment Types in List View
Select which type to view via the dropdown:
- **Meeting** — standard calendar appointments
- **Service** — appointments from Service Calendars / Services v2
- **Rental** — rental bookings (see `calendars-rentals.md` for Rentals-specific details)

### Smart Lists
Pre-built lists: **Upcoming**, **Cancelled**, **All**

Create custom Smart Lists by clicking **+ Smart list** — saves filters, sort order, and column config as a reusable view.

### Advanced Filters
Filter by (AND logic — all conditions must match):
- Appointment status (Confirmed, Cancelled, No Show, Showed, Invalid)
- Assigned user
- Calendar source
- Appointment date/time range
- Contact details

### Sorting
- Appointment Time (ascending/descending)
- Date Added (ascending/descending)

### Column Management
Configure visible columns per Smart List:
- Show/hide columns
- Reorder via drag-and-drop
- Some system columns are locked

### Updating Appointment Status from List View
Click the **Status** dropdown on any row to change status immediately:

| Status | Meaning |
|---|---|
| Confirmed | Appointment is scheduled and confirmed |
| Showed | Contact attended |
| No Show | Contact did not attend |
| Cancelled | Appointment was cancelled |
| Invalid | Appointment is invalid/duplicate |

**Note:** Updating to "Showed" or "No Show" updates GHL internally but does NOT push status changes to third-party calendars (Google, Outlook).

### Row Actions (three-dot menu)
| Action | What it does |
|---|---|
| View Details | Opens full appointment record |
| View Consent | Shows consent form details (if enabled) |
| Edit | Updates appointment details |
| Reschedule | Changes date and time |
| Delete | Permanently removes appointment |

---

## Appointment Notes

Notes allow internal documentation per appointment, visible across the contact record.

**Path:** Open appointment → Notes tab → + Add Note

**Syncing across records:** Appointment notes are linked to both the appointment record AND the contact's activity timeline — no double entry needed.

**Creating a note via workflow:**
- Workflow action: **Create Appointment Note**
- Use case: auto-create a "Booked via chatbot" note when a workflow books an appointment; log pre-appointment prep notes

---

## Book Appointment Workflow Action

Automatically books an appointment without any human interaction. Used in automated nurture and lead conversion flows.

**Path:** Workflows → + Add Action → Book Appointment

### Configuration Fields
| Field | Notes |
|---|---|
| Calendar | Select which calendar to book into |
| Team Member | Specific team member, or auto-assign (Round Robin logic) |
| Date/Time | Use workflow date fields or dynamic values from custom fields |
| Override availability | Option to book outside normal availability hours |

### Auto-Booking Logic
- System finds the next available slot on the selected calendar
- Assigns to specified team member or uses Round Robin if "auto-assign" is selected
- Fires "Appointment Booked" trigger downstream

### Key Limitations
- Does NOT support recurring calendars
- Does NOT support Class Booking calendars
- No payment collection at booking via workflow — if payment is required, route contact to the booking page instead

### Troubleshooting
| Issue | Likely Cause |
|---|---|
| Appointment not created | No available slots on calendar in the booking window |
| Wrong time zone | Contact's timezone not set; workflow uses sub-account timezone as fallback |
| Team member not assigned | Team member removed from calendar after workflow was built |

---

## Appointment Status Workflow Triggers

Use these triggers to fire automations based on appointment lifecycle events:

| Trigger | Filter options |
|---|---|
| **Appointment Booked** | Calendar name, assigned user, appointment type |
| **Appointment Confirmed** | Calendar name, assigned user |
| **Appointment Cancelled** | Calendar name, assigned user |
| **Appointment No-Showed** | Calendar name, assigned user |
| **Appointment Completed / Showed** | Calendar name, assigned user |

**Best practice:** Create separate workflows for each status (Booked → confirmation sequence; Cancelled → re-engagement; No Show → recovery sequence; Completed → review request).

---

## Calendar View (Grid View)

**Path:** Calendars → Calendar View

Standard date-based calendar grid. Switch between:
- **Day view** — single day, all appointments in time slots
- **Week view** — 7-day view
- **Month view** — overview

**Filtering:** Filter by team member, calendar, or appointment type using the dropdowns at the top.

**Color coding:** Each calendar has a color (set in calendar settings) — appointments display in that calendar's color.

**Linked calendar events:** External calendar events appear grayed out if Linked Calendar is configured. These are view-only — clicking them shows no GHL appointment details.

---

## Common Appointment Management Workflows

| Goal | Setup |
|---|---|
| Confirmation sequence | Trigger: Appointment Booked → Send email + SMS confirmation |
| 24-hour reminder | Trigger: Appointment Booked → Wait until 24h before start time → Send reminder |
| Post-visit follow-up | Trigger: Appointment Completed → Wait 1 hour → Send review request |
| No-show recovery | Trigger: Appointment No-Showed → Send re-engagement offer |
| Cancellation re-book | Trigger: Appointment Cancelled → Send rebook link |
| AI agent auto-booking | Conversation AI intent detected → Book Appointment action → Confirmation SMS |
