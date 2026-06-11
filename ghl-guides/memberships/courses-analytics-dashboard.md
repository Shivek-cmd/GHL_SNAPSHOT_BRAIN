# GHL Guide — Courses: Analytics & Dashboard

**Where in GHL:** Memberships → Analytics (sub-sections: Member Analytics, Revenue Analytics, Assessments)

---

## Courses Dashboard

The Courses Dashboard is the default landing page for course creators. It provides near-real-time metrics updated every 6 hours.

**Where in GHL:** Memberships → Courses → Dashboard

### Dashboard Sections

**Top & Least Performing Courses**
- Courses ranked by engagement over the past 30 days
- Shows: completion rate %, total enrollment count
- Click-through to detailed course analysis pages

**Revenue Generated**
- Total earnings from the previous 30 days
- Month-over-month percentage comparison
- Completed purchase counts
- Successful upsell conversion numbers

**Average Order Value (AOV)**
- Average order value calculations
- Highest individual transaction amounts
- Period-to-period change percentages

**Course Progress Funnel**
- Learner journey visualization: Sign-up → Course Start → Completion
- Cumulative progression percentages at each stage

**Setup:** Dashboard activates automatically. No configuration required.

**Actions:**
- Pin to sidebar for quick access
- Remove sample data via the menu
- Export 30-day data as CSV

---

## Member Analytics

Member Analytics tracks individual member activity, engagement, and course progress.

**Where in GHL:** Memberships → Analytics → Member Analytics (also accessible via Sites → Membership → Analytics → Member Analytics)

### What Member Analytics Shows

**List view columns:**
- Member name and email
- Start date (enrollment date)
- Last access date
- Login count
- Overall progress percentage

### How to Use

1. Access Memberships → Analytics → Member Analytics
2. Filter by Product or timeframe using the filter options
3. Click the **eye icon** on any member to view detailed progress:
   - Progress per category and lesson
   - Completed vs not-started breakdown
4. Toggle between products and categories to compare engagement
5. Check progress bars to identify struggling members or completion trends
6. Mark specific categories or lessons complete using checkboxes (updates progress bars)
7. Update offers based on member performance data

### Key Use Cases

| Use Case | Action |
|---|---|
| Find disengaged members | Filter by low login count or low progress % |
| Identify struggling learners | Look for high time-in-lesson with low completion |
| Find power users | Filter by high progress % for testimonial outreach |
| Spot dropout points | Compare start vs completion rates per category |
| Course improvement | Identify categories with consistently low completion |

---

## Revenue Analytics

Revenue Analytics provides financial insights on course offer sales.

**Where in GHL:** Memberships → Analytics → Revenue Analytics

### Net Revenue Tab

**Metrics shown:**
- Total units sold in the selected timeframe
- Total revenue generated
- Top 4 offers and their revenue contribution percentages

**Filters available:**
- Date range
- Purchase channel: Membership checkout | Funnel | Upsell checkout

**Use cases:** Track sales volume, monitor revenue across periods, identify top-selling offers

### Compare Offers Tab

Side-by-side analysis of up to 4 offers simultaneously.

**Metrics per offer:**
- Units sold
- Revenue generated

**Filters:** specific offers (up to 4), purchase channel, custom date range

**Use cases:** Benchmark offers against each other, optimize marketing focus on top performers, identify underperforming offers

---

## Assessment Analytics

View quiz and assignment results across all members and products.

**Where in GHL:** Memberships → Analytics → Assessments

### How to Use

1. Memberships → Analytics → Assessments
2. Filter by:
   - **Product** — view results for a specific course
   - **Assessment Result** — filter by status: Processing | Passed | Failed
3. Click the **eye icon** to view individual responses, scores, and question-level detail
4. Click **Export** to download results:
   - ≤ 500 rows: instant browser download
   - > 500 rows: secure email link valid for 24 hours

**Export includes:** submission date, learner email, quiz title, score, pass/fail status, individual question responses

**Access control:** Only Admin or Instructor roles can access the Export button.

---

## Connection to the Rest of the System

| What depends on analytics | How |
|---|---|
| Workflow triggers | "Lesson Completed", "Product Completed" fire based on progress tracked here |
| Smart Lists | Filter contacts by progress-related tags applied via completion workflows |
| Certificates | Issued when completion threshold is met (tracked via analytics) |
| Pipeline stages | Updated via workflows triggered by completion events |
| AI agents | Can reference member progress data stored in custom fields |
