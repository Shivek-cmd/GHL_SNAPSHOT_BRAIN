# GHL Guide — Payment Links

**Where in GHL:** Payments → Payment Links

---

## What Are Payment Links?

Payment Links allow you to combine one-time and recurring products into a single checkout experience. Instead of creating separate links per product, everything is bundled into one shareable, trackable link.

**Key benefits:**
- Unified checkout — customers see all one-time and recurring options in one place
- Upsell / cross-sell — present multiple offerings together to increase order value
- Recurring products are selectable one at a time; one-time products allow multiple selections
- Fewer links to manage — one link covers all offerings
- Custom branding, URL, and post-purchase behavior

---

## Payment Links Dashboard

**Where:** Payments → Payment Links

**Filters:** Start Date / End Date | Search

**Table columns:** Name | Link URL | Status | Price | Created At

---

## Creating a Payment Link

Click **+ Create New Payment Link** in the top-right corner.

---

### 1. Add Products

- **Select Product:** choose from your product library (one-time or recurring)
- **Let Customer Adjust Quantity:** ☐ checkbox — allows buyer to choose quantity; set min and max limits
- **+ Add Another Product:** add multiple products to the same link
  - One-time products: multiple can be selected at checkout
  - Recurring products: only one can be selected at checkout; grouped separately on the checkout page

---

### 2. Options (Checkboxes)

- ☐ **Require customers to add a phone number** — makes phone number field mandatory at checkout
- ☐ **Collect customer addresses** — adds street, city, state, country, postal code fields at checkout (for physical products or compliance)
- ☐ **Allow coupon codes** — displays a coupon code field at checkout (coupon must be created in Payments → Coupons first)
- ☐ **Enable redirection to custom URL** — redirects customer to a URL after payment
  - Enter destination URL
  - Open in: Existing Tab | New Tab

---

### 3. Advanced Options

**Call to Action Button Text:**
Select the button label shown to customers at checkout:
- Pay
- Book
- Donate

**Add Terms and Conditions:**
Add legal or policy text that appears below the Pay button — customers see it before completing the purchase. Supports formatted text.

**Branding:**
Add a custom "Powered by" label to the checkout page — enter your agency or business name.

**Automatic Deactivation:**
Set a date when the link expires automatically. After this date, the link is no longer accessible to customers. Useful for time-bound offers, limited campaigns, or promotional windows.

---

### 4. Payment Mode

- **Test** — simulate payments using test card numbers without processing real transactions
- **Live** — accepts real payments from customers

---

### 5. Name the Link

Enter an internal name for the payment link — used to identify it in the dashboard. Not shown to customers.

---

## Sharing a Payment Link

After saving, the link can be distributed via:

- **Copy Link** — copies the generic URL to share with any customer
- **Personalized Link** — generates a link prefilled with a specific contact's data (select contact from dropdown)
- **Send to Contacts** — delivers via Email | SMS | Both
  - Select contact
  - Choose channel
  - Customize subject and template

---

## Preview

Click **Preview** before publishing to verify:
- Product grouping (one-time vs recurring)
- Branding elements
- Form fields (phone, address)
- Button text and layout
- Terms and conditions placement

---

## Saving

Click **Save** to publish the payment link. The link becomes active and ready to share.

---

## How Payment Links Connect to the Rest of GHL

| Connection | Detail |
|-----------|--------|
| Products | Products must exist in Payments → Products before adding to a link |
| Coupons | Coupons must be created in Payments → Coupons before enabling coupon code field |
| Transactions | All payments through links appear in Payments → Transactions |
| Contacts | Personalized links pre-fill contact data; payments are recorded against the contact |
| Workflows | Payment link purchases can trigger the Order Submitted or Payment Received workflow triggers |
| Branding | Checkout page appearance controlled in Payments → Settings → Payment Link Customization |
