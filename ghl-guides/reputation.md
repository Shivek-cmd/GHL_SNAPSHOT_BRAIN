# GHL Guide — Reputation Management

**Where in GHL:** Reputation (left sidebar)

Reputation Management is GHL's built-in system for collecting, monitoring, responding to, and displaying customer reviews. It connects to Google, Facebook, and 50+ third-party review platforms.

---

## Sections

1. Overview
2. Requests
3. Reviews
4. Widgets
5. Listings *(paid add-on)*
6. Settings

---

## 1. Overview

The dashboard landing page. Split into two tabs: **My Stats** and **Competitor Analysis**.

### My Stats

**Onboarding Checklist** (shown until complete, 6 steps):
- Connect Google Business Profile
- Setup Review Link
- Configure Reviews AI
- Create a Review Widget
- Send your 1st Review Request
- Connect more platforms

**Filters:** date range (DD/MM/YYYY from → to), source platform

**AI Recap:** generates a concise AI summary of reviews from the selected source and date range.

**Stats Panels:**

- **Reviews and Ratings Trend** — chart showing average rating and review volume over time
- **Average Ratings** — overall average rating across all connected platforms
- **Total Reviews** — total review count
- **Sentiment Analysis** — breakdown of positive / neutral / negative sentiment across reviews
- **Review Link** — shows which platform the review link is currently pointing to (configurable in Settings)
- **Review Response Panel:**
  - Responded by AI — number of reviews replied to by Reviews AI
  - Unresponded Reviews — reviews with no reply yet
  - Avg Response Time (Manual + AI) — average days to respond
  - Response breakdown chart
  - Not Eligible Reviews — reviews that cannot be responded to
  - Drip Response prompt — if unreplied reviews exist, prompts to enable Drip Response to auto-reply to backlog
- **Review Request Panel** — shows request volume and conversion across Email, SMS, and WhatsApp

---

### Competitor Analysis

Compare the business against up to 3 competitors using real-time review data from Google and other major platforms.

**Setup steps:**
1. Click + Add Your Business → allow location permission → search and select the business → confirm
2. Click + Add Competitor (repeat up to 3 times) → search by name or address → confirm
3. Scroll down to see Rating by Source across Google, Facebook, TripAdvisor, etc.

Data is auto-fetched and refreshed regularly — no manual entry required. Competitors can be changed at any time.

**Comparison Insights:**
- **Score** — website performance breakdown: load time, mobile optimisation, web vitals
- **Competitive Grid** — side-by-side comparison of key reputation metrics across all added competitors. Unlimited reports can be built.
- **Sentiment Heat-map** — visualises customer sentiment by category across the business and competitors
- **Rating by Source** — shows ratings per platform (Google, Yelp, Facebook, etc.) for each competitor

### Competitor Analysis Report *(via Marketing Audit)*

A separate report that benchmarks business listings and review metrics against up to 3 competitors.

**Where:** Reporting → Local Marketing Audit → Compare Reports tab

**Setup:**
1. Go to Reporting → Local Marketing Audit → Generate Report (must run this first)
2. Navigate to Compare Reports tab
3. Enter up to 3 competitor business names → Click Compare Reports
4. System auto-generates a comprehensive Competitor Analysis Report

**Report covers:**
- **Listings Accuracy** — missing, inconsistent, or incorrect listings vs competitors
- **Reviews Performance** — comparative review volume, star ratings, and sentiment

Note: Exporting is not currently supported — use screenshots or internal sharing within GHL.

---

## 2. Requests

Send manual review requests to individual contacts.

**Send Review Request modal fields:**
- Contact Name: search or create a contact
- Contact Phone: enter phone number
- Contact Email: enter email address
- Mode: Email | SMS | WhatsApp
- Email Template: select from saved templates
- Attachments: up to 5 files (JPG, PNG, JPEG, max 5MB each)

---

## 3. Reviews

View and manage all incoming reviews.

**Filters:**
- Ratings (1–5 stars)
- Sources (connected platforms)
- Start Date / End Date
- Spam toggle
- Search (keyword)

**AI-Powered Review Summary:**
Auto-generated insight card that rolls up feedback from all connected review pages into a single summary.
- Appears as a purple card in both the Reviews tab (left side) and the Overview tab (right side)
- Includes: overall sentiment paragraph + highlight tags (e.g., "Great service", "Long wait", "Booking system")
- Tags update dynamically based on active filters
- **Filter:** click the purple AI Summary button → filter by specific pages/locations + date range
- **Refresh:** click the refresh icon next to the summary title to regenerate with current data and filters
- Summaries include both integrated and manually added reviews (if Manual Reviews is enabled)
- Different from Reviews AI auto-replies — this is analysis only, not response generation

