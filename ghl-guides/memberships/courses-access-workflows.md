# GHL Guide — Courses: Access, Workflows & Magic Links

**Where in GHL:** Automation → Workflows (for access automation) | Memberships → Members (for manual access)

---

## Granting Access

Members get access to an offer in two ways:
1. **Purchase** — they buy the offer at checkout (payment processed by GHL/Stripe)
2. **Manual grant** — admin or workflow grants access without payment

**Manual grant:**
1. Memberships → Members → **+ Add Member** (or search for existing contact)
2. Select the contact → select the offer → set access duration (Lifetime or expiry date)
3. Click **Grant Access**
4. This fires the **Offer Access Granted** workflow trigger

---

## Granting Access via Workflow

The **Course Grant Offer** workflow action automates enrollment at scale.

**Common triggers that feed into Course Grant Offer:**

| Trigger | Use case |
|---|---|
| Payment Received (Source = Memberships) | Grant access after purchase |
| Form Submitted | Grant access after opt-in |
| Tag Added | Grant access when a specific tag is applied |
| Contact Created | Grant free access on first signup |
| Offer Access Granted (another offer) | Grant a bonus course on purchase of a main offer |

**How to build the workflow:**
1. Automation → Workflows → + Create Workflow
2. Set trigger (e.g., Payment Received → Source = Memberships → select offer product)
3. Add action: **Course Grant Offer** → select the offer
4. (Optional) Add: Send Email with welcome content, Add Tag `member-active`, Create Opportunity in pipeline
5. Test → Publish

**Important on welcome emails:** If you include a Send Email (welcome email) inside the workflow, GHL automatically disables the default Welcome Email from Membership settings. Use only one method — workflow email OR membership settings email — not both.

**Revoking access via workflow:**
- Use the **Course Revoke Offer** action
- Common trigger: Subscription cancelled, Payment failed, Tag removed

---

## Workflow Triggers from Memberships / Courses

These triggers fire automatically when members interact with course content:

| Trigger | When it fires | Key filters |
|---|---|---|
| **New Signup** | New member account created (first enrollment) | Offer, Product |
| **Offer Access Granted** | Access granted to an offer (purchase or manual) | Offer |
| **Offer Access Removed** | Access revoked from an offer | Offer |
| **Product Access Granted** | Access granted to a specific product | Product |
| **Product Access Removed** | Access removed from a specific product | Product |
| **Product Started** | Member opens the first lesson in a product | Product |
| **Product Completed** | Member completes 100% of posts in a product | Product |
| **Category Started** | Member opens the first lesson in a category | Product, Category |
| **Category Completed** | Member completes all posts in a category | Product, Category |
| **Lesson Started** | Member opens a specific post | Product, Category, Post |
| **Lesson Completed** | Member marks a specific post complete | Product, Category, Post |
| **User Login** | Member logs into the membership portal | Offer |
| **Certificates Issued** | Certificate generated for a member | Certificate |

---

## Custom Values Available in Course Workflows

Custom values for use in email/SMS templates and workflow actions within membership triggers:

| Value | Tag |
|---|---|
| Member first name | `{{contact.first_name}}` |
| Member email | `{{contact.email}}` |
| Course/Product name | Available via `{{membership.product_name}}` (check current GHL version) |
| Login URL (magic link) | `{{membership.login_url}}` |
| Certificate download URL | Available in Certificates Issued trigger |

**Custom value categories for courses:**
- **Contact-specific:** learner name, individual details
- **Time-based:** time zone adjustments, schedule data
- **Course-specific:** dynamic category or post titles
- **Location-specific:** regional content variations

---

## Magic Links

Magic links are password-free, one-click login URLs that authenticate the member and take them directly to their course content.

**Two types:**

| Type | Who it's for | What it does |
|---|---|---|
| **Learner's Magic Link** | Contacts (members) | Shareable via email/SMS; authenticates and shows only their granted content |
| **User's Magic Link** | Location staff | Functions as custom sidebar menu links only — not for sharing with members |

### Sending Learner Magic Links

**Via Workflow:**
1. Use any membership trigger (New Signup, Offer Access Granted, etc.)
2. Add a Send Email or Send SMS action
3. Insert the **Login Url (Magic Link)** custom value in the message body

**Via Email Campaign:**
- Insert the `Login Url (Magic Link)` custom value in the email body

**How to generate a User Magic Link (for staff):**
1. Memberships → Courses → Settings → Site Details → **Regenerate Magic Link**
2. Copy the link and embed it in the staff sidebar

**Important rules:**
- Links expire when regenerated — old links stop working immediately
- Contacts must have a granted membership offer for the magic link to show their content
- Admin users testing magic links will see ALL courses (admin access). Always test learner-facing links using a contact incognito window instead
- Anyone who has the link can access the course — share only with the intended recipient

---

## Drip Content & Access Schedule

Drip controls when content unlocks after a member is enrolled in an offer.

**Set drip on a post or category:**
1. Open post or category → gear icon → toggle Drip ON → select type → enter value → Save

**Drip types:**

| Type | Behavior |
|---|---|
| No drip | Content available immediately on enrollment |
| Specific date | Unlocks on a fixed calendar date (same for all members) |
| Days after enrollment | Unlocks X days after offer access was granted |
| Days after completing previous post | Unlocks X days after member marks the previous lesson done |

**Validation:** GHL blocks drip values of "0" or other invalid values — must enter a positive integer.

**In-app notifications for drip unlocks:** Members receive bell icon alerts, email, and push notifications when dripped content becomes available.

---

## Offer Duration & Access Expiry

Set time-limited access:

**Path:** Memberships → Offers → select offer → Offer Access settings

- **Restrict access to specific amount of days:** Enter days of validity from enrollment date. System auto-revokes access at end of period.
- **Begin access at specific date:** Members who enroll early see the overview page but cannot access lessons until the activation date.

Both options can be combined.

**When a member upgrades** to a new offer that includes the same product, access extends based on the new offer's validity period.

---

## Member Progress Tracking

**Where in GHL:** Memberships → Members → select member

Visible data per member:
- Lesson-by-lesson progress (completed / not started)
- Quiz results
- Enrolled offers and products
- Last login date

**Admin actions:**
- Grant or revoke offer access
- Reset progress on a product (manual only — no workflow action exists for this)
- Export member data as CSV

---

## What Must Exist Before Building Access Workflows

| Prerequisite | Why |
|---|---|
| Offers (published) | Workflow actions reference specific offer names |
| Products (published) | Triggers filter by product name |
| Email templates | Used in Send Email actions after access granted |
| Tags | Used to filter workflow conditions and smart lists |
| Pipeline stages | Used to track member lifecycle on access events |
