# GHL Guide — Unsubscribe Links in LC Email

---

## What Unsubscribe Links Are

Every email sent via GHL LC Email must contain an unsubscribe link. When a contact clicks it, GHL automatically sets their Email DND to Enabled — removing them from all future email sends and any Smart List filtered by `Email DND = Disabled`.

Unsubscribe links are both a legal requirement (CAN-SPAM, GDPR) and a GHL platform requirement. Sending without one risks account suspension.

---

## Two Methods — Never Use Both Together

### Method 1 — Default Automatic Link

GHL automatically appends an unsubscribe link to the bottom of every email.

**Where to enable:**
Settings → Business Profile → General Tab → Toggle: **Include Unsubscribe Link → ON**

**What it does:**
The unsubscribe message is automatically added to all emails sent from this sub-account. You can customize the surrounding text inside that settings panel.

**When to use:** Simplest option. No manual work inside templates. GHL handles placement automatically.

---

### Method 2 — Manual Tag

Turn off the default and place the unsubscribe link manually inside the template at an exact position.

**Merge tag:**
```
{{email.unsubscribe_link}}
```

**Alternative method (via GHL UI):**
Inside the email builder → Custom Values → EMAIL → **UNSUBSCRIBE LINK**
This inserts the same tag without typing it manually — use this if typing the tag directly isn't being detected.

**How it works:**
When the email is sent, GHL converts `{{email.unsubscribe_link}}` into a live clickable hyperlink automatically.

**Works in:** Both HTML and plain text email templates.

**When to use:** When you have a custom-designed footer and need the link in a specific position with specific surrounding text.

**Example:**
```
You're receiving this because you're part of the Real with Ritesh community.
No longer want these emails? {{email.unsubscribe_link}}
```

---

## Which Method to Use

| Situation | Method |
|-----------|--------|
| Simple emails, no custom footer | Method 1 — Default ON |
| Custom designed footer, branded templates | Method 2 — Manual tag |
| Newsletter with full footer block | Method 2 — Manual tag |
| Text template with tag not being detected | Method 1 — Default ON (most reliable) |

**Never use both methods in the same email.** Two unsubscribe links appear — cluttered design, confuses contacts.

---

## Important: Preview Mode Behavior

The unsubscribe link **never appears in preview mode or test emails.** This is normal GHL behavior — it only renders in the actual live send to real contacts. The preview not showing the link is not a bug.

---

## Warning: "Unsubscribe Link is Missing"

This warning appears in GHL when:
- The default is turned OFF **and**
- No `{{email.unsubscribe_link}}` tag is detected in the template

**How to fix:**
- Option A: Turn the default back ON → Settings → Business Profile → General Tab → Include Unsubscribe Link → ON
- Option B: Insert `{{email.unsubscribe_link}}` into the template — if typing it manually doesn't work, use the GHL UI: Custom Values → EMAIL → UNSUBSCRIBE LINK

If Option B still shows the warning after saving, use Option A — it is the most reliable method and always clears the warning.

---

## Compliance

| Regulation | Requirement |
|-----------|-------------|
| CAN-SPAM Act | Unsubscribe link mandatory in every commercial email |
| GDPR | Right to opt out must be clearly available |
| GHL Platform Policy | No unsubscribe link = account suspension risk |

**Rule:** Every email must have exactly one unsubscribe link — either the default (Method 1) or the manual tag (Method 2). Never zero, never two.

---

## What Happens When a Contact Unsubscribes

1. Contact clicks the unsubscribe link
2. GHL sets **Email DND = Enabled** on that contact automatically
3. Contact drops off any Smart List filtered by `Email DND = Disabled`
4. All future GHL emails skip this contact automatically
5. No manual action needed — fully automatic

---

## For Newsletter — Real with Ritesh

**Recommended: Method 1 (Default ON)**

Settings → Business Profile → General Tab → Include Unsubscribe Link → **ON**

Remove any `{{email.unsubscribe_link}}` tag from the template footer. GHL appends the link automatically below your footer content.

Your footer block:
```
Ritesh Watts
Founder, Aifyze | President, Watts Group Ltd. (Canada)

Watts Group Ltd.
Aifyze @ Watts Group, Suite 209, 120 Traders Blvd E
Mississauga, Ontario, Canada L4Z 2H7

You're receiving this because you're part of the Real with Ritesh community.
```

GHL adds the unsubscribe link automatically below this.
