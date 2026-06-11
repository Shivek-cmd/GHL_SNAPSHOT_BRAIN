# GHL Guide — Communities: Setup & Groups

**What it is:** GHL's built-in community platform. A private or public space where members interact, access exclusive content, and build relationships — all inside the sub-account without any third-party tool.

**Where in GHL:** Memberships → Communities

---

## Core Architecture

```
Community (the top-level branded space)
│
└── Group (a focused community space — public or private)
    │
    ├── Channel (organized discussion area within the group)
    │   └── Posts (content, discussions, announcements)
    │
    ├── Learning Tab (courses attached to this group)
    │
    ├── Events (scheduled events for this group)
    │
    └── Members (people in this group with roles)
```

A member joins a **Group**. Inside the group they see **Channels** for discussion, a **Learning Tab** for courses, **Events** for scheduled sessions, and other members.

---

## Creating a Community

1. Memberships → Communities → **Create New Community**
2. Enter a name, URL slug, and description
3. Configure branding (see Branding section below)
4. Set up groups inside the community

---

## Groups

Groups are the primary community spaces. Each group has its own channels, members, courses, and events.

**Group privacy options:**
- **Public:** Anyone can see posts and members; instant access without approval
- **Private:** Only members view content; all join attempts require manual admin review even with invite links

### Creating a Group

1. Memberships → Communities → Groups section → **+ Create Group**
2. Enter group name, description, privacy setting (public/private)
3. Customize appearance (banner image, icon)
4. Assign moderators
5. Click **Create Group**

### Converting Between Public and Private

- **Public → Private:** Previous content becomes restricted to current members only
- **Private → Public:** Pending membership requests are auto-approved

**Visibility control:** The "Accessible from switcher" setting determines whether non-members can see the group in the navigation switcher.

### Group Settings

| Setting | Location |
|---|---|
| Group privacy (public/private) | Settings → Details |
| Member invitations by members | Settings → toggle "Allow members to invite new members" |
| Custom domain | Memberships → Communities → Settings |
| Branding (favicon, cover, logo) | Settings → Branding tab |

**Note:** Groups can only be deactivated, not deleted.

---

## Channels

Channels are organized discussion spaces within a group. Each channel has a name, description, and icon.

**Channel types:**
- **Standard channel** — all group members can post and comment
- **Private channel** — restricted to approved members only (see `communities-advanced.md`)
- **Announcement channel** — admin/owner-only posting; members have read-only access

### Creating a Channel

1. Open the group → click **+ Add Channel**
2. Enter Channel Name (max 15 characters) and Description (max 60 characters)
3. Select an icon
4. Toggle privacy if needed
5. Save

### Announcement Channel

An announcement channel is a specialized read-only channel for important updates.

**Setup:**
1. Create a new channel or edit an existing one
2. Toggle **Enable as Announcement Channel** ON
3. Select visibility: Public (all members) or Private (restricted)
4. Save

**Behavior:** Only admins and owners can post. Members can view and react. Can be converted back to a standard channel at any time.

### Channel Management

- **Move posts:** Three-dot menu on any post → Move to Channel → select destination (admins and post authors only)
- **Delete posts:** Admins and moderators can delete any post; members can delete their own
- **Pin posts:** Three-dot menu on a post → Pin → post appears at top of channel feed

---

## Member Roles

| Role | Create Posts | Moderate Posts | Manage Members | Deactivate Group |
|---|:---:|:---:|:---:|:---:|
| Owner | ✔ | ✔ | ✔ | ✔ |
| Admin | ✔ | ✔ | ✔ | ✗ |
| Channel Manager | ✔ | ✔ | ✔ | ✗ |
| Contributor | ✔ | ✗ | ✗ | ✗ |

**Owner:** Full control including deactivation and role assignment. Only one owner per group.
**Admin:** Manage members and content; invite, approve, and remove users.
**Channel Manager:** Moderate specific channels and their members.
**Contributor:** Participate based on group privacy and channel access.

**Group ownership transfer:** Available via Settings — transfer to another admin or owner.

---

## Inviting Members

### Via Invite Link

1. Memberships → Communities → Groups → open group
2. Click **Invite Members**
3. Copy the invite link
4. Distribute via email, SMS, WhatsApp, or any channel

### Via Email Invitation

1. Same path → **Invite Members**
2. Enter recipient name and email address
3. Toggle **Administrative Privileges** on/off if granting admin role
4. Click **Send Invite**

### Approving Join Requests (Private Groups)

1. Groups → open group → **Members** tab → **Requested**
2. Three-dot menu → **Approve** or **Decline**

---

## Branding a Community

**Where in GHL:** Memberships → Communities → Settings → Branding tab

| Asset | Recommended dimensions |
|---|---|
| Favicon | 32 × 32px or 64 × 64px |
| Cover image | 1600 × 400px recommended |
| Logo | Upload PNG with transparent background |

### Custom Domain for Community

1. Memberships → Communities → Settings → **Custom Domain**
2. Enter the branded domain (e.g., `community.yourbusiness.com`)
3. Add CNAME record in DNS:
   - **Name/Host:** your subdomain
   - **Value/Target:** GHL's CNAME target shown on screen
4. Click **Update Domain**
5. Wait for DNS propagation (up to 24–48 hours)

### Whitelabel Community App

GHL supports whitelabel community mobile apps. See the PWA guide in `courses-customization-branding.md` for the standard PWA approach. A fully native whitelabel app requires external development tools (PWABuilder, Capacitor).

---

## Email Notifications for Communities

**Where in GHL:** Sites → Client Portal → Memberships → Settings → Email Settings → Communities

Configurable notification emails:
- Group invitation and membership status notifications
- General group interactions (comments, likes, tags)
- Learning-related course emails
- Role change notifications
- Event reminders

Customize templates to match brand voice.

---

## Community vs Group vs Channel — Decision Rules

| Use this | When |
|---|---|
| Community | Top-level container — one per brand or business |
| Group | A distinct segment of the community (e.g., "Beginners", "VIP Members", "Masterclass Cohort 2") |
| Channel | A topic within a group (e.g., "Introductions", "Weekly Wins", "Questions") |
| Announcement Channel | Critical updates that should not be buried in discussion feeds |
| Private Channel | Restricted discussions — paid tiers, staff areas, cohort-specific content |

---

## Custom CSS/JS in Groups

Admins can inject custom CSS and JavaScript into a group to extend styling and functionality beyond the default theme options.

**Where:** Group → Settings → Advanced → Custom CSS/JS

Use cases: custom fonts, branded color overrides, embedded widgets, third-party tracking scripts.
