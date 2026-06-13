# GHL Guide — Services v2, Service Menus, Rooms & Equipment

**Where in GHL:** Calendars → Calendar Settings → Services tab (Services v2) | Service Menu tab | Rooms tab | Equipment tab

---

## Services v2 — Overview

Services v2 is a purpose-built booking system for service businesses that need advanced features beyond what standard Service Calendars offer. It lives inside the Calendars module but operates as a distinct booking engine.

**Key advantages over standard Service Calendars:**
- Multiple payment processors (Stripe, Square, Razorpay, Authorize.net, NMI)
- Variations (multiple versions of the same service at different prices)
- Add-ons (optional extras customers select at booking)
- Resources (rooms, equipment managed per service)
- Category organization
- Dedicated staff configuration with hierarchical availability
- More flexible pricing and checkout

**How to enable:** Services v2 must be enabled per sub-account. Once enabled, it coexists with existing calendars — existing bookings and calendar types are unaffected.

**Current payment processor support:** Stripe, Square, Razorpay, Authorize.net, NMI

---

## Creating a Service

**Path:** Calendars → Calendar Settings → Services tab → + New Service

### Step 1 — Basic Details
| Field | Notes |
|---|---|
| Service Name | Displayed to customers on the booking page |
| Description | What's included, what to expect |
| Service Image | Optional image for the booking widget |
| Category | Assign to a category for organization |
| Status | Active = visible; Inactive = hidden |
| Duration | Length of the appointment |
| Buffer Time | Gap after appointment before next slot opens |

### Step 2 — Advanced Details
| Field | Notes |
|---|---|
| Staff | Which staff members can deliver this service |
| Booking Form | Attach a custom form for additional data collection |
| Location | In-person, phone, video, custom |
| Custom URL Slug | For the service's direct booking link |

### Step 3 — Payments
| Field | Notes |
|---|---|
| Accept Payments | Toggle on to collect payment at booking |
| Price | Base price |
| Currency | Set per service |
| Payment Processor | Select from enabled processors for this sub-account |
| Security Deposit | Optional; requires global setting to be enabled |

### Step 4 — Variations
Variations = different versions of the same service (e.g., 30-min vs 60-min, basic vs premium).

**To add a variation:**
1. Toggle **Variations** ON
2. Click + New Variation
3. Set: Variation Name, Duration, Price, Staff assignment (if different from base)
4. Confirm

Example: A spa might have "Deep Tissue Massage" with variations: "60 min — $90" and "90 min — $130"

### Step 5 — Add-ons
Optional extras customers can select during booking.

**To add an add-on:**
1. Toggle **Add-ons** ON
2. Click + New Add-on
3. Set: Add-on Name, Description, Price, Duration impact (adds to total duration if applicable)
4. Confirm

Example: "Aromatherapy add-on — $15, +10 min"

### Step 6 — Resources
Link Rooms and Equipment to this service so availability is checked against physical resources at booking time. See Rooms and Equipment sections below.

---

## Categories in Services v2

Categories organize services for easier navigation on the booking page and internal management.

**Path:** Calendars → Calendar Settings → Services → Categories panel (left side)

### Creating a Category
1. Navigate to Services → Categories
2. Click **+ New Category**
3. Enter: Category Name (required), optional URL slug
4. Click Create

### Category Rules
- Each service belongs to exactly one category
- Services without a category go to the default category
- Up to **50 categories per sub-account**
- Categories can be deleted; their services move to the default category
- Drag categories in the left panel to reorder — public booking page reflects this order
- Sharing a category generates a direct booking link filtered to that category

---

## Configuring Staff in Services v2

**Path:** Calendars → Calendar Settings → Services → Staff panel

### Adding Staff
1. Services → Staff tab → Add Staff
2. Select the GHL user to add as a staff member

### Staff Configuration Tabs

**Basic Details**
- Profile photo, display name, bio
- Contact info (for internal reference)

**Assigning Services**
- Select which services this staff member can deliver
- Only assigned services appear in their availability for booking

**Weekly Working Hours**
- Set default availability by day of week
- Each day: toggle on/off, set start/end times
- Multiple time blocks per day are supported

**Date-Specific Hours**
- Override weekly schedule for specific dates
- Use for: holidays, vacation days, special events
- A date-specific override completely replaces that day's weekly schedule

**Bulk Date-Specific Hours**
- Apply the same date-specific override to multiple dates at once
- Useful for setting up public holiday schedules in bulk

### Availability Hierarchy (3-Level Priority)
| Priority | Level | What it Controls |
|---|---|---|
| 1 (highest) | Date-Specific Hours | Override for that exact date |
| 2 | Weekly Working Hours | Default schedule by day of week |
| 3 (lowest) | Global Calendar Availability | Sub-account level defaults |

The system checks from the top down. Date-Specific Hours always win.

---

## Service Menus

A unified booking page that displays multiple services from individual Service Calendars in one branded interface. Clients browse all available services and book what they need in a single flow.

**When to use:** A business offers multiple distinct services across different staff or rooms, and you want one booking URL that presents all options.

**Path:** Calendars → Calendar Settings → Service Menu tab → Create Service Menu

