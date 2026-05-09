# GHL Guide — Knowledge Bases

**What they are:** Structured information sources that AI agents draw from when answering questions. The AI reads the knowledge base at runtime to answer FAQs, describe services, explain policies, and handle objections — without hallucinating details the knowledge base doesn't contain.

**Where in GHL:** AI Agents → Knowledge Base (newer UI) | Settings → Knowledge Base (older UI)

---

## Knowledge Base UI

The Knowledge Base UI uses a tabbed, summary-first layout with a centralized component shared across products for consistency.

**Landing page:** View all existing KBs, create new ones, open a KB to manage its sources.

**Summary View:** Each KB opens with a summary showing connected sources and overall structure — a quick snapshot of what's in it without opening individual tabs.

**Tabbed Data Sources:** Each source type (Web Crawler, FAQ, Tables, Rich Text, File Upload, Web Search) appears as its own tab. Each tab shows the count of connected items and actions to add or manage. New source types appear as additional tabs as GHL releases them.

**Who sees management controls:** Admins and Editors. Viewer-only users can consume content but do not see management controls.

> This UI update does not change how content is written, permissions, indexing logic, AI behavior, or existing KBs and sources.

---

## Content Types

Each KB can contain multiple content types mixed together. All types appear as tabs inside the KB editor.

### FAQ

- Question and answer pairs
- Best for: specific questions the AI is frequently asked
- Keep answers concise (1–3 sentences) — the AI reads the full answer, so long answers increase response time
- Can have unlimited FAQ entries per KB
- When a user asks something matching or similar to an FAQ, the bot returns the exact configured response — more reliable than web-crawled content for high-stakes answers

### Rich Text

- Formatted text content — headings, bullet points, paragraphs — added directly in the editor
- Best for: service descriptions, policies, about-the-business content, hours, location
- Maximum 5 Rich Text sections per KB

### Tables (CSV / Table Search)

- Upload a CSV file and the AI can answer natural-language questions about the data — no SQL or formulas required
- Best for: pricing grids, service comparison, staff directory, schedule grids, customer records, inventory, product catalogs
- Uses semantic similarity matching — "Which customers have overdue invoices?" works without exact keyword matches
- Each row is converted to vector embeddings so the AI understands meaning, not just text

**CSV file requirements:**
- Format: .csv only (UTF-8 recommended)
- Max file size: 50 MB
- Max rows: 50,000 | Max columns: 500 (select the 20 most relevant for indexing)
- First row must contain column headers
- Remove null values, hidden formulas, merged cells before uploading
- Excel (.xlsx) not supported — export as CSV first

**After upload:** Indexing completes within a few minutes. Rows that informed an answer appear in the Response Info sidebar for verification. Only bots linked to the KB containing the Table Source can query that data.

### Web Crawler

- GHL crawls a URL and imports the content into the KB
- Best for: pulling in existing FAQ pages, service pages, about pages, or any public website content
- Maximum 50 URLs per crawl per KB
- Crawled content is a snapshot — if the website changes, the KB does not auto-update; re-crawl to refresh

**Enhanced Web Crawler (current version):**
The crawler now mimics real visitor interactions — expanding accordions, clicking tabs, scrolling, and revealing dynamically loaded content — capturing 30–50% more on-page content than basic crawlers.

- Works with static HTML, WordPress, React SPAs, Vue, Angular, Gutenberg, and any modern site type
- Extracts hidden content: accordions, tabs, modals, lazy-load and infinite-scroll sections
- Safe interaction engine: avoids form submissions, filter changes, cart actions — no accidental clicks
- Recursive sitemap crawling: discovers nested sitemaps and compressed sitemap files (.xml.gz, .gzip)
- Navigation guard: keeps crawl within the intended scope, reduces drift
- Parallel extraction: 12+ content-detection strategies running simultaneously for speed
- Crawl success rate: ~94.7% across business, ecommerce, and modern interactive sites
- Detailed metrics per crawl: processing time, interactions, content length, memory usage

**Crawl domain types:**
| Type | What it crawls |
|------|----------------|
| Exact URL | Only the specific page entered |
| All URLs with the Path | All pages sharing that URL path (e.g., /marketing/\*) |
| All URLs in this Domain | All pages under the root domain |

**How to add a Web Crawler source:**
1. AI Agents → Knowledge Base → open or create a KB
2. Click **+ Add Source** → Web Crawler
3. Choose domain type → enter the URL → click Extract Data
4. Once crawl completes → View All Pages → select URLs → click Train Bot

### File Upload

- Upload a document and the AI extracts and chunks the content for search
- Best for: brochures, treatment guides, policy documents, PDFs, presentations
- Supported formats: PDF, DOC/DOCX, PPT/PPTX, TXT
- Content is indexed automatically after upload — no retraining required; new data is available on the next query

