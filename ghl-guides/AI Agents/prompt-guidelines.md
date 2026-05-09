# GHL Guide — AI Prompt Writing Guidelines

> This guide applies whenever writing a system prompt for any GHL AI agent — Conversation AI or Voice AI. Follow these rules every time.

---

## The Three Elements of Every Prompt

Every prompt must contain all three elements. Missing one produces a weak, unpredictable agent.

---

### 1. Role — Who the Agent Is and How It Behaves

Define the agent's identity, persona, and interaction style. This steers the AI toward coherent, consistent responses.

**What to include:**
- Who the agent works for and what its primary goal is
- Whether it should behave like a human or identify as AI
- Tone, language style, and demeanor
- How to address the contact (use `{{contact.first_name}}` — first name only, at start and end of conversation)
- How to acknowledge user input (vary affirmations — don't repeat the user's words back every time)

**Worse:**
```
"You are a receptionist for {{custom_values.business_name}}, help customers book appointments."
```

**Better:**
```
- You work for {{custom_values.business_name}}. Your goal is to assist patients, answer their questions, 
  and help them book an appointment when they're ready.
- Always maintain the persona of a warm human assistant. Do not disclose, suggest, or hint at being 
  an AI unless directly asked.
- Use conversational language and phrases like "Got it," "Of course," or "Absolutely" instead of 
  formal phrases like "I apologize" or "I understand your concern."
- Acknowledge the user's input once at the start. After that, use varied transitions without 
  repeating their exact words.
- Use {{contact.first_name}} only at the beginning and end of the conversation.
```

---

### 2. Task — What the Agent Must Do

Define the specific goal and the step-by-step flow for achieving it. Vague task descriptions cause hallucination and off-track responses.

**What to include:**
- The exact sequence of steps or questions the agent should follow (the "script flow")
- What to do if the contact responds positively at each step
- What to do if the contact responds negatively or is not interested
- When and how to trigger a booking, collect information, or escalate
- Conditions that must be met before moving to the next step

**Worse:**
```
"Ask patients questions and help them book if they're interested."
```

**Better:**
```
Script Flow:
- Start by asking: "What brings you in today — is this a routine check-up or do you have a 
  specific concern?"
- If they have an active concern, acknowledge it warmly and ask: "Have you been seen here before, 
  or would this be your first visit with us?"
- Once you have their reason and new/existing patient status, offer to book: "I can get you 
  scheduled — do you have a preferred day or time that works best?"
- Before booking, confirm you have their name and phone number on file.
- Once booked, confirm the appointment details and let them know what to expect.
- If they're not ready to book, offer to send them information and end warmly.
```

---

### 3. Guidelines — The Guardrails

Rules that constrain behavior and prevent unwanted responses. These protect the business from the agent going off-script.

**What to include:**
- Response length and format rules
- Questions the agent must never answer (medical advice, pricing commitments, legal questions)
- What to do when the agent doesn't know something
- Escalation rules — when to hand off to a human
- What the agent must never claim or promise

**Worse:**
```
"Reply briefly. Don't give medical advice."
```

**Better:**
```
- Keep responses short — no more than 2–3 sentences per reply.
- Always wait for the user's response before asking the next question.
- Never give clinical advice, diagnose conditions, or comment on treatment outcomes.
- Never confirm or quote specific prices — say: "The team will go over all costs with you at 
  your visit."
- If someone asks if you are an AI, be honest. Say: "I'm a virtual assistant for 
  {{custom_values.business_name}} — but I'm here to help just the same."
- If a patient describes a dental emergency, stop the script flow and immediately say: 
  "That sounds urgent — let me connect you with our team right away." Then trigger the 
  emergency escalation action.
- If you genuinely don't know the answer to something, say: "That's a great question — let me 
  have someone from our team follow up with you on that."
```

---

## Best Practices

### Repetition

If a rule is important, say it more than once in different parts of the prompt. Repetition reinforces the behavior.

Example — if the agent must follow a script before booking, reference the script in both Role and Guidelines:

In Role:
```
"Your goal is to qualify the patient by asking the questions in the Script Flow before offering to book."
```

In Guidelines:
```
"Only offer to book an appointment after the patient has responded to all Script Flow questions."
```

---

### Examples / Illustrations

When a behavior is hard to describe in words, show it with examples. This is especially useful for tone and phrasing.

**Format:**

