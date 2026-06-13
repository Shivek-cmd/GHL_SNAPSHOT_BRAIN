uestio# GHL Guide — Rentals

**Where in GHL:** Calendars → Calendar Settings → Rentals tab

---

## What Rentals Is

Rentals is a distinct booking module inside GHL's Calendars for businesses that rent out items, spaces, or equipment by the hour, day, week, or month. It is separate from the Services and standard calendar systems.

**Use cases:** Property rentals, vehicle rentals, equipment rentals, studio time, room rentals, gear rental companies.

> **When NOT to use Rentals:** If your business has staff (engineers, technicians, therapists) whose individual availability determines whether a booking can be made — use Services v2 instead. Rentals has no staff concept. All availability is controlled by the listing's hours and inventory only. If an engineer is sick and Studio A should be unavailable, Rentals cannot reflect this automatically — you would have to manually block the time. Services v2 checks staff availability automatically per booking.

**Key capabilities:**
- Flexible booking periods (hourly, daily, weekly, monthly)
- Inventory management (track how many units are available)
- Variants (multiple versions of the same listing)
- Advanced pricing (seasonal, day-of-week, hour-of-day, duration discounts, quantity discounts)
- Security deposits
- Multi-item cart (customers can book multiple listings in one checkout)
- iCal sync with external platforms (Airbnb, VRBO, etc.) to prevent double-booking
- Customer-facing booking website with categories and real-time availability

---

## Navigation

- Calendars → Calendar Settings → **Rentals** tab
- Sub-sections: Listings, Global Settings, Bookings (in Appointment List View)

---

## Listings & Categories

### What Listings Are
Individual rentable items — each has its own images, description, pricing, booking rules, and availability.

### What Categories Are
Organizational containers that group similar listings (e.g., "Beach Houses", "Sedans", "Cameras"). Up to **50 categories** per account.

### Creating a Category
1. Rentals → Listings → **+ New Category**
2. Enter: Category Name (required), optional URL slug
3. Click Create

**Category rules:**
- Each listing belongs to exactly one category
- Uncategorized listings go to the Default Category
- Deleting a category moves its listings to Default
- Reordering categories updates the public booking page display order
- Share a category link: three-dot menu → **Share Category** → generates a filtered public link

### Creating a Listing

**Step 1 — Navigate**
Rentals → Listings → **+ New Listing**

**Step 2 — Basic Details (in creation modal)**
| Field | Notes |
|---|---|
| Listing Image | Upload/drag photos for booking page |
| Listing Name | Required; customer-facing title |
| Description | Features, what's included |
| Base Price | Cost per time unit (e.g., $50/hour) |
| Category | Assign to a category |
| Status | Active = visible; Inactive = hidden until ready |

**Step 3 — Advanced Settings (Edit Listing — 4 tabs)**

#### General Information Tab
| Field | Notes |
|---|---|
| Listing Images | Up to 30 images per listing |
| Listing Name | Update title |
| Description | Edit details |
| Category | Reassign |
| Status | Toggle Active/Inactive |
| Listing-Specific Form | Collect extra info for THIS listing at booking; skipped for multi-listing cart bookings |

#### Inventory & Pricing Tab

**Inventory section:**
| Field | Notes |
|---|---|
| Inventory toggle | Enable to manage available units; if off, whole listing = 1 bookable unit |
| Stock | Total units available (e.g., 3 cameras) |

**Variants:**
Variants = different versions of the same listing (e.g., Sedan vs SUV, Body Only vs With Lens).

To add a variant:
1. Toggle **Variants** ON → click + New
2. Set: Variant Name, Stock, Base Price, optional Security Deposit
3. Confirm

**Pricing — Base and Advanced rules:**

| Rule Type | How It Works |
|---|---|
| **Base Price** | Standard rate before any adjustments |
| **Seasonal Pricing** | % adjustment or flat rate override for a date range |
| **Day of Week Pricing** | % adjustment per weekday/weekend |
| **Hour of Day Pricing** | % adjustment per time block — **only for hourly bookings** |
| **Duration Discounts** | Flat or % discount when booking exceeds a duration threshold |
| **Quantity Discounts** | Flat or % discount for bulk unit bookings — **requires inventory enabled** |

**Pricing stacking order (applied in this sequence):**
1. Base Price
2. Seasonal Pricing (if date range matches)
3. Day of Week Pricing
4. Hour of Day Pricing (hourly only)
5. Duration Discounts
6. Quantity Discounts

**Security Deposit:**
- Optional refundable or card-on-file deposit
- Requires: Calendar Settings → Rentals → Global Settings → Payment Settings → enable Security Deposits
- Set to $0 = hidden from booking; displays separately on invoices when > $0

