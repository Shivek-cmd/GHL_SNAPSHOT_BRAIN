# GHL Guide — Calendars: Overview, Types & Settings

**Where in GHL:** Calendars → Calendar Settings → + New Calendar

---

## What Calendars Are

Booking systems inside GHL that allow contacts to self-book appointments or allow staff to manually book on their behalf. Each calendar has its own settings, availability, team routing, and confirmation flow. Workflows fire when appointments are booked, confirmed, cancelled, no-showed, or completed.

---

## Calendar Types

Choose the type at creation — **it cannot be changed afterward**.

| Type | Best For | Key Behavior |
|---|---|---|
| **Round Robin** | Multiple staff sharing one service | Distributes bookings across available team members |
| **Personal Booking** | One specific person | Always books to one user |
| **Service Booking** | Service menu / services v2 | Business-level service offering across staff |
| **Class / Group Booking** | Group classes, webinars, events | Multiple contacts book the same slot; capacity-limited |
| **Collective Booking** | Multi-person required meetings | ALL selected team members must be free for slot to appear |
| **Event** | One-time or predetermined events | Fixed date/time slots; contacts register |

### Round Robin Distribution Options
- **Even distribution** — rotate equally across all team members
- **Weighted** — assign a percentage of bookings per person
- **Check conflicts** — assign to whoever has availability (first available wins)

### Class / Group Booking: Show Seats Per Slot
Enable per-slot seat count display on the booking widget:
1. Edit the Class Booking calendar → **Customizations** tab
2. Toggle **Show seats per slot** ON → Save

Capacity logic: each confirmed appointment deducts 1 from the slot. Overlapping appointments do NOT fully block all affected slots prematurely — only deduct 1 seat per overlapping slot.

---

## Calendar Settings — All Options

### Basic Settings
- **Calendar Name** — use naming convention `CAL-##: Name`
- **Calendar Type** — set at creation, cannot change
- **Description** — internal use; not shown to bookers unless added to page
- **Color** — visual only, shown in GHL calendar view
- **URL Slug** — custom URL path for this calendar's booking page

### Availability
- Days of week available (can vary per day)
- Hours per day
- Timezone — defaults to sub-account timezone
- Date range — how far ahead contacts can book (e.g., 60 days)
- Minimum scheduling notice — how early in advance a contact must book (e.g., 24 hours)
- Maximum advance booking window — furthest date contacts can book ahead

### Appointment Settings
- **Duration** — length of each appointment slot
- **Buffer time** — gap after each appointment before next slot opens
- **Slot interval** — how frequently slots appear (every 15, 30, 60 min, etc.)
- **Daily appointment limit** — max bookings per day across the calendar
- **Seats per class** — for Class Booking only; sets maximum attendees per slot

### Confirmation Settings
- **Confirmation page** — redirect to custom URL or GHL default thank-you
- **Allow reschedule** — Yes/No
- **Allow cancellation** — Yes/No
- **Cancellation notice required** — minimum hours before appointment for cancellation

### Team Settings (Round Robin / Collective)
- Add team members (must have GHL user accounts)
- Set distribution rules
- Each team member sets their own availability in their user profile settings

### Meeting Location Options
- **In-person** — show address (`{{custom_values.business_address}}`)
- **Phone call** — contact's phone used
- **Zoom** — requires Zoom integration
- **Google Meet** — requires Google integration
- **Custom** — paste any meeting link or address

### Notifications
- Staff notification on booking — email/SMS to assigned team member
- Contact confirmation — best managed via workflow to avoid duplicate sends
- See `calendars-appointments.md` for full notification details

### Custom Questions at Booking
- Additional fields collected during self-booking
- Map every field to a corresponding custom field on the contact record
- Standard fields (name, email, phone) auto-map; custom fields must pre-exist in Settings → Custom Fields

### Forms & Payments Tab
- Attach a custom form to the booking flow
- Enable Accept Payments — Stripe, Square, Razorpay, Authorize.net, NMI (varies by calendar type)
- **Add Guests** — allow booker to add attendees
  - Toggle "Require Guests for Booking" — forces at least one guest before submission
  - Toggle "Accept Payments for All Attendees" — charges: price × (1 booker + guest count)

---

## Add Guests Feature

Enables customers to add additional attendees during booking. Useful for group therapy, fitness classes, event venues.

