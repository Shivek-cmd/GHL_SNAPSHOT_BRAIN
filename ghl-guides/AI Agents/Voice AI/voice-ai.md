# GHL Guide — Voice AI Agent

**What it is:** A single AI phone agent that handles both inbound and outbound calls. There is one Voice AI agent per sub-account. Its welcome message has two distinct fields — one for inbound calls (when someone calls in) and one for outbound calls (when the system dials out). Everything else — KB, instructions, actions, voice settings — is configured once and applies to both directions.

**Where in GHL:** AI Agents → Voice AI | Settings → Voice AI

> **IMPORTANT:** Voice AI only works on accounts using LC Phone or Twilio numbers.

---

## Key Benefits

- **Natural Conversations** — handles natural speech and understands context across the full call
- **Speech Recognition** — accurately transcribes and interprets spoken words in real time
- **Easy Integration** — connects with CRM, calendars, workflows, and external APIs
- **Customizable Responses** — tailor the agent's personality, voice, language, and responses
- **24/7 Availability** — continuous support with no downtime
- **Multi-Language** — supports 52+ languages with 80+ voice options
- **Custom Actions** — triggers real-time webhooks to external systems mid-call

---

## How to Configure the Voice AI Agent

1. AI Agents → Voice AI → Agent List → create or edit an agent
2. **Agent Name** — the name the agent uses to identify itself on calls
3. **Welcome Message — Inbound:** The first thing the agent says when an incoming call is answered. Write as natural spoken language — it will be spoken aloud by TTS. Example: "Thank you for calling {{custom_values.business_name}}, this is [agent name] — how can I help you today?"
4. **Welcome Message — Outbound:** The opening line when the agent dials out to a contact. Must identify the business and the reason for calling. Example: "Hi, this is [agent name] from {{custom_values.business_name}} — I'm reaching out about your upcoming hygiene appointment..."
5. **Knowledge Base:** Attach exactly 1 KB. This is the agent's only information source. Keep it focused — the KB should cover everything the agent needs for both inbound questions and outbound conversations.
6. **Agent Instructions / System Prompt:** The full written prompt for this agent. Follow `prompt-guidelines.md` when writing this — the prompt must cover Role, Conversation Context (set the scene for both inbound and outbound scenarios), Task/Script Flow, and Guidelines. Use `{{custom_values.*}}` and `{{contact.first_name}}` throughout — never hardcode names, numbers, or URLs.
7. **Language & Voice:**
   - Select language from 52+ supported options — greeting auto-translates when language is changed (review and edit the translation before saving)
   - Once language is selected, available voices update automatically
   - 80+ voices available across languages; custom voices can be imported from ElevenLabs
8. **Actions:** Maximum 8 actions total — shared across both inbound and outbound use (see full actions list below)
9. **Voice Settings:**
   - Voice — select TTS voice
   - Speed and pitch (if available)
10. **Post-Call Settings:**
    - Call summary — GHL auto-generates a summary on the contact record after each call
    - Follow-up workflow — fire a workflow when the call ends
    - Translation Service — enable to auto-translate transcripts and summaries into a target language

**Outbound calls are triggered by a workflow** — they do not fire automatically. A workflow action "Outbound Call" specifies this Voice AI agent. The outbound welcome message fires at the start of that call.

---

## Call Handling

### Inbound Calls

- **Call Routing:** Incoming calls to the assigned phone number are automatically handled by the AI agent during working hours
- **After-Hours Handling:** Calls received outside working hours follow the configured settings — forwarded to voicemail, another number, or a fallback workflow
- Multiple agents can be created, each with its own assigned phone number and unique configurations (for different departments or services)

### Outbound Calls

- Triggered only by a workflow action ("Outbound Call") — the agent does not dial out autonomously
- The outbound welcome message fires at the start of each outbound call
- Subject to TCPA (US) and equivalent laws — explicit prior consent required; include an opt-out mechanism in the agent instructions

---

## Actions

Actions are what the agent can do during and after a call. Maximum 8 actions total, shared across all call scenarios. If more complexity is needed, use Trigger Workflow to hand off to automation.

