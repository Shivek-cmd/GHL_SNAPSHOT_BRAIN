# GHL Guide — Communications
## Email Templates · SMS Templates · WhatsApp Templates

---

## Core Rule — No Content Inside Workflows

Templates must be created first in their respective template libraries. Workflows then reference the template by ID — they never contain inline message content. This keeps all message content in one place, makes editing fast, and keeps workflows readable.

---

## Email Templates

**What they are:** Reusable email designs stored in GHL's template library. Each template has a subject line and a body. Workflows reference templates by their ID.

**Where in GHL:** Marketing → Emails → Templates → + New

**How to create:**
1. Marketing → Emails → Templates → + New
2. Choose builder type: Drag & Drop (visual) or HTML (code)
3. Write subject line — always use custom values for the business name: `{{custom_values.business_name}}`
4. Build body content
5. Use merge tags for personalization: `{{contact.first_name}}`, `{{custom_values.*}}`, `{{contact.*}}`
6. Save with the naming convention: `ET-01: [Template Name]`

**Merge tags available in email:**
- `{{contact.first_name}}` — contact's first name
- `{{contact.full_name}}` — contact's full name
- `{{contact.email}}` — contact's email address
- `{{contact.phone}}` — contact's phone number
- `{{custom_values.*}}` — any custom value
- `{{contact.*}}` — any custom field (use the field key)
- `{{appointment.start_time}}` — appointment time (available in appointment-triggered workflows)
- `{{appointment.end_time}}` — appointment end time
- Unsubscribe link — required for marketing emails: `{{unsubscribe_link}}`

**Technical constraints:**
- Subject line and preview text both support merge tags
- GHL's drag-and-drop builder does not support all HTML — if precise HTML control is needed, use the HTML editor
- Images must be hosted externally or uploaded to GHL's media library — no inline base64 encoding
- Unsubscribe link is required for any marketing/promotional email — not required for transactional (appointment reminders etc.) but include it as best practice
- Email templates do not have a size limit but keep emails under 100KB total for deliverability

**Email types and when to use each:**
- Transactional — appointment confirmations, reminders, receipts. No unsubscribe required but include it.
- Marketing — promotions, newsletters, campaigns. Unsubscribe link mandatory. Must comply with CAN-SPAM / GDPR.
- Nurture — sequence emails that educate or build relationship. Treat as marketing for compliance.

**Naming convention:** `ET-01`, `ET-02`, etc. Number sequentially. Name describes the purpose clearly.

**Connected to:**
- Workflows (Send Email action — select template from dropdown)
- Automation trigger: Email Opened, Email Link Clicked (enables response-based branching)

---

## SMS Templates

**What they are:** Reusable SMS message bodies. GHL stores these as templates that workflows reference. Unlike email, SMS has strict character limits and regulatory requirements.

**Where in GHL:** Marketing → SMS → Templates → + New (or referenced directly in workflow SMS actions in some GHL versions)

**How to create:**
1. Marketing → SMS → + New Template (path may vary by GHL version)
2. Write the message body — keep under 160 characters if possible
3. Always include opt-out language on first contact: "Reply STOP to opt out"
4. Use merge tags: `{{contact.first_name}}`, `{{custom_values.*}}`
5. Save with naming convention: `ST-01: [Template Name]`

**SMS character limits:**
- 160 characters = 1 SMS segment (standard GSM-7 encoding)
- 153 characters per segment when message is over 160 (multi-part SMS overhead)
- Emoji or special characters switch encoding to UTF-16: 70 chars per segment
- GHL shows character count while editing — watch for merge tag expansion (a merge tag counts as ~30 chars for planning purposes but expands at send time)

**10DLC — US SMS compliance (critical):**
- All US SMS campaigns require 10DLC registration before messages will deliver
- Register: Settings → Phone Numbers → 10DLC → Register Campaign
- Required: Business name, EIN, website, campaign use case (appointment reminders, customer care, etc.)
- Approval time: 1–3 business days
- Without 10DLC, SMS messages will be filtered/blocked by US carriers
- Opt-out handling is mandatory: contacts who reply STOP must be removed from SMS outreach automatically. GHL handles this natively.

**Merge tags in SMS:**
- Same syntax as email: `{{contact.first_name}}`, `{{custom_values.business_name}}`
- Booking links should always be custom values, not hardcoded URLs

