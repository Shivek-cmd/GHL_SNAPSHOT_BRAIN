# GHL Guide — Courses: Customization & Branding

**Where in GHL:** Memberships → Site (portal settings) | Memberships → Products → Customize (per-product themes)

---

## Membership Site Settings

The membership site is the branded portal where members log in and access their content.

**Where in GHL:** Memberships → Site

| Setting | Description |
|---|---|
| **Site Name** | Internal label for the portal |
| **Custom Domain** | Branded domain (e.g., `members.yourbusiness.com`) |
| **Logo** | Displayed in the portal header |
| **Favicon** | Browser tab icon |
| **Brand Color** | Primary accent color throughout the portal |
| **Login Page Background** | Image or color behind the login form |
| **Default Language** | Portal interface language |

### Custom Domain Setup

1. Memberships → Site → Custom Domains → **+ Add Domain**
2. Enter the domain or subdomain
3. Add a CNAME record in your DNS provider:
   - **Name/Host:** your subdomain (e.g., `members`)
   - **Value/Target:** GHL's CNAME target shown on-screen
4. Wait for DNS propagation (up to 24–48 hours)
5. GHL auto-provisions SSL once CNAME resolves

**Default portal URL (no custom domain):** `[sub-account-name].gohighlevel.com/courses/`

### Navigation Tabs

Configure tabs visible to logged-in members:
- **Library** — shows all offers/products the member has access to
- **Community** — links to a connected GHL Community group
- **Custom Tab** — link to any internal or external URL

---

## Product Themes

Each product can have its own visual theme. Themes control the look of the course page and lesson pages.

**Where in GHL:** Memberships → Products → select product → Customize

### Selecting a Theme

1. Open the product → Click **Customize**
2. Browse the theme gallery — system themes and user-created options appear
3. Click **Apply** on a theme to use it as-is, or click **Customize** to modify it first

**Default theme:** Classic (applied to all new products)

### Theme Settings

After clicking Customize, two categories of settings are available:

**Theme Settings Properties (global for the theme):**

| Property | What it controls |
|---|---|
| Primary Color | Buttons, icons, progress indicators, titles |
| Secondary Color | Instructor info and descriptions |
| Primary Font | Buttons, icons, major titles |
| Secondary Font | Instructor details and descriptive text |
| Logo placement | Header or hero section positioning |

**Product Page Sections:**
- **Header:** background color, alignment
- **Hero:** size, course title/description formatting, background, button content
- **Lesson Progress:** background, font, progress bar color
- **Course Body:** category/lesson fonts, descriptions, backgrounds
- **Instructor:** background, heading, name, title, bio formatting

**Lesson Page Sections:**
- **Lesson Body:** title, description, button, next-lesson customization
- **Course Navigation:** category, lesson, highlight, breadcrumb styling
- **Instructor:** same formatting as product page

**Important:** Section-level customizations override theme settings. Use "Reset to Default" to revert a section.

### Saving Themes

- **Save Changes** — stores as a draft at the product level only; not globally available
- **Save Theme** — makes customizations available globally across the location for reuse on other products
- Saving a modified template globally does NOT retroactively update products already using that theme — reapply the theme to existing products to pick up changes

---

## Neo Classic Theme Customizer

The Neo Classic Theme has an expanded customizer with more control over individual page components.

**How to access:**
1. Memberships → Products → select product → Customize → Browse System Templates
2. Select **Neo Classic** Theme
3. Make modifications using the available sections

**Sections in the Neo Classic Customizer:**

### Logo (Mandatory)
- Show/Hide toggle
- Type: Text or Image
- Action: Redirect to Site Home or Product Home
- Height: Small | Medium

### Search Bar (Mandatory)
- Show/Hide toggle
- Helper text
- Background and text color overrides

### Hero Section (Mandatory)
- Show/Hide toggle
- Background: image or solid color with overlay (color + opacity)
- Course title and description with text formatting
- Spacing: Full Height | Medium | Small
- Start button text and color override