| Action | What It Does |
|--------|-------------|
| **Book Appointment** | Books directly into a selected calendar during the call |
| **Collect Contact Info** | Captures name, phone, email, reason for call — saves to contact record |
| **Update Contact Field** | Writes call outcome or collected data to a custom field |
| **Trigger Workflow** | Fires a workflow during or after the call based on conditions |
| **Transfer Call** | Forwards to a staff number — always use `{{custom_values.main_phone}}`, never hardcode |
| **Agent Transfer** | Transfers the conversation to another configured AI agent |
| **End Call** | Concludes the call politely when conditions are met |
| **Send SMS** | Dispatches a text message with relevant information or follow-ups |
| **Take Message** | Logs a note on the contact record |
| **Add Tag** | Tags contact based on call outcome (e.g., `recall-booked`, `not-interested`) |
| **Emergency Escalation** | Transfer + trigger emergency workflow simultaneously |
| **Custom Action (Webhook)** | Triggers a real-time POST webhook to an external API mid-call (see Custom Actions below) |
| **Add MCP** *(beta)* | Connects to an MCP server during the call |

---

## Custom Actions (Webhook Integration)

Custom Actions allow the Voice AI agent to trigger POST webhook calls to external APIs during a live conversation — mid-call, not after. The agent can retrieve or send data in real time based on what the caller says.

**Use case example:** A caller asks "What's the status of my recent order?" — the agent calls your order management system and retrieves the real-time status without putting the caller on hold.

### Conversation Triggers

Each Custom Action fires based on trigger conditions you define — phrase-based or logic-based. Triggers can be layered with conditions (e.g., "only run if parameter X is present").

Examples:
- When a user says "I want to check my appointment"
- When an email address is mentioned
- When a string of digits (e.g., an order number) is spoken

### Webhook Configuration

Each Custom Action is a POST request that includes:
- Webhook endpoint URL
- Headers (e.g., API keys, tokens)
- Request body with dynamic parameters
- Authentication (Bearer token, Basic Auth, or key in headers)

Only POST requests are supported. GET and other methods are not available for Custom Actions.

### Dynamic Parameter Collection

The agent extracts and labels relevant data from the conversation in real time and maps it to webhook parameters. Supported data types for dynamic parameters:
- Text (String)
- Number (Numeric)
- Email
- Phone Number
- Date

### How to Set Up Custom Actions

1. AI Agents → Voice AI → open the agent
2. Agent Goals tab → switch to **Advanced Mode** (if not already enabled)
3. Go to **Custom Actions** → click **+ New Action**
4. Configure:
   - Name the action
   - Set conversation trigger conditions
   - Enter the webhook URL (POST)
   - Add headers if needed
   - Add authentication details
   - Define dynamic parameters pulled from the conversation
5. Use the **Test Webhook** feature to validate before saving

### Real-Time Testing

The built-in Test Webhook tool lets you simulate a call scenario, pass test data, and view the response from the external system before going live. You can see:
- Full request (headers + body)
- Raw response (200 OK, 404 Not Found, etc.)
- Any misconfigurations to fix before saving

If the webhook fails during a live call, the system logs the failure and fallback behavior can be defined. Multiple Custom Actions can be active in a single call, each triggering independently based on its own conditions.

---

## Multi-Language Support

Voice AI supports 52+ languages. The agent operates only in the configured language — it does not auto-detect caller language.

**Supported languages include:** English, Spanish, French, German, Portuguese, Italian, Dutch, Hindi, Japanese, Polish, Romanian, Turkish, Vietnamese, Swedish, Norwegian, Russian, Indonesian, Greek, Danish, Finnish, Chinese, Korean, and 30+ more. Multilingual voices (English + Spanish) are also available.

> The voice library is continuously growing — more languages and voices are added over time. Custom voices can be imported from ElevenLabs.

### How to Configure Language

1. AI Agents → Voice AI → Agent List → open the agent
2. Use the **Language** dropdown to select the target language
3. The Initial Message (greeting) auto-translates — review and edit it before saving
4. The Voice dropdown updates automatically to show voices available for that language — select the best fit
5. Save and test the agent before deploying

**Best practices:**
- Do not include explicit language instructions in the prompt — the system handles the language automatically
- Always update the greeting message to match the selected language
- Test the agent in the selected language before going live

