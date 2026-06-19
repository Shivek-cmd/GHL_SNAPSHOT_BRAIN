# GHL Guide — Workflows & Trigger Links

---

## Trigger Links

**What they are:** Short trackable URLs that perform an action when clicked. The action is defined inside GHL — not by the destination URL. When a contact clicks a trigger link, GHL fires the associated action against that contact's record.

**Where in GHL:** Marketing → Trigger Links → + New Trigger Link

### How to Create a Trigger Link

1. Marketing → Trigger Links → + New Trigger Link
2. Name it — use naming convention `TL-##: Name`
3. Set the destination URL — where the browser goes after the click. Must reference a custom value, never hardcode: `{{custom_values.booking_link_new_patient}}`
4. Set the action: Add Tag, Remove Tag, or both
5. Save — GHL generates the trigger link URL

**How the tracking works:** The trigger link URL is a GHL-hosted redirect. When a contact clicks it from an email or SMS, GHL intercepts the click, fires the action on that contact, then redirects them to the destination URL.

**Why this matters:** The action fired by the trigger link can be a workflow trigger — "Tag Added" → workflow fires. This allows button clicks inside emails to start entirely new automation sequences.

### Technical Constraints

- Trigger link actions are limited to Tag Add / Tag Remove — more complex actions require the tag to trigger a workflow
- Trigger links only identify the contact if clicked from a tracked communication (email, SMS) — anonymous browser clicks do not identify the contact
- Trigger link destination should always be a custom value, not a hardcoded URL
- Trigger links should be created before the email or SMS templates that will embed them
- TL IDs are assigned by GHL — document them in the system design as you build

### What Must Exist Before Building Trigger Links