### Prerequisites Before Building a Service Menu
1. **Service Calendars must exist** — one per service type
2. **Calendar Groups must exist** — Service Calendars must be in a group; only grouped calendars can appear in a Service Menu (see `calendars-groups-menus.md`)

### How to Set Up a Service Menu

**Step 1 — Enable the feature**
Settings → Calendar Settings → Preferences tab → Account Preference → Services section → toggle **Service Menu** ON → Save Preferences

**Step 2 — Create the menu**
Settings → Calendar Settings → Service Menu tab → Create Service Menu

| Field | Notes |
|---|---|
| Name | Title displayed at the top of the booking page |
| Description | Optional summary shown to clients |
| Slug URL | Forms the menu's custom URL path |
| Form | Optional custom form for extra info at booking |

**Step 3 — Select services**
Service Menu editor → Select Services tab → check the calendars (services) to include

**Step 4 — Arrange and save**
Drag and drop services to set display order → Save

### Service Menu Limitations
| Limitation | Details |
|---|---|
| Payments | Stripe only — no other processors |
| Card-on-file | Not supported — cards not saved after booking |
| In-app payments | Not supported |
| Coupon codes | Not supported |
| Full payment flexibility | Use Services v2 for multi-processor support |

### Service Menu Key Points
- Multiple Service Menus can be created — use different Calendar Groups for different menus
- Clients can book multiple services in one session (unless "Limit to One Service" is enabled in menu settings)
- Custom tracking/pixel codes can be injected via the custom code field
- Fully mobile-responsive

---

## Rooms

Physical spaces (consultation rooms, treatment chairs, therapy rooms, service bays) linked to Service Calendars. When a Room is linked to a calendar, booking checks Room availability alongside staff availability — preventing double-booking of the physical space.

**Path:** Calendars → Calendar Settings → Rooms tab

### Prerequisites
- Service Calendars must exist before linking a Room
- Rooms feature must be enabled

### How to Set Up Rooms

**Step 1 — Enable Rooms**
Settings → Calendar Settings → Preferences tab → Account Preference → Services section → toggle **Rooms** ON → Save Preferences

**Step 2 — Create a Room**
Settings → Calendar Settings → Rooms tab → + Create Room

**Step 3 — Configure Room details**
| Field | Notes |
|---|---|
| Name | Clear identifier — e.g., "Consultation Room 2", "Massage Room A" |
| Description | Notes about intended use |
| Total Capacity | Max simultaneous appointments in this room |
| Select Calendar | Which Service Calendars this room is assigned to |

### Room Rules and Constraints
- A Room can be assigned to multiple calendars
- Rooms are **internal only** — clients cannot see or choose rooms; assignment is automatic
- A Room not linked to any calendar has no effect on booking logic
- Rooms can be edited or deleted at any time; deleting removes the availability constraint
- Users are notified when assigned to a Room
- No official limit on number of Rooms

---

## Equipment

Shared physical tools or devices required to deliver a service (massage tables, exam chairs, projectors, cameras, etc.). Equipment availability is tracked alongside staff and rooms — preventing double-booking of shared gear.

**Path:** Calendars → Calendar Settings → Equipment tab

### Prerequisites
- Service Calendars must exist before linking Equipment
- Equipment feature must be enabled

### How to Set Up Equipment

**Step 1 — Enable Equipment**
Settings → Calendar Settings → Preferences tab → Account Preference → Services section → toggle **Equipments** ON → Save Preferences

**Step 2 — Create Equipment**
Settings → Calendar Settings → Equipment tab → Create Equipment

**Step 3 — Configure Equipment details**
| Field | Notes |
|---|---|
| Equipment Name | Unique identifier — e.g., "Massage Table", "Hyper-Facial Machine" |
| Description | Brief description of purpose |
| Total Quantity | Total units available (e.g., 3 massage tables = quantity 3; one entry for all 3) |
| Out of Service Quantity | Units currently unavailable; GHL subtracts from available pool automatically |
| Select Calendar | Which Service Calendars this equipment is assigned to |

### Equipment Rules and Constraints
- Equipment can be linked to multiple calendars
- Out of Service Quantity automatically reduces the bookable pool — no manual calendar blocking needed
- Deleting equipment that is actively in use removes the availability restriction — may cause double-bookings; review linked calendars before deleting
- No native reporting for equipment usage — review via calendar view
- For multiple identical items (e.g., 3 chairs): create ONE entry, set Total Quantity to 3. Do NOT create three separate entries.

---

## How Services, Rooms & Equipment Work Together

When a booking comes in, GHL checks all three layers simultaneously:

```
Booking request
       ↓
Is staff available?          → NO → slot blocked
       ↓ YES
Is assigned Room available?  → NO → slot blocked
       ↓ YES
Is Equipment available?      → NO → slot blocked
       ↓ YES
Slot shown to customer → Booking confirmed
```

This triple-check prevents scheduling conflicts across staff, space, and tools without any manual calendar management.

**Workflows:** No direct trigger for Room/Equipment status. Availability constraints operate silently within the booking engine — workflows fire on appointment events as normal.
