# GHL Guide — Custom Data
## Custom Values · Custom Fields · Tags · Smart Lists

---

## Custom Values

**What they are:** Business-level variables stored once and referenced everywhere. When the snapshot is installed in a new sub-account, the client fills these in once — every template, workflow, funnel, and AI script that references them updates automatically.

**Where in GHL:** Settings → Custom Values → + Add Value

**How to create:**
1. Settings → Custom Values → + Add Value
2. Enter a name (this becomes the key)
3. Enter a default value (leave blank in the snapshot — the client fills it in)
4. Save

**How to reference in content:** `{{custom_values.key_name}}`
- Spaces in the name are replaced with underscores in the merge tag
- Example: a value named `Business Name` is referenced as `{{custom_values.business_name}}`

**Technical constraints:**
- No limit on number of custom values
- Values are sub-account level — shared across all contacts and workflows
- Keys are immutable after creation — renaming requires deleting and recreating
- Nested structure not supported — flat key/value only
- Cannot be used as workflow trigger conditions — only for content substitution

**What references custom values:**
- Email templates (subject lines and body)
- SMS templates
- WhatsApp templates
- Funnel and website pages
- AI agent scripts (conversation prompts, welcome messages)
- Calendar confirmation/reminder messages
- Workflow wait messages and notes

**Change impact:** If a custom value key changes, every template and page referencing that key will break silently — it renders blank instead of erroring. Always audit templates after renaming.

---

## Custom Fields

**What they are:** Per-contact data fields that extend GHL's default contact record. Used to store information specific to this industry or business — things like date of birth, last appointment date, insurance provider, treatment stage.

**Where in GHL:** Settings → Custom Fields → Contact (or Lead, Company depending on object type)

**How to create:**
1. Settings → Custom Fields → Select object (Contact is most common)
2. + Add Field
3. Choose field type (see types below)
4. Enter label — this becomes the display name
5. The field key is auto-generated from the label (can be edited)
6. Save

**Field types available:**
- Text — single line free text
- Text Area — multi-line free text
- Number — numeric only, supports decimals
- Date — date picker, stores as ISO date
- Dropdown — single select from predefined list
- Multi-select — multiple options from predefined list
- Checkbox — true/false boolean
- Radio — single select (visual difference from dropdown only)
- File Upload — stores file URL
- Signature — capture digital signature
- Monetary — currency-formatted number

**Naming convention:** Always prefix with the industry abbreviation — `dental_`, `gym_`, `spa_` etc. This prevents collision when merging with other snapshots and makes field lists readable.

**How to reference in workflows and templates:**
- `{{contact.field_key}}` — field key is shown in the custom field settings
- Example: a field keyed `dental_insurance_provider` → `{{contact.dental_insurance_provider}}`

**Technical constraints:**
- Fields are scoped to the object type they're created under — Contact fields cannot be used on Opportunity objects
- Dropdown/multi-select options are defined at creation — can be edited later but in-use values remain as-is
- Checkbox fields return `true` / `false` as strings in workflow conditions
- Date fields store UTC — display timezone is sub-account level
- File Upload fields store a URL to the uploaded file, not the file itself
- No formula or computed fields — values must be set explicitly via workflow or form

**What references custom fields:**
- Forms (each field maps to a custom field)
- Workflow conditions (`if contact.field = value`)
- Smart list filters
- Email/SMS/WA template merge tags
- AI agent conditional logic

**Change impact:** Changing a field key breaks every merge tag and workflow condition referencing it. Change the label freely; change the key only if nothing references it yet.

---

## Tags

**What they are:** String labels applied to contacts. Tags are the primary nervous system for triggering workflows, filtering smart lists, and tracking lifecycle stage. A contact can have any number of tags simultaneously.

**Where in GHL:** Tags apply through workflows. They are managed/viewed under Contacts → Tags (sub-account level tag list).

