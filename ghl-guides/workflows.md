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

**Category Started**

**Category Completed**

**Lesson Started**

**Lesson Completed**

**New Signup**

**Offer Access Granted**

**Offer Access Removed**

**Product Access Granted**

**Product Access Removed**

**Product Started**

**Product Completed**

**User Login**

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

**Group Access Revoked**

**Private Channel Access Granted**

**Private Channel Access Revoked**

**Community Group Member Leaderboard Level Changed**

---

**Certificates**

**Certificates Issued**

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

**Messenger**

**Instagram DM**

**WhatsApp**

**Send Live Chat Message**

**GMB Messaging**

**Conversation AI**

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

**AI Summarize**

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

**Course Revoke Offer**

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

**Revoke Group Access**

---

**Send Data**

**Webhook / Custom Webhook**

**Google Sheets**

---

**Internal Tools / Flow Control**

**If / Else**

**Wait**

**Wait Until**

**Goal Event**

**Split**

**Go To**

**Remove from Workflow**

**Drip Mode**

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