#### Booking Settings Tab

Three booking period modes — choose based on how customers select time:

**1. Date & Time Selector**
- Customer picks exact start and end date + time
- Best for hourly rentals requiring precise time selection
- Duration = exact difference between start and end

**2. Date Selector (date-only bookings)**
- Customer picks start and end dates only
- System applies Rental Start Time and Rental End Time
- **Day-based pricing:** End Time > Start Time (same date = 1 day; e.g., 11 AM check-in, 5 PM check-out)
- **Night-based pricing:** End Time < Start Time (two consecutive dates = 1 night; e.g., 3 PM check-in, 11 AM check-out)
- Hourly pricing NOT supported with this mode

**3. Fixed Durations**
- Customer books a predefined duration: 2 hours, 1 day, 1 week, or 1 month
- Optional: let customer choose start time; otherwise system uses Rental Start Time

**Additional booking control fields:**
| Field | Notes |
|---|---|
| Minimum Duration | Shortest booking allowed |
| Maximum Duration | Longest booking allowed |
| Pre/Post Buffer | Cleaning/setup time before and after each booking |
| Minimum Scheduling Notice | Required advance notice before booking start |
| Maximum Advance Window | Furthest date customers can book ahead |

#### Calendar Sync Tab
Sync with external calendar platforms (Airbnb, VRBO, Booking.com, etc.) to prevent double-booking:

| Direction | Feature | Details |
|---|---|---|
| Import | iCal URL import | Add .ics link from external platform; imported bookings appear as blocked time |
| Export | iCal export | Generate unique .ics link for external platforms to import GHL availability |
| Sync frequency | Automatic | External bookings imported every 1–2 hours; manual refresh available |

**Notes:**
- With variants enabled: imported calendars block all variants for the imported duration
- With inventory enabled: the whole inventory is blocked for the imported booking duration

---

## Bookings Management

### Accessing Rentals Bookings
Calendars → Appointment List View → select **Rentals** from dropdown

**Why separate rows:** Each row = one listing in the booking. A cart with 3 listings = 3 rows in the table.

### Appointments Table Columns
| Column | Description |
|---|---|
| Contact | Customer name and email |
| Listing | Name of booked listing |
| Start / End Time | Rental duration |
| Status | Unconfirmed / Booked / Active / Completed / Canceled |
| Payment Status | Pending / Paid / Partially Paid |
| Actions | View or Edit |

### Booking Status Definitions
| Status | Meaning |
|---|---|
| Unconfirmed | Booking initiated but not confirmed |
| Booked | Confirmed reservation |
| Active | Rental is currently in progress |
| Completed | Rental period ended |
| Canceled | Booking was canceled |

### Creating a Booking Manually
Calendars → Appointment List View → **Create Booking** (top-right)

---

## Pricing Calculation Examples

### Daily listing with seasonal + duration discount
- Base: $100/day | Seasonal: +20% (June–Aug) | Duration: 10% off for 6+ days | Booking: 7 days in July
1. $100 × 7 = $700
2. $700 × 1.2 = $840 (seasonal)
3. $840 × 0.9 = **$756 total**

### Hourly listing with time-based adjustments
- Base: $25/hr | Day of week: +10% Saturday | Hour of day: +15% (6–9 PM) | Booking: 3 hours Saturday 6–9 PM
1. $25 × 3 = $75
2. $75 × 1.10 = $82.50
3. $82.50 × 1.15 = **$94.88 total**

### Equipment with quantity discount
- Base: $50/day | Quantity: 5% off for 5+ units | Booking: 5 units, 1 day
1. $50 × 5 = $250
2. $250 × 0.95 = **$237.50 total**

---

## Important Pricing Nuances

- System checks the **start time** of each billed unit and applies rules to the entire unit — no mid-unit splits
- Time billing is precise (measures from exact start date/time); any overflow beyond a period starts a new billing cycle
- Example: Booking from 2:00 PM Oct 18 to 2:05 PM Oct 19 = 2 full days charged
- Same pricing logic applies to both the public booking website and manual in-app bookings

---

## Rentals vs Standard Calendars vs Services v2

| Feature | Standard Calendars | Services v2 | Rentals |
|---|---|---|---|
| Booking type | Appointments (time slots) | Appointments (time slots) | Duration-based (rental periods) |
| Inventory tracking | No | No | Yes |
| Multi-item cart | No | No | Yes |
| External iCal sync | Conflict-check only | No | Full import/export |
| Pricing complexity | Fixed | Variations + add-ons | Seasonal, duration, quantity discounts |
| Use case | Consultations, sessions | Service businesses | Property, equipment, vehicle rental |
