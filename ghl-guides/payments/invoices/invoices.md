# GHL Guide — Invoices & Estimates

**Where in GHL:** Payments → Invoices & Estimates

---

## Sections

- All Invoices
- Recurring Invoices
- Templates
- Estimates
- Settings

---

## All Invoices

**Summary cards at top:**
- Invoices in Draft — count + total value
- Invoices Due — count + total value
- Invoices Received — count + total value
- Invoices Overdue — count + total value

**Filters:**
- Start Date / End Date
- Search (by invoice name, invoice number, customer)
- Invoice Status: All | Draft | Sent | Overdue | Payment Processing | Paid | Partially Paid
- Payment Mode: All | Live | Test

**Table columns:** Invoice Name | Invoice Number | Customer | Issue Date | Amount | Status

Each invoice row has a **Copy Link** option — copies the direct invoice URL so it can be shared manually via any channel (SMS, email, WhatsApp, etc.) without re-sending through the system.

---

## Create Invoice — 3 Options

When clicking **+ New Invoice**, GHL presents three options:
1. New Invoice *(one-time)*
2. New Recurring Invoice
3. Import Invoice from CSV

---

## 1. New Invoice

### Business & Customer Information
- Business Information: auto-filled from Settings → Business Information
- Customer Information: select existing contact or create new

### Invoice Settings
- Invoice Number: auto-generated with prefix (e.g., `INV-000001`) — editable
- Issue Date: defaults to today
- Due Date: defaults to today + X days (set in Settings → Payment Settings)

### Add Products
- Add from product catalogue or create inline
- Enable Tax Automatically toggle
- Per line item: Item | Price | Quantity | Tax | Subtotal
- Subtotal auto-calculated

**Adjustments:**
- Add Discount: customer amount (fixed or percent)
- Add Tax: manually add tax rates (tax rates must be configured in Payments → Tax Settings)
- Enable Tax Automatically: applies tax rates to all products automatically

### Add Payment Schedule *(for partial/split payments)*
- Split total into multiple payments by percentage or fixed amount
- Per payment slot: percentage or fixed amount + due date
- Add as many payment slots as needed

### Additional Options

**Add Notes / Terms:** rich text field for invoice footer content

**Charge Late Fees:** applies to overdue invoices
- Type 1 — Flat Fee:
  - Amount (USD)
  - Frequency: One Time | Daily | Weekly | Monthly
  - Grace Period (days)
  - Max Late Fees (USD)
- Type 2 — Percentage of Remaining Amount:
  - Percentage (%)
  - Frequency: Every X Month(s)
  - Grace Period (days)
  - Max Late Fees (USD)

**Tipping:** allow customer to add a tip
- Preset tip options: 5% | 10% | 15% | custom %

---

## 2. New Recurring Invoice

### Business & Customer Information
- Same as one-time invoice — select customer

### Invoice Settings
- Invoice Prefix: `INV-` (auto-increments per send)

### Add Products
- Same as one-time invoice — line items, tax, discounts

### Recurring Invoice Settings

**How often?** (frequency options):

- **Yearly** — on [day] of [month] of every [X] year(s)
- **Monthly** — on [day] of every [X] month(s)
- **Weekly** — on [day(s) of week] of every [X] week(s)
- **Daily** — every [X] day(s)

**Start Date:** select date

**End:** select when the recurring series stops (never / specific date / number of occurrences)

**Send Invoice X days in advance:** how many days before the billing date to send the invoice to the customer

---

## Settings

**Where in GHL:** Payments → Invoices & Estimates → Settings

Settings are split into 8 tabs:

---

### 1. Business Information

Fields:
- Business Logo (recommended 350 × 180px)
- Business Name
- Phone No
- Address
- Country | State | City | Zip Code
- Website

All fields support custom values via the **Add Custom Value** button.

---

### 2. Email Configurations

- From Name
- From Email

Used as the sender identity on all invoice and estimate emails.

---

