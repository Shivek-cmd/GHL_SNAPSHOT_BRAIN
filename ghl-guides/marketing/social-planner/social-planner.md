# GHL Guide — Social Planner

**Where in GHL:** Marketing → Social Planner

---

## Sections

1. Planner
2. Content
3. Comments
4. Statistics
5. Social Listening
6. Settings

---

## 1. Planner

The main calendar/feed view of all scheduled and published social posts.

### Filters

**Content Type:**
- Post Composer
- CSV Upload
- Recurring Post
- Review Post
- RSS Post
- Template Library
- Category Queue
- Native Post

**Status:**
- Published
- Failed
- Scheduled
- Draft
- In Review
- Pending

**Approval Status:**
- Approved
- Rejected

**Other Filters:**
- Created By: dropdown of users
- Approver: dropdown of users
- Categories: dropdown of created categories

### Connect Social Accounts

Click **+ New Social** to connect accounts. Supported platforms:
- Facebook
- Instagram
- LinkedIn
- Google Business Profile (GBP)
- TikTok
- YouTube
- Pinterest
- Threads
- Bluesky
- GHL Community

---

## 2. Content

Manage post types in sub-tabs:

**Sub-tabs:** CSV | Recurring | Review | RSS | Template Library | Approval | Category Queue

**Table columns:** CSV Name | Status | Format | No. of Posts | Updated On | Social | Actions

---

### CSV Upload

Upload posts in bulk via CSV or XLSX file.

**Steps:** Upload File → Select Socials → Review Content

**File constraints:**
- Max file size: 50MB
- Max posts per CSV: 90
- Formats: CSV, XLSX

**Formatting rules:**

| Column | Rules |
|--------|-------|
| Date | YYYY-MM-DD HH:mm, YYYY-MM-DD HH:mm:ss, YYYY/MM/DD HH:mm:ss, MM/DD/YYYY H:mm:ss, MM-DD-YYYY H:mm:ss (24hr supported) |
| Text | Caption and hashtags |
| Link | OG meta tag — one link only |
| Image/Video | Multiple comma-separated URLs. One GIF only. |

**Advanced CSV (additional features):**
- Watermark automation — auto-brand media
- Smart media optimization — auto-resize/compress per platform
- Tag & Category assignment per post
- Pinterest board selection (add `Pinterest board` column with board name or ID)
- First-time comments on posts
- Platform-specific fields (GBP, YouTube, TikTok, Pinterest, Instagram Stories/Reels)
- Both .csv and .xlsx supported

**Media support by platform:**
- Facebook/Instagram: support image carousels (multiple comma-separated URLs)
- GBP: one image only (if posting to both Facebook + GBP, first image goes to GBP, all images go to Facebook)
- Reels/Videos: one video per post only — multiple URLs will cause failure

**After import:** System flags errors in review step — fix before scheduling. Click Schedule → Import to add to calendar queue.

---

### Category Queue

Groups posts by category and cycles them in a recurring loop — evergreen content automation.

**How it works:**
- Posts tagged to a category are pooled into a queue
- Queue cycles through all posts and resets when complete
- Future posts added to the same category are automatically included if **Enable Future Queue** is on

**Setup steps:**
1. Marketing → Social Planner → + New Post → Category Queue
2. Select or create a category
3. Toggle **Future Posting** and **Prioritise Content** if needed
4. Set posting schedule: days + time
5. Click Queue Posts
6. Review/edit content, fix errors, click Queue Post

**Editing an existing Category Queue (3-dot menu):**
- **Edit Category Queue:** update caption, media, frequency, timeslots, post order (drag-and-drop)
- **Queue Preference:** toggle Prioritise New Content (adds to top vs bottom of queue) / Enable Future Queue
- **View Queue Calendar:** weekly or monthly view of scheduled queue posts
- **Reschedule Entire Queue:** shift the entire queue to a new start date using date picker — all posts auto-adjust
- **Add Posts from Post Composer:** while creating a post, assign to an existing or new category to add to its queue

**Pausing/Resuming:** toggle on/off from the Content tab at any time

**Limitations:**
- Rescheduling a single post in a queue is not supported
- Rescheduling/reshuffling from the queue calendar is not supported

---

### Approval

Manage posts pending team review before publishing.

**Shareable Approval Links:** generate a link to share with an external approver
- Tracks: link creator, approver, expiry, post count, status
- Create from Content → Approval → filter by approver → Generate Shareable Link

---

## 3. Comments

