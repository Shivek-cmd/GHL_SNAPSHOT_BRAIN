# GHL Guide — How to Think & Build Service Calendars (Complete Process)

> Read this file every time you're about to build anything calendar-related.
> This is the thought process — not just the steps.

---

## The Mental Model in One Picture

### v1 (Service Booking Calendars)
```
SERVICE MENU         ← booking page (requires Calendar Group)
      │
CALENDAR GROUP       ← container that holds v1 calendars
      │
SERVICE CALENDARS    ← one per service type
      │         │
   STAFF      ROOMS + EQUIPMENT
 (who does)   (where + with what — v1 only)
```

### v2 (Services)
```
PUBLIC BOOKING PAGE  ← auto-generated, no setup needed (View Booking Page)

SERVICES             ← one per service type (or per service × tier for gating)
      │         │
   STAFF      RESOURCES
 (who does)   (physical space — one resource per booking)
```

**Build bottom to top. Never top to bottom.**

> v2 does NOT use Calendar Groups or Service Menu. It has its own booking page.

---

## Step 1 — Ask These 4 Questions First (Before Opening GHL)

Work these out on paper or in a doc BEFORE touching anything in GHL.

### Q1 — What services does this business offer?
Each distinct service = one Service Calendar.
Write them all out with durations.

> Barbershop: Haircut 30 min, Beard Trim 20 min, Hot Towel Shave 45 min
> Each one = its own calendar. 3 services = 3 calendars.

---

### Q2 — Who delivers each service?
Those people = Staff. They must be GHL users first.
Note which staff can deliver which service — not every person does every service.

> Barbershop: Alex does all 3. Marcus does all 3. Jade does haircut only.
> Attach Alex + Marcus to all 3 calendars. Attach Jade to CAL-01 only.

---

### Q3 — Is there a physical space that limits simultaneous bookings?
If yes → create Rooms and link to the relevant Service Calendars.
If no → skip Rooms entirely.

**Ask this:** "If I had 10 staff members, could I run 10 sessions simultaneously?"
- Yes → no room constraint (virtual services, mobile services, outdoor)
- No → there's a space limit → create Rooms

> Barbershop with 2 chairs: even if I have 5 barbers, only 2 can work at once → 2 Rooms
> Zoom consultant: no physical limit → no Rooms

**Hard rule:** Rooms only link to Service Booking calendars. Not Collective, not Round Robin, not Personal.

---

### Q4 — Is there a shared tool or piece of equipment with limited quantity?
If yes → create Equipment and link to the relevant Service Calendars.
If no → skip Equipment entirely.

**Ask this:** "Is there a tool that multiple staff share, and running out of it would block a booking?"
- Yes → create Equipment with the correct quantity
- No → skip

> Hot towel machine (qty 1): only 1 person can use it at a time → Equipment
> Each barber has their own scissors → no Equipment needed

**Hard rule:** Equipment only links to Service Booking calendars. Same restriction as Rooms.

---

## Step 2 — The Creation Order (Never Change This)

### v1 Order (Service Booking Calendars)
```
1. STAFF               Create GHL users. Set availability in their profile.
        ↓
2. SERVICE CALENDARS   One per service. Attach staff. Set duration, buffer, availability.
        ↓
3. ROOMS               Only if physical space limits bookings. Rooms tab → link to calendars.
        ↓
4. EQUIPMENT           Only if shared tools with limited quantity. Equipment tab → link to calendars.
        ↓
5. CALENDAR GROUP      Container. Add all Service Calendars into one group.
        ↓
6. SERVICE MENU        Booking page. Pulls from the Calendar Group.
```

### v2 Order (Services)
```
1. STAFF               Create GHL users. Set weekly hours in Services → Staff tab.
        ↓
2. CATEGORIES          Organize services by type (e.g., Studio A, Studio B).
        ↓
3. RESOURCES           Create physical spaces. Services → Resources section.
        ↓
4. SERVICES            Create services. Attach staff, set price, add variations/add-ons,
                       link resource in Resources tab within each service.
        ↓
5. DONE                Public booking page is auto-generated. No Calendar Group needed.
                       Share individual service URLs or the full booking page URL.
```

