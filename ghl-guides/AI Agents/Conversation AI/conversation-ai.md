# GHL Guide — Conversation AI

**What it is:** An advanced AI communication system that automates customer interactions across multiple inbox channels — SMS, Email, Facebook Messenger, Instagram DM, Web Chat, Live Chat. Uses conversation history reliably and maintains context across replies. Supports multiple bots per sub-account, each configurable for different purposes and channels.

**Where in GHL:** Settings → Conversation AI (older UI) | AI Agents → Conversation AI (newer UI)

---

## Bot Modes

Every bot runs in one of three modes:

| Mode | Behavior |
|------|----------|
| **Off** | Bot inactive. Bot training and trial still work — use this to build and test before going live. |
| **Suggestive** | Bot generates a suggested reply inside the message composer. A human reviews, edits if needed, and sends manually. |
| **Auto-Pilot** | Bot responds automatically on behalf of the business with no human review. |

**Guided Form (Form-Based Bots)**
- Automatically varies question phrasing to avoid repetition
- Adjusts tone based on prior user inputs
- Gently refocuses off-topic replies to keep the flow on track
- If Initial Message is configured: bot sends it as a standalone welcome, then starts the form flow on the contact's next reply
- If Initial Message is not configured: flow starts immediately on the first message
- Additional Instructions field supports up to 2,000 characters

---

## Supported Channels

- SMS
- Facebook Messenger
- Instagram DM
- Web Chat (SMS Chat)
- Live Chat
- Email

Configure which channels a bot communicates through: Settings → Conversation AI → Supported Channels dropdown.

---

## Creating a Bot

1. Settings → Conversation AI → **Create Bot**
2. **Select a Prompt Template** (affects only the Prompt section — all content is fully editable after creation):
   - **General Q&A Template** — for customer support and general inquiries
   - **Appointment Booking Template** — for scheduling and managing appointments
3. **Set Bot Status** — Off, Suggestive, or Auto-Pilot
4. **Assign Channels** — select all channels this bot should communicate on
5. **Set as Primary** (optional) — only one bot can be primary at a time

> Selecting a template only pre-populates the Prompt fields. Everything else is configured manually.

---

## Primary vs Non-Primary Bots

### Primary Bot

- Handles all inbound conversations NOT already assigned to another bot from within a workflow
- Acts as the default responder across all assigned channels
- Only one primary bot at a time — can be changed at any time without affecting other bot configurations
- Must have all relevant communication channels assigned; missing channels = bot cannot respond on those platforms

### Non-Primary Bots

- Respond only within workflows they are assigned to — not general inbound
- Channel assignments must match the channels used in the workflow
- Ideal for specialized tasks: appointment booking, lead nurture, follow-up sequences
- Multiple non-primary bots can be assigned to a single workflow (each for different tasks or channels)
- Only one bot can be active in a conversation at any given moment — bots hand off sequentially

**How to assign Primary status:**
Settings → Conversation AI → select bot → click **Set as Primary** → Save

**Non-primary channel matching rule:**
If a workflow includes Facebook and SMS steps, the non-primary bot assigned must have both Facebook and SMS as assigned channels — or use separate bots per channel.

---

## Bot Goals (Prompt Configuration)

Bot Goals define the bot's personality, intent, and instructions. Located in the **Bot Goals** tab inside each bot.

### Prompt

Combines personality, intent, and additional instructions into the bot's core behavior. Follow `prompt-guidelines.md` when writing — every prompt must have Role, Task (Script Flow), and Guidelines. Use `{{custom_values.*}}` and `{{contact.first_name}}` throughout — never hardcode names, numbers, or URLs.

> Do not include details about calendar slot availability in appointment booking prompts — this causes hallucinations.

### Personality

Sets the tone of the bot's responses. Examples:
- **Friendly** — casual and approachable
- **Professional** — business-like and formal
- **Formal** — reserved and highly structured

### Intent

Defines the bot's primary objective. Examples:
- **Resolving Queries** — answer customer questions
- **Generating Leads** — guide conversations toward lead generation and conversions

### Additional Information

Provide specific instructions or details to customize bot responses beyond the template.

---

## Appointment Booking Actions

These actions automate scheduling tasks independently of the Appointment Booking prompt template. Configure after selecting a calendar.

