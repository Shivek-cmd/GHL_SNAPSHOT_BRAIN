# GHL Guide — Communities: Member Management & Moderation

**Where in GHL:** Memberships → Communities → Groups → open group → Members tab

---

## Member Roles & Permissions

| Role | Create Posts | Moderate Content | Manage Members | Deactivate Group |
|---|:---:|:---:|:---:|:---:|
| Owner | ✔ | ✔ | ✔ | ✔ |
| Admin | ✔ | ✔ | ✔ | ✗ |
| Channel Manager | ✔ | ✔ | ✔ | ✗ |
| Contributor | ✔ | ✗ | ✗ | ✗ |

Roles are per-group — a person can be an Admin in one group and a Contributor in another.

---

## Managing Members

### View Members

Groups → open group → **Members** tab

**Member tabs:**
- **Members** — all active members with roles
- **Requested** — pending join requests (private groups)
- **Banned** — all banned members

**Filter available:** By role, join date, or activity

### Change a Member's Role

1. Members tab → locate the member
2. Click the three-dot menu → select new role (Admin or Contributor)

### Approve or Decline Join Requests (Private Groups)

1. Members → **Requested** tab
2. Three-dot menu → **Approve** or **Decline**

### Remove a Member

1. Members tab → locate the member
2. Three-dot menu → **Remove from Group**
3. Member is removed and can submit a new join request in the future

### Ban a Member

1. Members tab → locate the member
2. Three-dot menu → **Ban from group**
3. Banned member is removed and CANNOT rejoin — permanently blocked

**Mobile path for banning:**
1. Communities homepage → click **Manage**
2. Select Members from the settings page
3. Three-dot menu → **Ban from group**

**Banned members list:** Members → Banned tab — admins can view all banned members here

### Bulk Invitations

For mass onboarding: send an email or SMS campaign to your contact list with the group invite URL. GHL does not have a native bulk-invite import — use campaigns for scale.

---

## Reporting Content

Any member can report a post or comment. Admins receive email, in-app, and push notifications when content is flagged.

### How Members Report Content

1. Click the three-dot menu (⋮) on any post or comment
2. Select **Report**
3. Member receives confirmation that the content has been reported

### How Admins Review Reported Content

**Web:**
1. Communities homepage → **Settings**
2. Select **Reported Content** tab
3. Review flagged items → choose **Keep** or **Remove**

**Mobile:**
1. Communities homepage → click **Manage**
2. Select **To Review** from settings
3. Review and act on reported content

---

## Membership Approval Questions

When a group requires approval to join, admins can set custom questions that applicants must answer before their request is reviewed.

**Where:** Group Settings → Members → Approval Questions

**Use cases:**
- Qualify applicants (e.g., "What is your role in the industry?")
- Set expectations (e.g., "Have you read the community guidelines?")
- Collect context for the approval decision

Answers are visible when reviewing a pending request in the Requested tab.

---

## What Happens When a Contact is Deleted

If a GHL contact linked to a community group is deleted from the CRM:
- The member's account is removed from the group
- Their posts and comments remain visible in the group (content is not deleted)
- The member cannot log in or access the community

**Before deleting a contact:** Review their community membership. If they are a paying member of a Paid Group, delete after confirming their subscription has been cancelled.

---

## Group Ownership Transfer

Transfer group ownership to another admin or owner when the original owner leaves.

**Where:** Group → Settings → Transfer Ownership

**Note:** Ownership cannot be unassigned — it must be transferred to an existing admin.

---

## Member Chat (Private Messaging)

Community Chat enables one-on-one private messaging between group members.

**Starting a chat:**
1. Join a Group
2. Open the Community Chat tab
3. Select a member from the group roster
4. Start a private conversation

**Features:** Private messaging, push notifications, media sharing (photos, videos, documents), emojis and GIFs

**Privacy controls:**
- Members can disable chat for specific groups: Profile → Account Settings → Community Chat → toggle off per group
- Members can block specific users: open chat → Options → **Block User**

**Requirement:** Must be a group member before messaging other members — chat is scoped to group membership.

---

## Smart List Integration

Use GHL's Smart Lists to filter contacts by community group membership. This lets you target members (or former members) with campaigns or workflows.

**Where in GHL:** Contacts → Smart Lists → Create Smart List

**Filter by:**
- Tag added by a community workflow (e.g., `community-member-active`)
- Custom field set when access was granted
- Pipeline stage updated by community trigger workflow

**Use cases:**
- Email all active group members about an upcoming event
- Re-engage members who haven't logged in (combined with User Login workflow trigger)
- Offer a Paid Group upgrade to all free group members
