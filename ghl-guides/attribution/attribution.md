# GHL Guide — Attribution

---

## What Attribution Is

Attribution tracks which channel or source brought a contact into HighLevel. It answers the question: "Where did this lead come from?" — so you can see which ads, organic channels, or referral sources are generating the most leads and make informed decisions about where to invest.

Every contact in GHL stores two attribution records simultaneously: **First Attribution** and **Latest Attribution**.

**Where in GHL:** Contacts → select a contact record → Activity tab → bottom right column

---

## First vs. Latest Attribution

| | First Attribution | Latest Attribution |
|---|---|---|
| **What it captures** | The contact's very first recorded interaction with your system | The most recent recorded interaction before or after becoming a contact |
| **Changes over time?** | Never — locked to the first event | Yes — updates every time a new attribution event is recorded |
| **Example** | Contact fills out a Contact Us form via a Google Ad | Same contact later purchases via a Two-Step Order Form from a Facebook Ad |

**Rule:** Latest attribution always reflects the last event. First attribution never changes.

---

## What Events Record Attribution

Attribution is only captured when a contact completes one of these actions **on a HighLevel asset**:

- Form submission
- Survey submission
- Calendar booking
- Chat Widget (after submitting contact info)
- Order Form submission (one-step or two-step)

> Non-HighLevel events (external forms, third-party tools) will not capture attribution data, including UTM parameters.

---

## Attribution Sources

GHL classifies every contact into one of these sources based on URL parameters and referring domain:

| # | Rule Applied | Source Assigned |
|---|---|---|
| 1 | `utm_source` contains `adwords` | **Paid Search** |
| 2 | `gclid`, `wbraid`, `gbraid` (Google click IDs) or `msclkid` (Bing/Yahoo) is present | **Paid Search** |
| 3 | Any UTM parameter present + referring domain is google.com | **Paid Search** |
| 4 | `utm_source` contains `fb_ad`, `linkedin_ad`, `twitter_ad`, or `reddit_ad`; or `ctwa_clid` is present (WhatsApp) | **Paid Social** |
| 5 | Referring domain is a social media site | **Social Media** |
| 6 | Referring domain is a search engine (Google, Yahoo, Bing, DuckDuckGo) | **Organic Search** |
| 7 | Referring domain is present but not social or search | **Referral** |
| 8 | No referring domain and no tracking URL | **Direct Traffic** |
| 9 | Lead came from an inbound call, SMS, email, WhatsApp, or Facebook message | **Others** |
| 10 | Lead manually created inside the GHL CRM | **CRM UI** |
| 11 | Lead created by a third-party tool (e.g., Zapier) | **Third-Party** |

Rules are applied **in this exact order** — the first rule that matches wins.

---

## Source Descriptions

**Paid Search**
Leads from paid search campaigns (Google Ads, Bing Ads). Requires correct UTM parameters on the landing page URL — see UTM setup below.

**Paid Social**
Leads from paid social campaigns (Facebook, Instagram, LinkedIn, Twitter, Reddit Ads). Requires correct UTM parameters — see UTM setup below.

**Organic Search**
Non-paid search traffic from Google, Bing, Yahoo, DuckDuckGo. Keywords may show as "Unknown (SSL)" — search engines encrypt user queries.

**Social Media**
Organic social traffic — contacts who clicked a link shared on a social platform.

**Referral**
Traffic from external websites that link to your site (not search engines or social media).

**Direct Traffic**
No referrer detected — contact typed the URL directly or all query parameters were stripped before landing.

**Others**
Leads generated via inbound channels: calls, SMS, email, WhatsApp, or Facebook messages.

**CRM UI**
Contact was created manually inside the HighLevel CRM by a team member.

**Third-Party**
Contact was created via a third-party integration (e.g., a Zapier zap or external API call).

---

## UTM Parameter Setup

### Google Ads — Required UTM Template

Add this tracking template at the **Account Settings** level in Google Ads (recommended) or at Campaign / Ad Group level:

```
{lpurl}?utm_source=adwords&utm_medium={adname}&utm_campaign={campaignname}&utm_content={adgroupname}&utm_keyword={keyword}&utm_matchtype={matchtype}&campaign_id={campaignid}&ad_group_id={adgroupid}&ad_id={creative}
```

| Parameter | Key | Value | Notes |
|---|---|---|---|
| UTM Source | `utm_source` | `adwords` | Must be exactly `adwords` — case-sensitive |
| UTM Medium | `utm_medium` | `{adname}` | Auto-filled by Google |
| UTM Campaign | `utm_campaign` | `{campaignname}` | Auto-filled by Google |
| UTM Content | `utm_content` | `{adgroupname}` | Auto-filled by Google |
| Match Type | `utm_matchtype` | `{matchtype}` | Auto-filled by Google |
| Campaign ID | `campaign_id` | `{campaignid}` | Auto-filled by Google |
| Ad Group ID | `ad_group_id` | `{adgroupid}` | Auto-filled by Google |
| Ad ID | `ad_id` | `{creative}` | Auto-filled by Google |