---

## Translation Service (Post-Call)

Automatically translates AI-generated call transcripts and summaries into a target language after each call. Useful for multilingual teams and global clients.

**Cost:** Consumes 1 additional AI credit per minute of transcribed audio.

### How to Enable

1. AI Agents → Voice AI → create or edit an agent
2. Enable the **Translation Service** toggle
3. Select the target translation language from the dropdown
4. Save the agent — translation applies automatically to all calls handled by that agent from that point forward

The target language can be changed at any time by editing the agent. The original transcript and summary remain available — translation is provided in addition, not as a replacement.

### Where to Access Translations

Translated transcripts and summaries appear in **Dashboard & Logs** (the homepage of the Voice AI agents and inside individual agent settings) after each call completes.

**Post-call delivery:**
- **Notifications** — post-call notification includes translated summary and transcript
- **Automatic Notes** — translated summary is saved to the contact's Notes automatically
- **Workflows** — post-call workflows can use both translated summary and translated transcript as merge fields for follow-ups and internal handoffs

---

## Technical Constraints

## Technical Settings Reference

These settings are configured inside the Voice AI agent under the Settings tabs. Understanding each one lets you tune the agent for any deployment.

### Latency Fix Guide

If callers experience 3–4 second delays between speaking and the agent responding, work through this table in order:

| Layer | Cause | Fix |
|-------|-------|-----|
| **STT** | Accurate transcription model adds ~1–2s per turn | Switch to Fast + use boosted keywords for accuracy |
| **LLM** | Long prompt = more tokens = slower inference | Keep prompt under 900 words |
| **Webhook** | External API cold start or slow processing | Return `200 OK` immediately; process asynchronously |
| **TTS** | Long AI responses = more audio to synthesise | Write shorter sentences in the prompt |
| **GHL** | Wait Before Speaking set too high | Reduce to 0.1s |
| **Response Speed** | Set too low | Increase toward 0.8 |

**Quick wins (highest impact, do first):**
1. Transcription model: Accurate → **Fast**
2. Wait Before Speaking: 0.5s → **0.1s**
3. Response Speed: 0.65 → **0.8**
4. Webhooks: respond immediately, process asynchronously

---

### 1. Call Settings

| Setting | What It Does |
|---------|-------------|
| **Max Call Time** | Hard cap on call length. Set based on your expected call type. |
| **End Call After Silence** | Ends the call gracefully if the caller is silent for this many seconds after all idle reminders have played. |
| **Wait Before Speaking** | How long the agent waits before replying after the caller finishes. 0.1s is near-instant and still sounds natural. 0.5s adds dead air on every single turn. |

**Idle Time Reminders**

| Setting | What It Does |
|---------|-------------|
| **Enable** | Turns on silence reminders |
| **When Reminder Starts** | Seconds of silence before the first reminder fires |
| **How Often They Repeat** | Number of reminders before the agent ends the call |

Configure reminder messages to escalate gently — e.g., first: "Hey, are you still there?", second: "Just checking — did you want to continue?", final: "I'll go ahead and end the call if you're done. Thanks for calling!"

---

### 2. Agent Behaviour

| Setting | What It Does | Guidance |
|---------|-------------|----------|
| **Response Speed** | Controls how fast the LLM generates a response | Higher = faster. Most deployments work well at 0.7–0.8. |
| **Interruption Sensitivity** | How easily the agent stops speaking when the caller talks over it | Mid-range (0.55–0.65) lets callers cut in naturally without triggering on background noise. |
| **LLM Temperature** | Controls how creative/variable the agent's responses are | Low (0.2–0.4) = consistent and predictable. Use for order-taking, booking, any scripted flow. Higher = more varied and conversational. |

**Backchannel** — short affirmations the agent says while the caller speaks ("Got it", "Sure", "Mhm", "Yeah") to signal active listening.

| Setting | What It Does |
|---------|-------------|
| **Enable Backchannel** | Turns on mid-speech affirmations |
| **Backchannel Frequency** | How often affirmations play — 0.4 is natural; above 0.6 starts to feel repetitive |
| **Backchannel Word List** | The pool of words the agent picks from |

