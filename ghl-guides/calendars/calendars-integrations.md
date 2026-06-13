# GHL Guide — Calendar Integrations & External Sync

**Where in GHL:** Settings → My Profile → Calendar Settings (per user) | Calendars → Calendar Settings → Edit Calendar → Availability tab

---

## Types of External Calendar Connections

GHL supports three distinct relationship types with external calendars:

| Type | What it does | Direction |
|---|---|---|
| **Connected (Primary) Calendar** | New GHL appointments are created in the external calendar | GHL → External |
| **Linked Calendar** | External events appear in GHL calendar view | External → GHL (view only) |
| **Conflict Calendar** | External busy times block GHL availability | External → GHL (availability check) |

---

## Setting Up a Primary Calendar

A Primary Calendar is where new appointments land. Set per user in their profile.

**Path:** Settings → My Profile → Calendar Settings → Primary Calendar → Select from connected accounts

**Supported:** Google Calendar, Outlook/Microsoft 365

**Behavior:** When a contact books an appointment with this user, the appointment automatically creates in the selected external calendar — no manual sync needed.

---

## Linked Calendars & Conflict Calendars

**Path:** Settings → My Profile → Calendar Settings → Linked Calendars / Check for Conflicts

### Linked Calendar
Pulls events from an external calendar into the GHL calendar view so the user can see their full schedule in one place. Does NOT affect booking availability.

### Conflict Calendar
Reads busy times from an external calendar and blocks those slots on GHL booking pages. Prevents clients from booking when the user is already busy elsewhere.

**Important:** A calendar already set as the Primary Calendar is automatically disabled in the Conflict check list — it would conflict with itself.

### Sync Behavior
| Setting | Direction | Effect on availability |
|---|---|---|
| Linked only | External → GHL view | None |
| Conflict only | External → GHL availability | Blocks busy times |
| Both | External → view + availability | Full two-way-like experience |

---

## Google Calendar Integration

**Connecting Google Calendar:**
1. Settings → My Profile → Calendar Settings → Connect Google Calendar
2. Authorize with Google account
3. Select which Google calendar to use as Primary

**Two-way sync:**
- GHL creates appointments → appear in Google Calendar
- Google Calendar busy times → block GHL availability (if set as Conflict)

**Troubleshooting:**
- Writer Access Error: User needs to re-authorize with full write permissions (not read-only)
- Re-integration: Settings → My Profile → disconnect, then reconnect Google
- Missing time slots: Check if Google events are blocking availability via conflict settings
- Contact reassignment on Group Calendar: Caused by the booking system reassigning to an available team member — expected behavior for Round Robin

---

## Outlook / Microsoft 365 Integration

**Connecting Outlook:**
1. Settings → My Profile → Calendar Settings → Connect Outlook Calendar
2. Authorize with Microsoft account
3. Select calendar to sync

**Behavior:** Same as Google — new appointments create in Outlook; Outlook busy times can block GHL availability.

**Note:** Uses Microsoft OAuth. Requires Microsoft 365 or Outlook.com account.

---

## iCloud Calendar Integration

iCloud integration uses iCal URL format (one-way):

**Setup:**
1. In iCloud: Settings → Privacy & Security → Advanced → Generate iCloud-specific password
2. Settings → Calendar → Calendar Accounts → enable iCloud calendar
3. Find the CalDAV server URL
4. In GHL: Settings → My Profile → Calendar Settings → Add iCloud Calendar → paste credentials

**Limitation:** iCloud sync is typically import-only (iCloud events appear in GHL as blocked times). GHL appointments do not automatically push back to iCloud.

**Troubleshooting:** If the iCloud calendar stops syncing, regenerate the app-specific password and re-enter in GHL.

---

## Calendly Integration

Calendly can sync with GHL so Calendly bookings appear as blocked times in GHL.

**How it works:**
- Calendly generates an iCal feed URL
- Add that iCal URL as a Conflict Calendar in GHL (Settings → My Profile → Calendar Settings)
- GHL reads the Calendly feed and blocks those times on GHL booking pages

**Limitation:** GHL cannot write appointments back to Calendly. This is one-way: Calendly → GHL conflict blocking only.

**Use case:** Agencies migrating clients from Calendly to GHL — set up Calendly sync during the transition period so no double-bookings occur while both systems are active.

---

## Hide Third-Party Calendar Details

When external calendar events appear in GHL (via Linked Calendar), the event titles and details are visible by default. This can expose private event names.

**To hide event details from external calendars:**
Settings → My Profile → Calendar Settings → toggle **Hide Third-Party Calendar Details** ON

With this enabled: external events appear as "Busy" in GHL calendar view — no title, no description.

---

## Calendar Integration Disconnection Notifications

GHL sends a notification when a connected calendar account disconnects (e.g., expired Google OAuth, password change, revoked access).

**Where the notification goes:** The GHL user whose calendar disconnected (email notification)

**What to do when notified:** Settings → My Profile → Calendar Settings → reconnect the relevant calendar account

---

## Appointment Notifications: Email, SMS, WhatsApp

Configured per calendar in **Calendar Settings → Edit Calendar → Notifications tab**

### 6 Notification Types
| Notification | Trigger | Who receives |
|---|---|---|
| **Booking Confirmation** | Appointment booked | Contact |
| **Appointment Reminder** | X hours/minutes before appointment | Contact |
| **Reschedule Confirmation** | Appointment rescheduled | Contact |
| **Cancellation Confirmation** | Appointment cancelled | Contact |
| **Staff Booking Notification** | Appointment booked | Assigned team member |
| **No-Show Follow-up** | Status set to No-Show | Contact |

### Per-Channel Configuration
Each notification type can be configured independently per channel:

| Channel | Configuration location |
|---|---|
| **Email** | Notifications tab → Email → customize subject and body using merge fields |
| **In-App** | Notifications tab → In-App toggle |
| **SMS** | Notifications tab → SMS → compose message with merge fields |
| **WhatsApp** | Notifications tab → WhatsApp → requires approved WhatsApp template |

**WhatsApp requirement:** WhatsApp appointment notifications require a pre-approved Meta WhatsApp Business template. The template must be approved before it can be used in calendar notifications.

### Merge Fields for Calendar Notifications

Common appointment merge fields available in notification templates:

| Merge Field | Value |
|---|---|
| `{{appointment.title}}` | Appointment title |
| `{{appointment.start_time}}` | Start date and time |
| `{{appointment.end_time}}` | End date and time |
| `{{appointment.duration}}` | Duration in minutes |
| `{{appointment.location}}` | Meeting location |
| `{{appointment.zoom_join_url}}` | Zoom meeting link |
| `{{appointment.google_meet_url}}` | Google Meet link |
| `{{contact.first_name}}` | Contact first name |
| `{{contact.email}}` | Contact email |
| `{{assigned_user.name}}` | Assigned team member name |
| `{{assigned_user.email}}` | Team member email |
| `{{custom_values.business_name}}` | Business name custom value |

**Troubleshooting merge field issues:** If `{{appointment.start_time}}` shows blank, check that the workflow or notification is firing AFTER the appointment is created (not before), and that the calendar trigger is correctly linked.

### Recommendation: Use Workflows Instead of Built-In Notifications
For complex notification sequences (reminders at 24h, 2h, and 1h before; post-appointment follow-up; no-show recovery), build workflows instead of using the built-in notification fields. Using both duplicates messages.

- Built-in notifications: simple, no customization, fire once per event
- Workflow-based notifications: full control, conditional logic, multi-step sequences, no duplicates if built-in is disabled
