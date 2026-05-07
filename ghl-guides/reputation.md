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

Compare the business against up to 3 competitors.

**How to add a competitor:** search by business name or Google address — GHL pulls their public profile data.

**Comparison Insights:**
- **Score** — website performance breakdown: load time, mobile optimisation, web vitals
- **Competitive Grid** — side-by-side comparison of key reputation metrics across all added competitors. Unlimited reports can be built.
- **Sentiment Heat-map** — visualises customer sentiment by category across the business and competitors
- **Rating by Source** — shows ratings per platform (Google, Yelp, Facebook, etc.) for each competitor

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

**AI Summary:** auto-generated summary of the filtered review set. Can be regenerated.

**Review Card shows:**
- Reviewer initials + name
- Platform (e.g., Google)
- Business location name
- Star rating (1–5)
- Review date and time
- Review text
- Response (if replied) — shows responder name and "Replied By Reviews AI" if AI responded

**Actions per review:** reply manually, mark as spam, flag as not eligible

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
- **Auto Response** — AI replies to reviews automatically without human approval
- **Suggest** — AI drafts a response for the user to review and send manually
- **Off** — Reviews AI is disabled

**Wait Time Before Responding:** set a delay in minutes before the AI sends its response after a review comes in.

**Drip Response (for backlog):**
Automatically reply to old unreplied reviews on a controlled schedule.
- Campaign Name
- Only reply to reviews older than: X days
- Frequency: replies per day (e.g., 10/day)
- Timing: Daily schedule
- Time Window (optional): send replies between HH:MM AM and HH:MM PM (local time)
- Select AI Agent(s): choose which Review AI Agent handles the replies

---

### Review AI Agents

Create custom AI personas for responding to reviews.

**Preset Agents (built-in examples):**
- **Claire Flair** — Professional tone. Responds to positive reviews with expertise and authority.
- **Grace Space** — Empathetic + Solution Oriented. Responds to negative reviews with genuine apology and corrective action.
- **Taylor Sailor** — Optimistic. Focuses on customer success and continuous improvement.

**Custom Agent fields:**
- Agent Name
- Agent Instructions (full prompt — tells the AI how to respond)
- Tone (select up to 2): Professional | Funny | Empathetic | Optimistic | Playful | Grateful | Friendly | Concise | Inquisitive | Solution Oriented
- Language: Dynamic | English (US) | other languages
- Review Source: All | specific platform

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
