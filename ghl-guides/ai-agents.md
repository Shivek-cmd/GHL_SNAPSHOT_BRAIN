# GHL Guide — AI Agents
## Knowledge Bases · Conversation AI · Voice AI

---

## Knowledge Bases

**What they are:** Structured information sources that AI agents draw from when answering questions. The AI reads the knowledge base at runtime to answer FAQs, describe services, explain policies, and handle objections — without hallucinating details the knowledge base doesn't contain.

**Where in GHL:** Settings → Knowledge Base → + New

---

### Knowledge Base Content Types

Each KB can contain multiple content types mixed together:

**FAQ**
- Question and answer pairs
- Best for: specific questions the AI is frequently asked
- Keep answers concise (1–3 sentences) — the AI reads the full answer, so long answers increase response time
- Can have unlimited FAQ entries per KB

**Rich Text**
- Formatted text content — headings, bullet points, paragraphs
- Best for: service descriptions, policies, about-the-business content, hours, location
- Maximum 5 Rich Text sections per KB

**Tables**
- Structured data with rows and columns
- Best for: pricing tables, service comparison, staff directory, schedule grids

**Web Crawler**
- GHL crawls a URL and imports the content
- Best for: pulling in an existing FAQ page, services page, or about page from a website
- Maximum 50 URLs per crawl per KB
- Crawled content is a snapshot — if the website changes, the KB does not auto-update; re-crawl to refresh

**File Upload**
- Upload a document (PDF, Word, etc.) and the AI extracts content from it
- Best for: brochures, treatment guides, policy documents
- Supported formats vary by GHL version — check current documentation

---

### Knowledge Base Limits

**Conversation AI:** Maximum 4 Knowledge Bases attached per agent

**Voice AI:** Maximum 1 Knowledge Base attached per agent

**What this means when designing:**
- A Conversation AI agent with broad coverage (FAQs + services + policies + booking info) may need all 4 KB slots
- A Voice AI agent must be focused — its one KB should contain only what's needed for phone calls (keep it tight)
- There is one Voice AI agent — its single KB must cover both inbound and outbound call scenarios

---

### Building a Knowledge Base

1. Settings → Knowledge Base → + New
2. Name it — use naming convention `KB-##: Name`
3. Add content sections using the content types above
4. Review: the AI will answer based on what's in the KB — if something isn't in the KB, the AI should say it doesn't know rather than guess. Keep content accurate and current.
5. Attach to AI agent during agent configuration

---

### What Must Exist Before Building Knowledge Bases

- Business information (name, hours, address, phone) finalized — these go into KB content
- Services list confirmed — service descriptions go into KB
- FAQs drafted and reviewed — accuracy matters here; wrong AI answers damage trust

---

## Conversation AI

**What it is:** A text-based AI chat agent that handles conversations in GHL's inbox channels — web chat widget, SMS, Facebook Messenger, Instagram DM, WhatsApp. One agent configuration covers all connected channels.

**Where in GHL:** Settings → Conversation AI

---

### How to Configure Conversation AI

1. Settings → Conversation AI
2. Agent Name — what the AI calls itself in conversation
3. **Bot Persona / System Prompt:** The full written prompt for this agent. Follow `prompt-guidelines.md` when writing this — every prompt must have Role, Task (Script Flow), and Guidelines sections. Use `{{custom_values.*}}` and `{{contact.first_name}}` throughout — never hardcode names, numbers, or URLs.
4. **Knowledge Bases:** Attach up to 4 KBs. Each KB can have trigger instructions — a description of when the agent should specifically consult that KB.
5. **Actions:** Configure what the agent can do actively during a conversation:
   - Book Appointment — select calendar, specify booking conditions
   - Collect Info — capture contact fields during conversation
   - Update Contact — write data to custom fields
   - Trigger Workflow — fire a specific workflow when a condition is met
   - Handoff to Human — end AI mode and route to a live agent in the inbox
6. **Max Actions:** GHL limits to 8 actions per Conversation AI agent. If more are needed, design the agent to trigger workflows that handle the complexity.
7. **Response Settings:**
   - Auto-response delay — add a small delay (1–2 seconds) to feel less robotic
   - Working hours — AI can be active 24/7 or only during specific hours
   - AI active on channels — select which inbox channels the AI monitors

---

### Conversation AI Behavior Notes

**The AI reads the KB and the conversation history** — it does not access GHL contact fields directly unless you configure a "Collect Info" or "Update Contact" action that explicitly bridges that data.

**Handoff to human:** Configure a clear escalation trigger phrase or condition. Once handed off, the AI stops responding — it will not re-engage unless reactivated manually or via a workflow.

**Test requirement:** Before going live, run at least 10 test conversations covering:
- Common FAQ questions
- Booking request
- Edge case: question the KB doesn't answer
- Escalation trigger
- Each channel the AI is active on