| Action | What It Does |
|--------|-------------|
| **Picking a Calendar** | Select the calendar the bot books into — required first step |
| **Send Booking Link** | Bot sends a direct booking link instead of showing available slots |
| **Pause After Booking** | Bot stops responding after an appointment is successfully booked |
| **Transfer to Employee / Bot** | Hands off conversation to another AI bot seamlessly — the new bot continues without interruption |
| **Trigger Workflow After Booking** | Fires a workflow once appointment is booked (send confirmations, reminders, internal notifications) |

> The workflow must be created before you can connect it here.

---

## Bot Training

Two methods for training the bot — both free of cost.

### Web Crawler

Pulls content from online sources for context-aware responses. Can be configured to crawl:
- Specific URLs
- Directories
- Entire domains
- Google Docs

Crawled content is a snapshot — if the website changes, the KB does not auto-update. Re-crawl to refresh.

### Custom Bot Responses (FAQs)

Specify exact answers to frequently asked questions. When a user asks something that matches or is similar to an FAQ, the bot returns the exact configured response.

Training location: Bot Training tab inside each bot.

---

## Advanced Settings

### Business Name

Auto-fetched from account settings — no manual input needed. Ensures consistent branding in all conversations.

### Wait Time Before Responding

Adds a delay before the bot replies to create a more natural conversational flow. Recommended: 5–20 seconds. Consider industry norms and customer expectations.

### Maximum Message Limit

Sets a cap on the number of bot messages per interaction. Once the limit is reached, the bot stops responding until reset.

**Resetting the limit:**
- Manually via the contact record
- Via workflow action: **Update Conversation AI Bot and Status**

### Send Bot to Sleep

Temporarily disables the bot. Use when:
- A live agent is actively responding
- A workflow is executing a process that requires uninterrupted communication

> Guided Form enhancements (dynamic phrasing, tone adjustment, distraction handling) work automatically — no changes to timing or limits required.

---

## Conversation Summary and Transcript

Captures what happened during a Conversation AI interaction after a set inactivity period. Off by default — must be enabled per bot.

**Where to enable:** AI Agents → Conversation AI → select bot → Bot Goals tab → Enable Conversation Summary

**Two output types:**
- **Summary** — condensed overview of key points
- **Transcript** — full message history for recordkeeping, internal follow-up, or workflow automation

Generated summaries are NOT automatically stored in the CRM unless explicitly sent somewhere.

### Available Settings

| Setting | What It Does |
|---------|-------------|
| **Set Inactivity Time** | How long the conversation must be inactive before a summary generates (e.g., 15 minutes with no messages from contact or bot) |
| **Minimum Messages Required** | Prevents summaries for very short conversations — if message count is below the minimum, no summary generates even after inactivity time |
| **Trigger a Workflow** | Sends the generated summary/transcript into a workflow for saving to notes, CRM fields, or internal logs |
| **Receive Email Notification** | Emails the summary to: All Admins, All Users, Contact's Assigned User, Specific Users, or Custom Email |

### Sending Summary/Transcript to a Workflow

1. Automation → Workflows → Create new workflow (no trigger needed — triggered directly from Conversation AI)
2. Add an action (e.g., Add To Note)
3. Insert merge fields: **Conversation AI → Summary** and/or **Conversation AI → Transcript**
4. Return to bot → Conversation Summary settings → enable **Trigger a workflow** → select the workflow

---

## Auto Follow-Up

Automatically sends outbound messages to contacts who have gone inactive, asked for a follow-up, or stopped responding. Eliminates manual follow-up tasks and complex workflows.

**Where to configure:** AI Agents → Conversation AI → select bot → Bot Goals → Set Up Your Actions → Auto Followup

> Do not trigger follow-ups through a separate workflow — this breaks the follow-up logic.

### Three Follow-Up Scenarios

Each scenario supports up to 5 follow-up sequences. Each sequence has:
- Delay time (hours, days, or minutes)
- AI-generated message or Custom message
- Optional: Trigger a Workflow

