# GHL Guide — Memberships

**What it is:** GHL's built-in platform for selling and delivering digital courses, membership programs, and gated content. A fully hosted portal where members log in, access products, track progress, and complete lessons — all inside the same sub-account without any third-party tool.

**Where in GHL:** Memberships (left sidebar) — contains Products, Offers, Site, Analytics, Members, and Certificates sections.

---

## Core Architecture

```
Membership Site (portal — the login page members see)
│
└── Offer (the thing you sell — price + access bundle)
    │
    └── Product (the course or content library)
        │
        ├── Category (section/module inside the product)
        │   └── Post (individual lesson — video, text, file, quiz)
        │
        └── Category
            └── Post
```

**The relationship in plain terms:**
- A **Post** is one lesson or content piece
- A **Category** groups posts into a module or section
- A **Product** is the full course or membership content — made of categories and posts
- An **Offer** is what you sell — it bundles one or more products together with a price and access rules
- The **Membership Site** is the branded portal where members log in and access their offers

A member buys (or is granted) an **Offer**. The offer gives them access to its **Products**. Inside each product they see **Categories** and **Posts**.

---

## Products

**What they are:** The actual content library. A product is the course, membership vault, or content hub. It contains categories (sections) and posts (lessons).

**Where in GHL:** Memberships → Products → + New Product

### Creating a Product

1. Memberships → Products → **+ New Product**
2. Fill in:
   - **Title:** product name shown to members
   - **Description:** summary shown on the product page
   - **Image:** thumbnail shown on the member portal (recommended 1280 × 720px)
   - **Instructor:** team member name shown as the course instructor
3. Click **Save** — the product is now a shell. Build categories and posts inside it.

---

### Categories

Categories are the modules or sections inside a product. They group posts together.

**To add a category:**
1. Open the product → **+ Add Category**
2. Name it (e.g., "Module 1: Foundation", "Week 1", "Getting Started")
3. Add a description (optional — shows to members above the lesson list)
4. Reorder categories by dragging — order is the order members see them

**Category visibility:**
- **Visible** — members can see the category and its posts (subject to drip rules)
- **Hidden** — category is not shown in the portal even if access is granted

---

### Posts (Lessons)

Each post is one lesson inside a category. Posts can contain multiple content blocks stacked vertically (video + text + file, etc.).

**To add a post:**
1. Open the category → **+ Add Post**
2. Name the post
3. Add content blocks (see Content Types below)
4. Set post settings: free preview toggle, drip schedule
5. Save

**Post Settings:**
- **Free Preview:** when ON, this post is visible without purchasing the offer — used for sample lessons
- **Lesson Completion Button:** members must click "Complete & Continue" to mark the post done and unlock the next one

---

### Content Types (per post)

Each post can stack multiple content blocks in any combination:

| Content Type | Description |
|---|---|
| **Video** | Embed from Vimeo, YouTube, Wistia, Loom, or upload directly to GHL storage |
| **Text / Rich Text** | Formatted text — headings, bullet points, bold, links, inline images |
| **Audio** | Upload an MP3 or audio file — plays inline with a built-in player |
| **Image** | Static image displayed inline |
| **PDF / File** | Upload downloadable files — PDFs, worksheets, templates, zip files |
| **Quiz** | Multiple-choice or short-answer assessment (see Quizzes section below) |
| **Assignment** | Open-ended submission — member types or uploads an answer for review |
| **Code Block** | Display formatted code snippets (useful for technical courses) |
| **iFrame / Embed** | Embed any external tool or page via iframe URL |

**Video upload limits:** GHL-hosted video supports files up to 4 GB. Vimeo, YouTube, Wistia, and Loom embeds have no GHL-side size limit — just paste the URL.

---

### Drip Content

Drip controls when a post or category becomes accessible after a member enrolls. Without drip, all content is available immediately on enrollment.

**Drip is set per post or per category.**

**Drip options:**

| Type | How it works |
|---|---|
| **No drip** | Content is available immediately on enrollment |
| **Specific date** | Unlocks on a fixed calendar date — same date for all members regardless of when they enrolled |
| **Days after enrollment** | Unlocks X days after the member was granted access to the offer |
| **Days after completing previous post** | Unlocks X days after the member marks the previous post complete |