### Welcome Body (Add Section)
Add content blocks below the hero:
- **Image Block:** upload image with click action URL
- **Text Block:** alignment, color, bold/italic
- **Video Block:** direct upload
- **Custom Block:** combines text, image, CTA button, and video

### Course Syllabus (Mandatory)
- Show/Hide toggle
- Organize by Categories or Posts
- Customizable labels ("Coming Soon", "Show More" text)

### Course Sidebar
**Progress Bar:** Show/Hide, color override, custom text

**Instructor Section:** Show/Hide, headshot upload, name/title/bio customization

**Cross-Sell Section:** Promote additional offers — customizable CTA text

**Custom Blocks:** Text, image, CTA button with full styling control

### Lesson Page (within Neo Classic)
- Breadcrumb navigation Show/Hide
- Player background color override
- Auto-advance toggle
- Lesson body text alignment and color

### Category Page (within Neo Classic)
- Sidebar progress bar Show/Hide and color override
- Text overrides with tooltip support

**Save as Template:** Click "Save as Template" in the theme editor → name it → access from "My Templates" on the main Customize screen

---

## Whitelabel Membership App (PWA)

A Progressive Web App (PWA) delivers a mobile app-like experience from the browser — no App Store submission required.

**Where in GHL:** Memberships → Courses → Settings → App Settings tile

### PWA vs Native App Comparison

| Feature | PWA | Native App |
|---|---|---|
| Installation | Browser-based, no app store | App Store / Google Play |
| Updates | Automatic on page refresh | Manual update required |
| Offline use | Limited to cached content | Full functionality |
| Push notifications | Android supported; limited iOS | Fully supported |
| Store approval | None | Subject to store review |
| Cost to publish | None | Developer fees |

### Setup

**Before enabling PWA:**
1. Upload logo, select colors, add favicon in Memberships → Settings → Branding
2. Create products and offers in Memberships
3. (Optional) Set a custom domain in Settings → Domains

**Enable PWA:**
1. Memberships → Courses → Settings → App Settings
2. Toggle **Enable PWA** ON
3. Configure:
   - **Name:** full app title shown during installation
   - **Short Name:** abbreviated version for home screens
   - **Description:** brief app purpose
4. Upload icons: 512 × 512px and 192 × 192px in .jpg or .png
5. Select brand colors from the predefined palette (custom hex codes not currently supported)
6. Save

**Installation by device:**
- **Windows (Chrome):** click install icon in address bar
- **Mac (Chrome):** use download option when logged in
- **Android:** open Chrome → Add to Home Screen
- **iOS:** use Safari 11.3+ → follow the onscreen popup

**App Store submission:** Possible using third-party tools like PWABuilder or Capacitor — requires additional development work outside GHL.

---

## Email Notification Preferences for Courses

Instructors can control which automated emails are sent to members.

**Manageable notification types:**
- Course sign-up email
- Offer access email
- Drip content unlock email
- Course comment notification email
- New course materials unlocked email

**Where to configure:** Memberships → Courses → Settings → Email Settings

**Important:** If you build a welcome email inside a Workflow, the system automatically disables the default Welcome Email from Membership settings. Use only one method to deliver welcome communications — do not use both.

---

## Member Login: Password Setup & Reset

**First-time access (after purchase or workflow enrollment):**
1. Member receives an automated email with a magic login link
2. They click the link → prompted to create their own password
3. Redirected to their course/membership dashboard

**Forgotten password:**
1. Member goes to the login page → clicks "Forgot Password"
2. Enters their email → receives a reset link valid for **2 hours**
3. Creates new password → auto-logged in

**Security option:** Members can invalidate all active sessions across devices during password reset if account compromise is suspected.

**Admin note:** Admins cannot reset passwords on behalf of members for security reasons. Monitor email logs if reset emails are not being received — verify domain authentication.

**Magic links bypass the password system entirely** — see `courses-access-workflows.md` for magic link details.

---

## Instructor Profile

**Where to update:** Products → select product → Customize → Instructor Details

Fields: instructor name, title, bio, headshot image (uploaded per product)

Instructor information displays on both the Product page and the Lesson page within the portal (controlled by the theme visibility settings).
