# GHL Guide — AI, Live Chat & Engagement Score in Conversations

---

## AI Response Info

View and edit the components behind AI-generated messages directly inside a conversation.

**Where:** Conversations → open any conversation with an AI message → click the AI icon on the message

---

### What You Can See and Edit

| Component | What it is | Can you edit? |
|-----------|-----------|--------------|
| Response | The actual AI message sent | Yes — affects future responses only, not already-delivered messages |
| Prompt | Instructions the AI followed | Yes — edit directly in the sidebar |
| Intent | Purpose of the response | Edit via Conversation AI settings (not inline) |
| Sources | Knowledge chunks and FAQs used from knowledge base or URLs | Yes — changes affect all future AI responses |

**Edited entries show an "Edited" label.** Changes cannot be undone — re-edit manually to revert.

---

## Live Chat

Real-time website visitor chat that routes directly into Conversations alongside SMS and email.

**Where to set up:** Sites → Chat Widget → + New Widget → set type to Live Chat

---

### How It Works

1. Visitor initiates chat via the widget on your website
2. Message appears instantly in Conversations
3. Team member responds in real time
4. If no response within configured inactivity timeout → system collects visitor contact info for follow-up

---

### Setup Steps

1. Sites → Chat Widget → create new widget
2. Set type to **Live Chat** (not SMS/Email mode)
3. Customize: intro message, agent avatar, branding, timeout settings
4. Install: embed code in website footer/body OR use WordPress LeadConnector Plugin

---

### Filtering Live Chat

In Conversations → Filter by Last Message Channel → Live Chat
Shows only live chat messages, separate from SMS and email.

---

### Limitations

- Requires proper Chat Widget installation
- Only works when widget type is set to Live Chat
- Response speed depends on team availability

---

## Contact Engagement Score

A numeric score that tracks how actively a contact interacts with your business. Higher score = more engaged contact. Use to prioritize follow-up and filter smart lists.

**Where to view:** Contact profile page OR Conversations right panel during active messaging

**Where to configure:** Settings → Manage Scoring

---

### What Increases the Score

- Email opens
- Email link clicks
- Form submissions
- Trigger link clicks
- Contact replies
- Appointment bookings
- Survey submissions
- Payments received
- Order placements

### What Decreases the Score

- Email bounces
- Email unsubscribes
- Appointment cancellations

### What Adjusts the Score

- Custom field updates
- Tag additions or removals
- Appointment status changes

---

### Setup

1. Settings → Manage Scoring
2. Create rules — assign point values to specific behaviors
3. Use **Draft Mode** to test rules before activating
4. Switch to **Publish Mode** to apply rules to all contacts
5. Rules apply globally to all contacts in the sub-account

**Limitation:** Scores do not automatically decay for inactive contacts. Build a workflow to subtract points for inactivity if needed.

---

### Using Engagement Score in Workflows and Smart Lists

**Workflow trigger:** Contact Engagement Score
- Filter: Score Between / Equals / Greater Than / Less Than [value]
- Use to fire automations when a contact reaches a threshold (e.g., score > 50 → assign to sales rep)

**Smart List filter:** Numeric filter → Engagement Score → Greater Than [value]
- Build a list of highly engaged contacts for priority outreach
