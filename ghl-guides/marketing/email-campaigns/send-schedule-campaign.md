# GHL Guide — How to Send or Schedule an Email Campaign

---

## What Regular Email Campaigns Are

One-time broadcast emails sent to a selected audience from the Email Marketing area. Built for announcements, newsletters, and promotions. No workflow automation required — you design, select your audience, and send.

**Where in GHL:** Marketing → Emails → Campaigns

**Prerequisite:** A verified sending domain must be configured before any campaign can go out.

---

## Full Step-by-Step Process

---

### Step 1 — Create the Campaign

Marketing → Emails → Campaigns → **+ New Campaign**

Options:
- Start from a saved template
- Build from scratch in the email builder
- Duplicate a previous campaign (fastest for recurring sends like newsletters)

---

### Step 2 — Design the Email

Inside the email builder:
- Add content, headings, images, buttons, links
- Insert merge tags for personalization (e.g., `{{contact.first_name}}`)
- Insert unsubscribe link manually if using custom footer: `{{contact.unsubscribe_link}}`
- Use **Preview** to check desktop and mobile layout before sending
- Use **Send Test Email** to send a copy to your own inbox — test emails do not display the unsubscribe link (this is expected, not a bug)

---

### Step 3 — Go to Send / Schedule Page

After designing, click through to the Send or Schedule screen.

---

### Step 4 — Configure Send Settings

All fields below apply to both Send Now and Schedule:

| Field | Details |
|-------|---------|
| Sender Name | The name contacts see in their inbox (e.g., `Ritesh Watts`) |
| Sender Email | The from address (e.g., `hello@riteshwatts.com`) — must be on verified domain |
| Sender Domain | Confirm the verified domain is selected |
| Reply To | Email address replies go to — can differ from Sender Email |
| Subject Line | Required — write it here or it pulls from the template |
| Preview Text | Optional — appears after subject in inbox preview; keep under 90 characters |
| Recipients | Select audience — Smart List, segment, or all contacts |
| Link Tracking | Toggle ON to track which links were clicked and by whom |
| UTM Tracking | Toggle ON to auto-append UTM parameters to all links |
| Add Tags | Auto-tag contacts based on interaction (Opened / Clicked) |
| Attach Files | Optional — max 10MB per attachment |

---

### Step 5A — Send Now

Click **Send Now** → campaign goes out immediately to the selected audience.

Use when: you want instant delivery, no scheduling needed.

---

### Step 5B — Schedule for Later

Set:
- **Date** — the calendar date to send
- **Time** — the time to send (uses the sub-account's timezone)

Click **Schedule** → campaign is queued.

**Rescheduling:** You can change the date/time up to 1 hour before the scheduled send time. After that, the campaign is locked and cannot be rescheduled.

---

## Throttling (Batch Delivery)

For large lists, throttling releases emails in batches instead of all at once. Reduces server load and protects deliverability.

Configure batch size and interval on the send settings screen if needed.

---

## Version History

Previous versions of a campaign can be restored via the campaign edit menu. Use this if you need to roll back content changes.

---

## For Newsletter — Real with Ritesh (Weekly Process)

| Setting | Value |
|---------|-------|
| Sender Name | Ritesh Watts |
| Sender Email | hello@riteshwatts.com |
| Reply To | hello@riteshwatts.com |
| Recipients | Smart List → `Newsletter — Active` |
| Link Tracking | ON |
| UTM Tracking | ON |
| Add Tags | Opened → `newsletter-engaged` / Clicked → `newsletter-clicked` |
| Schedule | Every Wednesday at [your preferred time] |

---

## Key Rules

- Test email does not show unsubscribe link — this is normal
- Rescheduling is only possible more than 1 hour before send time
- Verified sending domain is required — campaign will not send without it
- If using a custom footer with `{{contact.unsubscribe_link}}`, turn OFF the default unsubscribe toggle in Settings → Business Profile → General Tab
- Duplicate last week's campaign as a starting point to save setup time each Wednesday