```
EXAMPLES — WHAT TO SAY AND WHAT NOT TO SAY:

Avoid: "I apologize for the confusion."
Use:   "Sorry about that — let me clarify."

Avoid: "I don't have information about that."
Use:   "That's something our team would be better placed to answer — want me to have someone reach out?"

Avoid: "I understand your frustration."
Use:   "That makes total sense — I'd feel the same way."
```

---

### Static Business Information

You can add business context directly in the prompt so the agent always has it available.

**Rules:**
- Keep static context under 100–200 words
- If context is too long, it crowds out the instructions and the agent loses focus
- Use delimiters to separate it from instructions (see below)
- Better to put detailed information in the Knowledge Base — use the prompt for the most essential facts only

**Example:**
```
# Business Context:
<context>
{{custom_values.business_name}} is a dental practice located at {{custom_values.business_address}}.
We offer general dentistry, cosmetic treatments, and emergency dental care.
Our hours are {{custom_values.weekday_hours}} Monday–Friday and {{custom_values.weekend_hours}} 
on weekends. New patients are always welcome.
</context>
```

---

## Delimiters

Use delimiters to visually separate sections of the prompt and emphasize important content.

| Purpose | Use |
|---------|-----|
| Section headings | `#` |
| Emphasize a block | `>` |
| Wrap a block of content | `<tag>` / `</tag>` or `"""..."""` |

**Example — wrapping an offer or key info block:**
```
# Offer:
<offer>
New patients receive a complimentary consultation and full X-ray set on their first visit.
This offer is available for a limited time — mention it when you confirm the booking.
</offer>
```

**Example — wrapping the script flow:**
```
# Script Flow:
<script>
Step 1: Ask why they're contacting us today.
Step 2: Ask new or existing patient.
Step 3: Offer booking once reason and status confirmed.
</script>
```

---

## Conversation Context

Open the prompt by telling the agent why the contact is reaching out. This helps the agent understand the situation before it receives the first message.

**Worse:**
```
"You are a customer support agent."
```

**Better:**
```
"A patient is reaching out because they want to book an appointment or have a question about 
our services. Your role is to greet them warmly, understand what they need, and either answer 
their question or guide them to book."
```

For outbound Voice AI, the context is always clear — set the scene for the call:
```
"You are calling {{contact.first_name}} because they are due for their recall hygiene appointment 
and have not rebooked yet. Your goal is to get them to schedule their next visit."
```

---

## Tone & Writing Style Reference

Choose tone and style based on the business type and the context of the conversation.

**Writing styles:** Conversational, Informative, Persuasive, Instructive, Descriptive

**Tones:** Warm, Friendly, Empathetic, Professional, Confident, Calm, Sympathetic

For most healthcare and service businesses: **Warm + Empathetic + Professional** is the default.

For outbound recall/reactivation: **Friendly + Confident** — the agent is doing a favour, not being pushy.

For emergency handling: **Calm + Empathetic** — the agent must not escalate the patient's anxiety.

---

## Prompt Structure Template

Use this as the starting point for any agent prompt:

```
# Role:
[Who the agent is, who it works for, persona, tone, how it addresses the contact]

# Conversation Context:
[Why is the contact reaching out / why is the agent calling — set the scene]

# Business Context:
<context>
[Essential business info — name, location, hours, key services — keep under 150 words]
</context>

# Task — Script Flow:
<script>
[Step-by-step instructions for the conversation — what to ask, when, what to do on yes/no]
</script>

# Guidelines:
[Guardrails — response length, what to never say, escalation rules, unknowns handling]

# Examples:
[Concrete do/don't examples for tone, phrasing, or edge case responses]
```

---

## Rules AI Must Follow When Writing Any Agent Prompt

1. Every prompt must have all three elements: Role, Task, Guidelines
2. Never hardcode business name, address, phone, hours, or URLs — always use `{{custom_values.*}}`
3. Never hardcode contact name — always use `{{contact.first_name}}`
4. Always include an escalation rule for situations the agent cannot handle
5. Always include a rule for when the agent doesn't know the answer
6. Always include what the agent must NEVER do — specific, not generic
7. Use delimiters for any block of information that is separate from instructions
8. Keep static business context under 150 words in the prompt — put detailed info in the KB
9. If behavior is hard to describe, use examples
10. Repeat critical rules in both Role and Guidelines — do not assume once is enough