**Key differences:**
- v2 Staff availability is set in Services → Staff tab (not user profile)
- v2 uses Resources (not Rooms/Equipment tabs)
- v2 needs no Calendar Group or Service Menu
- v2 booking page is automatic

---

## Step 3 — When to Use Each Calendar Type

Choosing the wrong calendar type is the most common mistake. Pick before creating.

| Situation | Calendar Type |
|---|---|
| One specific person does this service | Personal Booking |
| Multiple staff, one gets assigned per booking (round robin) | Round Robin |
| Any staff member can deliver this service | Service Booking |
| ALL assigned staff must be free simultaneously | Collective |
| Multiple people book the same time slot (class, webinar) | Class / Group |
| Fixed date/time events, people register | Event |

**For Services v2 and Service Menus → always use Service Booking.**
Rooms and Equipment only work with Service Booking.

---

## Step 4 — When to Skip Each Component

### v1 Components
| Component | Skip when... | Build when... |
|---|---|---|
| **Rooms** | Virtual/remote, no physical space limit | Physical space limits simultaneous bookings |
| **Equipment** | Staff own tools, no shared gear | Shared tools with limited quantity |
| **Calendar Group** | Never skip if building a Service Menu | Always needed before Service Menu |
| **Service Menu** | Single service, or each service has its own link | Multiple services, want one booking page |
| **Collective Calendar** | Single staff per service | ALL assigned staff must be free simultaneously |