---

## Smart Retrieval & Source Attribution

### Re-Ranking

A ranking layer sits between the initial search and the AI's answer generation. After the vector search returns potential matches, the re-ranker scores each chunk for semantic closeness to the user's question and sends only the top-ranked passages to the model. This reduces hallucinations and keeps answers tight and on-topic.

### Response Info (Source Attribution)

Every AI response in GHL Conversations shows a **Response Info** icon. Click it to open the side drawer and view:
- The exact knowledge chunk(s) used to generate the answer
- File or URL name, FAQ label, and timestamp
- Up to 3 chunks per response
- Quick-edit options to correct or replace a source on the spot

This applies to all source types — tables, rich text, files, FAQ, and web-crawled content.

---

## Knowledge Base Triggers (Conversation AI)

Knowledge Base Triggers control when specific KB content is used during a Conversation AI conversation. Instead of the AI always deciding freely, triggers activate at defined moments to surface the right content.

**Where to configure:** AI Agents → Conversation AI → select bot → Bot Training tab

### Always-On Trigger

Always active — baseline knowledge the bot can draw on in any conversation. Use for:
- Brand messaging and positioning
- General offers and pricing ranges
- Business hours and contact details
- Common FAQs and policies

If no Smart Trigger conditions are met, the Always-On trigger handles the response.

### Smart Triggers

Activate when specific conditions are met. Each agent supports up to 3 Smart Triggers (plus the 1 Always-On).

| Example | Condition | Content to surface |
|---------|-----------|-------------------|
| Real estate | After budget, location, preferences are shared | Relevant property listings |
| High-ticket sales | When objections or hesitation are expressed | Case studies |
| Appointment booking | When contact signals readiness to book | Booking instructions, calendar link |

**How to write trigger conditions:**
- Use plain natural language
- Focus on a specific conversation moment (qualification complete, objection raised, price asked)
- Avoid overlapping conditions between triggers
- Attach only relevant KBs to each trigger

**How to set up:**
1. AI Agents → Conversation AI → select bot → Bot Training tab
2. Configure Always-On trigger with general KBs — remove highly specific content from it
3. Click **Add Trigger** → name it → write the condition → attach relevant KBs → Save
4. Test in the preview window: simulate real conversations, verify which KB fires and when
5. Add up to 3 Smart Triggers covering different stages (qualification, objections, pricing, booking)

### Trigger Limits

| Limit | Value |
|-------|-------|
| Total triggers per agent | 4 (1 Always-On + 3 Smart) |
| Knowledge Bases per trigger | Up to 7 |
| Knowledge Bases per Conversation AI agent | Up to 4 (across all triggers combined) |
| Knowledge Bases per Voice AI agent | 1 |

### How to Structure KBs for Triggers

Create separate KBs for distinct content areas, then attach them to the right trigger:

| KB | Attach to |
|----|-----------|
| General FAQs | Always-On |
| Product / service information | Always-On |
| Case studies and testimonials | Smart Trigger (objection/hesitation) |
| Policies and compliance | Always-On |
| Pricing details | Smart Trigger (price inquiry) |
| Onboarding / implementation guides | Smart Trigger (post-booking) |

> Broad content → Always-On. Specific content → Smart Triggers. This improves accuracy and makes maintenance easier.

---

## Knowledge Base Limits

| Agent Type | Max KBs attached |
|------------|-----------------|
| Conversation AI | 4 per agent |
| Voice AI | 1 per agent |

**Design implications:**
- A Conversation AI agent with broad coverage (FAQs + services + policies + booking info) may need all 4 KB slots
- A Voice AI agent must be focused — its one KB should contain only what's needed for phone calls (keep it tight)
- The single Voice AI KB must cover both inbound and outbound call scenarios

---

## Building a Knowledge Base

1. AI Agents → Knowledge Base → **+ Create Knowledge Base**
2. Name it — use naming convention `KB-##: Name` — add a description
3. Click **+ Add Source** → choose a content type → add content
4. Review: the AI answers based only on what's in the KB — if something isn't there, the AI should say it doesn't know rather than guess. Keep content accurate and current.
5. Attach to an AI agent during agent configuration (Bot Training tab)

**Note for Conversation AI:** After attaching a KB, assign it to a trigger (Always-On or a Smart Trigger) to control when that KB is consulted.

---

## What Must Exist Before Building Knowledge Bases

- Business information (name, hours, address, phone) finalized — these go into KB content
- Services list confirmed — service descriptions go into KB
- FAQs drafted and reviewed — accuracy matters here; wrong AI answers damage trust
- CSV files cleaned and ready if using Table Search (remove nulls, merged cells, hidden formulas)
- Website URLs confirmed live and public if using Web Crawler (login-gated pages cannot be crawled)
