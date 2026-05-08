# GHL Guide — Ad Manager

**Where in GHL:** Marketing → Ad Manager

---

## What is Ad Manager?

Ad Manager brings Facebook, Instagram, Google, and LinkedIn Ads together into one unified dashboard inside GHL. Instead of switching between platforms, users can create campaigns, track performance, and optimize results without leaving GHL.

Supports both agency-level management across multiple clients and sub-account level campaign execution.

---

## Supported Platforms & Campaign Types

| Platform | Campaign Objectives | Ad Formats |
|----------|--------------------|-----------| 
| Meta (Facebook & Instagram) | Lead Generation, Website Traffic, Engagement, Sales | Single Image, Video, Carousel (up to 10), Lead Forms, Conversation Forms |
| Google Ads | Search Campaigns, Demand Generation *(coming soon)* | Search Ads, Image, Video, Carousel (Demand Gen) |
| LinkedIn Ads | Lead Generation, Website Visits | Single Image, Video, Carousel, Lead Forms |

---

## Key Benefits

- **All-in-One:** manage Facebook, Instagram, Google, and LinkedIn from one dashboard
- **Time-Saving:** guided setup for quick campaign launches
- **Clear ROI:** instant visibility into spend, conversions, and performance metrics
- **Agency Efficiency:** manage multiple clients' campaigns seamlessly
- **Resell Opportunity:** agencies can monetize Ad Manager access for sub-accounts

---

## Pricing & Access

- **Agencies:** Ad Manager is included at no cost
- **Sub-Accounts:** agencies set their own pricing — HighLevel's base cost is $0, full margin goes to the agency
- **Where to configure access:**
  - Agency → Reselling Tab — set default pricing for all sub-accounts
  - Sub-Account → Reselling Tab — set or override pricing individually
  - SaaS Configurator → Features Tab — include Ad Manager in a SaaS plan

---

## Sections

1. Campaigns
2. Statistics
3. Settings

---

## 1. Campaigns

Create and manage ad campaigns across connected ad platforms.

**Supported platforms:** Meta (Facebook/Instagram) | Google Ads | LinkedIn Ads

### Campaign Templates

Pre-built templates available to speed up campaign creation.

**How to use:**
1. + Create Campaign → choose Google or Meta → Next
2. Select **Ad Manager Templates** → Next
3. Filter by: Categories (Automotive, Legal, Marketing Agency, Financial, etc.) | Objectives (Engagement, Lead Generation, Sales, Web Traffic) | Tags
4. Preview template (eye icon) or click to see details
5. Click **Continue** → edit copy, images, URLs, settings → publish

Templates can be marked as favourites for quick access.

**How to create a campaign from scratch:** connect an ad account first (Settings → Platform Settings), then create a campaign using a template or from scratch.

---

## 2. Statistics

Track ad performance across all connected campaigns.

### Conversion Summary Metrics

| Metric | Description |
|--------|-------------|
| Impressions | Total number of times ads were shown |
| Clicks | Total clicks across all campaigns |
| Conversions | Total conversion events recorded |
| Average CPC | Average cost per click |
| Cost per Conversion | Total spend ÷ total conversions |
| CPM (Cost per Mille) | Cost per 1,000 impressions |
| Client Spends | Total ad spend |

### Performance Analytics

Visual charts — Impressions | Clicks | Conversions over time

### Campaign Details Table

- Search by campaign name
- Export data
- Columns: Campaign Name | Status | Clicks | Revenue | ROI% | CPC | CTR | Sales | CPS

---

## 3. Settings

### Platform Settings

Three platforms: **Meta** | **Google Ads** | **LinkedIn**

---

### Meta Settings

#### Ad Account
Connect and manage the Meta ad account.

| Field | Description |
|-------|-------------|
| Account | Account name |
| Account Status | Connected / Disconnected |
| Account Currency | Currency used for the account (e.g., INR, USD) |
| Account ID | Format: `act_XXXXXXXXXXXXXXX` |

---

#### Pages
Add and manage Facebook pages used for advertisements.

**Table columns:** Page | Page Status | Connected Date

---

#### Conversions (Datasets / Pixels)
Add and manage Meta datasets to track ad campaign performance.

**Table columns:** Dataset Name | Dataset ID | Pixel Code (Copy) | Conversion Created On

Each dataset has a copyable pixel code snippet to embed on websites for conversion tracking.

---

#### Audiences
Create and manage Facebook audiences for ad campaigns.