- Guest names required; guest emails optional
- Per-attendee pricing calculates automatically: **service price × total attendees**
- Guests do not receive confirmations unless their emails are collected and a workflow sends them
- Both "Require Guests" and "Per-Attendee Payments" are independent toggles — can enable either or both

---

## User Permissions in Calendars

Two permission types control access at the user level (set in Settings → Team Management → user permissions):

| Permission | What it Controls |
|---|---|
| **View Calendars** | See calendars in the interface |
| **Manage Calendars** | Create, edit, delete calendars |
| **View Appointments** | See appointments |
| **Manage Appointments** | Create, edit, delete appointments |
| **View Groups** | See calendar groups |
| **Manage Groups** | Create, edit, delete groups |

**Assigned Data toggle:**
- ON: User sees only appointments/calendars they are assigned to (or contacts they follow)
- OFF: Permissions apply globally to all calendars and appointments

---

## Custom Values in Calendars

Custom Values can be used as merge fields in:
- Appointment title
- Meeting location (Custom)
- Email/SMS notifications
- Workflow messages triggered by appointments

**How to use:**
1. Settings → Custom Values → create needed values
2. In calendar settings, click any field that supports merge fields → `{}` icon → Custom Values → search and select

Syntax: `{{custom_values.key_name}}`

Updates apply to future messages only — prior sent messages are unchanged.

---

## Embedding Calendars on External Websites

Embed calendar booking pages on any website via HTML iFrame or script.

**How to get the embed code:**
1. Calendar Settings → select calendar → three-dot menu → **Embed Code**
2. Copy the generated HTML snippet

**Embed methods:**
- iFrame embed — paste directly into any HTML page
- GHL widget code — for websites that support script injection

**Notes:**
- The embedded calendar respects all booking settings (availability, min notice, capacity)
- Works on any external website, Squarespace, Wix, WordPress, Webflow, etc.
- For GHL funnels and website pages, use the Calendar block in the page builder — no manual embed code needed

---

## Recurring Appointments

Manual recurring appointments can be set when booking from inside GHL:
1. Contacts → open contact → Appointments tab → +Add
2. In the booking modal → enable **Recurrence** toggle
3. Set recurrence pattern (daily, weekly, monthly) and end date

**Limitations:**
- Recurring appointments cannot be booked via the public self-service widget — only available for manually created appointments inside GHL
- The Book Appointment workflow action does NOT support recurring calendars

---

## Assigning a Primary Calendar

Each GHL user sets a Primary Calendar in **Settings → My Profile → Calendar Settings**:
- **Primary Calendar** — where appointments created for this user land (Google, Outlook, or GHL native)
- **Check for Conflicts** — which external calendars to check for busy times before showing availability

If a team member has Google Calendar as primary, appointments appear in Google automatically. Disabled external calendars in the conflict check list indicate they are already set as the Primary Calendar.

---

## How Calendars Connect to the Rest of the System

### Workflows that fire on calendar events
| Trigger | When it fires |
|---|---|
| **Appointment Booked** | Contact self-books or is manually booked |
| **Appointment Confirmed** | Status set to Confirmed |
| **Appointment Cancelled** | Status set to Cancelled |
| **Appointment No-Showed** | Status set to No Show |
| **Appointment Completed** | Status set to Showed/Completed |

Filter any of these by calendar name, team member, or appointment type.

### AI Agents booking into calendars
- Conversation AI → booking action → select calendar → agent books when conversation leads to booking intent
- Voice AI → same — each agent specifies exactly one calendar per booking action

### Trigger Links pointing to calendars
- Trigger link destination = calendar booking URL
- Find the URL: Calendar Settings → calendar → Share / Embed → Direct Link

### What must exist before building calendars
- Team members must have GHL user accounts
- Custom values for addresses, confirmation page URLs must be created first
- Custom fields for any booking questions must pre-exist
- Calendar Groups must exist before attaching to a Service Menu (see `calendars-groups-menus.md`)

---

## Disable Contact Timezone Adjustment

By default, contacts can adjust the timezone display on the booking widget. To prevent this:
- Calendar Settings → calendar → **Customizations** tab → toggle off "Allow contact to change timezone"

Use case: when all sessions are in-person at a fixed location and timezone confusion is a support issue.