Setup path in Google Ads: **Account Settings → Tracking → Tracking Template** → paste the template → run a test.

---

### Facebook & Instagram Ads — Required UTM Parameters

Add UTM parameters in Ads Manager: **Edit Ad → Tracking → Build a URL parameter**

```
{YourLandingPageUrl.com}?utm_source=fb_ad&utm_medium={{adset.name}}&utm_campaign={{campaign.name}}&utm_content={{ad.name}}&campaign_id={{campaign.id}}
```

| Parameter | Key | Value | Notes |
|---|---|---|---|
| UTM Source | `utm_source` | `fb_ad` | Must be exactly `fb_ad` — case-sensitive |
| UTM Medium | `utm_medium` | `{{adset.name}}` | Auto-filled by Facebook |
| UTM Campaign | `utm_campaign` | `{{campaign.name}}` | Auto-filled by Facebook |
| UTM Content | `utm_content` | `{{ad.name}}` | Auto-filled by Facebook |
| Campaign ID | `campaign_id` | `{{campaign.id}}` | Auto-filled by Facebook |

Setup steps in Ads Manager:
1. Edit the ad → scroll to **Tracking** section
2. Click **Build a URL parameter**
3. Set Campaign Source = `fb_ad`
4. Set Campaign Medium = `{{adset.name}}`
5. Set Campaign Name = `{{campaign.name}}`
6. Set Campaign Content = `{{ad.name}}`
7. Click **Add Parameter** → name: `campaign_id`, value: `{{campaign.id}}`
8. Hit **Apply**

> Facebook does NOT add UTM parameters when previewing an ad — this is expected. Parameters only fire on live clicks.

---

## Naming Rules for Paid Ads (Critical)

These apply to both Google and Facebook campaigns:

- Campaign names, Ad sets/groups, and Ads must all be **unique**
- Names **cannot be changed** during the lifetime of the campaign/ad set/ad — if you need to rename, create a new campaign/ad set/ad
- If you rename without creating a new entity, GHL will continue reporting under the original name, skewing your data
- Do **not** add custom UTM parameters beyond the HighLevel templates — doing so can break attribution recording entirely

---

## Attribution Custom Variables

Use these in workflows, templates, or conditions to reference a contact's attribution data:

| Variable | Data |
|---|---|
| `{{contact.attributionSource.utmCampaign}}` | Campaign name |
| `{{contact.attributionSource.utmMedium}}` | Ad set name |
| `{{contact.attributionSource.utmContent}}` | Ad name |
| `{{contact.attributionSource.campaignId}}` | Campaign ID |
| `{{contact.attributionSource.fbclid}}` | Facebook click ID |
| `{{contact.attributionSource.gclid}}` | Google click ID |
| `{{contact.attributionSource.referrer}}` | Referring URL |

> By default, these variables reference **Latest Attribution**. To reference First Attribution, use the First Attribution field on the contact record.

---

## Attribution in Custom Dashboard Widgets

Attribution and UTM parameters can be used as filters and grouping properties on **Contact** and **Opportunity** widgets in custom dashboards.

**Adding attribution as a filter:**
1. Edit Dashboard → Add Widget → select Contact or Opportunity widget
2. Go to **Conditions tab** → Add Condition → choose **Attribution**
3. Select **First** or **Latest** attribution
4. Click **Add Attribution Fields** → choose the UTM property to filter by

Supported UTM fields for widget conditions:
`utm_campaign`, `campaign_id`, `utm_content`, `utm_keyword`, `utm_matchtype`, `utm_medium`, `ad_id`, `ad_group_id`, `utm_source`, `Session Source`, `Medium`

**Grouping donut/line charts by attribution:**
- After adding the attribution condition, go to the **Configuration tab**
- Set **Group/View By** to `Session Source` or `Medium`
- Attribution condition must be added first — Group/View By options only appear after

**Adding attribution columns to a table widget:**
- Select **Table Chart** → click **Select Columns** → add UTM or attribution fields
- UTM columns only appear in the table if an Attribution condition (First or Latest) is already added

---

## Troubleshooting Attribution

**UTM data not recording:**
- Check for spaces, misspellings, or wrong casing in the UTM template — parameters are case-sensitive
- Confirm the contact completed a submission action (form, calendar, order form) on the exact landing page the UTM parameters were on — if they navigated to another page before submitting, UTMs are lost
- Use a pop-up or embedded form on the landing page to keep the contact on the UTM-tagged URL through submission

**First attribution showing empty:**
- First attribution only records on the entry point actions listed above (form, survey, calendar, chat widget, order form, inbound click-to-call)
- Inbound calls only record attribution in click-to-call scenarios — not when a contact dials a number pool directly

**Facebook UTMs not visible in ad preview:**
- Expected — Facebook does not inject UTM parameters during ad preview; they only fire on live ad clicks

**Reporting showing wrong campaign after a name change:**
- GHL stores the original campaign name at the time of the click — renaming in Ads Manager does not retroactively update GHL data
- Always create a new campaign/ad set/ad when renaming to avoid mixing historical data