**SMS types:**
- Transactional — appointment reminders, confirmations. Lower regulatory burden.
- Marketing/Promotional — campaigns, offers, win-back. Requires explicit opt-in and opt-out mechanism.

**Technical constraints:**
- Links in SMS must be shortened for good deliverability — GHL has a built-in link shortener
- Do not include more than one link per SMS if possible
- Emojis are allowed but count as UTF-16 (70 chars/segment)
- SMS cannot contain HTML
- Phone numbers must be SMS-capable — landlines will fail silently

**Connected to:**
- Workflows (Send SMS action)
- Automation trigger: SMS Reply Received, Keyword Replied (enables response-based branches)

---

## WhatsApp Templates

**What they are:** Pre-approved message templates submitted to Meta for approval. WhatsApp Business API (which GHL uses) requires that outbound messages outside the 24-hour customer service window use approved templates.

**Where in GHL:** Settings → WhatsApp → Message Templates → + Create Template

**How to create:**
1. Settings → WhatsApp → Message Templates → + Create Template
2. Select category:
   - **UTILITY** — appointment reminders, confirmations, order updates. Faster approval. Lower cost.
   - **MARKETING** — promotions, campaigns, win-back. Requires stronger justification. Higher cost.
   - **AUTHENTICATION** — OTP/verification codes (rarely used in snapshots)
3. Write the template — use numbered variables for dynamic content: `{{1}}`, `{{2}}` etc.
4. Add header (optional): text, image, document, or video
5. Add footer (optional): short text, typically opt-out instructions
6. Add buttons (optional): Call to Action (URL or phone), Quick Reply
7. Submit for Meta approval

**Meta approval process:**
- Approval time: 24–72 hours typically, can be longer
- Meta may reject templates that are too promotional in UTILITY category
- Rejections require editing and resubmitting — this resets the approval timer
- Build continues while waiting for approval — mark as pending in the build sequence

**WhatsApp 24-hour rule:**
- When a contact messages the business first, a 24-hour customer service window opens
- During this window, any free-form message can be sent (not just templates)
- Outside this window, only approved templates can be sent outbound
- Appointment reminders and scheduled follow-ups will always use templates since they're sent proactively

**Variable mapping:**
- Template variables `{{1}}`, `{{2}}` are mapped to GHL merge tags when the workflow sends the message
- Example: `{{1}}` → `{{contact.first_name}}`, `{{2}}` → `{{appointment.start_time}}`
- Map these in the workflow action that sends the WhatsApp message

**Technical constraints:**
- Each WhatsApp number (phone number registered with WhatsApp Business API) has a messaging limit that scales with quality rating
- Quality rating drops if contacts block or report messages — do not over-send marketing templates
- WhatsApp requires an active WhatsApp Business API connection in GHL settings — this must be set up at the sub-account level
- Media (images, PDFs) in templates must be hosted at a publicly accessible URL — no local files
- Button URLs in templates can use custom values but the full URL must be valid at approval time

**Naming convention:** `WA-01`, `WA-02`, etc. Template name in Meta must also follow this convention.

**Connected to:**
- Workflows (Send WhatsApp action)
- GHL WhatsApp Conversation inbox (agents can continue the conversation manually after AI or automation initiates)

---

## Cross-Channel Rules

**Opt-out must be respected across all channels:**
- SMS STOP replies → GHL marks contact as SMS unsubscribed automatically
- Email unsubscribes → GHL marks contact as email unsubscribed automatically
- WhatsApp blocks → reported to Meta, quality rating drops; GHL does not auto-update contact status for WhatsApp blocks

**Timing and frequency:**
- Never send the same message across all three channels simultaneously — stagger them
- Appointment reminders typically: Email at booking + Email 24h before + SMS 4h before
- Do not send marketing messages more than once per week unless the contact has explicitly engaged

**Compliance summary:**
- CAN-SPAM (US email) — require unsubscribe, honor within 10 days, no deceptive subjects
- TCPA (US SMS) — require explicit written consent before marketing SMS
- GDPR (EU) — consent must be granular, documented, revocable; data deletion on request
- HIPAA (healthcare US) — patient health information cannot be in email/SMS body; use generic language only
