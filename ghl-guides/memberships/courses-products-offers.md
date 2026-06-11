# GHL Guide — Courses: Products & Offers

**Where in GHL:** Memberships → Products (to build content) | Memberships → Offers (to sell content)

---

## Products

A Product is the full course or content library. It contains Categories (sections/modules) and Posts (individual lessons). Members access products through Offers — they never buy a product directly; they buy an Offer that grants product access.

**Where in GHL:** Memberships → Products → + Create Product

### Creating a Product

1. Memberships → Products → **+ Create Product**
2. Fill in:
   - **Title:** product name shown to members
   - **Description:** shown on the product page in the portal
   - **Image:** thumbnail (recommended 1280 × 720px)
   - **Instructor:** team member shown as the course instructor
3. Save — the product shell is created. Build categories and posts inside it.

---

### Categories

Categories are the modules or sections inside a product. They group posts together.

**To add a category:**
1. Open the product → **+ Add Category**
2. Name it (e.g., "Module 1: Foundation", "Week 1", "Getting Started")
3. Add a description (optional — shows above the lesson list)
4. Reorder categories by dragging

**Category visibility:**
- **Visible** — members can see the category and its posts (subject to drip rules)
- **Hidden** — category not shown even if access is granted

---

### Posts (Lessons)

Each post is one lesson inside a category. Posts can stack multiple content blocks (video + text + file + quiz, etc.).

**To add a post:**
1. Open the category → **+ Add Post**
2. Name the post
3. Add content blocks
4. Set post settings: free preview toggle, drip schedule
5. Save

**Post settings:**
- **Free Preview:** when ON, this post is visible without purchasing — used for sample lessons
- **Lesson Completion Button:** members click "Complete & Continue" to mark done and unlock the next post
- **Lock icon:** marks post as requiring prior completion to access

**Post status options:** Published | Draft | Locked

---

## Content Types Per Post

Stack multiple content blocks in any order inside a post:

| Content Type | Description |
|---|---|
| **Video** | Embed from Vimeo, YouTube, Wistia, Loom — or upload directly (max 4 GB per file) |
| **Text / Rich Text** | Formatted text — headings, bullet points, bold, links, inline images |
| **Audio** | Upload MP3, AAC, or WAV — plays inline with a built-in player |
| **Image** | Static image displayed inline |
| **PDF / File** | Uploadable downloadable files — PDFs, worksheets, templates, zip files |
| **Quiz** | Multiple-choice or short-answer assessment |
| **Assignment** | Open-ended submission — member types or uploads an answer for review |
| **Code Block** | Formatted code snippets |
| **iFrame / Embed** | Embed any external tool or page via URL or iframe code |

**Video upload:** GHL-hosted video supports files up to 4 GB. External embeds (Vimeo, YouTube, Wistia, Loom) have no GHL-side size limit — paste the URL.

**Thumbnail for posts:** Instructors can upload a custom thumbnail image per lesson, or pick a specific video frame from within the video player to use as the lesson thumbnail.

---

## Drip Content

Drip controls when a post or category becomes accessible after enrollment. Without drip, all content unlocks immediately.

**Drip options (set per post or per category):**

| Type | How it works |
|---|---|
| **No drip** | Content available immediately on enrollment |
| **Specific date** | Unlocks on a fixed calendar date — same for all members |
| **Days after enrollment** | Unlocks X days after the member was granted access |
| **Days after completing previous post** | Unlocks X days after member completes the prior post |

**How to set drip:**
1. Open the post or category → Settings (gear icon)
2. Toggle **Drip** ON
3. Select drip type and enter value
4. Save

**Important:** Drip value of "0" is not allowed — system blocks saving invalid drip values.

**What members see when dripped:** Locked content appears in the portal with a lock icon and the unlock date.

**Admin preview:** In Neo Classic Theme, admins can toggle between locked and unlocked views in Preview Mode to verify drip behavior without affecting live members.

---

## Quizzes & Assignments

Quizzes and Assignments are post content blocks used to assess members.

**Quiz settings:**
- **Question types:** Multiple Choice (mark correct answers) | Short Answer (manual review, no auto-grade)
- **Pass Percentage:** minimum correct score required (e.g., 80%)
- **Required to Complete Lesson:** member must pass to mark the lesson done
- **Show Correct Answers:** display correct answers after submission (only when no passing grade is required — with passing grade enabled, members see if answers were correct/incorrect but not the correct answers)
- **Attempts Allowed:** unlimited or fixed number

**Assignment settings:**
- Title and instructions
- **Ungraded Assignment** toggle — if enabled, no grading required
- Upload supporting document templates
- Custom confirmation message shown after submission

**Viewing results:** Memberships → Analytics → Assessments — filter by Product or Result Status (Processing, Passed, Failed). Export as CSV (instant for ≤500 rows; email link for >500 rows).

**Reuse:** Assessments are product and location-specific — they cannot be reused across products.

---

## Offers

An Offer is what members buy. It bundles one or more products together with a price, access rules, and duration.

**Where in GHL:** Memberships → Offers → + Create Offer

### Pricing Types