### v2 Components
| Component | Skip when... | Build when... |
|---|---|---|
| **Resources** | No physical space constraint | Physical room/space limits simultaneous bookings |
| **Variations** | Tier-gated pricing (members shouldn't see other tiers) | Customer CHOOSES between options (duration, configuration) |
| **Add-ons** | No optional extras | Business sells upgrades at checkout |
| **Calendar Group** | Always skip for v2 | Never — v2 doesn't use Calendar Groups |
| **Service Menu (v1)** | Always skip for v2 | Never — v2 has its own booking page |

---

## Step 4b — Variations vs Separate Services (Critical Decision for v2)

**Use Variations when:** Customer should choose between options themselves.
→ Example: 60-min or 90-min massage. Economy or premium package.

**Use Separate Services when:** Access should be restricted by membership/tier.
→ Example: Gold members should only see Gold pricing. VIP should only see VIP pricing.

```
Tier gating with Variations = ❌ broken
  → All variations visible to everyone
  → No native way to hide a variation based on who is viewing

Tier gating with Separate Services = ✅ correct
  → Each tier = its own service = its own URL
  → Portal/membership system shares only the correct URL per tier
  → 5 service types × 3 tiers = 15 services total
  → More to build but tier gating is clean and native in GHL
```

---

## Step 4c — When to Use Rentals vs Services v2

| Use Rentals when... | Use Services v2 when... |
|---|---|
| Pure space/item rental — no staff involved | Staff (engineer, therapist, technician) are part of every booking |
| Availability = opening hours only | Availability depends on specific staff members' schedules |
| iCal sync needed (Airbnb/VRBO) | Add-ons at checkout are required |
| Duration pricing (seasonal, day-of-week discounts) | Staff-specific pricing needed |
| No individual engineer/staff scheduling | Resources (room blocking) needed |

**Hard rule:** If an individual staff member being sick or on leave should affect booking availability — use Services v2, not Rentals. Rentals cannot track individual staff availability.

---

## Step 5 — The Collective Calendar vs Rooms Tradeoff

**This is the one thing that trips everyone up.**

Collective calendar = ALL staff must be free → slot appears.
Rooms = only links to Service Booking calendar (not Collective).

**You cannot have both.** When a service needs multiple staff AND room management:

| Choose | When |
|---|---|
| **Collective Calendar** (no room link) | Staff count required = rooms available. Staff is the tighter bottleneck. Room conflict is impossible in practice. |
| **Service Booking Calendar** (with room link) | Room is genuinely scarce. Multi-staff requirement is less critical or manageable manually. |

**Example:** Couples massage needs 2 therapists. You have 2 massage rooms.
→ Use Collective. If both therapists are booked, both rooms are claimed anyway. No room conflict can happen.

**Example:** Podcast studio. 2 engineers, 3 recording booths. Session needs 1 engineer.
→ Use Service Booking + Rooms. Engineers are not scarce enough to be the limiter. Booths are.

---

## Step 6 — Staff Availability Hierarchy

When does a staff member show as available? GHL checks in this order:

```
1. Date-Specific Hours    ← Always wins (vacation days, holidays, one-off changes)
         ↓ not set
2. Weekly Working Hours   ← Default schedule (Mon–Fri 9am–5pm etc.)
         ↓ not set
3. Global Calendar Hours  ← Sub-account level fallback
```

Set Date-Specific Hours when: staff is unavailable on a day they normally work, or working different hours for a specific date.

---

## Step 7 — How Availability Is Calculated at Booking Time

For a slot to appear as bookable, ALL of these must be true simultaneously:

```
Staff available (per their 3-tier hierarchy)   → NO = blocked
         +
Room available (if linked)                     → NO = blocked
         +
Equipment available (unit count > 0)           → NO = blocked
         ↓ ALL YES
Slot shown to customer
```

The customer sees none of this logic. They only see "available" or "unavailable."

---

## Quick Reference — Field by Field When Creating a Service Calendar

**Path:** Calendars → Calendar Settings → + New Calendar → Service

| Tab | Field | What to set |
|---|---|---|
| Basic | Calendar Name | `CAL-##: Service Name` |
| Basic | Duration | Exact length of the service |
| Basic | Buffer Time | Cleaning/prep time after each session |
| Basic | Slot Interval | How often slots appear (match duration usually) |
| Availability | Days + Hours | When this service can be booked |
| Availability | Min Scheduling Notice | How far ahead customer must book |
| Availability | Max Advance Window | How far ahead customer can book |
| Team | Staff | Only people who deliver THIS specific service |
| Forms & Payment | Payment | Enable + set price if collecting at booking |
| Forms & Payment | Add Guests | Enable if per-person pricing or attendance tracking needed |
| Notifications | Confirmations | Disable built-in if using workflow-based notifications |

---

## Naming Conventions (Always Follow)

| Component | Format | Example |
|---|---|---|
| Service Calendar | `CAL-##: Name` | `CAL-01: Haircut`, `CAL-03: Hot Towel Shave` |
| Room | Descriptive physical name | `Massage Room A`, `Barber Chair 2`, `Laser Suite` |
| Equipment | Tool name + quantity context | `Hot Stone Set`, `Laser Machine`, `Pro Mic Rig` |
| Calendar Group | `[Business] Services` | `Barbershop Services`, `Wellness Services` |
| Service Menu | Customer-facing CTA | `Book Your Appointment`, `Choose Your Service` |

---

## Complete Build Checklist

Use this every time:

```
□ Listed all services with durations
□ Confirmed staff exist as GHL users
□ Set weekly working hours for each staff member
□ Identified which staff delivers which service
□ Answered: does physical space limit simultaneous bookings? → Rooms yes/no
□ Answered: are there shared tools with limited quantity? → Equipment yes/no
□ Decided: Collective or Service Booking for each calendar (multi-staff services)
□ Created Service Calendars in order (CAL-01, CAL-02 ...)
□ Created Rooms (if applicable) and linked to correct calendars only
□ Created Equipment (if applicable) and linked to correct calendars only
□ Created Calendar Group and added all calendars
□ Created Service Menu and arranged service order
□ Tested: booked one slot, confirmed availability logic works
□ Tested: booked same slot twice, confirmed second booking blocks correctly
```

---

## The Three Business Sizes at a Glance

```
SIMPLE (solo/small)
  → Staff + Service Calendars + maybe 1 Room
  → Example: Solo nail tech, single massage therapist

MEDIUM (small team, physical space)
  → Staff + Service Calendars + Rooms + 1-2 Equipment
  → Example: Barbershop, yoga studio, dental clinic

COMPLEX (multiple specialties, shared resources)
  → Staff (different availability per person) +
    Service Calendars (different staff per service) +
    Rooms (multiple, each linked to specific calendars) +
    Equipment (multiple types, different quantities) +
    Mix of Service Booking + Collective calendars +
    Service Menu with categories
  → Example: Wellness center, med spa, podcast studio
```