**How to set drip:**
1. Open the post or category → Settings (gear icon)
2. Toggle **Drip** ON
3. Select drip type and enter the value
4. Save

**Drip by category vs by post:**
- Setting drip on a category locks all posts inside it until the category unlocks
- Setting drip per post gives finer control — each post has its own schedule
- Both can be combined — category unlocks on day 7, then individual posts inside it drip day by day

**What members see when content is dripped:**
- The locked category or post appears in the portal but shows a lock icon and the unlock date
- Members cannot access the content until the drip condition is met

---

### Quizzes

Quizzes are content blocks added inside posts. They are assessment tools — members answer questions to test understanding or unlock the next lesson.

**How to add a quiz:**
1. Inside a post, click **+ Add Content Block** → **Quiz**
2. Add questions — each question can be:
   - **Multiple Choice** — add 2–10 answer options, mark the correct one(s)
   - **Short Answer** — member types a response (no auto-grading — admin reviews manually)
3. Set quiz settings:
   - **Pass Percentage:** minimum correct score to pass (e.g., 80%)
   - **Required to Complete Lesson:** if ON, member must pass the quiz to mark the lesson complete
   - **Show Correct Answers:** display correct answers to members after submission
   - **Attempts Allowed:** unlimited or a fixed number

**Quiz results are stored per member** and viewable in Memberships → Members → select member → Quiz Results.

---

### Certificates

Certificates are awarded to members on product or offer completion. GHL generates a downloadable certificate PDF.

**Where in GHL:** Memberships → Certificates

**How to create a certificate:**
1. Memberships → Certificates → **+ New Certificate**
2. Design the certificate:
   - Upload background image or use GHL template
   - Add text blocks — supports merge tags:
     - `{{member.name}}` — member's full name
     - `{{product.title}}` — product name
     - `{{certificate.issued_date}}` — date the certificate was issued
   - Add signatures, logos, borders
3. Attach the certificate to a product:
   - Open the product → Settings → Certificate → select the certificate template
4. Set completion condition:
   - **100% posts completed** — member must complete every lesson
   - **Specific percentage** — member must complete X% of lessons

**Certificate issuance fires a workflow trigger:** Certificates Issued (see Workflow Integration below).

---

## Offers

**What they are:** The packaged product for sale. An offer defines what the member gets (which products), how much they pay (pricing), how they access it (immediately or dripped), and for how long (lifetime or subscription).

**Where in GHL:** Memberships → Offers → + New Offer

### Pricing Types

| Pricing Type | How it works |
|---|---|
| **Free** | No payment required — member is granted access on signup |
| **One-Time Payment** | Single charge — lifetime access (or until revoked) |
| **Subscription** | Recurring charge — daily, weekly, monthly, or annual — access continues while subscription is active |
| **Trial + Subscription** | Free or reduced-price trial period, then transitions to the full subscription price |
| **Payment Plan** | Fixed number of installments — e.g., 3 × $100 — access granted on first payment |

### Access Types

| Access Type | How it works |
|---|---|
| **All Products** | Member gets access to every product currently in the offer |
| **Specific Products** | Select which products this offer grants access to |
| **Dripped by Offer** | Products unlock on a schedule relative to enrollment — set per product inside the offer |

### Creating an Offer

1. Memberships → Offers → **+ New Offer**
2. Fill in:
   - **Name:** internal label
   - **Title:** shown to members on the portal
   - **Description:** summary shown at checkout or on the offer page
   - **Image:** cover image shown on the portal
3. **Pricing:** select pricing type → fill in amount, currency, billing interval (if subscription)
4. **Trial:** toggle ON to add a trial period → set length and trial price (or $0)
5. **Products:** add products this offer includes — reorder by drag
6. **Access:** set access type (all products or specific) + drip schedule per product (if applicable)
7. **Upsell / Order Bump:** attach an upsell or bump offer shown at checkout
8. **Thank You Page:** custom page shown after successful purchase (or redirect URL)
9. **Custom Domain:** link to a specific membership site domain
10. Save → GHL generates a checkout URL for this offer

**Checkout URL:** Every offer gets a unique checkout URL. Share it directly, embed in funnels, or link from any page.

