# GHL Guide — Conversations Overview

---

## What Conversations Is

The Conversations module is the unified inbox for all contact communication — Email, SMS, WhatsApp, Facebook, Instagram, Live Chat, and Internal Comments — in one place. Every channel appears in the same thread per contact.

**Where in GHL:** Conversations (left sidebar)

---

## Layout — Four Panel Structure

| Panel | What it shows |
|-------|--------------|
| Inbox Panel (left) | Switch between My Inbox, Team Inbox, Internal Chat |
| Chat List (second column) | All conversations with sorting, filtering, bulk actions |
| Message History (center) | Full thread — read and reply here |
| Right Panel (collapsible) | Contact details, appointments, opportunities, payments |

Both side panels collapse independently.

---

## Inbox Types

**My Inbox**
- Assigned to Me — conversations assigned to the logged-in user
- Internal Chat — private team conversations

**Team Inbox**
- All conversations across the sub-account (admins see all; users see assigned)

---

## Message History Panel

- Displays all channels in one thread: Email, SMS, WhatsApp, Facebook, Instagram, Internal Comments
- Switch channels via composer selector without leaving the thread
- **New divider** automatically marks where unread messages begin
- Divider persists until you reply or manually mark as read
- Timeline filter: All / Conversations / Activities / specific message type
- Search within message history
- View call transcripts inline

---

## Right Panel

Collapsible panel on the right. Tabs:

| Tab | What you can do |
|-----|----------------|
| Contact | View/edit contact fields, custom fields, tags, owner, DND status |
| Activities | See appointments, workflow history, notes |
| Associations | Linked opportunities, other contacts |
| Documents | Contracts and documents |
| Payments | Invoices and payment history |

Appointments and Opportunities can be created and edited directly from the Right Panel without leaving Conversations.

---

## Message Composer

- Channel selector — switch between Email, SMS, WhatsApp, etc.
- Full-screen drafting mode (⌘/Ctrl + Shift + E)
- File attachments via paperclip, clipboard paste (Ctrl+V / Cmd+V), or media library
- Internal Comment option — private team note, contact never sees it
- Drafts auto-save when switching channels or navigating away
- Composer remembers last selected channel

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| ⌘/Ctrl + K | Global search |
| ⌘/Ctrl + Enter | Send message |
| ⌘/Ctrl + Shift + E | Toggle full-screen composer |
| ? | Open full shortcut list |

---

## Bulk Actions

Select multiple conversations → bulk action options:
- Mark as Read / Unread
- Star / Unstar
- Delete

---

## Mark as Read

Opening a conversation does NOT automatically mark it as read — intentional design to prevent missed messages.

**Three ways to mark read:**
1. Reply to the conversation — marks read automatically
2. Click the **Mark as Read** icon (top right of conversation)
3. Workflow automation — use the **Edit Conversation** workflow action

---

## Draft Messages

Drafts save automatically. Behavior:
- Unsent messages are retained when you navigate away
- Internal comment drafts persist when switching channels or collapsing the composer
- Composer remembers your last selected channel when you collapse

---

## Performance

- Action response time ~70% faster than previous version
- Page navigation ~35% faster
- Memory usage reduced from ~1.7 GB to ~0.45 GB

---

## FAQs

**What attachment types are supported?**
`.pdf .docx .doc .csv .xlsx .xls .txt .jpg .jpeg .png .gif .svg .mp4 .mpeg .mp3 .wav .wave .aiff .aif .aifc .gsm .ulaw .vcf .vcard .pptx`

**Why is Gmail showing delivery incomplete errors with BCC?**
Gmail may send error notifications when BCC addresses are used because it doesn't get a delivery receipt for BCC addresses. Emails typically post to the CRM successfully despite the error.

**Why can't I send Instagram DMs to people who commented on my posts?**
Recipients must initiate contact first — the contact must send at least one DM within the last 24 hours. For comment replies, use the **Instagram Interactive Messenger** workflow action with reply type set to "Reply to comment via DM."