---

### What Must Exist Before Configuring Conversation AI

- All Knowledge Bases built and populated
- All calendars the agent will book into
- All workflows the agent might trigger
- Chat widget configured (if widget is an entry point) — connect to Conversation AI after

---

## Voice AI Agent

**What it is:** A single AI phone agent that handles both inbound and outbound calls. There is one Voice AI agent per sub-account. Its welcome message has two distinct fields — one for inbound calls (when someone calls in) and one for outbound calls (when the system dials out). Everything else — KB, instructions, actions, voice settings — is configured once and applies to both directions.

**Where in GHL:** Settings → Voice AI

---

### How to Configure the Voice AI Agent

1. Settings → Voice AI
2. **Agent Name** — the name the agent uses to identify itself on calls
3. **Welcome Message — Inbound:** The first thing the agent says when an incoming call is answered. Write as natural spoken language — it will be spoken aloud by TTS. Example: "Thank you for calling {{custom_values.business_name}}, this is [agent name] — how can I help you today?"
4. **Welcome Message — Outbound:** The opening line when the agent dials out to a contact. Must identify the business and the reason for calling. Example: "Hi, this is [agent name] from {{custom_values.business_name}} — I'm reaching out about your upcoming hygiene appointment..."
5. **Knowledge Base:** Attach exactly 1 KB. This is the agent's only information source. Keep it focused — the KB should cover everything the agent needs for both inbound questions and outbound conversations.
6. **Agent Instructions / System Prompt:** The full written prompt for this agent. Follow `prompt-guidelines.md` when writing this — the prompt must cover Role, Conversation Context (set the scene for both inbound and outbound scenarios), Task/Script Flow, and Guidelines. Use `{{custom_values.*}}` and `{{contact.first_name}}` throughout — never hardcode names, numbers, or URLs.
7. **Actions:** Maximum 8 actions total — shared across both inbound and outbound use. Common actions:
   - Book Appointment — select calendar
   - Collect Contact Info — capture name, phone, reason for call
   - Transfer Call — forward to a staff number (use `{{custom_values.main_phone}}`, never hardcode)
   - Take Message — log a note on the contact record
   - Add Tag — tag based on call outcome (e.g., `recall-booked`, `not-interested`)
   - Update Contact Field — write call outcome to a custom field
   - Trigger Workflow — fire a workflow during or after the call
   - Emergency Escalation — transfer + trigger emergency workflow
8. **Voice Settings:**
   - Voice — select TTS voice
   - Speed and pitch (if available)
9. **Post-Call Settings:**
   - Call summary — GHL auto-generates a summary on the contact record after each call
   - Follow-up workflow — fire a workflow when the call ends

**Outbound calls are triggered by a workflow** — they do not fire automatically. A workflow action "Outbound Call" specifies this Voice AI agent. The outbound welcome message fires at the start of that call.

---

### Voice AI — Technical Constraints

- 1 KB maximum — one KB covers both inbound and outbound, so design it to be broadly useful
- 8 actions maximum — shared across all call scenarios; if more are needed, use "Trigger Workflow" to hand off complexity
- Voice AI only processes speech — no links, no forms, no visual content during the call
- Transfer action forwards to a real phone number — must be in a custom value, never hardcoded
- The agent cannot access real-time data (live wait times, staff schedules) — it books based on calendar availability exposed to GHL
- Call recordings stored in GHL — verify HIPAA/compliance requirements before enabling if healthcare data is discussed
- Outbound AI calls are subject to TCPA (US) and equivalent laws — explicit prior consent required; include an opt-out mechanism in the agent instructions

---

### What Must Exist Before Configuring Voice AI

- Knowledge Base built and populated
- All calendars the agent will book into
- All workflows triggered by call outcomes
- Phone number configured in the sub-account (Settings → Phone Numbers)
- Custom values for business name, phone, and any script variables

---

## Cross-Agent Rules

**Conversation AI and Voice AI are separate systems** — they do not share configuration, KBs, or memory. A contact who chats with the Conversation AI and then calls will get the Voice AI with no context of the chat conversation unless you build a workflow that updates a custom field with conversation context before the call.

**Handoff gaps:** When AI hands off to a human (or ends), the conversation thread in GHL Conversations is available for human review. Ensure staff are trained to check the AI conversation history before responding so they don't ask questions the AI already answered.

**AI should never:**
- Confirm specific pricing (unless the practice has fixed prices and the owner has approved AI quoting)
- Give clinical or medical advice
- Make guarantees about outcomes
- Override a human decision that was made earlier in the contact's history
- Claim to be a human if directly asked

Always include explicit "never do" instructions in every agent's system prompt.
