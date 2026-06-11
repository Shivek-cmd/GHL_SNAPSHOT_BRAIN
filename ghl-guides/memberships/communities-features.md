# GHL Guide — Communities: Features (Gamification, Events, Live, Announcements)

**Where in GHL:** Memberships → Communities → Groups → open group

---

## Gamification: Points, Badges & Leaderboards

Gamification motivates member participation through a points-based progression system with levels, badges, and leaderboards.

**Where in GHL:** Group → Settings → **Gamification & Rewards**

### How Points Work

- Members earn **1 point per "like"** received on their posts, comments, and replies
- Points accumulate over time — they do not reset
- Levels are **group-specific** — a member at Level 3 in one group starts at Level 1 in a new group

### Level Structure (Fixed)

| Level | Points Required |
|---|---|
| Level 1 | 0 |
| Level 2 | 5 |
| Level 3 | 20 |
| Level 4 | 65 |
| Level 5 | 155 |
| Level 6 | 515 |
| Level 7 | 2,015 |
| Level 8 | 8,015 |
| Level 9 | 33,015 |

Maximum 9 levels. The point thresholds are fixed — only the level names are customizable.

### Setting Up Gamification

1. Group → **Settings** → **Gamification & Rewards** tab
2. Edit level names (e.g., "Beginner", "Rising Star", "Champion")
3. Add rewards (up to 3 rewards per group)
4. Enable leaderboard settings
5. Save

**Rewards:** Text-based offline incentives displayed in the leaderboard navigation. Cannot currently be linked directly to automated GHL actions — they require manual fulfillment.

### Level-Up Notifications

Members receive in-app and push alerts when they advance to a new level.

**Level-based course unlock notifications:** In-app, email, and push notifications when courses become available tied to member achievement levels.

---

## Leaderboard

A ranking system showing member performance across the community.

**Access:** Group → Leaderboard section (visible to all members)

**Displayed:** Members ranked by total points; badges shown alongside names; level progress visible per member.

---

## Community Events

Events allow admins and owners to schedule and manage community gatherings with registration, reminders, and calendar integrations.

**Where in GHL:** Group → **Events** tab → + Create Event

### Creating an Event

1. Group → Events tab → **Create Event**
2. Fill in:
   - **Title** and **Description**
   - **Banner image**
   - **Date and time**
   - **Location:** physical address, Zoom link, Google Meet link, or other meeting URL
3. Configure access restrictions (optional):
   - Restrict to specific course, private channel, or engagement level
4. Set pricing: **Free** or **Paid** (configure currency and price)
5. Enable reminder notifications
6. Publish

### Member Experience

- Members browse and register for events in the Events tab
- One-click calendar add: Google Calendar or iCal
- In-app notifications and email reminders before the event
- Discussions Tab alerts for upcoming events

### Event Reminder Customization

**Path:** Sites → Client Portal → Memberships → Settings → Email Settings → Communities → **Event Reminder Email**

Customize subject line and body content to match brand voice.

### Live Rooms in Events

Events can include a Live Room for real-time sessions. See the Go Live section below for Live Room functionality.

**Admin note:** The system does not send admins or event creators a notification when someone registers for an event.

---

## Go Live (Meetings & Broadcasts)

Host real-time video sessions directly inside a community group and channel — no external tools required.

**Where in GHL:** Group → click the **Go Live** button (red video-camera icon) near the posting tab

### Two Operating Modes

| Mode | Best for | What members can do |
|---|---|---|
| **Meeting Room** | Interactive workshops, Q&A, panels | Join with camera/mic, chat, react, raise hand, screen share |
| **Stream Software** | Professional broadcasts via OBS/Zoom/StreamYard | Watch, chat, react |

### Starting a Go Live Session

1. Group → click **Go Live**
2. Enter **Title** and **Description**
3. Configure settings:
   - **Keep livestream as post:** saves the session as a post after it ends
   - **Notify members:** sends in-app and push notifications
4. Select the channel for publishing
5. Set timing (defaults to "Now")
6. Choose video source: Meeting Room or Streaming Software

### Meeting Room Mode

After selecting Meeting Room and clicking Go Live:
1. Allow browser camera and microphone access
2. Members join via the **Join Stream** button on the post
3. Host controls available:
   - **View:** Speaker layout or Gallery layout
   - **Audio/Video devices:** select mic, speakers, camera
   - **Participants:** view Host and Attendee lists; manage permissions
   - **Chat:** send messages, emoji reactions, file attachments
   - **Reactions & Raise Hand:** manage speaking queue
   - **Screen Share:** window or full desktop
   - **Pin:** highlight a specific speaker for all viewers
4. End: click **End Session** → confirm to end for all participants
5. A post appears automatically showing stream completion and recording status

**Recordings:** Post authors and group admins can download recordings directly from the post.

### Streaming Software Mode (OBS, Zoom, StreamYard)

1. Select **Streaming Software** as video source
2. Copy the **Server URL** and **Stream Key** provided
3. Paste into your encoder's RTMP settings
4. Start broadcasting from the encoder
5. Click **Go Live** in GHL — broadcast appears live in the selected channel

**Stream Keys are persistent** — reuse across sessions without reconfiguration. Reset only if accidentally shared.

### Recording Notes

- Sessions can be recorded when enabled — replays available after processing
- Sessions ending due to inactivity show a notification that no recording occurred
- No maximum participant cap or stream duration limit

---

## Announcement Channel & Notifications

**What it is:** A read-only channel where only admins and owners can post. Members see all announcements but cannot reply.

**Setup:** Channel → Settings → toggle **Enable as Announcement Channel** ON

**Visibility:** Public (all group members) or Private (restricted members only)

**Converting back:** Announcement channels can be converted back to standard channels at any time, restoring member posting access.

### Notification Types Tied to Announcements

| Notification | Delivery |
|---|---|
| Level upgrade | In-app + push |
| Level-based course unlock | In-app + email + push |
| Time-based course unlock | In-app + email + push |

---

## Communities — Automatic Newsletters

GHL can automatically generate and send periodic newsletters to community members summarizing recent activity.

**Where in GHL:** Group → Settings → Automatic Newsletters

**Use cases:** Keep inactive members re-engaged; surface recent popular posts; drive members back into the community.

---

## Learning Tab (Courses Inside Communities)

A dedicated tab in every group that hosts courses for group members.

**Adding a free course to a group:**
1. Group → **Learning Tab** → **+ Add Course**
2. Select an existing course from the course library
3. Publish — all group members immediately gain access

**Deleting a course from Learning Tab:** Delete button next to the course.

**Members are notified via email** whenever a new course is added to their group's Learning Tab.

For paid courses in the Learning Tab, see `communities-monetization.md`.

---

## Navigation Tabs (Customizable)

Group navigation tabs can be customized to control what members see in the group menu.

**Where:** Group → Settings → Navigation Tabs

Add, remove, reorder, or rename tabs. Standard tabs: Home, Channels, Learning, Members, Events. Custom tabs can link to any internal or external URL.