**Table columns:** Audience Name | Audience Type | Audience Status | Created On | Modified On

**Create New Audience — 2 options:**

**Option 1: Lookalike Audience**
Reach new people who are similar to your existing audience.
- Data Source: select an existing audience or data source
- Audience Name: text input (max 50 characters)
- Geographic Location: search and add locations
- Audience Size: 0% to X% (0–1% = closest match; increasing % = larger but less similar audience)

**Option 2: Custom Audience**
Re-engage people who have already shown interest in the business.

Select a source:
- **Website** — audience based on website visitors from Meta pixel
- **Facebook Page** — people who follow or interacted with the page
- **Lead Form** — people who opened or completed a Facebook/Instagram lead gen form
- **Customer List** — upload a customer list or use GHL Smart Lists

---

### Google Ads Settings

#### Ad Account
Connect and manage the Google Ads account.

| Field | Description |
|-------|-------------|
| Account | Account name |
| Account Status | Connected / Disconnected |
| Account Currency | Currency used |

---

#### Conversions
Create and manage Google Ads conversion tracking.

**Filters:** Date range (from / to)

**Table columns:** Conversion Name | All Conversion Value | All Conversions | Conversion Source

---

#### Audience Segments
Create and manage Google audience segments for ad campaigns.

**Types:**
- Customer List
- Website Visitor List
- Other audience segments

**Table columns:** Segment Name | Segment Status | Segment Type | Segment ID

---

### LinkedIn Settings

#### Ad Account
Connect and manage the LinkedIn ad account.

| Field | Description |
|-------|-------------|
| Account | Account name |
| Account Status | Connected / Disconnected |
| Account Currency | Currency used |

---

### Global Settings

#### Subscription
View and manage the Ad Manager subscription.

| Field | Description |
|-------|-------------|
| Subscription ID | Unique subscription identifier |
| Status | Active / Inactive |
| Amount | Monthly cost (e.g., $0 for free tier) |
| Renewal Cycle | Monthly |

---

## LinkedIn Ads — Detailed Setup

### Prerequisites
- LinkedIn Ad Account active in LinkedIn Campaign Manager
- LinkedIn Company Page linked to the ad account
- Campaign Manager access on the Ad Account + Admin access on the Company Page

### Campaign Structure (3-tier hierarchy)
- **Campaign Group** — top-level budget container
- **Campaign** — objective, targeting, and spend layer
- **Ad** — creative assets and copy

Multiple campaigns per group; multiple ads per campaign (for A/B testing).

### Campaign Objectives

| Objective | Purpose |
|-----------|---------|
| Lead Generation | Capture B2B leads via LinkedIn Lead Gen Forms — auto-sync to GHL CRM |
| Website Traffic | Drive verified clicks to a landing page |

### Ad Formats
- Single Image
- Single Video
- Carousel (unique headline + URL per card)

**Ad components:** Introduction | Description | Headline | CTA | Destination URL

**Live Preview Panel:** confirm desktop and mobile layouts before publishing.

### Audience Targeting
- Mandatory: geographic location
- Optional refinements: Job Title | Industry | Company Size | Education | Skills | Seniority | Interests | Traits
- Up to 3 attribute groups:
  - OR logic within each group
  - AND logic between groups
  - Include or exclude attributes

### Budget & Schedule
- Daily Budget or Lifetime Budget (set at Campaign Group level)
- Optimization: Maximum Delivery (default) | Cost Cap
- Launch: immediately or set start/end dates

### Performance Dashboard
- Go to Ad Manager → Statistics → LinkedIn tab
- Metrics: Impressions | Clicks | CTR | CPC | CPM | CPL | Leads | Spend | Conversions
- Drill down: Campaign Group → Campaign → Ad level
- Pause, resume, or edit campaigns from the dashboard

### Where LinkedIn Leads Go
Leads from LinkedIn Lead Gen Forms automatically appear under **Contacts** with source `LinkedIn Ads`.

---

## How Ad Manager Connects to the Rest of GHL

| Connection | Detail |
|-----------|--------|
| Meta Pixel | Pixel code from Conversions section embedded on Funnels/Website pages |
| Smart Lists | Used as Customer List source when creating Custom Audiences |
| Contacts | Lead data from ad forms synced to GHL contacts |
| Workflows | Ad events (e.g., form submission, conversion) can trigger GHL workflows |
| Funnels/Website | Landing pages tied to ad campaigns — pixel must be embedded |