**Connecting offers to GHL payments:**
- Offer pricing is handled by GHL's built-in payment processor (Stripe required)
- Payments feed into Payments → Transactions
- Subscription offers create a subscription record in Payments → Subscriptions
- `Payment Received` workflow trigger (Source = Memberships) fires on every successful charge

---

## Membership Site

**What it is:** The member-facing portal. The branded login page and dashboard where members access their offers and track progress.

**Where in GHL:** Memberships → Site

### Site Settings

| Setting | Description |
|---|---|
| **Site Name** | Internal label for this portal |
| **Custom Domain** | Connect a branded domain (e.g., `members.yourbusiness.com`) — requires DNS CNAME pointing to GHL |
| **Logo** | Displayed in the portal header |
| **Favicon** | Browser tab icon |
| **Brand Color** | Primary accent color used throughout the portal |
| **Login Page Background** | Image or color behind the login form |
| **Default Language** | Sets the portal interface language |

### Custom Domain Setup

1. Memberships → Site → Custom Domains → **+ Add Domain**
2. Enter the domain or subdomain (e.g., `members.yourbusiness.com`)
3. Log into your DNS provider — add a CNAME record:
   - **Name/Host:** `members` (or your chosen subdomain)
   - **Value/Target:** GHL's CNAME target (shown on screen after adding the domain)
4. Wait for DNS propagation (up to 24–48 hours)
5. GHL auto-provisions SSL once the CNAME resolves

**The default GHL portal URL** (without custom domain): `[sub-account-name].gohighlevel.com/courses/`

### Navigation Tabs

The portal can display custom navigation tabs visible to members after login:

- **Library** — shows all offers/products the member has access to
- **Community** — links to a connected GHL Community group
- **Custom Tab** — link to any internal or external URL (e.g., a support page, booking link, Zoom room)

---

## Member Management

**Where in GHL:** Memberships → Members

**Member table columns:** Name | Email | Enrolled Date | Offers | Progress | Last Login

**Actions per member:**
- View enrolled offers and products
- View lesson-by-lesson progress (completed / not started)
- View quiz results
- Grant or revoke access to an offer
- Reset progress on a product
- Export member data (CSV)

### Granting Access Manually

To add a member to an offer without them paying:
1. Memberships → Members → **+ Add Member** (or find existing contact)
2. Select the contact → select the offer → set access duration (lifetime or expiry date)
3. Click **Grant Access**
4. This fires the **Offer Access Granted** workflow trigger

This is the method used in workflows via the **Course Grant Offer** action — it does the same thing automatically.

### Revoking Access

- Memberships → Members → find member → select offer → **Revoke Access**
- Or via workflow: **Course Revoke Offer** action
- Revoking fires the **Offer Access Removed** workflow trigger
- Member's progress data is retained — only access is removed

---

## Workflow Integration

Memberships fires workflow triggers and responds to workflow actions. Build these workflows after the offers and products are set up.

---

### Workflow Triggers (Memberships / Courses)

**New Signup**
Fires when a new member account is created (first purchase or first grant of any offer).
Filters:
- Offer: Is | Is Not → select offer name
- Product: Is | Is Not → select product name

**Offer Access Granted**
Fires when a member is granted access to a specific offer — whether via purchase, manual grant, or workflow action.
Filters:
- Offer: Is | Is Not → select offer name

**Offer Access Removed**
Fires when a member's access to an offer is revoked.
Filters:
- Offer: Is | Is Not → select offer name

**Product Access Granted**
Fires when access to a specific product is granted.
Filters:
- Product: Is | Is Not → select product name

**Product Access Removed**
Fires when access to a specific product is removed.
Filters:
- Product: Is | Is Not → select product name

**Product Started**
Fires when a member opens the first lesson inside a product (first engagement).
Filters:
- Product: Is | Is Not → select product name

**Product Completed**
Fires when a member completes 100% of posts inside a product.
Filters:
- Product: Is | Is Not → select product name

**Category Started**
Fires when a member opens the first lesson inside a category.
Filters:
- Product: Is | Is Not → select product name
- Category: Is | Is Not → select category name

**Category Completed**
Fires when a member completes all posts inside a category.
Filters:
- Product: Is | Is Not → select product name
- Category: Is | Is Not → select category name

**Lesson Started**
Fires when a member opens a specific post/lesson.
Filters:
- Product: Is | Is Not → select product name
- Category: Is | Is Not → select category name
- Post: Is | Is Not → select post name

