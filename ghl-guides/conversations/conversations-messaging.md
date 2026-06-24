# GHL Guide — Conversations Messaging Features

---

## Attachments

**Supported file types:**
`.pdf .docx .doc .csv .xlsx .xls .txt .jpg .jpeg .png .gif .svg .mp4 .mpeg .mp3 .wav .wave .aiff .aif .aifc .gsm .ulaw .vcf .vcard .pptx`

**Size limits:**
| Channel | Limit | Behavior if exceeded |
|---------|-------|---------------------|
| Email | 20MB | Auto-converted to media library link |
| SMS | No direct attachment | Automatically converted to media library link |

**Three ways to attach:**
1. Click the **paperclip icon** in the composer → select from device or media library
2. **Paste from clipboard** — Ctrl+V (Windows) / Cmd+V (Mac) after copying a file
3. **Media library** — reuse previously uploaded files without re-uploading

**Viewing attachments:**
All uploaded files are stored in the media library and accessible from Conversations. Videos uploaded via media library auto-generate animated GIF previews in emails.

---

## CC and BCC (Email Only)

**Where:** New Email or Reply composer → CC/BCC fields alongside To field

**CC (Carbon Copy):** Sends to additional recipients. All recipients can see each other's addresses.

**BCC (Blind Carbon Copy):** Sends to additional recipients. BCC addresses are hidden from all other recipients.

**How to use:**
1. Open email composer
2. Click to expand CC/BCC fields
3. Enter addresses from dropdown or type manually
4. Collapse fields after adding

**Key rules:**
- Available only in the New Message Composer (via Labs)
- Adding outside emails to CC/BCC does NOT create new contacts in GHL
- Conversations display only under the primary recipient's thread — not under CC/BCC contacts
- Once CC/BCC recipients exist in a thread you can use "reply all" — you cannot remove them mid-thread
- Compatible with: Mailgun, Gmail, Outlook, SMTP, custom providers via 2-way sync

**Known issue:**
Gmail may show delivery incomplete errors for BCC addresses — this is a Gmail notification behavior. Emails still post to the CRM correctly.

---

## SMS — Selecting To and From Numbers

**From number (who you're sending from):**
- Open Conversations → SMS composer → click From dropdown
- Shows all available phone numbers with friendly name and assigned user
- Defaults to the last-used number for that contact

**To number (which contact number you're sending to):**
- If a contact has multiple phone numbers → dropdown beside the To field
- Defaults to primary contact number if no prior conversation exists

**Access by role:**
| Role | Numbers accessible |
|------|------------------|
| Admin | All configured account numbers |
| User | Default account number + numbers previously used with the contact + numbers assigned to them + unassigned numbers |

---

## Group Chat for SMS

Send one SMS thread to multiple contacts simultaneously.

**Participants:** 2–9 contacts maximum
**Geographic restriction:** US and Canada phone numbers only
**Requirement:** LeadConnector number enabled for SMS/MMS

**How to create (Desktop):**
1. Conversations → Create New Message
2. Select Message Contacts (or Message Teammates for internal groups)
3. Choose Group Conversation
4. Select SMS number + add 2–9 participants
5. Create Conversation → send

**How to create (Mobile):**
1. Open HighLevel / LeadConnector app
2. Conversations tab → Group Chat
3. Choose phone number → add contacts → optionally name the group → Start Chat

**Critical limitations:**
- DND contacts cannot be added or messaged in a group
- Cannot modify participants or sender number after creation — must create a new group
- Attachments supported — images show inline, files appear as downloadable chips

---

## Draft Messages

Drafts save automatically across all channels.
- Unsent messages persist when you navigate away
- Internal comment drafts survive channel switches and conversation changes
- Composer remembers last selected channel when collapsed
- No manual save needed
