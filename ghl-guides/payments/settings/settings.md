# GHL Guide — Payments Settings

**Where in GHL:** Payments → Settings

---

## Sections

1. Receipts
2. Taxes
3. Notifications
4. Shipping & Delivery
5. Shipping Origin
6. Subscriptions
7. Miscellaneous Charges
8. Payment Link Customization

---

## 1. Receipts

Auto-sends a receipt to the customer after a successful payment.

**Fields:**
- Enable Automatic Sales Receipts: toggle on/off
- Title: default `RECEIPT`
- Receipt Prefix: default `REC-`
- Receipt Start Number: defines the starting number (e.g., `10001`) — auto-increments with each receipt
- From Name: name used when sending receipt notifications (if blank, uses business name)
- From Email: email address used when sending receipt notifications (if blank, uses business email)
- Subject: default `[{{receipt.company.name}}] Thank you for your recent purchase`
- Email Template: select or use Default
- Add Notes / Terms: rich text editor for footer content

**Tax Display Setting:**
- Include Tax in Prices:
  - Yes — tax is included in the purchase price; the price shown to the customer already includes the tax amount
  - No — tax is not included in the purchase price; the price shown to the customer does not include tax (tax added at checkout)

---

## 2. Taxes

Manage tax rates applied to products and invoices.

### Tax Rates (Manual)

Create manual tax rates to apply to products or invoices.

**Table columns:** Name | Rate | Description | Tax ID Number | Tax Agency | Created At

**Add Tax fields:**
- Name: name of the tax
- Rate: percentage (e.g., 12%)
- Description
- Tax ID Number
- Tax Agency

### Automatic Taxes

Automatically calculates tax based on the customer's address and/or the business's address.

- Enable Automatic Tax: toggle on/off

> Manual tax rates and automatic taxes can coexist. Automatic taxes override or supplement manual rates based on location rules.

---

## 3. Notifications

### Customer Notifications

**Abandoned Cart**
- Enable Abandoned Cart Email: toggle
- Email Template: select or Default
- Subject: `Complete your purchase`
- Send After: X Hours (default: 1 hour)

**Order Confirmation for Stores**
- Enable Order Confirmation Email: toggle
- Email Template: select or Default
- Subject: `Order Confirmation For Stores`
- Deliver digital products directly after purchase for Store orders: toggle

**Order Fulfillment Email**
Sent when an order is fulfilled — includes Shipping Carrier, Tracking Number, Tracking URL.
- Enable Order Fulfillment Email: toggle
- Email Template: select or Default
- Subject: `Order Fulfillment Email`

---

### Team Notifications

**Order Confirmation for Stores**
Receive confirmation when customers place a store order.
- Enable Order Confirmation Email: toggle
- Enable Order Confirmation SMS: toggle

---

## 4. Shipping & Delivery

Manage shipping profiles and zones for e-commerce store orders.

### General Profile

The default shipping profile that applies to all products and stores not assigned to a custom profile.

**What it covers:**
- Applies to all products automatically
- Covers most standard shipping needs
- Easy to set up and manage

**Profile Details:**
- Profile Name: General Profile
- Stores: all stores not assigned to another shipping profile
- Products: all products not assigned to another shipping profile

### Custom Profiles

Create custom profiles to set specific rates and destinations for certain products.

### Shipping Zones

Define regions you deliver to and the rates for each zone.

**Zone setup:**
- Zone Name: text input
- Countries / Regions: search by country name or code and select regions within each country
- Shipping Rates: set rate per zone (flat rate, free, weight-based, etc.)

**Countries supported:** GHL supports shipping zones for all countries globally, including regional breakdowns (states/provinces) for countries like United States (62 regions), Canada (13), Australia (8), India (37), UK (5), Germany, France, Brazil (27), Mexico (32), Japan (47), and many more.

---

## 5. Shipping Origin

Defines where shipments originate from — used for automatic shipping rate calculation.

**Fields:**
- Business Name
- Phone
- Email
- Street 1
- Street 2
- Country
- State
- City
- Zip Code

---

## 6. Subscriptions

Manage how GHL handles failed subscription payments.

### Failed Payment Retry Settings

Configure automatic retry steps when a subscription payment fails.

- Add retry attempts manually (e.g., Retry 1 day after previous attempt)
- Multiple retry steps can be chained
- If all retries fail, or if no retries are configured — set the **Subscription Status** to update to (e.g., Cancelled, Paused)

### Manage Invoices for Failed Subscription Payments

- **Automatically create invoices for failed subscription payments:** toggle
- **Automatically send invoices for failed subscription payments to customers via:** select channel

---

## 7. Miscellaneous Charges

### Processing Charges

Pass payment processing fees on to customers instead of absorbing them internally.

- Enable Passing Processing Charges to Customers: toggle
- Fees that can be passed: Credit Card processing fees, convenience fees
- When enabled, the processing fee is added to the customer's total at checkout

---

## 8. Payment Link Customization

Customise the visual appearance of payment links sent to customers.

**Fields:**
- Background Color: hex color picker (default `#FFFFFF`)
- Button Color: hex color picker (default `#155EEF`)
- Live Preview: shows how the payment page will look to the customer, including product name, price, description, quantity, and subtotal

---

## How Payment Settings Connect to the Rest of GHL

| Setting | Where it matters |
|---------|-----------------|
| Tax Rates | Applied when adding tax to invoices, order forms, and products |
| Receipts | Auto-sent after any successful payment (invoices, orders, subscriptions) |
| Shipping Zones | Used at checkout in e-commerce stores |
| Shipping Origin | Used for automatic shipping rate calculation |
| Subscription Retry | Controls what happens when a subscription charge fails |
| Processing Charges | Applies to all payment collection points (invoices, order forms, payment links) |
| Notifications | Fires on abandoned cart, order confirmation, and order fulfillment events |