### 3. Title, Terms and Layout

**Estimate:**
- Title (default: `ESTIMATE`)
- Terms/Notes (rich text editor)

**Invoice:**
- Title (default: `INVOICE`)
- Terms/Notes (rich text editor)
- Invoice Layout selector

> Pro tip: Invoices that include "please" and "thanks" get paid up to 2 days faster.

---

### 4. Payment Settings

- Estimate expires after X days (default: 14)
- Estimate Prefix (default: `EST-`)
- Invoice due after X days (default: 14)
- Invoice Prefix (default: `INV-`)
- Manage default Stripe payment methods for invoices
  - Note: invoices created from Workflows, Documents & Contracts, or Estimates use these default settings
- Allow Partial Payments: customer can pay any amount less than total (set minimum percentage)
- Charge Late Fees: auto-applies to overdue invoices (can be overridden per invoice)
- Allow Tip Payments: customer can add a tip at checkout

---

### 5. Product Settings

- **Import Product Description:** when enabled, product description is pulled from the catalogue into the invoice (editable)
- **Make Product Description Optional:** choose whether descriptions show by default or behind a toggle button in the editor

---

### 6. Reminder Settings

Invoice reminders apply to all one-time and recurring invoices where Automatic Payment is disabled and no payment schedule exists.

Multiple reminders can be configured. Each reminder has:
- Reminder Name
- Email Template (select or use Default)
- SMS Template (select or use Default)
- Subject line (supports merge tags)
- Reminder Frequency: Every X [Hours / Days] [Before / After] invoice is overdue
- Max Reminders: number of times this reminder fires
- Business Hours: HH:MM AM to HH:MM PM
- Preferred Timezone

**Default reminder subjects (examples):**
- Reminder 1: `[{{ invoice.company.name }}] Friendly Reminder: Payment Due Soon for Invoice #[{{ invoice.number }}]` — 3 days before overdue
- Reminder 2: `[{{ invoice.company.name }}] Action Required: Payment Due Today for Invoice #[{{ invoice.number }}]` — 1 hour before overdue
- Reminder 3: `[{{ invoice.company.name }}] Urgent: Invoice #[{{ invoice.number }}] is Overdue` — 7 days after overdue

---

### 7. Billing Custom Fields

Add custom fields to capture additional billing information on invoices.
- Up to multiple custom fields selectable from the custom field list

---

### 8. Notifications

#### Customer Notifications

| Event | Channels |
|-------|----------|
| Invoice received | Email + SMS |
| Estimate received | Email + SMS |
| Invoice payment successful | SMS only (email uses receipt settings) |
| Invoice payment failed | Email + SMS |
| Auto payment information (upcoming debit) | Email + SMS |
| Auto payment amount changed | Email + SMS |
| Auto payment failed | Email + SMS |
| Payment schedule received | Email + SMS |

Each notification has:
- Email Template (select or Default) + Subject
- SMS Template (select or Default)

#### Team Notifications

| Event | Channel |
|-------|---------|
| Invoice payment successful | Email |
| Invoice payment failed | Email |
| Auto payment failed | Email |
| Auto payment skipped (amount changed manually) | Email |
| Invoice could not be sent | Email |
| Estimate accepted | Email |
| Estimate declined | Email |

Each has Email Template (select or Default) + Subject.

**Merge tags used in notification subjects:**
- `{{ invoice.company.name }}` — business name
- `{{ invoice.number }}` — invoice number
- `{{ invoice.customer.name }}` — customer name

---

## Auto-Payments

### On a Single Invoice with a Payment Schedule

- Enable when sending the invoice: click **Send** → toggle **Enable Auto-Payment** in the modal
- Choose payment source:
  - **Customer Card** — card used the first time the customer pays
  - **Saved Card** — card already stored on the contact's profile
  - **New Card** — enter a new card; saved for future auto-charges
- View auto-paid invoice details in **Payments → Transactions**

### On Recurring Invoices