**Review Card shows:**
- Reviewer initials + name
- Platform (e.g., Google)
- Business location name
- Star rating (1–5)
- Review date and time
- Review text
- Response (if replied) — shows responder name and "Replied By Reviews AI" if AI responded

**Actions per review:** reply manually, mark as spam, flag as not eligible

### Manual Reviews

Add customer feedback collected outside connected platforms (paper forms, emails, calls) directly into GHL.

**Add single review:** Reviews tab → Add Reviews → Add Manually tab
- Fields: Rating | Review Text | Date | Platform | Profile Picture | Customer Name
- Click Submit Review

**Bulk import:** Reviews tab → Add Reviews → Upload CSV tab
- Download CSV template → populate → select platform → Upload Reviews

**CSV format:**

| Column | Format | Example |
|--------|--------|---------|
| name | Text | Alice Johnson |
| comment | Text | Fantastic place — would visit again! |
| rating | Number (1–5) | 3 |
| profile photo | Single image URL | https://... |
| images | Multiple image URLs, comma-separated | https://...,https://... |
| date | DD-MM-YYYY | 24-06-2023 |

**Display in widgets:** Reputation → Widgets → choose widget → set Review Source to "Manual" → embed

Manual reviews:
- Appear in Reviews tab with a "Manual Pages" label
- Are included in AI Summary analysis
- Can be filtered by Source → Manual Pages
- Support custom/unlisted platforms (select existing, create custom, or choose No Platform)
- Can be combined with other sources in widgets

---

## 4. Widgets

Create embeddable review widgets to display on websites or funnels.

*(Widget builder — configure style, layout, source filter, and embed code)*

---

## 5. Listings *(Paid Add-on)*

Manages business listings across directories to improve local SEO and online presence.

**What it offers:**
- Listing Management — push and sync business info across directories
- Premium Backlinks — generate authoritative backlinks for SEO
- Sync Functionality — keep NAP (Name, Address, Phone) consistent everywhere
- Duplicate Suppression — detect and suppress duplicate listings

**To activate:** scan the business first to see current listing health, then subscribe.

---

## 6. Settings

### Reviews AI

Controls how GHL automatically responds to incoming reviews.

**Mode — select one:**
- **Auto Response (Auto-Pilot)** — AI replies to reviews automatically without human approval. Customise automated responses by star rating, set wait time before sending, add response footers, and tailor auto-responses per source (Facebook, Google, etc.)
- **Suggest (Suggestive Mode)** — AI drafts a response for the user to review; user clicks AI Reply button to generate, then edits and sends manually. Each regeneration costs $0.01 after the first 3 free trials.
- **Off** — Reviews AI is disabled

**Wait Time Before Responding:** set a delay in minutes before the AI sends its response after a review comes in.

### Drip Mode *(Reviews AI backlog campaign)*

Replies to large backlogs of historical unreplied reviews at a paced, human-like cadence.

**Setup:**
1. Settings → Reviews AI → Create Campaign (or New Drip Campaign)
2. Name the campaign
3. Set eligibility: Only Reply to Reviews Older Than X days
4. Set pace: Replies Per Day (daily cap) | Frequency (daily/weekly/monthly) | Time Window (business hours)
5. Select AI Agent and tone
6. Review summary (eligible review count, estimated days to clear) → Click Start

**Campaign controls:**
- **Edit** — update age threshold, caps, cadence, time window, agent; only affects future scheduled replies
- **Pause** — halts future sends, preserves settings for resumption
- **Delete** — cancels all pending replies, permanently removes campaign; sent replies remain in history

**Monitoring:**
- Scheduled Queue — upcoming replies and next send window
- Sent History — which reviews were replied to, timestamps, response content
- Backlog Progress — remaining eligible reviews and estimated days to completion
- Failures & Retries — identify and action failed sends

**Limits:**
- Editing does not alter already-sent replies
- Actual send timing depends on cadence, time window, and daily caps
- Pausing halts future sends until resumed

---

### Review AI Agents

Create custom AI personas for responding to reviews. Currently available to Agency Users only.

**Quick start:** click **Create Starter Agents** to enable all pre-built template agents at once.