- Destination custom values (e.g., `booking_link_new_patient`) must exist
- Any tags the link will add/remove must be documented (they'll auto-create when first used)

---

## Workflows

**What they are:** The automation engine of GHL. A workflow has a trigger (what starts it) and a sequence of actions (what it does). Workflows run per-contact — each contact gets their own instance of the workflow.

**Where in GHL:** Automation → Workflows → + New Workflow

---

### Workflow Structure

**Trigger** → one or more entry conditions that start the workflow for a contact

**Actions** → sequential steps executed for each contact that enters
- Actions execute top-to-bottom in order
- Wait steps pause execution until a condition or time delay is met
- Conditional branches split the path based on contact data
- A contact can exit the workflow from any point (via Exit action or If/Else branch)

---

### Workflow Triggers

A workflow needs at least one trigger. All available GHL triggers are listed below by category.

---

**Contact**

**Birthday Reminder**
Runs on each Contact's birthday at the time you select.
Filters:
- After: number of days (numeric value)
- Day: 1–31
- Month: January–December

**Contact Changed**
Fires when the chosen Contact fields are updated.
Filters:
- Assigned User: Has Changed | Has Changed To → select user
- City: Has Changed | Has Changed To → text input
- Contact Type: Has Changed | Has Changed To → Customer or Lead
- Country: Has Changed | Has Changed To → select country
- DND: Has Changed | Has Changed To → Disable DND for All Channels / Enable DND for All Channels
- Email: Has Changed | Has Changed To → text input
- Phone: Has Changed | Has Changed To → number with country code
- Postal Code: Has Changed | Has Changed To → text input
- State: Has Changed | Has Changed To → text input
- Street Address: Has Changed | Has Changed To → text input
- Tag: Added | Removed → select tag
- Website: Has Changed | Has Changed To → text input
- Custom Field (any): Has Changed | Has Changed To → depends on field type
- Note: "Has Changed" requires no value. "Has Changed To" requires a value input.

**Contact Created**
Activates the moment a new Contact record is added.
Filters:
- Contact Type: equals to | not equals to → Lead / Customer
- Email: equals to | not equals to → any value
- Phone: equals to | not equals to → any value (with country code)
- Tag: equals to | not equals to | any of | none of → select tag from list
- Custom Field (any): contains phrase → any value | exact match phrase → any value | intent type → Positive (Yes) / Negative (No) | is not empty → no value

**Contact DND**
Triggers when Do-Not-Disturb is enabled or removed.
Filters:
- DND Direction is: Outbound | Inbound
- DND Flag is: DND Disabled for All Channels | Disabled DND for Specific Channels | Enable DND for All Channels | Enabled DND for Specific Channels
- Tag: equals to | not equals to | any of | none of → select tag from dropdown
- Custom Field (any): contains phrase → any value | exact match phrase → any value | intent type → Positive (Yes) / Negative (No) | is not empty → no value

**Contact Tag**
Runs when the specified tag is applied or cleared.
Filters:
- Tag Added: select tag from list
- Tag Removed: select tag from list
- Custom Field (any): contains phrase → any value | exact match phrase → any value | intent type → Positive (Yes) / Negative (No) | is not empty → no value

**Custom Date Reminder**
Enrolls Contacts on a date stored in any custom field.
Filters:
- Contact Date Field: dropdown → all date-type fields (Created On, Updated On, custom date fields)
- Has Tag: select tag from list
- Opportunity Date Field: dropdown → all date-type opportunity fields
- Custom Field (any): contains phrase → any value | exact match phrase → any value | intent type → Positive (Yes) / Negative (No) | is not empty → no value
- ☐ Checkbox: Match on the year along with the day and month

**Note Added**
Fires whenever a new note is attached to the Contact.
Filters:
- Doesn't Have Tag: select tag from list
- Have Tag: select tag from list

**Note Changed**
Activates when an existing note is edited.
Filters:
- Doesn't Have Tag: select tag from list
- Have Tag: select tag from list

**Task Added**
Triggers when a task is created for the Contact.
Filters:
- Assigned User: select user

**Task Reminder**
Runs at the reminder time of a task.
Filters:
- After no. of days: numeric value
- Before no. of days: numeric value

**Task Completed**
Task completed trigger.
Filters:
- Assigned User: select user

**Contact Engagement Score**
Use this trigger to initiate workflow when a contact's engagement score meets a specific condition.
Filters:
- Score: Between | Equals To | Greater Than | Greater Than or Equal To | Less Than | Less Than or Equal To | Is Empty | Is Not Empty | Not Equal To → numeric value

---

**Events**

**Inbound Webhook**
Starts the workflow when an external system posts to your webhook URL.
Details:
- URL (POST / GET / PUT): GHL generates a unique webhook URL for this workflow. Max payload size: 1MB.
- Mapping Reference: map incoming payload fields to GHL contact fields
- Fetch Sample Requests: pull a recent request to inspect the payload structure
**Scheduler**
Adds a workflow trigger, and on execution, the Contact gets added to the workflow.
Filters:
- Interval: Hourly | Daily | Weekly | Monthly | Cron
  - Hourly: enter number of hours
  - Daily: select time (24-hour format)
  - Weekly: select days of the week + time
  - Monthly: select pattern →
    - Days of Month: select date (1–31) + time
    - Week and Day of Month: select week (First / Second / Third / Fourth) + time
  - Cron: enter cron expression in standard format → `*minute *hour *day *month *weekday`
    - Examples: `0 9 * * 1` (Mondays at 9 AM) | `30 14 1 * *` (1st of month at 2:30 PM) | `0 */2 * * *` (every 2 hours)
    - Note: expressions that run more than once per hour are not allowed
- Advanced Setting — Skip Weekends: when enabled, scheduled executions skip Saturdays and Sundays
- Stop On: select a date/time to stop the scheduler from running after that point
**Call Details**
Fires after a call ends with the selected status.
Filters:
- Call Direction: Incoming | Outgoing
- Call Status: ☐ Busy ☐ Cancelled ☐ Completed ☐ No Answer ☐ Voicemail
- Custom Disposition: ☐ Follow Up ☐ Incorrect Number ☐ No Answer ☐ Not Interested ☐ Requested Appointment ☐ Voicemail
- In Number Pool: select number pool
- In Phone Number: select phone number

**Email Events**
Triggers on open, click, bounce, or reply events.
Filters:
- Event: ☐ Bounced ☐ Clicked ☐ Complained (Spam) ☐ Opened ☐ Unsubscribed
- In Workflow: select workflow

**Customer Replied**

**Conversation AI Trigger**

**Custom Trigger**

**Form Submitted**

**Survey Submitted**

**Trigger Link Clicked**

**Facebook Lead Form Submitted**

**TikTok Form Submitted**

**Video Tracking**

**Number Validation**

**Messaging Error – SMS**

**LinkedIn Lead Form Submitted**

**Funnel/Website PageView**

**Quiz Submitted**

**New Review Received**
Triggers when a new review comes in from Facebook or Google. This trigger is contactless — reviews are not linked to any specific contact.
Filters:
- Is Review Spam: Is | Is Not → Yes / No | Is Empty | Is Not Empty → no value
- Review Rating: Between → min value + max value | Equals To → value | Greater Than → value | Greater Than or Equal To → value | Less Than → value | Less Than or Equal To → value | Not Equal To → value | Is Empty → no value | Is Not Empty → no value
- Review Source: Is | Is Not → Facebook / Google | Is Empty → no value | Is Not Empty → no value

**Prospect Generated**

**Click To WhatsApp Ads**

**External Tracking Event**

---

**Appointments**

**Appointment Status**

**Customer Booked Appointment**

**Service Booking**

**Rental Booking**

---

**Opportunities**

**Opportunity Status Changed**

**Opportunity Created**

**Opportunity Changed**

**Pipeline Stage Changed**

**Stale Opportunities**

---

**Affiliate**

**Affiliate Created**

**New Affiliate Sales**

**Affiliate Enrolled In Campaign**

**Lead Created**

---

**Courses**

**New Signup**
Fires when a new member account is created — their first enrollment in any offer (via purchase, manual grant, or workflow).
Filters:
- Offer: Is | Is Not → select offer name
- Product: Is | Is Not → select product name

**Offer Access Granted**
Fires when a contact is granted access to a specific offer — whether via purchase, manual admin grant, or the Course Grant Offer workflow action.
Filters:
- Offer: Is | Is Not → select offer name

**Offer Access Removed**
Fires when a contact's access to an offer is revoked — whether manually or via the Course Revoke Offer workflow action.
Filters:
- Offer: Is | Is Not → select offer name

**Product Access Granted**
Fires when access to a specific product is granted to a contact.
Filters:
- Product: Is | Is Not → select product name

**Product Access Removed**
Fires when access to a specific product is removed from a contact.
Filters:
- Product: Is | Is Not → select product name

**Product Started**
Fires when a member opens their first lesson inside a product (first engagement with that product).
Filters:
- Product: Is | Is Not → select product name

**Product Completed**
Fires when a member completes 100% of posts inside a product. Use this to issue certificates, send completion emails, grant bonus offers, or move a pipeline stage.
Filters:
- Product: Is | Is Not → select product name

**Category Started**
Fires when a member opens the first lesson inside a specific category/module.
Filters:
- Product: Is | Is Not → select product name
- Category: Is | Is Not → select category name

**Category Completed**
Fires when a member completes all posts inside a specific category/module.
Filters:
- Product: Is | Is Not → select product name
- Category: Is | Is Not → select category name

**Lesson Started**
Fires when a member opens a specific post/lesson.
Filters:
- Product: Is | Is Not → select product name
- Category: Is | Is Not → select category name
- Post: Is | Is Not → select post name

**Lesson Completed**
Fires when a member marks a specific post/lesson complete (clicks "Complete & Continue").
Filters:
- Product: Is | Is Not → select product name
- Category: Is | Is Not → select category name
- Post: Is | Is Not → select post name

**User Login**
Fires each time a member logs into the membership portal. Use for re-engagement detection — pair with a Wait + Condition to identify members who haven't logged in recently.
Filters:
- Offer: Is | Is Not → select offer name

---

**Payments**

**Invoice**
Fires on invoice creation, send, or overdue reminder.
Filters:
- Invoice Status: Sent | Paid | Partially Paid | Viewed | Void
- Tag: select tag from list

**Payment Received**
Fires whenever a matching payment is received across the CRM — one-time purchases, subscriptions, invoices, order forms, etc. Fires on both successful and failed transactions by default.
Filters:
- Global Product: Is | Is Not → select product from product library
  - Sub-filter: Price → select price name per selected product
- Payment Status: Is | Is Not → Failed | Success
- Source: Is | Is Not → Calendar | External | Form | Funnel | Invoice | Manual Payment | Memberships | Survey | Website
  - Sub-source (when Source = Invoice): Text2Pay Link | One-time Invoice | Recurring Template
  - Sub-source (when Source = Funnel / Website): One-step Order Form | Two-step Order Form | Upsell
  - Sub-source (when Source = Calendar): select calendar name
  - Transaction Type (when Source = Funnel / Website): Customer Present / First Transaction | Customer Not Present / Subscription Transaction

**Transaction Type Explained:**
- Customer Present / First Transaction — customer is on-session making the payment; includes all one-time purchases and the first order placement for a subscription product
- Customer Not Present / Subscription Transaction — runs in the background after a subscription is already created (e.g., recurring charge after trial ends)

**If/Else Conditions available inside the workflow:**

| Condition | Operator | Options |
|-----------|----------|---------|
| Product | Is / Is Not | Global product names |
| Funnel/Website | Is / Is Not | Funnel/Website names |
| Calendar | Is / Is Not | Calendar names |
| Source | Is / Is Not | Invoice / Funnel / Website / Calendar |
| Payment Status | — | Success / Failed |
| Amount | Equals To / Not Equal To / Greater Than / Greater Than or Equal To / Less Than / Less Than or Equal To / Is Empty / Is Not Empty | Numeric value |

**Custom Values available in this trigger:**

| Custom Value | Tag |
|-------------|-----|
| Payment Source | `{{payment.source}}` |
| Currency Symbol | `{{payment.currency_symbol}}` |
| Currency Code | `{{payment.currency_code}}` |
| Customer ID | `{{payment.customer.id}}` |
| Customer First Name | `{{payment.customer.first_name}}` |
| Customer Last Name | `{{payment.customer.last_name}}` |
| Customer Name | `{{payment.customer.name}}` |
| Customer Email | `{{payment.customer.email}}` |
| Customer Phone | `{{payment.customer.phone}}` |
| Customer Full Address | `{{payment.customer.address}}` |
| Customer City | `{{payment.customer.city}}` |
| Customer State | `{{payment.customer.state}}` |
| Customer Country | `{{payment.customer.country}}` |
| Customer Postal Code | `{{payment.customer.postal_code}}` |
| Invoice Name | `{{payment.invoice.name}}` |
| Invoice Number | `{{payment.invoice.number}}` |
| Invoice Issue Date | `{{payment.invoice.issue_date}}` |
| Invoice Due Date | `{{payment.invoice.due_date}}` |
| Invoice URL | `{{payment.invoice.url}}` |
| Invoice Recorded By | `{{payment.invoice.recorded_by}}` |
| Sub-Total | `{{payment.sub_total_amount}}` |
| Discount Amount | `{{payment.discount_amount}}` |
| Coupon Code | `{{payment.coupon_code}}` |
| Tax Amount | `{{payment.tax_amount}}` |
| Created On | `{{payment.created_on}}` |
| Total Amount | `{{payment.total_amount}}` |
| Transaction ID | `{{payment.transaction_id}}` |
| Payment Status | `{{payment.payment_status}}` |
| Payment Gateway | `{{payment.gateway}}` |
| Card Last 4 Digits | `{{payment.card.last4}}` |
| Card Brand | `{{payment.card.brand}}` |
| Payment Method | `{{payment.method}}` |

**Order Form Submission**

**Order Submitted**

**Documents & Contracts**

**Estimates**

**Subscription**

**Refund**

**Coupon Code Applied**

**Coupon Redemption Limit Reached**

**Coupon Code Expired**

**Coupon Code Redeemed**

---

**Ecommerce Stores**

**Shopify Order Placed**

**Order Fulfilled**

**Product Review Submitted**

**Abandoned Checkout**

**Shopify Abandoned Cart** *(deprecating)*

**Shopify Order Fulfilled** *(deprecating)*

---

**IVR**

**Start IVR Trigger**

---

**Facebook / Instagram**

**Facebook – Comment(s) On A Post**
Fires when a comment on a Facebook post matches the filters you set.
Filters:
- Page Is: select from connected Facebook pages
- Post Type: Published Post (all posts on the page) | Custom Post (enter URL)
- Post Is: select the specific post (based on Page Is + Post Type selection)
- Contains Phrase: fires if the comment body contains the exact text string → e.g., phrase "I bought from you" matches "I bought from you yesterday" but NOT "I bought one from you"
- Exact Match: fires only if the entire comment body exactly matches the text string → e.g., phrase "I bought from you" matches only "I bought from you" — not "I bought from you yesterday"
Toggle:
- Track First Level Comments Only → ON: trigger fires only for top-level comments, not for replies under a comment | OFF: fires for all comments including nested replies
Note: Automatic comments posted by workflow actions do not re-trigger this workflow — no infinite loop risk.

**Instagram – Comment(s) On A Post**
Fires when a comment on an Instagram post matches the filters you set.
Filters:
- Page Is: select from connected Instagram accounts
- Post Type: Published Post (all posts on the account) | Custom Post (enter URL)
- Post Is: select the specific post (based on Page Is + Post Type selection)
- Contains Phrase: fires if the comment body contains the exact text string → e.g., phrase "I bought from you" matches "I bought from you yesterday" but NOT "I bought one from you"
- Exact Match: fires only if the entire comment body exactly matches the text string → e.g., phrase "I bought from you" matches only "I bought from you" — not "I bought from you yesterday"
Toggle:
- Track First Level Comments Only → ON: trigger fires only for top-level comments, not for replies under a comment | OFF: fires for all comments including nested replies
Note: Automatic comments posted by workflow actions do not re-trigger this workflow — no infinite loop risk.

---

**Communities**

**Group Access Granted**
Fires when a contact is given access to a community group — whether via manual admin action, invite acceptance, paid group purchase, or the Grant Group Access workflow action.
Filters:
- Group: Is | Is Not → select group name

**Group Access Revoked**
Fires when a contact's access to a community group is removed — whether manually or via the Revoke Group Access workflow action. Also fires on subscription cancellation for Paid Groups.
Filters:
- Group: Is | Is Not → select group name

**Private Channel Access Granted**
Fires when a contact is added to a private channel inside a community group.
Filters:
- Group: Is | Is Not → select group name
- Channel: Is | Is Not → select channel name

**Private Channel Access Revoked**
Fires when a contact is removed from a private channel inside a community group.
Filters:
- Group: Is | Is Not → select group name
- Channel: Is | Is Not → select channel name

**Community Group Member Leaderboard Level Changed**
Fires when a community member advances to a new gamification level (points-based progression). Use to send congratulations, deliver level rewards, or unlock course access.
Filters:
- Group: Is | Is Not → select group name
- Level: Greater Than | Equals To → enter level number (1–9)

---

**Certificates**

**Certificates Issued**
Fires when GHL generates a certificate for a member upon reaching the product completion threshold (set on the certificate template). Use to send the certificate download link, add a completion tag, or move a pipeline stage.
Filters:
- Certificate: Is | Is Not → select certificate name from the list

---

**Communication**

**TikTok – Comment(s) On A Video**

**Transcript Generated**

---

**Google Ads**

**Google Lead Form Submitted**

---

### Workflow Actions

---

**Contact**

**Create Contact**

**Find Contact**

**Update Contact Field**

**Update Contact**

**Add Contact Tag**

**Remove Contact Tag**

**Assign to User**

**Remove Assigned User**

**Edit Conversation**

**Disable/Enable DND**

**Add Note**

**Add Task**

**Copy Contact**

**Delete Contact**

**Modify Contact Engagement Score**

**Add/Remove Contact Followers**

---

**Communication**

**Send Email**

**Send SMS**

**Send WhatsApp**

**Send Internal Notification**

**Send Review Request**
Sends a review request to the contact.
Fields:
- Action Name: label this action
- Review Type: SMS | Email | WhatsApp (template must be created inside Reputation → Settings first)
- Override Review Link: dropdown → No Override | select a specific review link to override the default

**Manual Action**

**Call**
Initiates a call to the assigned user or a default number and plays a whisper message before bridging to the contact. If the contact is assigned to a user, that user is called. If unassigned, the number in Settings → Company → Company Phone is called. If the receiver presses any number key during the call, the system dials the contact and bridges the two.
Fields:
- Action Name: label this action
- Call Whisper: short message played to the receiver before the call connects — supports Custom Values — plays up to 3 times (TTS billed at $0.00084 per 100 characters)
- Call Timeout (s): maximum seconds to wait before terminating the call attempt if not connected
- Disable Voicemail Detect: if ON, skips voicemail detection — eliminates the detection delay but if Stop On Reply is also ON, the workflow stops whether a person or voicemail answers; recommended only for shorter call timeouts
- Connect Call After Keypress: if ON, the call only bridges to the contact after the receiver presses a key — confirms a live person answered before connecting
Key notes:
- Voicemail detection: by default, GHL detects whether a person or voicemail answered — this adds a slight delay. If Stop On Reply is ON and voicemail is detected, the contact continues in the workflow. Disabling detection removes the delay but removes that distinction.
- Stop On Reply interaction: if the business answers but the contact does not, the workflow carries on regardless of Stop On Reply / Disable Voicemail Detect settings — those settings only apply to the contact side of the call
Example:
- Trigger: Appointment Confirmed
- Action: Call
- Action Name: "Appointment Call Reminder"
- Call Whisper: "You have a new appointment scheduled with {{contact.first_name}} at {{appointment.time}}. Press any key to confirm."
- Call Timeout: 30 seconds
- Disable Voicemail Detect: ON (for quicker connection)
- Connect Call After Keypress: ON (ensures a live person answers before bridging)

**Log External Call**
Records details of a call made or received through a third-party calling tool directly into the contact's CRM record and Conversations section. Use when calls happen outside GHL and need to be centralised in the contact timeline. Typically paired with an Inbound Webhook trigger — use Custom Values to map webhook data into each field.
Fields:
- Action Name: label this action
- Direction: enter call direction — `inbound` or `outbound`
- Date: date and time in ISO 8601 format — if left blank, current date and time is applied automatically
- To: receiver's phone number
- From: dialer's phone number
- Call Status: allowed values — `completed` | `answered` | `busy` | `no-answer` | `failed` | `canceled` | `voicemail` | `pending`
- Attachment: call recording URL(s) — separate multiple URLs with a comma; leave blank if no recording
Key notes:
- Requires an Inbound Webhook trigger to receive call data from the third-party system — the webhook provides the URL the calling tool posts to on each call event
- Phone numbers must be correctly mapped to identify or create the right contact — for inbound calls map the From Number to the contact's phone; for outbound calls map the To Number
- Add an If/Else branch after the trigger to split inbound and outbound calls before logging
- Add a Create Contact action before Log External Call in each branch so the call is associated with the correct contact record
- Recordings appear in the contact's Conversations section once logged
- Incomplete field mappings (missing direction, status, or phone numbers) result in incomplete or missed logs — double-check all Custom Value mappings before publishing
Example:
- Trigger: Inbound Webhook (receiving call event from third-party dialer)
- Branch: If direction = inbound → map From Number to contact phone; if outbound → map To Number
- Action: Create Contact (map phone from webhook data)
- Action: Log External Call
  - Direction: `{{trigger.direction}}`
  - Date: `{{trigger.date}}`
  - To: `{{trigger.to}}`
  - From: `{{trigger.from}}`
  - Call Status: `{{trigger.status}}`
  - Attachment: `{{trigger.recording_url}}`

**Messenger**
Sends a Facebook Messenger message to the contact. The contact must have previously messaged a connected Facebook page no more than 24 hours before reaching this action — required by Facebook's messaging policy for successful delivery.
Fields:
- Action Name: label this action
- Templates: select a pre-configured message template (optional — ensures consistency and compliance with Facebook message format guidelines)
- Message: the message content — supports Custom Values and dynamic content to personalise per contact
- Add Attachment: attach files or media (images, documents, promotional content)
- Add Files through URL: include files hosted online via URL instead of uploading directly
- Test Phone Number: send a test message to a specified number before finalising the workflow (optional)
Example:
- Trigger: Contact Form Submission
- Condition: Contact form submitted through a Facebook ad campaign
- Action: Messenger
- Message: "Thank you for reaching out! We received your inquiry through our Facebook ad. Our team will get back to you shortly."
- Template: Select a template aligned with the message purpose (if applicable)
- Add Attachment: Include a brochure or image relevant to the campaign

**Instagram DM**
Sends a direct message to the contact via Instagram. The contact must have previously messaged a connected Instagram page no more than 24 hours before reaching this action — required by Instagram's messaging policy for successful delivery.
Fields:
- Action Name: label this action
- Templates: select a pre-configured message template (optional — helps maintain consistency and compliance with Instagram guidelines)
- Message: the DM content — supports Custom Values to personalise per contact
- Add Attachment: attach files or media (images, documents) to the message
- Add Files through URL: include files hosted online via URL instead of uploading directly
Example:
- Trigger: Instagram Ad Lead Form Submitted
- Condition: Lead form submitted through a targeted Instagram ad
- Action: Instagram DM
- Message: "Thank you for showing interest in our products! We've received your inquiry through Instagram. Stay tuned for more updates."
- Template: Select a template aligned with the message intent
- Add Attachment: Attach a product catalog or promotional image

**WhatsApp**
Sends a WhatsApp message to the contact directly from a workflow. Supports free-form messages within the 24-hour messaging window and pre-approved templates for messages outside it.
Fields:
- Action Name: label this action
- Message Type: WhatsApp Template — select a pre-approved template to send messages outside the 24-hour window; free-form messages only available within the 24-hour window
- Template: choose from approved WhatsApp templates (must be created and approved before use — see WhatsApp Subaccount Setup)
- Message content: supports dynamic Custom Values (e.g., `{{contact.first_name}}`, `{{appointment.date}}`) for personalisation
Key notes:
- WhatsApp must be enabled and configured on the sub-account before this action works
- Business-initiated messages outside the 24-hour window require an approved template
- Free Entry Point Conversations: when a contact replies to a WhatsApp message, a Free Entry Point conversation opens — allows free-form or template messages for up to 72 hours at no additional cost
- DND: WhatsApp respects DND settings — contacts who opt out will not receive messages
Example:
- Trigger: Appointment Reminder
- Action: WhatsApp
- Action Name: "Send WhatsApp Appointment Reminder"
- Message Type: Template — Appointment Reminder
- Message: "Hi {{contact.first_name}}, this is a reminder for your appointment scheduled on {{appointment.date}}."
- Outcome: Contact receives a personalised WhatsApp reminder 24 hours before their appointment

**Send Live Chat Message**

**GMB Messaging**

**Conversation AI**
Sends a single AI-generated message to a contact, waits for their reply, and routes the workflow through branches based on the response. Uses the bot's prompt, training data, and conversation history to craft the message.
Fields:
- Action Name: label this action
- Advanced Bot Configuration (toggle): override the bot's defaults for this action only
  - Personality: define the tone for this message
  - Additional Instructions: add goals, intent, or specific guidance; if off, uses the bot's existing configuration
- Question: the message the AI sends — supports Custom Values
- Timeout: how long to wait for a reply before routing to the Time Out branch (set in minutes, hours, or days)
- Channel: select one channel per action — SMS | Facebook | Instagram | WhatsApp | Live Chat
- Skip if answered: toggle ON to bypass this action if the contact has already replied
- Bot responses limit: max number of AI messages before routing to No Condition Met if nothing matches
- Wait time: delay in seconds before the bot replies, allowing incoming messages to arrive first
- Branches & Conditions: Time Out and No Condition Met are always present and cannot be removed — add additional branches with matching conditions for different reply outcomes
Note: The AI uses Personality, Additional Instructions, the Question, training data, and conversation history to generate its response.

**Facebook Interactive Messenger**
Automates Facebook Messenger conversations with interactive buttons and quick replies.
Note: Follows Meta's 24-hour messaging policy — messages only deliver within 24 hours of the contact's last interaction with the Facebook Page.
Fields:
- Action Name: label this action
- Reply Type: Reply to Comment via DM (use when trigger is a comment, takes conversation private) | Reply to DM (use when responding to an existing DM)
- Templates: pull from Marketing → Snippets
- Message Body: text with Custom Values and Trigger Links
- Add Attachment: upload file or add via URL
- Add New Button (up to 3): each button has a label and an action →
  - Open Website: enter URL, opens in new tab, button stays visible after click
  - Call Number: enter phone number, opens dialer, button stays visible after click
  - Perform Action: creates a workflow branch, no specific external event
- Add Quick Reply (up to 13): label displayed in conversation; disappears after user selects it
- Wait Step: time to wait for user interaction before routing to Default Timeout branch

**Instagram Interactive Messenger**
Automates Instagram DM conversations with interactive buttons and quick replies. Only available when workflow uses an Instagram trigger (Instagram Comment on Post or Customer Reply — Instagram).
Note: Instagram follows Meta's 24-hour messaging rule — DMs only send within 24 hours of the last user interaction.
Fields:
- Action Name: label this action
- Reply Type: Reply to Comment via DM | Reply to DM
- Templates: pull from Marketing → Snippets
- Message Body: text with Custom Values and Trigger Links
- Add Attachment: upload file or add via URL (Quick Replies cannot be added in the same message when an attachment is included)
- Add Buttons OR Quick Replies (not both in one message):
  - Buttons (persistent, stay visible after click): Open Website | Call Number | Perform Action (creates workflow branch)
  - Quick Replies (disappear after selection, max 13): one-tap response options that create workflow branches
- Wait Step: pause duration while waiting for user interaction — contacts who don't respond route to Default Timeout branch

**Reply in Comments**
Replies to a Facebook or Instagram comment with a comment underneath it. Must be used with Facebook Comment(s) On A Post or Instagram Comment(s) On A Post trigger.
Fields:
- Comments: create up to 10 reply variations — system picks randomly. Supports manual text and merge tags from custom values or previous AI action output.
- Like Comment: toggle ON to like the comment being replied to | OFF to skip liking
Note: Automatic replies do not re-trigger the comment trigger — no infinite loop risk.

**Send Slack Message**

---

**Pipeline**

**Create/Update Opportunity**

**Move Opportunity**

**Remove Opportunity**

---

**AI — Premium Actions** *(each execution incurs an additional charge)*

**AI Translate**
Automatically translates text from a source language to a target language within a workflow. Used to personalize communications for multilingual audiences — translate an incoming message, then pass the output to a subsequent email, SMS, or notification action.

Fields:
- Action Name: label this action (e.g., "Translate Welcome Email to Spanish")
- From Language: the source language the input text is written in (e.g., English)
- To Language: the target language to translate into (e.g., French)
- Input Text: the content to translate — supports static text or Custom Variables from contact fields or prior workflow steps (e.g., `{{contact.message}}`)

Output: translated text is stored as a custom variable usable in all subsequent actions:
`{{workflow_ai_translate_content.INDEX.response}}` — where INDEX is the step number of this action

Example:
- Trigger: Contact Created
- Action: AI Translate — From: English / To: French / Input: "Hello, thank you for signing up!"
- Action: Send Email — Body includes `{{workflow_ai_translate_content.2.response}}`
- Result: French-speaking contact receives a correctly translated welcome message automatically

**AI Summarize**
Condenses long content into a concise summary of a specified length using AI. Preserves key points while removing redundant information — useful for converting verbose form submissions, notes, reviews, or transcripts into SMS-friendly or exec-ready summaries.

Fields:
- Action Name: label this action (e.g., "Summarize Customer Review")
- Max Length Input: specify the desired output length — options:
  - Number of words (e.g., 50 words)
  - Number of characters (e.g., 280 characters)
  - Number of sentences (e.g., 3 sentences)
  - Number of paragraphs (e.g., 1 paragraph)
- Input Text: the content to summarize — supports static text or Custom Variables from contact fields or prior workflow steps

Output: summarized text stored as a custom variable usable in subsequent actions (send email, SMS, store in custom field, pass to another action)

Common use cases:
- SMS confirmation: summarize detailed appointment notes to 160 characters, send via SMS
- Pipeline update: summarize opportunity notes to 1 paragraph, email to account manager on stage change
- Review digest: summarize a Google/Facebook review to 50 words, post to a Slack channel
- Meeting notes: condense a full transcript to 1 paragraph for stakeholder distribution
- Chain summaries: summarize to 500 words first, then summarize that output again to 100 words in a second action

**AI Intent Detection**

**AI Decision Maker**

**AI Prompt** *(GPT Powered by OpenAI)*
Sends a prompt to a GPT model and returns a completion you can use in later workflow steps.
Fields:
- Action Name: label this action
- Model: GPT 5 | GPT 5.1 | GPT 5 Mini (default) | GPT 5 Nano | GPT 4o | GPT 4 Turbo | GPT 4o Mini
- Prompt: natural language instruction — supports custom values for dynamic prompts (e.g., `Write a follow-up email for: {{contact.message}}`)
- Temperature (Advanced): 0.1–1.0 — lower = focused/predictable, higher = creative/random
Output: `{{chatgpt.1.response}}` — use in subsequent steps
Output can be:
- Stored in a Custom Field
- Used directly in Send Email or Send SMS actions
- Sent to a team via Webhook or Slack

---

**Appointments**

**Update Appointment Status**

**Generate One Time Booking Link**

---

**Opportunities**

**Create/Update Opportunity**

**Remove Opportunity**

---

**Payments**

**Stripe One-Time Charge**

**Send Invoice**
Sends a one-time invoice to the contact.
Fields:
- Action Name: label this action
- From User: select user
- Invoice Template: select template created inside Payments → Invoices & Estimates → Templates
- Payment Mode: Live
- Channel: Email | Text | Email & Text

**Send Recurring Invoice**
Sends a recurring invoice to the contact on a defined schedule.
Fields:
- Action Name: label this action
- From User: select user
- Invoice Template: select template created inside Payments → Invoices & Estimates → Templates
- Payment Mode: Live
- Start Date: Action (date the action fires) | Fixed Date (select specific date)
- End: select when the recurring series stops
- How Often: select frequency
- Every X: number of intervals
- Enable Auto-Payment: when enabled, the card used to pay the first invoice is auto-deducted for all subsequent invoices
- Channel: Email | Text | Email & Text

**Send Documents and Contracts**

---

**Marketing**

**Add to Google Analytics**

**Add to Google AdWords**

**Add to Custom Audience (Facebook)**

**Remove from Custom Audience (Facebook)**

**Facebook Conversion API**

---

**Affiliate**

**Add to Affiliate Manager**

**Update Affiliate**

**Add/Remove from Affiliate Campaign**

---

**Courses**

**Course Grant Offer**
Grants a contact access to a membership offer without requiring payment. The contact receives immediate access to all products included in that offer.
Fields:
- Action Name: label this action
- Offer: select the offer to grant access to (only published offers appear in the list)
- Access Expiry: Lifetime | Custom Date | Days After Enrollment
Key notes:
- This is the primary action for automating enrollment after a purchase, form submission, or any other trigger
- If a welcome email is built inside this workflow, GHL automatically disables the default Welcome Email from Membership settings — use only one welcome email method
- Fires the Offer Access Granted trigger in any workflow that is listening for it
- Contacts already enrolled in the offer receive the grant again — if the offer has time-limited access, their access start date resets
Common use cases:
- Grant course access after a payment is received (Source = Memberships)
- Enroll a contact in a free course after they submit a form
- Grant a bonus offer when a contact completes a primary course (triggered by Product Completed)
- Re-grant access when an offer is updated with new products

**Course Revoke Offer**
Removes a contact's access to a membership offer. Their progress data is retained — only access is removed.
Fields:
- Action Name: label this action
- Offer: select the offer to revoke access from
Key notes:
- Fires the Offer Access Removed trigger in any workflow listening for it
- Does not delete progress — if access is re-granted later, the member's progress history is still there
- Subscriptions in Payments → Subscriptions are NOT automatically cancelled when access is revoked here — cancel the subscription separately in Payments if needed
Common use cases:
- Revoke access when a subscription payment fails
- Remove access when a trial period ends without conversion
- Remove access when a contact is offboarded or refunded
- Time-gate a course by granting access on day 0 and revoking on day X via a Wait + Revoke pattern

---

**IVR (Interactive Voice Response)**

**Gather Input on Call**

**Play Message**

**Connect to Call**

**End Call**

**Record Voicemail**

---

**Communities**

**Grant Group Access**
Adds a contact to a specified community group. The contact receives access as a Contributor (default member role) unless role is changed manually after enrollment.
Fields:
- Action Name: label this action
- Group: select the community group to grant access to
Key notes:
- Fires the Group Access Granted trigger in any workflow listening for it
- For Private Groups, the contact is added directly without requiring admin approval — workflows bypass the approval flow
- The contact must have a valid email address to receive the community invitation / login link
Common use cases:
- Add a contact to a free community group when they submit a lead form
- Add a paying member to a private group after a successful payment
- Grant community access as part of an onboarding sequence after course enrollment
- Move a member to a higher-tier group when they complete a course or reach a leaderboard level

**Revoke Group Access**
Removes a contact from a specified community group. Their posts and comments remain in the group — only access is removed.
Fields:
- Action Name: label this action
- Group: select the community group to revoke access from
Key notes:
- Fires the Group Access Revoked trigger in any workflow listening for it
- Does not ban the contact — they can request to rejoin unless separately banned
- For Paid Groups: cancelling a subscription in Payments fires this automatically; use this action if you need to revoke access based on a different condition
Common use cases:
- Remove a contact from a private group when their subscription is cancelled
- Downgrade a member from a premium group to a free group on plan change
- Remove access during offboarding or refund processing
- Time-gate community access by granting on day 0 and revoking on day X

---

**Send Data**

**Webhook / Custom Webhook**

**Google Sheets** *(Premium Action — $0.01 per execution)*
Integrates Google Sheets directly into workflows, automating data transfers between GHL and a connected Google Sheet without third-party tools. Supports creating, looking up, updating, and deleting rows.
Prerequisites:
- Google account integrated with the GHL subaccount
- Google Sheet prepared with clearly defined headers in the first row
- Premium Triggers & Actions enabled on the Agency account and Subaccount

Basic setup fields (shared across all functions):
- Choose An Account: select the integrated Google account
- Choose a Drive: select the Google Drive containing the target sheet
- Choose a Spreadsheet: select the specific spreadsheet
- Choose a Worksheet: select the specific tab/worksheet within that spreadsheet
- Refresh Headers: fetches the latest first-row headers — use after renaming columns in Google Sheets
- Select Columns: include all columns or define a starting and ending column range

Functions:

**Create Spreadsheet Row**
Adds a new row at the end of the spreadsheet.
Fields:
- Account, Drive, Spreadsheet, Worksheet (as above)
- Starting Column / Ending Column: define the column range to write into
- Column values: map each column header to a value — supports Custom Values (e.g., `{{contact.first_name}}`, `{{contact.email}}`)
Note: New rows are always appended after the last existing row.

**Create Multiple Spreadsheet Row(s)**
Adds one or more new rows in a single action execution.

**Lookup Spreadsheet Row**
Finds the first row matching a search criteria. Matched row data is stored as custom variables usable in later steps.
Fields:
- Worksheet: select the worksheet to search
- Search Order: From the Top (returns first match) | From the Bottom (returns most recent match)
- Lookup Column + Lookup Value: the column to search and the value to match (e.g., Email = `{{contact.email}}`)
- Extra Column + Extra Lookup Value (optional): adds a second condition — both must match
- Create row if not found (toggle): when ON, fires a Create Spreadsheet Row action if no match is found (logged and charged separately)
Output: All matched row values stored as `{{sheet.INDEX.HEADER}}` variables — e.g., `{{sheet.1.email}}`. Use `{{sheet.1.rowNumber}}` to get the matched row's number.
Note: If no match is found, all subsequent actions referencing this lookup are skipped. Use an If/Else after the lookup to branch on whether a result exists.

**Lookup Multiple Spreadsheet Row(s)**
Same as Lookup Spreadsheet Row but returns multiple rows. Add a Row Count field to specify how many rows to retrieve.

**Update Specific Spreadsheet Row**
Updates data in a row identified by its row number.
Fields:
- Worksheet: select worksheet
- Row Number: the exact row to update — supports Custom Values (use `{{sheet.INDEX.rowNumber}}` from a prior Lookup)
- Starting Column / Ending Column: define the column range to update
- Column values: map headers to new values — leave blank to skip updating that column

**Update Spreadsheet Row Using Lookup**
Finds a row via a prior Lookup action and updates its values. Requires a Lookup action placed above this action in the workflow.
Fields:
- Select Lookup Action: choose the Lookup action to reference (only Lookup actions above this step are listed)
- Starting Column / Ending Column: define the range to update
- Column values: map headers to new values — leave blank to skip
Note: If the Lookup returned no rows, this action is skipped automatically.

**Update Multiple Spreadsheet Row(s)**
Updates multiple rows in a single action.

**Delete Specific Spreadsheet Row**
Clears all values in a row identified by its row number. The row itself is not removed — only its contents are cleared.
Fields:
- Worksheet: select worksheet
- Row Number: exact row to clear — supports Custom Values

**Delete Spreadsheet Row Using Lookup**
Finds a row via a prior Lookup action and clears its contents. Requires a Lookup action placed above this action in the workflow.
Fields:
- Select Lookup Action: choose the Lookup action to reference
Note: If the Lookup returned no rows, this action is skipped automatically. Row is cleared, not deleted.

Common patterns:
- To update or delete using a lookup: add Lookup → then Update/Delete Using Lookup
- To upsert (create if not exists): use Lookup with "Create row if not found" toggled ON
- To branch on lookup result: add If/Else after Lookup, condition on `{{sheet.1.rowNumber}}` existing
- To get row number for update/delete: use `{{sheet.INDEX.rowNumber}}` from Lookup output

Troubleshooting:
- Headers renamed in Google Sheets → click Refresh Headers in HighLevel and reconfigure column mappings
- Google account not appearing → reauthorize the Google account in HighLevel
- Spreadsheet not listed → confirm the correct account and Drive permissions are selected
- Lookup-dependent actions being skipped → Lookup returned no match; add If/Else to handle the no-result branch

---

**Internal Tools / Flow Control**

**If / Else**

**Wait**
Holds a contact in the workflow until a time condition is met or a CRM event occurs. Controls when the next steps fire so communications are timely and relevant.

**Action Name:** Always label the wait step (e.g., "Wait — 3 Days After Sign-Up") so it's identifiable in the builder.

---

**Wait Type 1 — A Set Period of Time**
Holds the contact for a fixed duration before continuing.
Fields:
- Time period & unit: Seconds | Minutes | Hours | Days
- Value type: Standard (fixed number) | Dynamic (pull from a custom variable)
- Advance Window (optional):
  - Resume On: select specific weekdays (e.g., Mon–Fri only)
  - Resume Between Hours: define a time window (e.g., 9 AM–5 PM)
  - Additional date filters: specific day, month, or year
Note: If the resume condition fires outside the allowed window (e.g., contact hits the wait on Saturday but resume is weekdays only), GHL holds until the window reopens.

---

**Wait Type 2 — A Specific Date and Time**
Waits until an exact calendar date and time before continuing.
Fields:
- Date selection: Standard (manually set) | Dynamic (pulled from a contact date field)
- Proceed timing: On the date | Before (enter offset) | After (enter offset)
- If date already passed: Continue next action | Exit automation | Go to specific step | Skip outbound actions until next wait/event

---

**Wait Type 3 — A Recurring Schedule**
Repeats on an ongoing cadence — contact waits until the next scheduled occurrence.
Fields:
- Frequency: Weekly | Monthly | Yearly
  - Weekly: select days (Sunday–Saturday) + time
  - Monthly: specific day of month OR Nth weekday of selected months + time
  - Yearly: select month and day + time
- Proceed timing: On date | Before (enter offset) | After (enter offset)
- Preview: shows the next 5 scheduled occurrences before saving
Note: Timezone shown on preview reflects the sub-account timezone.

---

**Wait Type 4 — An Upcoming Appointment or Booking**
Waits relative to a scheduled event on the contact's record.
Fields:
- Type: Appointment / Calendar Event | Service Booking | Invoice Due Date
- Proceed timing: At scheduled time | Before (enter offset in months/days/hours/minutes) | After (enter offset)
- If already passed: Continue next action | Go to specific step | Exit automation | Skip outbound communications

---

**Wait Type 5 — The Contact to Reply**
Pauses until the contact sends a reply on the selected channel.
Fields:
- Channel: SMS | Email (requires a prior send action on that channel to exist above this step)
- Timeout (optional): auto-advance after a set duration if no reply received
Note: When placed directly after a Send Email or Send SMS action, GHL surfaces this option first as the default suggestion.

---

**Wait Type 6 — The Contact to Take an Action**
Waits until the contact engages with a specific link or email event.
Fields:
- Action type: Clicks trigger link | Email events (open / click / bounce / unsubscribed / complained)
- Step selection: choose which trigger link or email send step to monitor (must exist above this step)
- Timeout (optional): auto-advance after a set duration if the action doesn't occur

---

**Wait Type 7 — Specific Conditions to be Met**
Waits until one or more custom logic conditions evaluate as true.
Fields:
- Segments: groups of conditions — add as many segments as needed
- Conditions within each segment: use AND/OR logic on any contact field, tag, custom field, pipeline stage, etc.
- A contact exits the wait the moment ANY segment evaluates true (segments are OR'd against each other)
- Timeout (optional): auto-advance after a set duration if no segment is ever satisfied
Example: Wait until Tag = "VIP" OR Custom Field "Budget" > 5000

---

**Timeout — When to Always Use It**
Always add a Timeout to Wait Types 5, 6, and 7 (Reply, Action, Condition). Without it, contacts whose event never fires remain paused in the workflow indefinitely.

**If Already in the Past — Options for Types 2, 3, 4**
- Continue next action: skips the wait and moves forward
- Go to specific step: jumps to a chosen step number
- Exit automation: removes the contact from the workflow entirely
- Skip outbound actions until next wait/event: skips all send actions between here and the next wait step

**Workflow AI Builder**
Supports conversational edits to any Wait action — change time delays, window settings, reply conditions, add/remove timeout branches, or convert between wait types without manual reconfiguration.


**Goal Event**
Tracks a specific milestone or contact behavior (click, form submit, appointment, payment, etc.) and automatically moves the contact to the goal step the moment the condition is met — regardless of where they are in the workflow. Replaces complex If/Else branching for common "did they do X yet?" patterns.
Note: Only one Goal Event action can be added per workflow. Multiple criteria can be configured inside that single action.

Supported goal types:

| Goal Type | Triggers When |
|---|---|
| Form Submitted | Contact submits any selected form (multi-select) |
| Payment Received | Payment event fires — filter by success/failure status and by product |
| Document Status | Document reaches: Viewed, Signed, Declined, or Completed |
| Email Events | Contact opens, clicks, unsubscribes, complains, or email bounces |
| Trigger Link Clicked | Contact clicks a specific tracked trigger link |
| Tag Added or Removed | A specific tag is added to or removed from the contact |
| Appointment Status | Appointment changes to: New, Confirmed, Showed, No-Show, etc. |

Configuration fields:
- Action Name: label this goal step (e.g., "Lead Conversion Goal")
- Select Type of Goal: choose the goal type from the list above
- Goal criteria: define the specific event — which form, which link, which tag, which status
- If contact reaches this goal step without meeting conditions:
  - End this workflow — stops the contact here
  - Continue anyway — moves contact forward regardless
  - Wait until the goal is met — holds the contact at this step until the condition is satisfied

How it works:
- The system continuously monitors all active contacts in the workflow for the goal condition
- The moment any contact meets the condition (even mid-wait or mid-sequence), they jump to the goal step immediately
- A contact will not be evaluated for the same goal event twice within the same workflow
- Goal Events fire outside business hours — monitoring is continuous
- A single contact event (e.g., email open) can meet goal conditions across multiple workflows simultaneously

Common use cases:
- Skip remaining nurture steps the moment a contact books an appointment
- Stop a follow-up sequence the instant payment is received
- Branch contacts who click a specific link into a targeted sub-sequence
- Move contacts forward when a contract is signed without waiting for a timed step

**Split**
Divides contacts into different workflow paths based on random percentage distribution. Used for A/B testing, lead routing, and campaign optimization.
Note: Split only supports random distribution — it has no criteria-based logic. To split contacts by a condition (e.g., order size, tag, field value), use If/Else instead.

Configuration fields:
- Action Name: label this action
- Distribution Type: Random Split (only option)
- Paths: add 2–5 named paths, each with a percentage weight
  - All path percentages must sum to exactly 100% — the builder blocks saving if they don't
  - A path can be set to 0% (no contacts routed there) as long as the total still equals 100%

Key rules:
- Once a contact is assigned to a path, they stay on that path — re-entering the same split sends them down the same path again, not a new random assignment
- Changes to split percentages only apply to contacts entering the action after the change
- Statistics tab on the action shows how many contacts entered each path and the total

Common use cases:
- A/B testing: 50/50 split to test two email subject lines or SMS copy variations
- Lead routing: 75% to a senior rep, 25% to a trainee
- Campaign optimization: run variant sequences in parallel, then consolidate the winner

**Go To**
Jumps a contact from the current position in a workflow to another action step within the same workflow. Used to loop contacts back through earlier steps or redirect them to a different branch without duplicating actions.
Constraint: Go To can only be placed as the last step of a workflow or branch — it cannot be inserted between existing actions.

Configuration:
- Action Name: label this action (e.g., "Go To — Wait Step")
- Target step: after saving, all other actions in the workflow are highlighted — click the target action to link it
- Disconnect: click the "Disconnect GoTo" icon on the action to unlink and re-select a different target step

Common use cases:
- Loop a contact back to a Wait step if a condition was not yet met (e.g., re-check every day until a tag is added)
- Skip a contact past steps in a branch they've already satisfied (e.g., jump from Branch 1 directly to a shared Wait in Branch 2)
- Retry a sequence segment without creating a separate workflow

**Remove from Workflow**
Automatically removes a contact from one or more workflows based on a trigger or condition. Keeps workflows clean by ensuring contacts only remain in automations relevant to their current status.

Configuration fields:
- Action Name: label this action (e.g., "Remove from Marketing Campaign Workflow")
- Workflow Removal Option:
  - Current Workflow — removes the contact from the workflow this action lives in
  - Another Workflow — removes the contact from a specific workflow you select
  - All Except Current Workflow — removes the contact from every active workflow except the one currently executing
  - All Workflows — removes the contact from every active workflow, including the current one

Key rules:
- Removal is immediate and cannot be automatically undone — the contact must be manually re-enrolled if needed
- Contacts are not notified when removed — the action only affects internal workflow state
- Commonly placed after a purchase, booking, or tag event to stop nurture or marketing sequences

**Drip Mode**
Regulates the flow of contacts through a workflow by releasing them in batches at set intervals. Instead of all contacts advancing simultaneously, Drip processes them in controlled groups — critical for high-volume email/SMS campaigns, protecting deliverability, and staying within API/sending limits.

Configuration fields:
- Action Name: label this action
- Batch Size: number of contacts to release per interval — any value from 1 to 10,000
- Drip Interval: how often each batch releases — minutes (1–60), hours (1–24), or days (1–7)

Drip Preview (first-time setup):
- A live schedule table shows the projected send time for each batch (up to 10 batches) before publishing
- If a Workflow Time Window is active (e.g., 8 AM–7 PM Mon–Fri), an inline warning appears — some batches may be shifted to the next available slot
- Preview is hidden when editing a Drip action that already has contacts queued in it

Action Statistics (published workflow):
- Click the statistics icon on the Drip action (blue icon showing contacts waiting) to open a detailed batch view
- Shows: summary cards (contacts in drip, next batch, ETA), full batch schedule table, status per batch, and active time window constraints
- Available controls: move contact to next step, delete contact from drip, contact hyperlink
- If drip settings were changed after contacts entered, a warning shows how many contacts are using old vs. new settings

Batch size change behavior:
- Changes to batch size or interval apply only to contacts entering the Drip action after the change
- Contacts already queued continue using the previous settings
- An informational note appears in the builder when editing settings on a workflow with contacts already in the drip

Draft / Publish behavior:
- If a workflow moves to Draft while contacts are sitting in a Drip action, those contacts are automatically paused
- When the workflow is re-published, the drip resumes from where it left off — contacts do not burst out all at once
- This preserves pacing and protects sender reputation

Key rules:
- New contacts entering mid-drip start their own drip schedule — they do not join an in-progress batch
- Drip works with any action type: email, SMS, task assignment, webhook, etc.
- Always pair with a Workflow Time Window if your sends must respect business hours

**Arrays**

**Text Formatter**

**Custom Code**

**Update Custom Value**

---

### Wait Steps — Time-Based vs Event-Based

**Time-based wait:** Pauses for a fixed duration (e.g., "Wait 24 hours"). The clock starts when the contact reaches the wait step.

**Event-based wait:** Pauses until something happens (e.g., "Wait until Tag 'appt-confirmed' is added"). If the event never happens, the wait can be open-ended — always pair with a timeout condition to avoid contacts getting permanently stuck.

**Wait until date/time:** Useful for appointment reminders — wait until "1 day before appointment time."

---

### If / Else Conditions

Conditions check contact data at the moment they are evaluated (not at workflow entry):

**Tag conditions:** Contact Has Tag / Does Not Have Tag / Tag Was Added (within X time)
**Custom field conditions:** Field equals / does not equal / contains / is empty / greater than / less than
**Pipeline conditions:** Contact is in Stage X of Pipeline Y
**Appointment conditions:** Has appointment / appointment is on / appointment status is
**Contact conditions:** Standard fields (email, phone, etc.) are empty or match a value

**Multi-branch logic:** GHL's If/Else supports one true branch and one false branch. For more than two paths, chain If/Else blocks.

---

### Workflow Settings

**Re-Entry:**
- Allow re-entry: Yes / No
- If Yes, the same contact can enter the workflow multiple times (each entry is independent)
- If No, a contact already in the workflow (or who has already completed it) will not re-enter
- Choose based on whether the automation should fire once ever, or every time the trigger condition occurs

**Contact Status:**
- What should happen if the contact is opted out of SMS or email? Options: skip the action, skip the whole workflow, exit workflow
- Configure per-workflow based on the communication type

**Stop on Response:**
- If the contact replies to an email or SMS, optionally stop the workflow (or a specific branch)
- Prevents sequences from continuing to send to a contact who has already responded

---

### Workflow Dependency Order

Workflows reference: tags, pipeline stages, trigger links, templates, calendars, custom fields.

All of these must be created before the workflow that references them. Build in this order:
1. Custom Values and Custom Fields
2. Tags (documented, will auto-create when used)
3. Templates (Email, SMS, WhatsApp)
4. Calendars
5. Pipelines and Stages
6. Trigger Links
7. Workflows (in dependency order — if WF-02 is triggered by WF-01's tag, build WF-01 first)

---

### Testing a Workflow

Before activating:
1. Create a test contact (use a real email/phone you can receive on)
2. Manually trigger the workflow entry condition (add the tag, submit the form, etc.)
3. Watch the contact's workflow history in real time: Contact Record → Workflows tab
4. Verify: correct tags applied, correct pipeline stages moved, correct messages sent, correct timing

After testing:
- Remove test tags and pipeline entries from the test contact
- Set workflow to Active

---

### Technical Constraints

- Workflows must be in Active status to fire — Draft status means the workflow exists but never runs
- A workflow can have up to 200 steps — for complex automation, split into connected workflows
- Contacts can be in multiple workflows simultaneously — manage this with re-entry settings and exit conditions
- Wait steps do not count against a contact's "time in workflow" for billing purposes
- GHL processes workflow steps asynchronously — expect a few seconds of lag between consecutive steps in high-volume scenarios
- Workflow execution history is stored per-contact and visible in the contact record under the Workflow tab
- Deleting a workflow removes it from the active queue — any contacts currently in it are removed immediately
- Workflow names must be unique within the sub-account

---

## Connection to the Rest of the System

Workflows are the connective tissue of the entire GHL system. Almost every other component either:
- **Triggers** a workflow (tag added, form submitted, appointment booked, pipeline stage changed)
- **Is acted on** by a workflow (template sent, pipeline moved, tag added, task created, AI invoked)

This means workflows are the last thing to build — everything they reference must exist first.
