# GHL Guide — Smart Lists & Advanced Filters

---

## What Smart Lists Are

Smart Lists are saved contact views built from one or more filters. They are dynamic — the list updates automatically as contacts meet or stop meeting the filter conditions. They are not static exports. A contact added today that meets the filters appears in the list immediately. A contact who no longer meets the filters drops off automatically.

**Where in GHL:** Contacts → Filters → Save as Smart List

---

## How to Build a Smart List

1. Go to **Contacts**
2. Click **Filters** (top right of the contacts table)
3. Add your filter conditions
4. Click **Save as Smart List**
5. Name it using the convention `Category — Description` (e.g., `Newsletter — Active`)
6. Save — the list appears in the left sidebar under Smart Lists

---

## Filter Logic — AND vs OR

GHL smart list filters support two logic modes:

**AND logic (Nested Filters):**
- All conditions must be true for a contact to appear
- Use when you need to narrow down (e.g., has tag AND email is not empty)

**OR logic (Add Filter — separate filter blocks):**
- Contact appears if any one condition is true
- Use when you need to broaden (e.g., came from Form A OR came from Form B)

You can combine both: multiple conditions inside one block use AND; multiple blocks use OR between them.

---

## Filter Categories

GHL filters are organized into five types. The operators available depend on which field you select.

---

### 1. Date Filters

Used to segment contacts by when something happened.

**Relative date operators:**
| Operator | What it matches |
|----------|----------------|
| Today | Activity on the current date |
| Tomorrow | Activity scheduled for tomorrow |
| Yesterday | Activity from the previous day |
| This Week | Activity within the current calendar week |
| This Month | Activity within the current month |
| This Quarter | Activity within the current quarter |
| This Year | Activity within the current calendar year |

**Exact date operators:**
| Operator | What it matches |
|----------|----------------|
| On | Specific date exactly |
| Between | A date range (start date → end date) |
| After Date | Any date after the specified date |
| Before Date | Any date before the specified date |

**Rolling window operators:**
| Operator | What it matches |
|----------|----------------|
| More Than [X] Ago | Activity older than X days/weeks/months |
| Less Than [X] Ago | Activity within the last X days/weeks/months |
| In the Next [X] | Activity scheduled within the next X days/weeks/months |
| In the Last [X] | Activity within the past X days/weeks/months |

**Empty operators:**
| Operator | What it matches |
|----------|----------------|
| Is Empty | No date recorded in this field |
| Is Not Empty | A date exists in this field |

**Every date operator also has an "Is Not" inverse** for exclusion logic.

**Common date fields available:**
- Created On
- Last Activity On
- Last Email Opened Date
- Last Appointment At
- Date of Birth
- Any custom date field

---

### 2. DND Filters (Do Not Disturb)

Used to include or exclude contacts based on their opt-out status per channel.

**Operators:**
| Operator | What it matches |
|----------|----------------|
| Enabled | Contact has opted out of this channel |
| Disabled | Contact has not opted out |

**DND fields available:**
- DND All (opted out of all channels)
- Email DND
- SMS DND
- Calls & Voicemails DND
- WhatsApp DND
- FB Messenger DND
- GMB Messenger DND
- Inbound DND

**Key use:** Always filter `Email DND = Disabled` or `Email Unsubscribe Status = Subscribed` when building newsletter or email campaign audiences to exclude opted-out contacts.

---

### 3. String Filters

Used to match contacts based on text-based fields — names, emails, tags, IDs, attribution, pipeline info, and custom text fields.

**Operators:**
| Operator | What it matches |
|----------|----------------|
| Is | Exact single value match |
| Is Not | Excludes one specific value |
| Contains | Partial text match anywhere in the field |
| Does Not Contain | Excludes contacts where the field contains the text |
| Is any of | Matches any of the listed values (comma-separated) |
| Is None of | Excludes all listed values (comma-separated) |
| Is Empty | Field has no value |
| Is Not Empty | Field has any value |

**Common string fields available:**
- First Name
- Last Name
- Email
- Phone
- Address, City, State, Country, Postal Code
- Timezone
- Tags (add/remove tag-based filters)
- Email Status (Subscribed / Unsubscribed)
- Last Updated By
- Source (where contact came from)
- Opportunity Pipeline name
- Opportunity Stage name
- Custom Fields: single-line text, multi-line text, dropdown, radio button, checkbox, text box list

---

### 4. Numeric Filters

Used to segment contacts by measurable number values.

**Operators:**
| Operator | What it matches |
|----------|----------------|
| Equal To | Exact numeric match |
| Does Not Equal | Excludes a specific number |
| Between | Numeric range (min → max) |
| Greater Than | Values strictly above the threshold |
| Greater Than or Equal To | Values at or above the threshold |
| Less Than | Values strictly below the threshold |
| Less Than or Equal To | Values at or below the threshold |
| Is Empty | Field has no value |
| Is Not Empty | Field has a value |

**Common numeric fields available:**
- Engagement Score
- Custom Fields: number type, monetary type
- Quiz scores (if mapped to custom numeric fields)

---

### 5. Opportunity Filters

Used to segment contacts by their pipeline, stage, or opportunity status.

**Common opportunity filters:**
- Opportunity Pipeline: Is / Is Not → select pipeline name
- Opportunity Stage: Is / Is Not → select stage name
- Opportunity Status: Is / Is Not → Open / Won / Lost / Abandoned
- Opportunity Value: numeric operators (Greater Than, Less Than, Between, etc.)
- Opportunity Created On: date operators
- Opportunity Last Stage Change: date operators

---

## Common Smart Lists to Build in Any System

| Smart List Name | Filters | Use |
|----------------|---------|-----|
| Newsletter — Active | Email Is Not Empty AND Email DND = Disabled | Weekly newsletter audience |
| Leads — New | Tag = `lead-new` | New unworked leads |
| Leads — No Response | Tag = `lead-new` AND Created On > 3 days ago | Leads not yet contacted |
| Appointments — Upcoming | Last Appointment At = In the Next 7 days | Reminder sequences |
| Appointments — No Show | Tag = `appt-no-show` | Re-booking follow-up |
| Customers — Active | Tag = `customer-active` | Retention campaigns |
| Newsletter — Engaged | Tag = `newsletter-engaged` | High-open-rate audience |
| Newsletter — Cold | Tag = `newsletter-cold` | Re-engagement campaigns |
| Unsubscribed — Email | Email DND = Enabled OR Email Status = Unsubscribed | Audit / cleanup |

---

## Newsletter — Active Smart List (Full Spec)

**Name:** `Newsletter — Active`

**Filters (AND logic):**

| Field | Operator | Value |
|-------|----------|-------|
| Email | Is Not Empty | — |
| Email DND | Disabled | — |

**How to build:**
1. Contacts → Filters
2. Add filter → **Email** → **Is Not Empty**
3. Add filter → **DND** → **Email DND** → **Disabled**
4. Save as Smart List → name: `Newsletter — Active`

**Behavior:**
- Every new contact with an email address appears automatically
- Anyone who clicks unsubscribe or is marked Email DND drops off automatically
- No manual maintenance ever needed
- Use this as the audience for every weekly newsletter campaign

---

## Key Rules

- Smart Lists update in real time — no manual refresh needed
- A contact can appear in multiple smart lists simultaneously
- Smart Lists cannot trigger workflows directly — use a tag or scheduler to connect them to automation
- Deleting a Smart List does not delete the contacts inside it
- Smart Lists are viewable and usable from Marketing → Email Campaigns as audience targets
