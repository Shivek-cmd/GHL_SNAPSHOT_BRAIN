# GHL Guide — Conversation Filters

---

## What Filters Are

Filters narrow the conversation list to show only the conversations matching your conditions. Multiple filters can be combined using AND/OR logic. Filter sets can be saved as **Saved Views** for one-click access.

**Where in GHL:** Conversations → Filters (top of chat list panel)

---

## All Available Filters

**Filter by Assigned**
Narrows to conversations where a specific user is the assigned owner.
- Select a specific user OR select "Logged In User" (dynamic — always shows your own conversations)

**Filter by Follower**
Shows conversations where a user is following (has visibility) without being the primary owner.
- Select a specific user OR "Logged In User"

**Filter by Mention**
Surfaces conversations where a user received an @mention notification.
- Useful for finding flagged discussions directed at you

**Filter by Last Message Direction**
- Inbound — last message came from the contact
- Outbound — last message was sent by a user or automation

**Filter by Last Outbound Message Type**
- Manually — last message was sent manually by a user
- Automated — last message was sent by a workflow or campaign

**Filter by Last Message Channel**
- SMS
- Email
- Calls
- Voicemail
- Live Chat
- WhatsApp
- Facebook
- Instagram
- GBP (Google Business Profile)
- Supports selecting multiple channels simultaneously

**Filter by Tag**
Filters by contact tags applied to the contact in the conversation. Use for custom segmentation — e.g., show only conversations with contacts tagged `newsletter-replied`.

---

## Filter Logic

| Logic | Behavior |
|-------|----------|
| AND | All conditions must be true |
| OR | Any condition being true is enough |

Applies both within a filter group and between multiple filter groups. Combine as needed for precise segmentation.

---

## Saved Views

Save any filter combination as a named view for one-click access.
- Create from the Filters panel after setting conditions
- Appears in the left sidebar for fast switching
- Useful for sales team views, support queues, newsletter repliers, etc.

**Example saved views:**
- Newsletter Replied — Filter by Tag = `newsletter-replied`
- My Unread — Filter by Assigned = Logged In User + Last Message Direction = Inbound
- Warm Leads — Filter by Tag = `newsletter-warm`
