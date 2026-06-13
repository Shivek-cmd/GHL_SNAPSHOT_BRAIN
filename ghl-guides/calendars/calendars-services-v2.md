# GHL Guide — Services v2

**Where in GHL:** Calendars → Calendar Settings → Services tab

---

## Services v2 — Overview

Services v2 is a purpose-built booking system for service businesses that need advanced features beyond what standard Service Calendars offer. It lives inside the Calendars module but operates as a distinct booking engine.

**Key advantages over standard Service Calendars:**
- Multiple payment processors (Stripe, Square, Razorpay, Authorize.net, NMI)
- Variations (multiple versions of the same service at different prices/durations)
- Add-ons (optional extras customers select at booking — upsells at checkout)
- Multi-service checkout — customers book multiple services in one transaction (cart)
- Coupon codes and promotions
- Card-on-file payment processing
- Staff-specific pricing — individual staff members can have different prices for the same service
- Resources (rooms + equipment managed per service via Resources tab)
- Category organization for the booking page
- Dedicated staff configuration with hierarchical availability (3-tier)
- Multi-location support
- Built-in appointment reporting and analytics
- Branded booking page customization

**How to enable:** Activate per sub-account via Agency View → Subaccounts → select account → Calendar Settings → enable Services module. Once enabled, existing service calendars automatically transfer. Both legacy calendars and v2 Services can run simultaneously.

**Current payment processor support:** Stripe, Square, Razorpay, Authorize.net, NMI

---

## Services v2 — Customer Booking Flow (How It Works)

Services v2 does NOT use Calendar Groups or the v1 Service Menu. It has its own booking system.

```
Services v2 Booking Flow:

Services tab → Services are created → Auto-published to booking page

Customer accesses via:
1. Public Booking Page  → shows ALL active services grouped by category
2. Individual Service URL → direct link to one specific service
3. Category URL → shows only services in that category
```

**Finding your booking page:**
Calendars → Calendar Settings → Services tab → **View Booking Page** button

**Sharing options:**
- Public page URL → all services visible
- Individual service URL → set via Custom URL field during service creation
- Category URL → generated per category

**This replaces Calendar Groups + Service Menu entirely for v2 builds.**

---

## Critical: Variations vs Separate Services for Tier Gating

This is a design decision that must be made before building.

**Variations** = multiple price/duration options inside one service. All variations are visible to EVERYONE on the booking page. Customer picks which one they want.

**Use Variations when:** You WANT the customer to choose (e.g., 60-min vs 90-min session, economy vs premium).

**Do NOT use Variations for membership tier pricing.** If a Gold member should never see VIP pricing — variations break this. There is no native way in GHL to hide a variation based on who is logged in.

**The correct approach for tier gating:**

Create separate services per tier. Each service has its own URL. The portal reads the contact's tag and sends them to only their tier's service URL.

```
❌ Wrong approach (variations):
  Service: Studio A Recording
    → Variation: Non-Member $160  ← VIP can see this
    → Variation: Gold $120        ← Non-Member can see this
    → Variation: VIP $80          ← Gold can see this

✅ Correct approach (separate services):
  Service: Studio A — Non-Member  → URL: /studio-a-non-member  → share with Non-Members only
  Service: Studio A — Gold        → URL: /studio-a-gold        → share with Gold only
  Service: Studio A — VIP         → URL: /studio-a-vip         → share with VIP only
```

With 5 service types × 3 tiers = **15 services total**. More to build upfront but tier gating is clean and native. No custom portal logic needed for the basic gating.

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
| Card-on-File | Save customer card for future charges without capturing payment now |
| Coupon Codes | Enable to allow customers to apply discount codes at checkout |
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
Resources are physical assets (rooms, chairs, studios) required to deliver a service. When a resource is booked, it is automatically reserved — preventing double-bookings.

**IMPORTANT — Resources in v2 is a completely separate system from Rooms & Equipment:**

| System | Location | Works With |
|---|---|---|
| **Resources** | Services → Resources section | v2 Services only |
| **Rooms & Equipment** | Calendar Settings → Rooms tab / Equipment tab | v1 Service Booking calendars only |

Do NOT use the Rooms or Equipment tabs when building with Services v2. Use Resources instead.

**Critical limitation:** Each service can book only ONE resource per appointment. You cannot attach a room AND separate equipment items — the system picks one resource per booking.

**Practical solution:** Make each resource represent the full physical space including its fixed equipment. Example: "Studio A" = the room + its camera rig + lighting + mics. No need to track equipment separately if it lives permanently in that space.

**How to create Resources:**
**Path:** Calendars → Calendar Settings → Services → **Resources** section → + New Resource