| Scenario | When It Fires |
|----------|--------------|
| **Contact Stopped Responding** | Contact goes silent with no reply |
| **Contact Marked as Busy** | Contact indicates they're busy or unavailable |
| **Contact Requested a Follow-Up** | Contact asks to be contacted later (first sequence delay pre-set per contact's request) |

### Follow-Up Settings

**Active Hours (applies to follow-ups only, not main bot conversations):**
- Set specific hours when follow-up messages can send (e.g., 9 AM–6 PM)
- Choose timezone: Contact Timezone or Business Timezone
- If contact timezone is unavailable, system defaults to Business Timezone
- If disabled, follow-ups send regardless of time

**Dynamic Channel Switching:**
- If contact is unresponsive on the current channel, bot switches to another available channel
- Live Chat → SMS (if phone number available)
- Facebook / Instagram / WhatsApp → SMS (if no response within 24 hours)
- Optional — can be disabled

**Language:**
If a contact has a preferred language set, follow-ups are sent in that language automatically — no extra setup required.

### Smart Detection — When Follow-Ups Are Suppressed

Auto Follow-Up cancels a scheduled message if the conversation indicates follow-up is no longer appropriate:
- Contact is disqualified (e.g., out of service area)
- Contact shows disinterest or opts out ("Not interested," "Stop texting me")
- Contact responds with anger or frustration
- Conversation ends with a soft closure that signals completion

All scheduled follow-ups are visible in the **Response Info panel** for full transparency.

---

## Testing the Bot

**Bot Trial** is free and available before going live.

- Chat with the bot with no limitations or cost
- Give feedback on responses:
  - Thumbs Up → improves bot behavior
  - Thumbs Down → automatically creates a new FAQ entry in the training section
- Edit prompts directly during testing via the edit icon next to feedback buttons
- Reset the conversation without refreshing — test changes immediately

**Test requirement before going live:** Run at least 10 conversations covering:
- Common FAQ questions
- Booking request
- Edge case — question the KB doesn't answer
- Escalation trigger
- Each channel the bot is active on

---

## Workflow Integration

Bots can be used inside workflows via the **Conversation AI Action**:
- Customize the entire prompt per workflow step
- Move contacts conditionally based on their replies
- Ask specific questions and branch based on the contact's response

The **Update Conversation AI Bot and Status** workflow action can:
- Reset the message limit
- Reactivate a bot that's in sleep mode
- Switch which bot handles the conversation

### Trigger a Workflow (Bot Goals Action)

The **Trigger a Workflow** action lets a bot fire a published workflow when a specific condition is met during a conversation — without requiring the condition to be hardcoded into the prompt.

**Where to configure:** Bot Goals tab → Set Up Your Actions → Trigger a Workflow

**Fields to configure:**

| Field | What to enter |
|-------|--------------|
| **Action Name** | A label for this action (e.g., "Subscription Workflow", "Appointment Trigger") |
| **Select a published workflow** | Choose from the dropdown — the workflow must be published before it appears here |
| **When to trigger** | Plain-English description of the condition (e.g., "Customer wants to purchase the subscription", "Customer wants to book an appointment") |

The bot reads the trigger condition and activates the workflow when a similar scenario arises in the conversation. Save after configuring each action.

**Important notes:**

- **Write conditions that the prompt naturally leads to** — if the trigger is "Customer wants to book an appointment", structure the prompt so the bot asks "Would you like to book an appointment?" — the condition must arise naturally, not by surprise
- **Duplicate trigger conflicts** — if two actions share the same trigger condition (e.g., "Update Contact Info" and "Trigger Workflow" both fire when DOB is provided), the AI determines which executes based on its own prioritisation; avoid overlapping conditions
- **Either bot or user can satisfy the trigger** — the condition can be met by something the bot says or something the user says; both count
- **Do not duplicate published workflow triggers** — if a workflow is already published with the same trigger in Workflow Automation, do not also connect it here; it will execute twice

> Updating contact fields via a triggered workflow is supported — add an "Update Contact Field" action inside the workflow itself.

---

## Mobile Support

Available from v3.71 or later on HighLevel, LeadConnector. WhiteLabel requires a manual update request.

| Feature | Behavior |
|---------|----------|
| Suggestive Mode | AI suggestions appear for new messages on supported channels — send as-is or edit first |
| Auto-Pilot Mode | Automatically responds to new incoming queries |
| Feedback & Training | Provide feedback on auto-generated responses to train the bot |

---

## Behavior Notes

- The AI reads the KB and conversation history — it does not access GHL contact fields directly unless a Collect Info or Update Contact action explicitly bridges that data
- Handoff to human: once handed off, the AI stops responding and will not re-engage unless reactivated manually or via a workflow — staff should check the AI conversation history before responding
- If renamed standard CRM objects (e.g., Contacts → Clients), Conversation AI displays those names throughout the bot UI
- Only one bot can be active in a conversation at any given moment

---

## What Must Exist Before Configuring Conversation AI

- All Knowledge Bases built and populated
- All calendars the bot will book into
- All workflows the bot might trigger (including post-booking and summary workflows)
- Chat widget configured (if widget is an entry point) — connect to Conversation AI after
- Custom values for business name and any script variables
