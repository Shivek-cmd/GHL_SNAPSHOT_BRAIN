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

**Payment Received**

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

**Instagram – Comment(s) On A Post**

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
- Create Contact — adds a new contact to the CRM; automates lead capture from external sources
- Find Contact — locates an existing contact based on provided data; use before updating or referencing
- Update Contact Field — writes a value to a specific custom field on the contact
- Update Contact — updates standard contact fields (name, email, phone, address, etc.)
- Add Contact Tag — adds a tag to a contact for segmentation and workflow triggering
- Remove Contact Tag — removes a tag from a contact
- Assign to User — assigns the contact to a specific team member
- Remove Assigned User — clears the assigned user from the contact
- Edit Conversation — marks, archives, or unarchives a conversation in the inbox
- Disable/Enable DND — turns Do Not Disturb on or off; controls whether outbound messages are suppressed
- Add Note — adds a custom note to the contact record
- Add Task — creates a task tied to the contact; if no contact exists (e.g., inbound webhook), creates a contact-less task
- Copy Contact — duplicates a contact into another sub-account
- Delete Contact — permanently removes a contact from the CRM
- Modify Contact Engagement Score — adjusts the contact's engagement score up or down
- Add/Remove Contact Followers — adds or removes team members as followers on the contact

---

**Communication**
- Send Email — sends an email using a saved template (ET-##). Never write content inline — always reference a template.
- Send SMS — sends an SMS using a saved template (ST-##) or entered text
- Send WhatsApp — sends a WhatsApp message using an approved template (WA-##)
- Send Internal Notification — sends an email or SMS to an assigned user or team member (not the contact)
- Send Review Request — sends a review request to the contact
  - Action Name: label this action
  - Review Type: SMS | Email | WhatsApp (template must be created inside Reputation → Settings first)
  - Override Review Link: dropdown → No Override | select a specific review link to override the default
- Manual Action — prompts a team member to take a manual action; pauses the workflow until marked done
- Call — dials the contact; if they answer, connects to the assigned user; used for auto-dialing and outreach
- Messenger — sends a Facebook Messenger message to the contact
- Instagram DM — sends an Instagram Direct Message to the contact
- WhatsApp — sends a WhatsApp message at the channel level
- Send Live Chat Message — sends a message via the live chat channel
- GMB Messaging — responds to a Google My Business message thread
- Conversation AI — hands the contact's active conversation to Conversation AI for AI-managed replies
- Facebook Interactive Messenger — responds to Facebook comments on a post
- Instagram Interactive Messenger — responds to Instagram comments on a post
- Reply in Comments — replies to comments on Facebook or Instagram posts
- Send Slack Message — sends a message to a Slack channel or user (requires Slack integration)

---

**Pipeline**
- Create/Update Opportunity — creates a new opportunity in a pipeline or updates an existing one (stage, value, owner)
- Move Opportunity — moves the opportunity to a specific stage (pipeline name + exact stage name required)
- Remove Opportunity — removes the opportunity from one or all pipelines

---

**AI — Premium Actions** *(each execution incurs an additional charge)*
- AI Translate — translates a text input from one language to another. Configure: From Language, To Language, Input Text (supports merge tags). Use when messaging contacts in their preferred language.
- AI Summarize — generates a condensed summary of a long text. Configure: Max Length (e.g., "3 sentences", "100 words"), Input Text. Use to summarise call transcripts, notes, or form responses before storing or forwarding.
- AI Intent Detection — analyses the sentiment and intent of a text input. Returns a classification of what the contact is trying to communicate. Feed output into If/Else or AI Decision Maker to route accordingly.
- AI Decision Maker — routes the contact into one of several named branches based on AI evaluation of contact data. Configure: Instructions (plain-language criteria with merge tags), Additional Context (business background), and Branches (each with a name and description). Always include a Default Branch. Use when routing logic is better expressed in plain language than hard If/Else conditions.
- AI Prompt (GPT-3 Powered) — generates an AI response based on a custom prompt. Use for dynamic content generation, personalised message drafting, or data enrichment.

---

**Appointments**
- Update Appointment Status — updates an appointment's status: rescheduled, no-show, completed, cancelled
- Generate One Time Booking Link — generates a single-use booking link to send via SMS or email; prevents the same link being used for multiple bookings

---

**Opportunities**
- Create/Update Opportunity — creates a new opportunity in a pipeline or updates an existing one (stage, value, owner)
- Remove Opportunity — removes the opportunity from one or all pipelines

---

**Payments**
- Stripe One-Time Charge — charges the contact a one-time fee via Stripe using their stored Stripe Customer ID
- Send Invoice — sends a GHL invoice to the contact
- Send Documents and Contracts — sends a document or contract from a saved template to the contact for signing

---

**Marketing**
- Add to Google Analytics — sends contact event data to Google Analytics
- Add to Google AdWords — adds the contact to a Google AdWords audience
- Add to Custom Audience (Facebook) — adds the contact to a Facebook custom audience for ad targeting
- Remove from Custom Audience (Facebook) — removes the contact from a Facebook custom audience
- Facebook Conversion API — sends conversion event data to Facebook for improved ad attribution

---

**Affiliate**
- Add to Affiliate Manager — creates a new affiliate record in the affiliate manager
- Update Affiliate — updates existing affiliate details
- Add/Remove from Affiliate Campaign — adds or removes an affiliate from a specific campaign

---

**Courses**
- Course Grant Offer — grants access to a course offer for the contact
- Course Revoke Offer — revokes access to a course offer

---

**IVR (Interactive Voice Response)**
- Gather Input on Call — collects keypad or voice input from a caller to determine their next IVR path
- Play Message — plays a pre-recorded or text-to-speech message during the IVR call
- Connect to Call — forwards the call to a specific user or phone number
- End Call — terminates the call
- Record Voicemail — records a voicemail message from the caller

---

**Communities**
- Grant Group Access — grants a contact access to a specific community group
- Revoke Group Access — removes a contact's access to a community group

---

**Send Data**
- Webhook / Custom Webhook — sends data from GHL to an external URL (Zapier, Make, custom endpoint). Use `{{custom_values.*}}` for endpoint URLs — never hardcode.
- Google Sheets — reads from or writes to a Google Sheets spreadsheet (requires Google integration); useful for reporting and data exports

---

**Internal Tools / Flow Control**
- If / Else — branches the workflow on conditions: tag, custom field value, pipeline stage, appointment status, or contact field. One true + one false branch — chain blocks for more than two paths.
- Wait — pauses for a fixed duration (hours/days) or until a specific date/time
- Wait Until — pauses until a condition is met; always set a timeout to prevent contacts getting permanently stuck
- Goal Event — moves a contact directly to a target step if a condition is met, skipping steps in between; optimises journey paths
- Split — A/B split test within the workflow; divides contacts between two paths for comparison
- Go To — redirects to another step in the same workflow or into a different workflow entirely
- Remove from Workflow — removes the contact from this or another active workflow
- Drip Mode — processes contacts through the workflow in controlled batch sizes to protect deliverability rates
- Arrays — handles multiple values as a single unit; supports sorting, searching, and iterating over data collections
- Text Formatter — transforms text: capitalise, trim, replace, extract, reformat dates, etc.
- Custom Code — executes a custom JavaScript block for advanced data processing or logic not available through standard actions
- Update Custom Value — updates a sub-account-level custom value during workflow execution

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