View and manage comments from connected social accounts — all platforms in one unified inbox.

---

## 4. Statistics

**Summary metrics:**
- Number of Posts
- Total Likes
- Total Followers
- Total Impressions
- Total Comments

**Social Post Performance** (per platform: Facebook, Instagram, LinkedIn, Pinterest, YouTube, GBP, TikTok, Threads, Bluesky):
- Impressions
- Likes
- Comments
- Week-over-week comparison (e.g., May 1–7 vs Apr 24–30)

**Engagement Stats:** per platform — Impressions | Followers | Likes | Comments | % change

**Post Reach:** per platform with % change

**Link Clicks by Social:** count per platform

**Link Performance Table:** link shortener | Campaign Name | Socials | Clicks | Actions
- Only populated when posts use shortened links created inside Social Planner

**Gender Demography**

**Top Performing Posts**

---

## 5. Social Listening

Displays trending content from external sources to inform post strategy.

**Google Trends:** top 50 trending searches with volume and trend status (New / Falling / Rising)

**Pinterest Keywords:** top 50 trending keywords with pin count

**Wikipedia Pageviews:** trending Wikipedia pages

> Note: GHL is expanding Social Listening with in-depth analysis and smarter insights in future updates.

---

## 6. Settings

### Social Accounts (Social Integration)

Connect and manage all social accounts.

**Filter by platform:** All | GBP | Facebook | Instagram | Threads | LinkedIn | TikTok | Pinterest | YouTube | Community | Bluesky

**Table columns:** Social Account | Status | Type | Validity

**Account types:** Location | Page | Professional | Profile

**Validity:** shows days until token expires — accounts must be reconnected before expiry to avoid post failures

---

### Communities

Manage GHL Community group channels and posting users.

- Select default user to post and sync changes to each community channel
- Table: Group Name | User | Updated On

---

### Pinterest

Select the default Pinterest board per connected Pinterest account.

- Table: Account | Board | Updated On

---

### Notifications

Send alerts for post approvals, failures, and account expirations.

| Notification Type | Description |
|------------------|-------------|
| Account Pre-Expiry | Email when a social account token is about to expire |
| Account Expired | Email when a social account token has expired |
| Request for Post Approval | Email to approver when a post is pending review |
| Approved Post | Email to creator when their post is approved |
| Rejected Post | Email to creator when their post is rejected (includes comment) |
| Post Failed | Email to creator when a scheduled post fails (includes reason) |

Per notification: Email Template | Users to Notify | Reminder Frequency | Status

---

### Social Categories

Create and manage categories for organizing posts and driving Category Queue automation.

- Table: Social Category Name | Status | Updated On
- Categories can be active or inactive
- A category linked to a queue shows a badge in this view

---

### Watermark

Add a single watermark applied across social accounts.

- Table: Watermark | Social | Last Updated
- Control: size, opacity, position per account

---

### Global Settings

| Setting | Description |
|---------|-------------|
| Media Optimization | Auto-optimizes all images for required content formats across all channels |
| Apply Watermark | Automatically applies saved watermark to supported images when posting |

---

### Manage Links

Track approval links created from Content → Approval.

- Table: Shareable Link | Created By | Approver | Updated On | Post Count | Status

---

## Instagram — Connection & Post Sync

---

### Connecting Instagram: Facebook-Linked vs. Direct Integration

Instagram can be connected to Social Planner using one of two methods. Choose based on the account type and what features are needed.

**Before connecting — requirements:**
- Instagram profile must be a **Business** or **Creator** account (personal accounts not supported)
- If using Facebook-Linked method: must have Admin or Editor role on the linked Facebook Page
- If the Page lives in Facebook Business Manager: also need management access inside Business Manager

| Feature | Facebook-Linked (Classic) | Direct Integration (Recommended) |
|---|---|---|
| Requires a Facebook Page | Yes | No |
| Supports Creator Accounts | Limited | Yes |
| Auto-post Stories | No | Yes |
| Schedule Reels | Yes | Yes |
| View Engagement Metrics | Yes | Yes (view counts excluded by Instagram API) |
| Setup Complexity | Higher — multiple logins | Lower — single Instagram login |

> Important: Even with Direct Integration, Instagram/Facebook (not GHL) still requires the underlying profile to be either a Business profile linked to a Facebook Page, or a Creator profile. This is a Meta platform requirement — GHL cannot bypass it.

