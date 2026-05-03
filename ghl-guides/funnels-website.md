# GHL Guide — Funnels, Website & Chat Widget

---

## Funnels

**What they are:** Single-goal, linear page sequences designed to convert a visitor into a lead or booking. A funnel has one or more pages in sequence — typically a landing page, an opt-in or booking page, and a thank-you page. Unlike a website, a funnel has no navigation — visitors move through it in one direction.

**Where in GHL:** Sites → Funnels → + New Funnel

---

### How to Build a Funnel

1. Sites → Funnels → + New Funnel
2. Name the funnel — descriptive name, reflects the campaign or offer
3. The funnel is created with one default page — add pages with + New Page
4. Each page has a path (e.g., `/book`, `/thank-you`) and a page builder

**Page builder elements:**
- Sections → Rows → Columns → Elements
- Elements include: Text, Image, Video, Button, Form, Calendar (embed), Countdown Timer, Social Proof
- Form elements embed a GHL form — forms must be created in Sites → Forms before embedding
- Calendar elements embed a calendar booking widget — calendar must exist before embedding

**Page settings per page:**
- SEO title and description
- Custom header/footer code (for tracking pixels, Meta Pixel, Google Tag, etc.)
- Custom CSS
- Tracking codes — add Meta Pixel, Google Analytics tag here

**Funnel-level settings:**
- Custom domain — connect a domain in Settings → Domains before assigning to a funnel
- Funnel URL — default is a GHL subdomain; custom domain replaces it

---

### CTAs and Trigger Links

Buttons on funnel pages can link to:
- The next step in the funnel (internal step link)
- A calendar booking URL — always use `{{custom_values.booking_link_[calendar]}}` not a hardcoded URL
- A trigger link — see Workflows guide for how trigger links work
- An external URL — must use a custom value if it's a business URL

Never hardcode any URL directly in a button. If the URL ever changes, every page using it must be updated manually. With custom values, one edit updates everywhere.

---

### Technical Constraints

- Funnels do not share pages with other funnels — each funnel has its own pages
- Funnel pages do not have GHL's navigation/header/footer unless you build them manually on each page
- Funnel domains are separate from website domains — same domain can power both but requires subdomain routing
- A/B testing is available on funnel pages (split traffic between two variants)
- Funnel statistics track page views, opt-ins, conversion rate per step
- Mobile responsiveness must be manually checked — the builder has a mobile preview mode
- Embeds (forms, calendars) inherit their own settings — ensure the embedded component is configured before publishing

---

### What Must Exist Before Building Funnels

- All forms that will be embedded
- All calendars that will be embedded
- All custom values for URLs, business name, phone, address, offer details
- Custom domain registered and pointing to GHL (if using custom domain)

---

## Website

**What it is:** A full multi-page website built inside GHL. Unlike funnels, websites have a shared navigation header and footer, multiple pages under one domain, and are designed for browsing rather than linear conversion.

**Where in GHL:** Sites → Websites → + New Website

---

### How to Build a Website

1. Sites → Websites → + New Website
2. Name the website
3. Configure settings: domain, favicon, global header/footer code (tracking pixels go here — applied to all pages)
4. Build pages using the same page builder as funnels
5. Navigation: Website → Navigation → add menu items linking to pages

**Key difference from funnels:** Websites share a navigation bar and footer. The navigation is built once and applies to all pages. Funnels have no shared navigation.

**Pages to consider:**
- Home page
- Services / Treatments page
- About / Team page
- Contact page
- Booking page (embeds a calendar)
- Blog (GHL has a native blog builder under Sites → Blog)
- Sitemap and privacy policy pages (good practice; required for GDPR)

---

### Technical Constraints

- Website and funnel can coexist on the same domain using path routing (e.g., `/` for website, `/book` for funnel)
- Website pages must be published individually — draft state does not make the page live
- GHL's blog is separate from websites but uses the same domain
- Form and calendar embeds work the same way as in funnels
- Website does not auto-generate a sitemap for search engines — submit manually to Google Search Console if SEO matters

---

### What Must Exist Before Building the Website

- All forms and calendars to be embedded
- All custom values used in page content (business name, phone, address, hours)
- Custom domain configured in Settings → Domains
- Tracking pixel IDs if needed (Meta Pixel ID, Google Tag ID)

---

## Chat Widget

**What it is:** A floating chat button that appears on website and funnel pages. When a visitor clicks it, it opens a chat conversation that routes to either a live agent, an automated bot, or GHL's Conversation AI.

**Where in GHL:** Settings → Chat Widget → + Add Widget

---

### How to Configure the Chat Widget

1. Settings → Chat Widget → + Add Widget (or edit default widget)
2. **Widget Appearance:**
   - Icon style, color (match brand)
   - Position on screen (bottom-right recommended)
   - Widget title and greeting message
   - Agent avatar image
3. **Widget Behavior:**
   - Show on: All Pages / Specific Pages (whitelist by URL pattern)
   - Hide on: specific page URLs
4. **Chat Type:**
   - Live Chat — goes to GHL Conversations inbox for a human agent
   - Bot — connects to Conversation AI (must be configured first)
   - Email Capture — ask for email before starting chat
5. **Domain Setup:**
   - Allowed domains — list every domain where the widget will appear
   - Without this, the widget code will be rejected by GHL

**Installing on website/funnels:**
- After configuring, GHL generates an embed code snippet
- For GHL websites and funnels: Install via Settings → Chat Widget → Website Snippet → copy the script tag → paste into the website/funnel's header code section
- For external websites: paste the script tag into the site's HTML `<head>` or before `</body>`

---

### Connecting to Conversation AI

If using the Chat Widget as the entry point for Conversation AI:
1. First configure Conversation AI (Settings → Conversation AI) — see AI Agents guide
2. Return to Chat Widget settings
3. Set Chat Type to Bot
4. Select the Conversation AI bot
5. The widget will now hand off to the AI agent when a visitor opens it

**Build order dependency:** Configure the chat widget first (appearance, domain), then connect Conversation AI after the AI agent is built. Do not skip the widget configuration step just because the AI isn't built yet.

---

### Technical Constraints

- One sub-account can have multiple chat widgets (one per use case or domain)
- Widget appearance cannot vary by page — if you need different behavior on different pages, use different widgets
- Live chat requires someone in the GHL Conversations inbox to respond — no auto-response without Conversation AI or a workflow
- Widget loads asynchronously — it does not block page load
- Mobile: the chat widget stacks on top of other page elements on small screens; test on mobile after installation
- If Conversation AI is not configured and Chat Type is set to Bot, visitors will get no response
