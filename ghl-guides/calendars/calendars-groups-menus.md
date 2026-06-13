# GHL Guide — Calendar Groups

**Where in GHL:** Calendars → Calendar Settings → Groups tab

> **Calendar Groups are for v1 calendars only (Round Robin, Personal, Service Booking, Class/Group, Collective, Event). They do NOT work with Services v2. Services v2 has its own public booking page — Calendar Groups are not required or compatible.**

---

## What Calendar Groups Are

A Calendar Group is a container that holds multiple **v1 calendars** under one shareable booking link. Instead of sharing 5 separate calendar links, you give clients one Group link that lets them pick from all grouped calendars.

**When to use:**
- You are building with v1 Service Booking calendars (not Services v2)
- Show multiple v1 service types under one booking page
- Required before creating a v1 Service Menu
- Organize v1 calendars by team, location, or service category

**When NOT to use:**
- You are building with Services v2 → use the v2 public booking page instead (View Booking Page)

---

## How to Create a Calendar Group

**Step 1 — Navigate**
Calendars → Calendar Settings → Groups tab → + Create Group

**Step 2 — Fill in Group details**
| Field | Notes |
|---|---|
| Group Name | Internal label and displayed header on the booking page |
| Description | Optional; appears on the booking page |
| URL Slug | Custom URL path for the group booking page |

**Step 3 — Add calendars to the group**
- After saving, open the group → Add Calendar
- Select from existing calendars in the sub-account

**Step 4 — Arrange and publish**
- Drag calendars to set display order
- Save — the group link is now live

---

## Calendar Group Key Points

- **One calendar can only belong to one group at a time** — assigning to a new group removes it from the previous group
- Groups can be deactivated: Groups tab → three-dot menu → Deactivate. Deactivated groups are hidden from the booking page but not deleted.
- **Neo Group View Template** is available as a visual upgrade for group booking pages (modern layout with calendar cards)
- The **Group Calendar ID** can be found by opening the group → Settings → ID shown in the URL or settings panel (useful for API calls)
- External calendar syncing per team member (Google, Outlook) works normally for all calendars inside a group

### Adding Unassigned Calendars to Groups
Calendars that are not yet in any group can be added:
1. Groups tab → open the target group → Add Calendar
2. Browse unassigned calendars → select and add

### Deactivating Calendar Groups
Deactivating hides the group link but preserves all calendars and existing appointments within it. Use deactivation instead of deletion when a group is seasonal or temporarily paused.

---

## Calendar Groups vs Service Menus

| Feature | Calendar Group | Service Menu |
|---|---|---|
| Purpose | Container for calendars | Styled booking UI with service browsing |
| Booking page | Simple list of calendars | Branded service cards with pricing |
| Payments (v1 calendars) | Per-calendar settings | Stripe only |
| Payments (v2 Services) | Per-service settings | Stripe, Square, Razorpay, Authorize.net, NMI |
| Coupon codes | No | Yes (v2 only) |
| Card-on-file | No | Yes (v2 only) |
| Multi-service cart | No | Yes (v2 only) |
| Required for Service Menu | Yes — prerequisite | N/A |
| Multiple per account | Yes | Yes |

**Key rule (v1 only):** A v1 Service Menu CANNOT be built without first creating a Calendar Group and assigning the relevant v1 Service Calendars to it. This rule does not apply to Services v2 which has its own booking page.

---

## Group Calendar URL

Each Calendar Group has a direct booking link:
- Found in: Groups tab → open group → **Share** option (copy link or embed code)
- Format: `https://[subdomain].ghl.io/[group-slug]`

Use this link in:
- Trigger Links pointing to a booking page
- Website/funnel CTAs
- AI agent booking prompts
- Email/SMS booking links (`{{custom_values.booking_link}}`)
