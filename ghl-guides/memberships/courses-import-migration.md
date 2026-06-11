# GHL Guide — Courses: Import & Migration

**Where in GHL:** Memberships → Products → Create Product → Import (for Kajabi) | Memberships → Products → select product → Import Content (for same-account imports)

---

## Kajabi Importer

Migrate courses from Kajabi to GHL's course platform.

**Where in GHL:** Memberships → Courses → Products → Create Product → **Import**

### Before You Start

- Avoid using custom CSS in Kajabi before migrating — it can interfere with the import
- Create theme backups before starting so you can restore if needed
- Schedule imports during off-hours to minimize disruption to active learners
- Recommended themes for imported courses: **Encore Site** (Library) and **Premier Product** (Products section)

### Import Process

**Step 1: Create a Learner Profile in Kajabi**
- Create a new learner account in Kajabi (not admin — a dedicated import account)
- Return to GHL importer → enter the associated email and password
- Enter the learner domain (the login page URL)
- Click **Import**

**Step 2: Import Running**
- System logs in as the learner and begins course migration
- Click **Refresh** for accurate status updates
- Click **Cancel** to stop the process
- You can switch browser tabs but do NOT close the window
- Videos, images, and text content all transfer

**Step 3: Completion**
- Imported courses appear under Products
- Import timestamp shows completion time

### What Imports Successfully
- Published lessons
- Videos, images, text content
- Categories and nested subcategories
- Content behind "Show More" expandable sections (auto-detected)
- Hidden lessons within nested categories (recursive extraction)

### What Does NOT Import
- Draft (unpublished) lessons — only published lessons are imported
- Assignments and quizzes/assessments — must be recreated manually in GHL
- Custom CSS/JS — must be rebuilt using GHL's theme customizer

### Troubleshooting

| Issue | Solution |
|---|---|
| Authentication errors | Verify domain and credentials are correct |
| Course import failures | Check theme, re-verify credentials, confirm domain uses "/login" path |
| Missing lessons after import | Click Refresh; new detection captures previously hidden expandable content |
| Partial import | Retry — enhanced detection now handles large payloads more reliably |

---

## Import Content from Another Course (Same Account)

Copy categories, posts, and content from one existing product into another product within the same GHL sub-account.

**Where in GHL:** Memberships → Products → select target product → **Import Content**

**Use cases:**
- Reuse a module across multiple courses
- Build a new course from a template product
- Copy content from a deprecated product to a new one

---

## Import from Media Storage

Import video or audio files already uploaded to GHL's Media Storage directly into course lessons — no re-upload needed.

**Where in GHL:** Memberships → Products → open a lesson → add content block → **Import from Media Storage**

**Use cases:**
- Reuse existing recordings across multiple courses
- Avoid duplicate uploads when the same video is used in several products

---

## Skool Importer

Migrate a Skool group (community + courses) to GHL's Communities + Courses platform.

**Where in GHL:** Memberships → Communities → Import (or accessible from Communities setup)

**What transfers:** Group content, members, and course structure — specific content coverage depends on Skool's export capabilities at the time of import.

---

## Legacy Membership to Client Portal Migration

For sub-accounts still using the legacy membership system (pre-Client Portal architecture), GHL provides a migration path to the current Memberships platform.

**Key points:**
- The migration is one-way — you cannot revert after migrating
- Member data, course content, and offer structures migrate
- Member login credentials are preserved
- Review member access settings after migration — some legacy access rules may need to be reconfigured under the new Offer system

**When to use:** Only relevant for sub-accounts created before GHL's Client Portal launch that haven't yet migrated to the current Memberships platform.

---

## Pushing Updated Offers to Existing Members

When you modify an offer (add a new product, change access rules, add drip), existing members who already enrolled do NOT automatically receive the update.

**To push updates to existing members:**
1. Identify existing members using a Smart List filtered by membership tag or enrollment custom field
2. Build a workflow:
   - Trigger: Contact Tag Added (or Scheduler — one-time)
   - Action: Course Grant Offer → select the updated offer
3. Run the workflow against the segment of existing members

**Alternative:** Use the "Push Updated Offer" feature if available in your GHL version under Memberships → Offers → three-dot menu.

**Caution:** Re-granting access to an existing member under a modified offer resets their access start date (relevant if the offer has time-limited access). Test with a single contact first before running at scale.