---

### 3. Transcription & Speech

**Transcription Model**

| Model | Trade-off |
|-------|-----------|
| **Fast** | Low latency (~0s added). Slightly less accurate on unusual words — compensate with Boosted Keywords. |
| **Accurate** | Higher accuracy on complex or uncommon words. Adds ~1–2 seconds per turn — noticeable on live calls. |

Use **Fast** for real-time phone calls and pair it with Boosted Keywords for any industry-specific vocabulary. Switch to **Accurate** only when accuracy matters more than response speed.

**Vocabulary Specialisation** — sets the speech domain the STT model expects.
- **General** — most business types including international terms, product names, branded words
- **Medical** — healthcare contexts where clinical terminology dominates

**Boosted Keywords** — a list of words the STT model should prioritise recognising. Use for:
- Industry-specific terms the model commonly mishears (food names, product names, brand names, medication names)
- Proper nouns not in standard speech datasets
- Any word that shows up wrong in call transcripts repeatedly

Add each term exactly as it should be recognised. If a word still gets misheard after boosting, also add common phonetic variants as separate entries.

**Pronunciation Dictionary** — tells the TTS engine exactly how to say specific words. Add as word + phonetic pronunciation pairs. Use for:
- Foreign words or names the TTS mispronounces
- Brand names with non-standard pronunciation
- Any word callers react to when the agent says it wrong

---

### 4. Voice Settings

**Noise Cancellation**

| Option | When to use |
|--------|------------|
| **Remove Noise** | Caller in noisy environment (kitchen, car, street) — removes ambient noise without stripping speech |
| **Remove Noise + Background Speech** | Louder environments — more aggressive, test before deploying as it can strip parts of the caller's voice |
| **None** | Quiet, controlled call environments |

**Background Sound** — adds ambient audio to the agent's side of the call. Use **None** for most business deployments — artificial sounds add no value on a professional call.

**Voice Levels**

| Setting | What It Controls | Guidance |
|---------|-----------------|----------|
| **Voice Speed** | How fast the TTS speaks | 1.0 is natural. Let Dynamic Voice Speed handle per-caller adjustment. |
| **Voice Temperature** | How expressive/varied the TTS delivery is | 0.6–0.7 = warm and natural. Above 0.8 can produce uneven delivery. |
| **Voice Volume** | Output volume level | 1.0 is default — adjust only if testers consistently report issues. |

**Toggles**

| Toggle | What It Does | Recommendation |
|--------|-------------|----------------|
| **Speech Normalization** | Converts symbols to spoken form — `$38.95` → "thirty-eight ninety-five", `7:15 PM` → "seven fifteen PM" | **ON** whenever the agent speaks prices, times, dates, or formatted data |
| **Dynamic Voice Speed** | Automatically adjusts speaking pace to match the caller's own pace | **ON** for any consumer-facing deployment — makes the agent feel significantly more human |

---

## Technical Constraints

- Requires LC Phone or Twilio numbers — does not work with other number providers
- 1 KB maximum — design the KB to cover both inbound and outbound scenarios
- 8 actions maximum — shared across all call scenarios; use Trigger Workflow to handle additional complexity
- Voice AI only processes speech — no links, no forms, no visual content during the call
- Transfer action forwards to a real phone number — must always be in a custom value, never hardcoded
- The agent cannot access real-time data (live wait times, staff schedules) — books based on calendar availability exposed to GHL
- Call recordings stored in GHL — verify HIPAA/compliance requirements before enabling if healthcare or sensitive data is discussed
- Custom Actions: only POST webhooks supported; login-gated or private data cannot be accessed
- Agent cannot access GHL contact fields directly during a call unless a Custom Action or workflow bridges that data explicitly

---

## What Must Exist Before Configuring Voice AI

- LC Phone or Twilio phone number configured in the sub-account (Settings → Phone Numbers)
- Knowledge Base built and populated
- All calendars the agent will book into
- All workflows triggered by call outcomes (including post-call follow-up workflows)
- Custom values for business name, phone, and any script variables
- External API documentation ready if setting up Custom Actions (webhook URL, auth details, parameters)

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