**Lesson Completed**
Fires when a member marks a specific post/lesson complete.
Filters:
- Product: Is | Is Not → select product name
- Category: Is | Is Not → select category name
- Post: Is | Is Not → select post name

**User Login**
Fires each time a member logs into the membership portal.
Filters:
- Offer: Is | Is Not → select offer name

**Certificates Issued**
Fires when a certificate is generated for a member on product completion.
Filters:
- Certificate: Is | Is Not → select certificate name

---

### Workflow Actions (Memberships / Courses)

**Course Grant Offer**
Grants a contact access to a membership offer without requiring payment. Used for: free onboarding, manual enrollments, bonus access, gifted courses, and access recovery.
Fields:
- Action Name: label this action
- Offer: select the offer to grant access to
- Access Expiry: Lifetime | Custom Date | Days After Enrollment

**Course Revoke Offer**
Removes a contact's access to a membership offer. Used for: subscription cancellations, payment failures, access expiry, and disciplinary removal.
Fields:
- Action Name: label this action
- Offer: select the offer to revoke access from

---

### Common Workflow Patterns

| Pattern | Trigger | Actions |
|---|---|---|
| Welcome new member | Offer Access Granted | Send email (ET-##), add tag `member-active`, move pipeline to "Member Enrolled" |
| Drip engagement nudge | Lesson Completed (module 1 final lesson) | Wait 1 day → Send SMS encouraging Module 2 |
| Course completion celebration | Product Completed | Send email with certificate download link, add tag `course-complete`, update pipeline |
| Subscription cancellation | Offer Access Removed | Send email (re-engagement), add tag `churned-member`, move pipeline to "Churned" |
| Failed payment recovery | Payment Received (Source = Memberships, Status = Failed) | Send SMS payment failed, wait 24 hours, send email with update link |
| Re-engagement | User Login (after 14-day wait condition with no logins) | Send check-in SMS, assign task to team member |

---

## Technical Constraints

- A product can have unlimited categories and posts
- Drip schedules apply per-member from their individual enrollment date (days-after-enrollment type) — not a global date
- Members can only access the portal via the membership site URL — content is not publicly accessible
- GHL does not support SCORM or xAPI files — use video + quiz blocks as the alternative
- Video hosted on GHL is not downloadable by members — they can only stream
- Certificate PDF generation requires the member to complete the defined threshold — it does not auto-generate; members download it from their portal dashboard
- A member's progress resets only via manual admin action or a workflow using custom code — there is no built-in "reset progress" workflow action
- Subscription access is tied to the subscription record — if a subscription is paused or cancelled in Payments → Subscriptions, access is not automatically revoked; pair with a workflow on Subscription trigger to revoke access
- Multiple offers can grant access to the same product — a member who buys two offers that both include Product A sees Product A once in their library (no duplicates)
- Memberships does not support team accounts or multi-seat pricing natively — each member needs a unique contact/login

---

## Connection to the Rest of the System

**Memberships depends on:**
- **Stripe integration** — required for paid offers (one-time, subscription, payment plan)
- **Products catalogue** (Payments → Products) — offer prices sync with the product/price catalogue
- **Custom Values** — used in certificate merge fields and post content
- **Email/SMS Templates** — referenced by workflows triggered from membership events
- **Pipelines** — track member lifecycle stages (lead → enrolled → completed → churned)
- **Tags** — workflow conditions and smart list filters for member segments

**What depends on Memberships:**
- **Workflows** — all membership event triggers feed into automation sequences
- **Payments → Transactions** — every offer purchase records a transaction
- **Payments → Subscriptions** — subscription offers create subscription records
- **Communities** — membership portal navigation can link to a GHL Community group
- **Certificates** — issued on product completion and stored in the member's record
- **Smart Lists** — filter contacts by membership tag, pipeline stage, or custom field set via membership workflows

**Build order:**
1. Design products (categories + posts) first — content drives everything else
2. Create offers and attach products — set pricing and drip rules
3. Configure the membership site — domain, branding
4. Build email/SMS templates for member communications
5. Build pipelines for member lifecycle tracking
6. Build workflows using membership triggers (enrollment, completion, churn)
7. Test with a real contact: purchase or manually grant offer → verify portal access → complete a lesson → verify workflow fired
