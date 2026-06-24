# GHL Guide — Snippets & Quick Replies

---

## Snippets

Reusable pre-written message templates for consistent, fast communication across all team members.

**Where in GHL:** Conversations → Snippets icon OR Marketing → Snippets

---

### Creating Snippets

1. Marketing → Snippets → + Add Snippet
2. Select format: **Text** (for SMS/WhatsApp) or **Email**
3. Name it clearly (e.g., "Follow-Up — Missed Appointment")
4. Write the message body — use custom values/placeholders for personalization (e.g., `{{contact.first_name}}`)
5. Preview → Test → Save

**No limit** on number of snippets.

---

### Organizing Snippets

- Create folders to categorize by use case (e.g., Newsletter, Support, Sales)
- Move snippets individually or in bulk to folders
- Search by name
- Filter by type: Text or Email

---

### Using Snippets in Conversations

1. Open a conversation
2. Click the **Snippets icon** at the bottom of the composer
3. Search or browse folders
4. Select → snippet populates in the text box
5. Edit if needed → send

---

### Permissions

Users need **Conversations → View & manage conversation** permission enabled to access snippets.
Configure: Settings → My Staff → select user → Roles & Permissions

---

### Managing Snippets

Three-dot menu on any snippet:
- Edit
- Duplicate
- Delete

---

## Quick Replies (Facebook & Instagram Only)

Predefined single-tap response options shown to contacts in Facebook or Instagram conversations. Contacts tap one to reply instantly.

**Channel support:** Facebook Messenger and Instagram DM only — not available for SMS or Email.

---

### Rules

| Rule | Detail |
|------|--------|
| Max quick replies per message | 13 |
| Max characters per reply | 20 |
| Visibility | Only appear with the most recent message in the thread |
| After selection | Cannot be changed — interaction is final |
| Facebook | Quick replies can coexist with buttons and images |
| Instagram | Choose either buttons OR quick replies per message — not both. No attachments allowed in the same message as quick replies |

---

### How to Set Up

Quick replies are configured inside workflows — not in Conversations directly.

1. Automation → Workflows → create or open workflow
2. Trigger: Facebook Comment on Post OR Instagram Comment on Post (or Customer Reply)
3. Action: **Facebook Interactive Messenger** or **Instagram Interactive Messenger**
4. Reply Type: Reply to Comment via DM (takes conversation private) OR Reply to DM
5. Add Quick Replies: enter up to 13 labels (max 20 characters each)
6. Each quick reply creates a workflow branch for routing

**Selected quick replies appear in Conversations as inbound messages in blue** — indicating they came from a predefined option.