Fields:
- **Resource Name** — descriptive name (e.g., "Studio A", "Massage Room A")
- **Description** — what's included
- **Select Services** — which services require this resource
- **Select Locations** — where this resource exists (supports multi-location)
- **Capacity** — how many simultaneous appointments this resource can handle

**Quantity vs Capacity:**
- **Quantity** = number of physical units (e.g., 2 identical rooms → create 2 separate resources)
- **Capacity** = how many people/appointments ONE unit handles at once (e.g., a classroom = 1 room, capacity 20)

Resources can be assigned from either the Resources section OR from inside the service itself.

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
- **Staff-specific pricing:** When assigning a service to a staff member, you can override the service's base price with a price specific to that staff member. Example: Senior engineer charges $500 for a session; junior engineer charges $350 for the same service — same service, different staff, different price shown at booking.

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

## Service Menus (v1 Only — NOT for Services v2)

> **If you are using Services v2, skip this section entirely. Services v2 has its own public booking page — no Service Menu setup needed.**

Service Menus are a v1 concept. They display multiple v1 Service Booking calendars in one branded booking page. They require a Calendar Group as a prerequisite and only pull from v1 calendars.

**Services v2 replacement:** The public booking page auto-generated by v2 (View Booking Page) serves the same purpose — no setup required.

**Path (v1 only):** Calendars → Calendar Settings → Service Menu tab → Create Service Menu

### Prerequisites (v1 only)
1. **v1 Service Calendars must exist** — one per service type
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

### Service Menu with Services v2
When the Service Menu is backed by Services v2 (not v1 Service Calendars), the following are all supported:
- Multiple payment processors (Stripe, Square, Razorpay, Authorize.net, NMI)
- Card-on-file
- Coupon codes and promotions
- Multi-service checkout (customer adds multiple services to cart in one session)
- Add-ons at checkout

**Note:** The limitations (Stripe only, no coupon codes, no card-on-file) only apply when the Service Menu is backed by v1 Service Booking calendars. With v2 Services, those restrictions are lifted.

### Service Menu Key Points
- Multiple Service Menus can be created — use different Calendar Groups for different menus
- Clients can book multiple services in one session (unless "Limit to One Service" is enabled in menu settings)
- Custom tracking/pixel codes can be injected via the custom code field
- Fully mobile-responsive

---

## Rooms & Equipment (v1 Only — NOT for Services v2)

> **If you are using Services v2, do not use this section. Use Resources instead (see Step 6 above).**

The Rooms tab and Equipment tab in Calendar Settings are for **v1 Service Booking calendars only**. They operate at the calendar level and cannot be used with Services v2.

**Path:** Calendars → Calendar Settings → Rooms tab / Equipment tab

**Rooms** — physical spaces linked to v1 Service Calendars. Prevents double-booking of the space.
**Equipment** — shared tools with limited quantity linked to v1 Service Calendars.

**Rules:**
- Rooms and Equipment only link to Service Booking (v1) calendar type
- Cannot be linked to Collective, Round Robin, Personal, Class/Group, or Event calendars
- Cannot be used with Services v2 — use Resources instead

**How availability works in v1 with Rooms + Equipment:**
```
Booking request
  → Is staff available?     NO → blocked
  → Is Room available?      NO → blocked
  → Is Equipment available? NO → blocked
  → All YES → slot shown
```

For v1 setup details, see `calendars-overview.md`.

---

## Critical Design Note — Rooms, Equipment, and Collective Calendars

**Rooms and Equipment only work with Service Booking calendars.** This creates a real design conflict when a service requires both:
1. Multiple staff present simultaneously (needs Collective calendar)
2. Room or Equipment management (needs Service Booking calendar)

GHL cannot do both at once. You must choose:

| Priority | Calendar Type | What You Get | What You Lose |
|---|---|---|---|
| Enforce multi-staff requirement | Collective | Both staff must be free for slot to appear | Room/Equipment not managed |
| Enforce room/equipment constraint | Service Booking | Room and equipment availability tracked | No guarantee both staff are present |

**When Collective without Rooms is safe:**
If the number of staff required per booking equals or exceeds the number of available rooms, room conflicts are impossible — the staff constraint is the tighter bottleneck. Example: 2 therapists required for a couples massage, 2 massage rooms total → if both therapists are booked, both rooms are effectively claimed anyway. Collective calendar is safe here.

**When you must use Service Booking instead of Collective:**
If rooms are fewer than possible staff combinations and a double-booked room is a real risk, use a Service Calendar and manage multi-staff availability manually (block one person's calendar, or use a workflow to create a blocked slot).
