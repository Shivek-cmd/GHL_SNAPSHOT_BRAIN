# GHL Guide — Communities: Advanced Features

**Where in GHL:** Memberships → Communities → Groups

---

## Private Channels

Private channels restrict visibility and participation to approved members only. Non-members cannot see the channel exists.

**Where in GHL:** Group → + Add Channel (during creation) OR open existing channel → Settings (gear icon) → Settings tab

### Creating a Private Channel

1. Group → click **+ Add Channel**
2. Enter Channel Name (max 15 characters) + optional description and icon
3. Toggle **Make this Channel Private** to ON
4. Click **Create Channel**

**Auto-members:** Group owner and channel creator are automatically added as channel managers for private channels.

### Converting a Public Channel to Private

1. Open the channel → Settings (gear icon) → **Settings** tab
2. Click **Make Channel Private**
3. Read the acknowledgement popup → click **Confirm**

After conversion: non-members can no longer see the channel.

### Converting a Private Channel Back to Public

1. Channel → Settings → **Settings** tab
2. Click **Make Channel Public** → **Confirm**

After conversion: channel becomes visible to all group members; post history remains accessible.

### Adding & Removing Members in a Private Channel

**Add:** Channel → Settings (gear icon) → **Members** tab → search and add users

**Remove:** Members tab → three-dot menu beside the user's name → **Remove from Channel**

**Channel managers** act as admins for their specific channel — they can add/remove members and moderate content.

**Group owner cannot leave** a private channel — they maintain permanent access.

### Channel Emojis & Icons

Each channel can have a custom emoji or icon displayed alongside its name.

**How to set:**
1. Open channel → Settings (gear icon) → click **Edit** beside Channel Name
2. Click **Channel Icon option** → choose Emoji or Icon
3. Save

**Who can change it:** Channel owner or a user with channel-level manage permissions.

---

## Private Channel-Based Course Access

Link courses to specific private channels so only members of those channels can see and access the course in the Learning Tab.

**Setup:**
1. Learning Tab → select course → **Edit Course**
2. Visibility dropdown → select **Private Channel**
3. Choose one or more private channels
4. Save

**Behavior:** Members of linked private channels automatically gain course access. Members outside the channels cannot see the course at all.

**Limitation:** Module-level restrictions are not supported — access controls apply to entire courses only.

---

## Private Course & Member-Specific Course Access

GHL also supports fully private courses and member-specific access assignment, beyond channel-based controls.

**Private courses:** Set a course to Private visibility — the course does not appear in the general Learning Tab and must be directly shared or granted via workflow.

**Member-specific access:** Assign course access to individual members or segments without making the course visible to the entire group.

**Use cases:** 
- One-on-one coaching material visible only to that client
- Onboarding course visible only during the first 30 days of membership
- Beta course released to a test group before full launch

---

## Workflow Triggers for Communities

Communities fires workflow triggers when members join or leave groups.

### Workflow Triggers

**Group Access Granted**
Fires when a member is given access to a community group.
Use this to: add a tag, send a welcome email, move a pipeline stage, enroll in a course.

**Group Access Revoked**
Fires when a member's group access is removed.
Use this to: remove a tag, send a re-engagement email, update a pipeline stage.

### Workflow Actions

**Grant Group Access**
Automatically adds a contact to a specified community group.
Fields: select the group to grant access to.

**Revoke Group Access**
Automatically removes a contact from a specified community group.
Fields: select the group to revoke access from.

### Common Workflow Patterns for Communities

| Pattern | Trigger | Actions |
|---|---|---|
| Welcome new community member | Group Access Granted | Send welcome email, add tag `community-active`, create opportunity |
| Paid group access on payment | Payment Received (Source = Community) | Grant Group Access → specific group |
| Remove access on cancellation | Subscription cancelled | Revoke Group Access → specific group |
| Re-engagement after inactivity | User Login (absence condition) | Send check-in SMS, assign task to team |
| Level-up reward delivery | Community Leaderboard Level Changed | Send congratulations email, add tag for reward tier |

### Community-Specific Workflow Triggers (Full List)

| Trigger | When it fires |
|---|---|
| **Group Access Granted** | Member added to a group |
| **Group Access Revoked** | Member removed from a group |
| **Private Channel Access Granted** | Member added to a private channel |
| **Private Channel Access Revoked** | Member removed from a private channel |
| **Community Group Member Leaderboard Level Changed** | Member reaches a new gamification level |

---

## Communities Smart List Filter

Filter GHL contacts by their group membership status for targeted messaging.

**Where:** Contacts → Smart Lists → Create Smart List → filter by Communities Group

**Available filters:** Group Is / Is Not → select group name

**Use cases:**
- Identify all members of a specific group
- Compare engagement between paid and free group members
- Target group members with an upsell campaign

---

## Communities & Courses Integration Points

Communities and Courses are separate but tightly integrated:

| Integration | Where it lives |
|---|---|
| Learning Tab inside Groups | Free or paid courses attached to a group for member access |
| Level-unlock courses | Gamification level triggers course access |
| Private channel courses | Private channel membership triggers course access |
| Buy Now courses | One-time or subscription purchase inside the Learning Tab |
| Time-unlock courses | Enrollment date + days = course access |
| Workflow triggers | Both Courses and Communities fire into the same Workflow engine |
| Certificates | Issued on course completion; can trigger Community recognition posts |

**Design principle:** Use Communities for the social and engagement layer; use Courses (Memberships) for the structured learning layer. Connect them through the Learning Tab, access rules, and shared workflow triggers.
