# GHL Guide — Communities: Monetization

**Where in GHL:** Memberships → Communities → Groups → open group → Settings → Subscriptions (for Paid Groups) | Learning Tab (for Paid Courses inside Communities)

---

## Paid Groups

Charge members for access to a community group. Both Public and Private groups can be monetized.

**Where in GHL:** Group → **Settings → Subscriptions**

### Payment Options

**One-Time Payment**
Members pay once and receive unlimited access to the group.

Setup:
1. Group → Settings → **Subscriptions**
2. Click **Add new price**
3. Set Amount, set Type to **one-time**
4. Click **Add** → **Save**
5. Optionally enable Test Mode for payment verification

**Recurring Subscription**
Members are billed on a recurring schedule. Access continues while the subscription is active.

Setup:
1. Group → Settings → **Subscriptions**
2. Click **Add new price**
3. Set Amount, Type to **Recurring**, optional Trial Days, Billing Period (Monthly or Annually)
4. Save → toggle Test Mode if needed

### Taxes on Paid Groups

Paid Group checkouts apply taxes using your existing Payments → Settings → Taxes configuration. Same tax engine as course offers — automatic address-based taxes and manual rates both supported.

### Access After Payment

- **Private Groups:** Admins approve memberships manually after payment — People tab → Filter → Requested
- **Public Groups:** Members gain automatic access immediately after payment

### Notifications

- Admins and owners receive payment notification emails
- Members receive payment confirmation
- Members notified upon approval (Private Groups)

### Cancellations

- **GHL Payments cancellation:** Contact's subscription is cancelled → confirmation email sent → member automatically removed from group
- **Stripe cancellation:** Same behavior — automatic removal on cancellation

### Refunds

- **Via GHL:** Payments → Transactions → select transaction → issue refund
- **Via Stripe:** Refund from the Stripe contact details screen

**Card deletion/restoration:** If a contact's payment card is deleted and restored, membership typically reinstates without requiring new payment.

**Currency limits:** Minimum and maximum charge amounts vary by currency — refer to Stripe documentation.

---

## Paid Courses Inside Communities

Sell courses directly within a community's Learning Tab — members can browse and purchase without leaving the platform.

**Where in GHL:** Group → Learning Tab → course → pricing settings

### Adding a Paid Course

1. Navigate to the group's Learning Tab as an admin or owner
2. Create or add a course
3. Set pricing: one-time fee or recurring subscription
4. Enter price and currency
5. Configure taxes if needed (supports automatic and manual rates)
6. Enable Test Mode for verification before launch
7. Publish

**Course access flow:**
- Members browse available courses in the Learning Tab
- Member selects and reviews pricing
- Completes purchase → receives confirmation and access details via email
- Immediate access to course content

### Free Courses in the Learning Tab

Free courses can coexist alongside paid courses in the Learning Tab. All group members automatically gain access to free courses without any additional steps.

### Reordering Courses in the Learning Tab

1. Learning Tab → locate the course
2. Three-dot menu → **Move Courses**
3. Drag to rearrange the display order

### Copying Course Share Link

Three-dot menu on any course → **Copy Link** — share on social media, email campaigns, or any channel to drive direct purchases.

### Notifications for Paid Courses

- Course creators receive email notifications on successful payments and subscription cancellations
- Members receive payment confirmation and access details

---

## Advanced Course Unlock Options in Communities

Four methods to control how members unlock courses in a community's Learning Tab:

| Unlock Method | How it works |
|---|---|
| **All Members** | Open access to all group members — no restrictions |
| **Level Unlock** | Member must reach a specific leaderboard level to unlock the course |
| **Buy Now** | One-time purchase or subscription — instant access on payment |
| **Time Unlock** | Access granted after a set number of days from enrollment date |

**To configure:**
1. Learning Tab → select course → Edit Course
2. Under Access Settings, select the unlock method
3. Enter required parameters (level number, price, or days)
4. Save

**Important rules:**
- Only one unlock method can be applied per course
- Changes to unlock settings apply to future enrollments only — existing members retain current access
- Level Unlock requires the Gamification feature to be set up (see `communities-features.md`)

---

## Private Channel-Based Course Access

Restrict course visibility to members of specific private channels only. Members who are not in the designated channel cannot see the course at all in the Learning Tab.

**Where in GHL:** Learning Tab → select course → Edit Course → Visibility dropdown → **Private Channel**

**Setup:**
1. Learning Tab → select course → **Edit Course**
2. Visibility dropdown → select **Private Channel**
3. Choose one or more private channels from the list
4. Save

**Behavior:**
- Only members of the selected private channels can view the course
- When a member joins a linked private channel, they automatically gain course access immediately
- A "Private-channel based access" tag appears on the course for easy identification by admins

**Limitation:** Access controls apply to entire courses — module-level restrictions are not currently supported.

**Use cases:**
- Premium tier content available only to paid private channel members
- Moderator training accessible only to channel managers
- Early access content for a specific cohort channel

---

## Connection to Payments

All paid group and paid course transactions flow through GHL's payment engine:
- Transactions recorded in Payments → Transactions
- Subscriptions (recurring) tracked in Payments → Subscriptions
- Stripe is required for payment processing
- `Payment Received` workflow trigger fires on each successful charge (Source varies by entry point)