**How to create tags:** Tags do not need to be pre-created. When a workflow action adds a tag that doesn't exist, GHL creates it automatically. However, document all planned tags in the system design before building — inconsistent tag names cause ghost contacts that no workflow catches.

**How to apply tags:**
- Workflow action: Add Tag (single tag per action; chain multiple actions for multiple tags)
- Workflow action: Remove Tag
- Manually from the contact record

**How tags trigger workflows:**
- Workflow trigger: Tag Added → specify exact tag name
- Workflow trigger: Tag Removed → specify exact tag name
- Workflow condition: Contact Tag → Is / Is Not → [tag name]

**Naming convention:** kebab-case only — `lead-new`, `appt-scheduled`, `appt-completed`, `no-show`, `treatment-plan-open`. No spaces, no underscores, no capitals.

**Technical constraints:**
- Tags are case-insensitive in GHL — `Lead-New` and `lead-new` are the same tag
- Tags are global to the sub-account — one tag list shared across all contacts
- Tag names cannot be changed after creation without breaking existing workflow triggers — delete and recreate
- A single contact can hold unlimited tags
- Workflow trigger fires once per tag-add event — if the same tag is added twice, the trigger fires twice
- Tags are not pipelines — they track state cheaply but don't provide the stage history that a pipeline does

**Tag categories to think about when designing:**
- Lifecycle stage (where is this contact in the journey)
- Source (how did they enter the system)
- Appointment state (scheduled, confirmed, completed, no-show, cancelled)
- Product/service interest (which service are they interested in)
- Communication preference or opt-out status
- Special flags (VIP, emergency, referral-source, payment-overdue)

**Change impact:** Renaming a tag breaks every workflow trigger and condition that references it. The old tag stays on existing contacts; new contacts get the new tag. You end up with a split population. Always rename a tag by creating the new one, updating all workflows, then removing the old one.

---

## Smart Lists

**What they are:** Saved contact filters. A smart list is a dynamic view — it shows every contact that currently matches the filter conditions. It updates in real time as contacts enter and leave the conditions.

**Where in GHL:** Contacts → (apply filters) → Save as Smart List

**How to create:**
1. Contacts → Apply filter(s) using the filter bar
2. Combine multiple filters (AND/OR logic)
3. Click Save → give the smart list a name
4. The list appears in the left sidebar under "Smart Lists"

**Filter types available:**
- Tag — Is / Is Not / Contains / Does Not Contain
- Custom Field — equals, not equals, contains, greater than, less than, is empty, is not empty
- Pipeline Stage — contact is in specific stage of specific pipeline
- Date conditions — created date, last activity, appointment date
- Source — where contact came from
- Contact standard fields — name, email, phone, address

**Technical constraints:**
- Smart lists are read-only views — you cannot bulk-edit contacts from a smart list directly (though you can select → bulk action)
- Maximum filter depth is not officially documented but complex filters (8+ conditions) can slow load
- Smart lists update in real time but large sub-accounts may have a few minutes of lag
- Cannot use smart lists as workflow triggers — they are for manual review and operational visibility only
- Smart list names must be unique within the sub-account

**When to build smart lists:**
- Build core smart lists (based on tags and pipeline stages) early in the build sequence — they validate that pipeline stages and tags are named correctly
- Add workflow-specific and pipeline-specific lists after workflows are running — some lists only make sense once automation is active and populating contacts

**Operational uses:**
- Daily dashboards for staff (e.g., "Today's Appointments", "Open Treatment Plans", "Overdue Balances")
- Quality checks (e.g., "Contacts With No Tag", "Leads Not Contacted in 7 Days")
- Campaign audiences (e.g., "Patients Not Seen in 18 Months", "Implant Interest")
- Handoff lists (e.g., "Awaiting Insurance Verification")

**Change impact:** If a tag is renamed or a pipeline stage is renamed, smart lists filtering on those values will silently return zero results — they don't error, they just become empty. Always update smart list filters when tags or stage names change.