**Setup steps:**
1. Reputation → Settings → Reviews AI → Create Agent
2. Configure: Agent Name | Tone | Prompt (concise instructions for the agent)
3. Set Assignment Rules: assign by Review Sentiment (Positive / Neutral / Negative) | enable Round Robin to rotate agents automatically
4. Configure Language Detection: AI auto-detects review language; set a Fallback Language if detection fails
5. Optionally assign agent to specific Google Business Pages (useful for multi-location or multi-brand setups)
6. Save — agent is active

**Agent management:** Edit | Clone | Delete at any time. Preview AI-generated responses before publishing. Each reply card shows which agent crafted the response.

**Preset Agents (built-in examples):**
- **Claire Flair** — Professional tone. Responds to positive reviews with expertise and authority.
- **Grace Space** — Empathetic + Solution Oriented. Responds to negative reviews with genuine apology and corrective action.
- **Taylor Sailor** — Optimistic. Focuses on customer success and continuous improvement.

**Custom Agent fields:**
- Agent Name
- Agent Instructions / Prompt (full instructions for how to respond)
- Tone (select up to 2): Professional | Funny | Empathetic | Optimistic | Playful | Grateful | Friendly | Concise | Inquisitive | Solution Oriented
- Language: Dynamic | English (US) | other languages
- Review Source: All | specific platform
- Google Business Page assignment (optional)

---

### Review Link

Configures where the review link sends customers.

- **Auto Balance** — when enabled, GHL automatically distributes review requests across connected platforms to balance volume
- **Review Balancing** — set which platforms receive reviews and in what ratio
- Per platform: connect account, set page, view the generated review URL

---

### SMS Requests

Automated SMS sent to request reviews after a contact checks in.

**Settings:**
- When to send after check-in: Immediately | X days/hours
- Repeat until clicked: Don't Repeat | every X hours/days
- Maximum retries: number
- SMS Templates: manage Name / Message / Type per template. Uses merge tags:
  - `{{location.name}}` — business name
  - `{{reputation.review_link}}` — the configured review link

---

### Email Requests

Automated email sent to request reviews after check-in.

**Settings:**
- When to send after check-in: Immediately | X days/hours
- Repeat until clicked: Don't Repeat | every X hours/days
- Maximum retries: number
- Email Template: select from saved templates (Recurring Emails or Draft Emails)

---

### WhatsApp Requests

Automated WhatsApp message sent to request reviews after check-in.

**Settings:**
- When to send after check-in: Immediately | X days
- Repeat until clicked: Don't Repeat | every X hours
- Maximum retries: number

---

### Reviews QR

Generate a QR code that links directly to the review link.

- Create and customise QR codes
- Download and print for in-person use (reception desk, receipts, packaging)

---

### Spam Reviews

Toggle spam detection on or off.

**When enabled:**
- All new incoming reviews are automatically scanned for spam
- Users can manually override the system's spam decision
- Automatic AI replies are not sent to spam-detected reviews
- Scheduled Drip replies can be stopped by manually marking a review as spam
- Spam reviews are hidden from the Review Widget
- Spam reviews are excluded from the Overview Dashboard stats

---

### Integrations

Connect third-party review platforms to import and display reviews inside GHL.

**How to connect:** enter the public page link for the platform.

**Supported Platforms:**

Agoda | Airbnb | AliExpress | Amazon | Angi | Apple App Store | Avvo | Better Business Bureau | Booking.com | Capterra | CarGurus | Caring.com | Cars.com | Citysearch | Consumer Affairs | DealerRater | Doordash | eBay | Expedia | Facebook | FindLaw | Foursquare | Glassdoor | Goodreads | Google Business Profile | Google Play | Google Shopping | Healthgrades | HomeAdvisor | Hotels.com | Houzz | IMDb | Indeed | Lawyers.com | OpenTable | Product Hunt | Product Review | RateMDs | The Knot | Thumbtack | TripAdvisor | Trustpilot | TrustRadius | Uber Eats | WebMD | WeddingWire | Yell | Yellow Pages | Yelp | Zillow | Zocdoc | Zomato

**Custom Links:** add any platform not in the list using a direct URL.

---

## How Reputation Connects to the Rest of GHL

| Action | Where it connects |
|--------|------------------|
| Send Review Request | Workflows → Send Review Request action |
| New Review Received | Workflows → New Review Received trigger |
| Review Link URL | Custom Values → use `{{reputation.review_link}}` in templates |
| Review Widget | Embed in Funnels or Website pages |
| SMS/Email Templates | Reputation Settings pull from saved SMS/Email templates |
| Conversation AI | Can be configured to send review requests at end of conversation |