Auto-Payment automatically charges the customer's card on each billing date of a recurring invoice. No manual follow-up needed after setup.

**Prerequisites:**
- Recurring invoice must exist
- Supported payment gateway must be connected (Stripe)
- Valid customer card must be available
- Auto-Payment is card-only — cash and manual entry are not supported

**Card Options:**

| Card Type | When Auto-Pay Starts | Notes |
|-----------|---------------------|-------|
| Customer Card | After the first successful manual payment | Card is captured on first pay; auto-charges begin from the next occurrence |
| Saved Card | From the first occurrence immediately | No manual first payment required |
| New Card | From first occurrence after saving | A small authorization may occur when card is added |

**Where to manage cards on file:** Contact record → Payments → Cards on File (only last 4 digits and expiry visible)

---

### Auto-Pay Behaviour: New vs Existing Schedules

| Scenario | First Invoice | Future Invoices |
|----------|--------------|-----------------|
| Auto-Pay enabled on an existing recurring schedule | Manual | Auto |
| New schedule + Saved Card on file | Auto | Auto |
| New schedule + No Saved Card | Manual | Auto |

- Editing a generated child invoice before its charge time **pauses** auto-pay for that invoice only
- Future occurrences are unaffected unless also edited
- Invoice dates already created cannot be changed

---

### Failed Payments & Retry

- Customer and location user are both notified on failure
- Customer can pay manually with same card or new card
- System retries **2 additional times, 24 hours apart**
- If still unpaid after retries: no further automatic attempts — must be paid manually
- Paying with a new card makes it the default for future auto-charges in that schedule

---

### How to Enable Auto-Pay on a Recurring Invoice

1. Go to **Payments → Invoices & Estimates → Recurring Invoices**
2. Open an existing schedule or click **New → New Recurring Invoice**
3. Click **⋮ (three dots)** menu → **Manage Auto Payment**
4. Toggle **Enable Auto-Payment ON**
5. Select card source: Customer Card | Saved Card | New Card
6. Click **Save**

**To disable:** same path → toggle OFF → Save. Stops from the next occurrence.

**Verification checklist after enabling:**
- Auto-Pay shows as enabled in recurring invoice config
- Correct payment method is selected
- Next scheduled occurrence has not already passed
- Customer has a valid card available

---

### Troubleshooting Auto-Pay

- Next invoice was already generated before Auto-Pay was enabled
- No valid card available for the customer
- Recurring invoice was updated after an earlier occurrence was already created
- Payment gateway not configured for automatic charging

---

## Recording a Payment Manually

Payments can be recorded manually (cash, cheque, bank transfer, or card) from multiple places in GHL.

**Methods:**

| Entry Point | How |
|------------|-----|
| Payments → Invoices (desktop) | Open invoice → Record Payment (top right) |
| Payments → Invoices (mobile) | Long-press invoice → Record Payment |
| Contact record | Payments tab → Add Card on File / Charge Card / Create Subscription |
| Appointment / Calendar | Open appointment → Payments tab → Collect Payment |
| Conversations tab | Click **$** icon in SMS section → generates a payment link |
| Mobile App (POS) | Open appointment → Record Payment → select instrument including Tap to Pay |

**Manual payment types supported:** Cash | Cheque | Bank Transfer | Other

After recording, invoice status updates to **Paid** and the transaction appears in financial reports.

---

## How Invoices Connect to the Rest of GHL

| Action / Trigger | Where |
|-----------------|-------|
| Send Invoice | Workflows → Send Invoice action |
| Invoice trigger | Workflows → Invoice trigger (created, sent, due, paid) |
| Payment Received trigger | Workflows → Payment Received trigger |
| Documents & Contracts | Can generate an invoice after signing |
| Estimates | Can be converted to an invoice on acceptance |
| Products catalogue | Used when adding line items to invoices |
| Tax Settings | Payments → Settings → Tax (must exist before adding tax to invoices) |
| Stripe integration | Required for payment processing and auto payments |