**Method 1 — Facebook-Linked (Classic):**
Use this if legacy Facebook permissions or video/image view count analytics are needed.
1. Link Instagram to Facebook Page first: Facebook → Page Settings → Linked Accounts → Instagram → Connect Account
2. In GHL: Marketing → Social Planner → Settings (gear icon) → Add Socials → Instagram → **Instagram with Facebook**
3. Follow prompts to authorize both accounts

**Method 2 — Direct Instagram Integration (Recommended):**
Use this for Creator accounts, Story auto-posting, or faster setup without Facebook.
1. Marketing → Social Planner → Settings (gear icon) → Add Socials → Instagram → **Direct Instagram Integration**
2. Grant Instagram permissions and select the Business or Creator account

> Note: Instagram does not allow clickable links in post captions (native app or Graph API restriction). Any link in a caption publishes as plain text.

---

### Instagram Post Sync

> **Labs feature** — must be enabled by Agency for Sub-accounts before it appears.

Automatically imports existing Instagram posts into Social Planner so past content and engagement data are visible alongside scheduled posts — no manual recreation needed.

**What syncs:**
- Posts from the **last 30 days** only
- Content types: images, videos, carousels, reels
- Insights refresh every **24 hours** (not real-time)

**Limitations (Instagram API restrictions):**
- Location tags, collaborator details, and mentions may not be available
- Deleted posts on Instagram still appear in Social Planner — sync is one-way
- Only Instagram Professional accounts (Business or Creator) are supported

**How to enable — Method 1 (during account connection):**
1. Marketing → Social Planner → **+ Socials**
2. In the Connect Socials popup, toggle **Sync Posts Automatically** ON
3. Connect Instagram and complete account authorization

**How to enable — Method 2 (account already connected):**
1. Marketing → Social Planner → **Settings**
2. Social Accounts → Instagram
3. Enable the **Sync Posts** toggle for the relevant account
4. Sync runs in the background automatically

**After enabling:**
- Open **Planner** to see synced historical posts in the calendar
- Open **Statistics** to see synced performance data
- If a disconnect or expired-access message appears, follow the reconnect prompt — sync pauses until the account is reconnected

---

## Creating Posts

### Post Composer (standard post)

1. Marketing → Social Planner → + New Post → Create New Post
2. Select social accounts (Post to)
3. Add text, images/videos, hashtags, mentions
4. Choose action: Save as Draft | Post Now | Schedule | Send for Approval | Schedule as Recurring

**@Mentions:**
- Facebook: live search for public profiles/pages
- LinkedIn (company pages only): live search
- Instagram / TikTok / GBP: plain text `@username` — no auto-suggestions; user must have mentions enabled
- If multiple channels selected, enable "Customise for each channel" to configure mentions per platform
- Not available for CSV, Review Post, or RSS Post

**Media:**
- Add from Media Library via image/video icon
- Preview in the left composer panel
- Edit video thumbnail: hover over media → pencil icon → Custom Thumbnail tab → upload image
- Custom video thumbnails supported for: Facebook Pages, Instagram Business, LinkedIn Profiles/Pages, YouTube

**Best Time to Post:**
- Available in Post Composer and CSV Bulk Action (desktop only — not mobile)
- Click Schedule Post dropdown → view suggested optimal times based on audience engagement
- Can be manually overridden after recommendation is shown
- Coming to Recurring, Review, RSS, and Category Queue in future updates

---

### Content AI — Image Generation

Generate images from text descriptions directly inside the post composer.

**Access:** Post Composer → Image icon → Generate Image with AI

**Requires:** Content AI enabled on the sub-account (Settings → My Staff → Edit User → User Permissions)

**Fields:**
- Describe the image: natural language description
- Number of variations: 1–5
- Style: Photography | Digital Art | Fine Art | 3D Model | Film | Dreamlike | Poster | Vector | Colorful | Pastel Art | Sketch | Watercolor | Color Pencils

**Best practices:**
- Describe realistically — avoid "discount," "sale," or symbols like $
- Be clear and concise
- Specify important details (colors, objects, environment)
- Experiment with styles to find what works for the brand

---

## How Social Planner Connects to the Rest of GHL

| Connection | Detail |
|-----------|--------|
| Reputation → Reviews | Review Post type pulls from connected review platforms |
| Workflow trigger | Social post events can trigger workflows via external tracking |
| Media Library | Images and videos sourced from the shared Media Library |
| Content AI | Image generation powered by Content AI (must be enabled) |
| RSS feeds | RSS Post type converts feed items to scheduled posts automatically |
| Trigger Links | Shortened links in posts tracked via Link Performance stats |