| Pricing Type | How it works |
|---|---|
| **Free** | No payment required — member granted access on signup |
| **One-Time Payment** | Single charge — lifetime access (or until revoked) |
| **Subscription** | Recurring charge — daily, weekly, monthly, or annual |
| **Trial + Subscription** | Free or reduced-price trial, then transitions to full subscription |
| **Payment Plan** | Fixed installments (e.g., 3 × $100) — access granted on first payment |

**Note on payment plans:** If you set a subscription offer with X payments, the subscription ENDS and CANCELS automatically after the number of payments selected.

### Offer Access Types

| Access Type | How it works |
|---|---|
| **All Products** | Member gets every product currently in the offer |
| **Specific Products** | Select which products this offer includes |
| **Dripped by Offer** | Products unlock on a schedule relative to enrollment date |

### Offer Duration

Set time-limited access or a fixed start date:

**Restrict to specific number of days:**
- Enable "Restrict access to specific amount of days" in Offer Access settings
- Enter validity period in days (e.g., 6 months = 180 days, 1 week = 7 days)
- System automatically revokes access when the period ends

**Begin access at specific date:**
- Enable "Begin access at specific date" in Offer Access settings
- If members register before the start date, they see the overview page but cannot access lessons until the activation date

Both options can be combined — a start date AND an expiry duration on the same offer.

### Creating an Offer

1. Memberships → Offers → **+ Create Offer**
2. Fill in:
   - **Name** (internal), **Title** (shown to members), **Description**, **Image**
3. **Pricing:** select type → fill in amount, currency, billing interval
4. **Trial:** toggle ON → set trial length and trial price ($0 for free trial)
5. **Products:** add products → reorder by drag
6. **Access:** set type (all / specific) + drip schedule per product
7. **Upsell / Order Bump:** attach upsell shown at checkout
8. **Thank You Page:** custom URL or page shown after purchase
9. **Custom Domain:** link to a specific membership site
10. Save → GHL generates a unique checkout URL

### Taxes on Course Offers

Taxes connect course checkout to GHL's Payments tax engine.

**Setup path:**
1. Payments → Settings → Taxes → Enable automatic tax toggle ON
2. Add nexus addresses (countries/states where you collect tax)
3. Payments → Products → set Product Tax Code on each course product
4. Choose tax-inclusive or tax-exclusive pricing (global or per product)
5. Test: open offer checkout → enter billing address in a nexus region → verify tax line items display

**Manual taxes:** Create manual rates in Payments → Settings → Taxes → Add Tax. Attach to products for jurisdictions not covered by automatic taxes.

**Coupons + tax:** Coupons reduce the taxable subtotal first; taxes calculate on the discounted amount.

---

## Checkout Orchestrator

GHL's rebuilt checkout pipeline for course offer transactions.

**Performance:**
- Reduces checkout time to 3–4 seconds (previously 8–12 seconds)
- 100% duplicate prevention — one charge per order guaranteed
- Up to 5 automatic retries with exponential back-off on failures
- Live transaction traces at Memberships → Checkouts → Activity Log

**No configuration needed** — applies automatically to all existing offers and funnels.

**Testing:**
1. Memberships → Offers → select offer → Checkout → Preview Checkout → process a $0 test order
2. Memberships → Checkouts → Activity Log — verify "Success" status

---

## Connecting an Offer to GHL Payments

Offer pricing is handled through GHL's product catalogue (Payments → Products):

1. Payments → Products → **+ Create Product**
2. Fill in title, pricing (one-time or recurring), amount, currency
3. Enable **Membership Offer** toggle → select the published offer from dropdown

**Critical:** Only published offers appear in the Membership Offer dropdown. Publish the offer before linking the product.

4. Save — members who purchase this product automatically receive access to the linked offer

After purchase:
- Transaction records in Payments → Transactions
- Subscription records in Payments → Subscriptions (for recurring offers)
- `Payment Received` workflow trigger fires (Source = Memberships)

---

## Managing Comments on Lessons

Comments on lessons can be enabled, hidden, or locked per category or per individual post.

**Comment states:**
- **Enabled:** comment box visible; members can post new comments and see existing ones
- **Hidden:** no comment box visible; no comments shown
- **Locked:** no new comments allowed; existing comments still visible

**To manage:**
1. Products → select product → Comments section → select category or individual lesson
2. Set state per category (applies to all posts inside it) or override per post

**Global comment manager:** Products → Manage Comments
- Change visibility: **User Only** (only the member and creator see the comment) | **Public** (all students and creator)
- Delete or restore comments (deleted comments go to a "Deleted" tab and can be restored)

**In-app notifications for comments:** Members receive bell icon alerts, email, and push notifications when someone replies to their comment. Instructors receive notifications about learner comments via the Client Portal Notifications tab.

---

## Pushing Updated Offers to Existing Members

When you update an offer (add a new product, change access rules), existing members who already purchased the offer do not automatically receive the update. You must push the updated offer to their accounts manually or via workflow.

**Use the Course Grant Offer workflow action** targeting existing members with a filter on their enrollment tag to re-grant access under the updated offer terms.

---

## What Must Exist Before Building Products & Offers

- Custom Values for any dynamic content inside post descriptions or quiz questions
- Payment processor connected (Stripe) — required for paid offers
- Team member profiles — for instructor attribution
- Tax settings configured (Payments → Settings → Taxes) — required for tax-enabled offers
