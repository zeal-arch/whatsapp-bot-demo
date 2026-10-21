# firstbriq Round 2: prep pack

45-minute video call. Three parts: (1) the WhatsApp problem and a lead-management extension,
(2) firstbriq product and website ideas plus global companies, (3) the Indian interiors industry.
They said they care about **how you think**, not polish. So walk them through your reasoning, name
trade-offs, and say "I'd measure that" whenever you are unsure.

---

## 0. One-page cheat sheet (read this just before the call)

**Your 30-second framing of the WhatsApp problem**
> "The project manager is acting as a human data-entry layer between WhatsApp and the ERP. I'd build
> a bot that sits in the project's WhatsApp group (or receives forwarded messages), turns every text,
> voice note and bill photo into a structured record such as *who, what item, how many, rate,
> amount, which project*, and posts it to the ERP. The important part is the decision step: the bot
> auto-posts only what it is confident about, sends the rest to a one-tap review queue for the PM,
> and never silently guesses on money."

**Three ideas to repeat**
1. **Refuse rather than guess.** A wrong cost entered automatically is worse than one the PM checks.
2. **Human-in-the-loop that shrinks over time.** Start with the PM approving everything, then let
   the bot auto-post the categories where it proved accurate.
3. **Measure it.** Field accuracy, % auto-posted, how many PM edits, minutes saved per project per week.

**firstbriq in one line (from their public site):** a Bengaluru marketplace that helps homeowners
find *verified* interior designers, with structured portfolios, real timelines and costs, a free
"Homeowner Guide – 9 Traps to Avoid" sent on WhatsApp, and a "Studio" workspace (moodboard, decor
tasks, vendor quotes, an AI copilot).

**Your bridge idea (strongest point to make):** the round-1 WhatsApp bot is the missing link for
firstbriq. Today they help homeowners *choose* a designer. The bot could give homeowners
*transparency after hiring*: what was bought, at what price, against the quote, and progress
milestones, all pulled from the WhatsApp chatter that already happens.

**Questions to ask them at the end** (pick 2):
- Is the WhatsApp bot for designers' internal teams, for homeowners, or both?
- Who is your paying customer today: homeowners, designers (leads/subscription), or brands?
- How do you verify a designer today, and how much of it is manual?
- Which ERP/SaaS would the bot write into: your own or the designers' existing tools (Tally, Excel, Zoho)?

---

## 0.5 What firstbriq is (LinkedIn overview) and how both problems fit

> "firstbriq is India's home interior planning platform. Homeowners use it to estimate costs, plan
> rooms, compare materials, and set realistic budgets, all before talking to a single vendor.
> Interior design firms use it to connect with clients who already know what they want and what they
> can spend."

- firstbriq is **not a chatbot company**. It is a two-sided platform: homeowners plan, and design
  firms get qualified clients.
- **Lead management = their core business** ("better-qualified clients"). Expect deep questions.
- **WhatsApp → ERP bot = likely a SaaS tool for the design firms** ("backend ERP/SaaS tool"), used
  after a client signs. It gives firms a reason to use firstbriq every day, beyond leads.

**The full story to tell:**
Homeowner plans on firstbriq (budget, rooms, materials) → AI qualifies and matches them to the right
firm (lead management) → during the project the WhatsApp bot records purchases and costs → actual
spend is compared with the planned budget → that data improves cost estimates for future homeowners.

**Lead management, starting from firstbriq's own data:** the homeowner has already given budget,
rooms and materials, so the AI only confirms and fills gaps (possession date, location, style,
decision-maker). Score using "finished a plan?", "budget realistic for this scope?", "possession soon?".

**Ask them:** "Is the WhatsApp bot a SaaS product for design firms, or an internal tool?"
**Product observation:** LinkedIn says "planning platform"; the website still reads mostly as
"find verified designers". Is the planning tool the front door?

---

## 1. Technical problem: WhatsApp → ERP extraction bot

### 1.0 Basics: ERP, SaaS, API (know these words cold)
- **ERP (Enterprise Resource Planning):** one central system for a firm's operations, split into
  modules: Projects, Purchase, Inventory, Vendors, Accounts (GST), Budget/Costing, Labour. One
  purchase entry updates project cost, vendor balance, stock and accounts together.
  India: Tally, Zoho Books/Inventory, Odoo, SAP Business One; construction: Onsite, Powerplay, RDash.
  Many small interior firms still run on **Excel + WhatsApp + Tally**.
- **SaaS (Software as a Service):** online software paid monthly, data on the provider's cloud, provider
  does updates. Inside: frontend (screens) → backend (business rules) → database. **Multi-tenant**:
  many firms on one system, each sees only its own data, so every record carries `company_id` + `project_id`.
- **How the bot updates the ERP:** through the ERP's **API**, not the screen:
  `POST /api/purchases {project_id, vendor_id, items, total, source:"whatsapp", message_id}`.

| Term | Meaning | Why it matters for the bot |
|---|---|---|
| API | Door for programs to send/read data | Bot writes purchases, payments, progress |
| Auth (API key / OAuth) | Proof the bot is allowed | Each firm connects its own account |
| Webhook | Other system calls you on an event | WhatsApp → bot on every message; ERP → bot "PM approved" |
| Schema | Fixed fields and types | AI must fill exactly these fields |
| Validation | Check before saving | total = qty × rate? vendor exists? project open? |
| Idempotency | Same request twice = one record | Re-sent webhook or re-forwarded bill must not double cost; key = `message_id` |
| Master data | ERP's lists: vendors, projects, items | Match "Raju bhaiya" → vendor V-221 |
| Draft vs posted | Pending vs final | Bot makes drafts, PM approves → posted |
| Audit trail | Who changed what, when | Each record links to the original message |
| Connector / sync | Keep systems consistent | Zoho via API, Tally via XML/connector, Excel/CSV fallback |
| Rate limits + queue | Max requests/min | Queue absorbs bursts, nothing is lost |

**Tricky questions:**
- *Firm uses Tally (no easy cloud API)?* One internal format + adapters (Zoho API, Tally XML import,
  CSV export fallback). Start with one system, not all.
- *Bot makes a wrong entry?* Money entries start as drafts; one-tap edit/reject; every entry links to
  its message; corrections become test cases.
- *Vendor not in ERP?* Bot suggests "New vendor: Raju Traders?", PM confirms once, auto-matched after.

> **One line:** "The ERP is the source of truth; the bot is a smart data-entry assistant that talks to
> the ERP's API, creates drafts, and lets the PM approve. It saves time without putting wrong numbers
> in the books."

### 1.1 Restate the problem (do this first in the interview)
- Many people (PM, carpenters, material suppliers, electricians, painters, the client) talk in
  WhatsApp groups per project.
- Messages are **mixed**: Hinglish/Kanglish text, regional languages, voice notes, photos of
  handwritten bills, printed GST invoices, site progress photos, PDFs of quotations.
- The PM currently re-types the important bits (purchases, payments, labour, progress) into a sheet
  or ERP. This is slow, error-prone and depends on one person.
- Goal: capture this automatically and update the ERP, **with the bot making decisions** about what
  is important, what it means, and whether it is safe to write.

**Clarifying questions to ask them** (shows good ambiguity handling):
1. One group per project, or one big group for everything?
2. Which records matter most: material purchases, payments to contractors, labour attendance,
   progress, client approvals / change requests?
3. Does the ERP have an API? What is the "source of truth" if the bot and the PM disagree?
4. Is the client (homeowner) in the group? (Affects privacy and what the bot may say out loud.)
5. Scale: how many projects, messages a day, voice notes vs photos?

### 1.2 How messages get to the bot (an important real-world constraint)
| Option | Good | Bad |
|---|---|---|
| **Official WhatsApp Cloud API, bot number in the group** | Legal, reliable, webhooks | Groups API is new and restricted (reported: Official Business Account needed, small group size cap, members join by invite link only). Check Meta's docs before promising it. |
| **Bot as a 1:1 contact: people forward bills / voice notes to it** | Works today with the normal Cloud API; clear intent ("I'm sending this on purpose") | Relies on people remembering to forward |
| **PM uploads a WhatsApp chat export (.txt + media)** daily or weekly | Zero behaviour change, works with any group | Not real-time; batch only |
| Unofficial WhatsApp Web automation | Reads everything | Against WhatsApp's terms, numbers get banned. **Do not propose for production.** |

**Recommendation to say:** start with forwarding to a bot number plus chat-export upload (fast to
ship, no ban risk), and move to the official Groups API where it is available.

### 1.3 Pipeline (draw this if they let you share a screen)
```
WhatsApp message (text / voice / image / PDF)
   │
   ▼
1. Ingest      webhook → queue → store raw message + media (never lose the original)
   │
   ▼
2. Normalise   voice → text  (Sarvam speech-to-text, "codemix"/"translit" mode for Hinglish)
               image → is it a bill, a site photo, a design, or a screenshot?
               bill → OCR + vision model reads the line items
               text → language detect; keep original + English gloss
   │
   ▼
3. Understand  classify intent: purchase / payment / payment request / labour / progress /
               change request / approval / question / chit-chat (ignore)
               extract fields to a fixed JSON schema (below)
   │
   ▼
4. Resolve     "Raju bhaiya", "plywood wala", "Sharma ji" → which vendor in the ERP?
               "same as yesterday", "2 more" → link to earlier message (context window)
               which project? (group id, or ask)
   │
   ▼
5. Decide      confidence + business rules → AUTO-POST | ASK PM | ASK SENDER | IGNORE
   │
   ▼
6. Write       ERP API (idempotent; one message id = one record), audit trail with link to original
   │
   ▼
7. Close loop  short WhatsApp confirmation ("Noted: 20 sheets 18mm ply, ₹54,000, Raju. ✔ / ✏")
               daily digest to the PM; weekly cost vs budget per project
```

### 1.4 The record the bot fills (schema)
```json
{
  "project_id": "PRJ-104 (HSR 3BHK)",
  "event_type": "material_purchase",
  "vendor": {"name_raw": "Raju plywood", "vendor_id": "V-221", "match_confidence": 0.86},
  "items": [
    {"name": "BWP plywood 18mm", "qty": 20, "unit": "sheet", "rate": 2700, "amount": 54000}
  ],
  "total": 54000, "gst": null, "paid": false, "payment_mode": null,
  "room": "kitchen",
  "evidence": {"message_ids": ["wamid..."], "bill_image": "s3://...", "transcript": "..."},
  "confidence": {"overall": 0.78, "amount": 0.95, "vendor": 0.86},
  "status": "needs_review", "reason": "vendor match below threshold"
}
```
Use the LLM's **structured output / JSON schema** mode so the output always matches this.

### 1.5 "The bot has to make decisions": the part you said you lacked depth on
Turn "decisions" into explicit, testable rules:

| Situation | Decision |
|---|---|
| Chit-chat, "ok", "👍", good morning | Ignore (but keep for context) |
| Clear purchase, bill photo, amounts add up, known vendor, within normal price range | **Auto-post**, confirm in chat |
| Amount read from a voice note only (no bill) | Post as *"claimed"*, ask the sender for the bill |
| Bill total ≠ sum of line items, or rate far from the usual rate for that item | **PM review**, show both numbers |
| Vendor or project unclear | Ask one short question in the sender's language ("Ye kaunse site ka bill hai? 1) HSR 2) Whitefield") |
| Same bill sent twice (same image hash or same vendor + amount + date) | Mark duplicate, do not double-count |
| Correction ("sorry 12 nahi 10 sheet") | Update the earlier record, keep history |
| Payment request or change request from a contractor | Never auto-approve; route to PM with summary |
| Anything involving money above a limit (e.g. ₹50k) | Always PM approval in phase 1 |

How confidence is built (not just "the LLM said 0.9"):
- Agreement checks: line items add up; OCR total = vision-model total; voice amount = bill amount.
- Lookups: vendor known? item in catalogue? price within the historical range?
- Model self-reported confidence is the weakest signal; use it last.

Start with **everything goes to PM review** (shadow mode), measure accuracy per event type, and
switch on auto-post one category at a time when it crosses a target (e.g. 98% correct on amounts).

### 1.6 Indian language reality
- People write Hindi in English letters ("2 bori cement bhej do"), English in Devanagari, mix three
  languages, use trade slang (bori = bag, "sutli", "ply", "laminate 1mm", "running feet", "sq ft").
- Build a **domain glossary** (units, materials, brands such as Century Ply, Greenply, Hettich,
  Asian Paints) and give it to the model in the prompt; normalise units (rft, sqft, nos, sheets).
- Voice: Sarvam's speech models (Saaras v3 is the current default; modes include `codemix` and
  `translit`; short REST calls take up to ~30 s audio, a batch API handles longer). Keep both the
  transcript in the original language and an English version.
- Images: handwritten kacha bills are the hardest. Use a vision model (GPT-class, Gemini, or an
  open model such as Qwen-VL) and cross-check totals. Ask for a retake when it is blurry instead of guessing.

### 1.7 Things interviewers love to hear about
- **Cost:** most messages are chit-chat; use a cheap classifier first and call the expensive vision
  model only for bills. Roughly estimate cost per project per month.
- **Latency:** nothing here must be instant; a queue with minutes of delay is fine; a digest
  every evening may be enough.
- **Privacy / law:** India's DPDP Act 2023. Tell group members a bot is present, get consent,
  keep data per company, and delete media after a retention period.
- **Evaluation:** collect 200–300 real messages from 3–4 projects, label them by hand, and measure
  per field (amount, qty, vendor, project). Split by **project**, not by message, so you don't test
  on what you tuned on.
- **Failure modes:** wrong project, double counting, hallucinated amounts, the bot being too chatty
  in the group (annoys contractors, so keep replies minimal or only 1:1).
- **Adoption:** contractors won't change behaviour. The bot must work with how they already talk.
  The PM's benefit must be visible in week 1 (daily summary, "pending bills" list).

### 1.8 Your own relevant experience (keep it general, no client data)
You built a system that reads values from field photos (electricity meter readings sent by
operators) and refuses rather than guesses: every refusal has a reason and a message asking the
operator to retake the photo. That is the same pattern: unstructured WhatsApp-style input →
structured value → confidence check → accept / refuse with a reason → feedback to the sender.
Mention what you learned: wrong-but-accepted readings were the worst outcome, held-out testing
mattered, and some errors only a previous value or history check can catch (here: price history,
duplicate bills).

---

## 2. Extension: AI-powered lead management

### 2.1 What a "lead" looks like for interiors
A homeowner who has just bought a flat or is about to get possession. Leads come from the website form
(firstbriq's form asks for pincode, property type, BHK), Instagram DMs, WhatsApp, Google, referrals,
builder tie-ups, and the "free homeowner report on WhatsApp" (that is a lead magnet).

The usual pain: designers get many leads, most are not serious or have a small budget, response is
slow, follow-up is forgotten, and the lead goes to a competitor.

### 2.2 What AI can do along the funnel
| Stage | AI help |
|---|---|
| Capture | One inbox for web, WhatsApp, Instagram; dedupe the same person across channels |
| Qualify | WhatsApp conversation in the homeowner's language that collects: city/pincode, BHK, scope (full home / kitchen / wardrobes), budget band, possession date, style, decision-maker. Voice notes understood too |
| Score | Likelihood to convert and value, e.g. budget fits designer minimum, possession soon, answered fast |
| Match / route | For a marketplace like firstbriq: match lead to 2–3 designers by area, budget, style, capacity, response rate. Fair rotation so new designers also get leads |
| Follow-up | Reminders and nudges at the right time ("possession in 2 months"), book site visit / consultation slots, send relevant portfolio projects |
| Handover | Summarise the whole chat for the designer before the first call |
| Learn | Track outcome (won / lost / why) and feed it back into scoring and matching |

### 2.3 Decisions and risks (same thinking as part 1)
- Don't let the bot promise prices or timelines; it only collects and shares verified info.
- Hand over to a human when the lead asks something complex or is high value.
- Don't spam: WhatsApp templates cost money and users block spammy numbers (which hurts the number's quality rating).
- Metrics: first-response time, qualified-lead rate, consultation-booked rate, lead→contract
  conversion, designer satisfaction with lead quality, cost per won project.

### 2.4 How part 1 and part 2 connect
Same engine: WhatsApp in → understand messages in mixed languages → structured record → decision →
CRM/ERP. Lead management happens *before* the contract; the expense bot runs *after* it. One platform covers the whole journey.

---

## 3. firstbriq: what I could see on the public site, and ideas

> Note: I looked at the public website's code and text, not screenshots. **Open the site yourself
> before the call**, click through Home → Designers → a designer profile → Resources → Studio, and
> check that these points still hold. Note anything that feels slow or confusing on your phone.

### 3.1 What it is
- **Who:** homeowners in **Bengaluru** looking for an interior designer; designers/firms who want leads.
- **Promise:** "Independent. Objective. On your side." "From confusion to clarity before you spend a
  rupee." Verified designers, real portfolios, transparent timelines and costs, no middleman.
- **Pieces:**
  - *Designer directory* with filters (highest rated, fastest timeline, most experience).
  - *Designer profiles*: minimum budget, milestone-based payments, in-house factory or not,
    warranty, cities served, awards, Google reviews, and an **AI "Review Insights" / customer
    sentiment summary** ("Powered by firstbriq AI").
  - *Resources*: articles by phase of the interior journey, homeowner guide "9 Traps to Avoid",
    a home interiors report delivered on **WhatsApp** after entering a mobile number.
  - *Lead form*: "Book Free Consultation" with pincode, property type.
  - *Studio* (homeowner workspace): moodboard, sticky-note brainstorm canvas, room spaces, decor
    task board (Concept → Layout & Quotes → In Procurement → Installed), vendor quote comparison,
    budget summary, and an "Agentic AI Copilot" that creates tasks from a sentence.
  - *Vendor onboarding* forms (projects, materials and brands used, process phases, payment terms).
- **Tech they use (visible):** React single-page app, Payload CMS, PostHog and Microsoft Clarity
  for analytics. Mention this lightly; it shows you looked closely.

### 3.2 Observations / improvement ideas (pick 3–4 to say; lead with the first two)
1. **Link previews and SEO.** The page HTML that crawlers and WhatsApp receive contains only the title
   "FirstBriq" and no description or preview image; everything else loads with JavaScript. For a
   WhatsApp-first audience, a shared designer profile link may show a bare preview, and Google may
   index the pages poorly. Fix: pre-render or server-render pages and add a description and preview
   image (Open Graph tags) per designer and project. *Check by pasting a firstbriq link into WhatsApp yourself.*
2. **Post-hire transparency (the bridge to round 1).** The site helps people *choose*. Most homeowner
   pain comes *after* signing: delays, cost creep, "extra work" bills. Offer a project tracker
   fed by the WhatsApp bot: quote vs actual, milestones, photos, payments due. This also gives
   firstbriq real data to verify designers ("on-time rate 85%, average cost overrun 6%").
3. **Make "verified" concrete.** Publish what verification checks (site visit, past client calls,
   GST, completed-project photos, timelines vs promised). Show a badge with a date.
4. **Price clarity up front.** They already store budget, BHK, area and materials per project.
   Show "3BHK full home in Bengaluru with these designers: ₹X–Y" and a simple budget estimator
   (Studio already has a "Calculate Budget" idea).
5. **Language and WhatsApp-first flow.** Offer Kannada / Hindi / Tamil content and let the
   consultation request continue in WhatsApp instead of a long form.
6. **Studio focus.** The Studio has many features (matrix canvas, stickies, colour swatches). The
   most valuable piece is probably *quote comparison*: upload 3 designers' quotes, AI normalises them
   line by line (ply grade, hardware brand, laminate thickness) and highlights the differences. That is
   a real homeowner pain and a strong AI use case.
7. **Positioning copy.** "Elite Design & Build Marketplace", "Lived-in Luxury · Architectural
   Precision" and "No hidden jargon" pull in different directions (premium vs simple). Pick one voice.
8. **City clarity.** Say clearly it is Bengaluru for now and offer a waitlist for other cities (also
   a demand signal).

### 3.3 Business model questions to be curious about
Designers pay per lead or a subscription? Commission on signed projects? Brand partnerships
(plywood, hardware brands paying for visibility)? Each choice changes what "independent and
objective" means, so it is a good, respectful question to ask.

---

## 4. Global companies worth knowing (and what firstbriq can learn)

Check the latest details on each site before quoting numbers.

| Company (country) | What they do | Lesson for firstbriq |
|---|---|---|
| **Houzz** + **Houzz Pro** (US) | Huge inspiration photo site + directory of pros; Houzz Pro is SaaS for pros (CRM, estimates, invoices, 3D). Houzz AI writes estimates and change orders, and logs expenses from **receipt photos** | Marketplace + SaaS for the pros is a proven combo. Receipt-photo expense logging is exactly the round-1 bot |
| **Angi** / **Thumbtack** (US) | Lead marketplaces for home services; pros pay per lead | Pay-per-lead brings complaints about poor leads. Quality of matching and lead verification is the product |
| **Sweeten** (US) | Free matching of homeowners with vetted renovation contractors, support through the project | Stay involved after the match; that builds trust and repeat referrals |
| **Block Renovation** (US) | Vetted contractors, standardised scope and bids, milestone payments with oversight | Standardised scopes make quotes comparable, which is the same idea as quote comparison |
| **Checkatrade** (UK), **hipages** (Australia) | Vetted trades directory with reviews; hipages also sells job-management software to trades | Vetting + reviews + software for the supply side |
| **Buildertrend**, **Procore** (US) | Project management for builders: schedules, budgets, daily logs, client portal | The client portal (homeowner sees progress and money) is standard abroad and rare in India |
| **Havenly** (US) | Online interior design packages + shopping | Productised, fixed-price design packages reduce uncertainty |
| India: **Livspace**, **HomeLane** (bought DesignCafe in 2024), **Bonito Designs** | Full-stack: own designers, factories, execution, warranties | They solve trust by owning everything (expensive, less choice). firstbriq's angle: trust through **verification and transparency** while keeping the independent designer |
| India software: **Foyr**, **EmptyCup**, **Zeyka**, **InteriorOS** | 3D design tools / apps for Indian designers (leads, quotes, projects) | Designers already use some tools; integrate rather than replace |

---

## 5. Indian home interiors industry: key points

**Size and shape**
- Estimates range widely, roughly **US$20–35 billion** in 2025–26 with strong growth (Mordor
  Intelligence: ~$31B in 2025 → ~$65B by 2031). Say "estimates vary" rather than one exact number.
- Mostly **unorganised**: local carpenters, contractors and small studios. Organised players (Livspace,
  HomeLane) hold a small share.
- Demand driver: new apartments at possession, rising incomes, nuclear families, and modular kitchens
  and wardrobes becoming standard.

**Key problems**
1. **Trust and quality**: Instagram portfolios can't be verified; quality varies (ply grade swaps, cheaper hardware).
2. **Opaque pricing**: quotes are not comparable (different materials, "per sq ft" vs lump sum).
3. **Delays and cost overruns**: "extra work" bills, labour shortages, material price swings.
4. **Coordination chaos**: many vendors and trades; all on WhatsApp; nothing recorded (the round-1 problem).
5. **Payments and disputes**: large advances, unclear milestones, cash and kacha bills, GST confusion.
6. **Fragmented supply chain**: many brands, distributors, local dealers; no price visibility.
7. **Skilled labour**: dependence on a few carpenters; no standard of workmanship.

**Where AI can make a difference**
- WhatsApp-native project records (expenses, progress, approvals) → transparency for PM and homeowner.
- Quote normalisation and comparison; budget estimation from past projects.
- Lead qualification and matching in local languages.
- Review summarisation and verification (firstbriq already does AI review insights).
- Site-photo progress tracking (is the kitchen carcass installed? compare to plan).
- Design: AI renders and moodboards (crowded; differentiation is weaker here).
- Vernacular voice interfaces for carpenters and contractors who don't type.

---

## 6. Likely questions and short answers

- **"How would you handle a voice note in Kannada mixed with English?"** Speech-to-text in
  codemix mode, keep the original and an English version, extract against the schema with a domain glossary,
  and if the amount came only from voice, mark it "claimed" and ask for the bill.
- **"What if the bot gets an amount wrong?"** Every record links to the original message; the PM can
  fix it in one tap; corrections are logged and become test cases. High-value items always need approval.
- **"How do you know it works?"** Labelled set from real projects, accuracy per field and per
  event type, shadow mode before auto-posting, and track PM edits per week.
- **"Why not just build an app?"** Contractors won't install or use it; WhatsApp is where the work
  already happens. Meet them there; the app is for the PM and the homeowner, not the contractor.
- **"Which model would you use?"** Cheap model for classifying every message, a stronger
  vision/LLM only for bills and hard cases, Sarvam for Indian speech. Keep the design model-agnostic and
  compare models on your own labelled set; costs and quality change every few months.
- **"Build vs buy?"** Use APIs for speech, vision and LLMs; build the schema, rules, entity matching,
  review UI and evaluation set. Those are the value and they don't come off the shelf.
- **"What would you ship in 4 weeks?"** Week 1: forward-to-bot number + chat-export import, store
  everything. Week 2: bill photo → line items + PM review screen. Week 3: voice notes + vendor
  matching + daily digest. Week 4: shadow-mode metrics on 3 live projects, pick the first category to auto-post.

---

## 7. Suggested flow for the 45 minutes
- 2 min: intro, one line on your background (field-photo reading system, refuse-not-guess).
- 15 min: WhatsApp bot. Restate, ask clarifying questions, pipeline, decisions, evaluation.
- 8 min: lead management extension and how it shares the engine.
- 10 min: firstbriq observations (2–3) + 2 global companies + bridge idea.
- 5 min: industry problems → where AI helps.
- 5 min: your questions for them.

## 8. Day-of checklist
- [ ] Open firstbriq.com on your **phone**; paste a designer link into WhatsApp and see the preview.
- [ ] Note one thing you liked (the WhatsApp report delivery and AI review summaries are good).
- [ ] Have the pipeline diagram (section 1.3) ready to share or draw.
- [ ] Quiet room, charger, test camera and mic, water.
- [ ] It's fine to say "I don't know, here's how I'd find out."

---

### Sources used
- firstbriq.com public site (text read from the page code, 2026-10-21)
- Sarvam AI docs: https://docs.sarvam.ai/api-reference-docs/getting-started/models/saaras.md ,
  https://docs.sarvam.ai/api/changelog.md
- WhatsApp Groups API (third-party write-ups, verify with Meta): https://kapso.ai/blog/whatsapp-groups-api-state-2026 ,
  https://www.unipile.com/whatsapp-group-api/
- Houzz Pro AI: https://www.newyorkbuildexpo.com/industry-news-1/houzz-pro-highlights-year-ai-powered-workflows-ahead-ny-build-2026
- Market size: https://www.mordorintelligence.kr/industry-reports/india-interior-design-market ,
  https://inc42.com/?p=566464 , https://themorningcontext.com/internet/livspace-and-homelane-in-a-race-to-profit
- Indian design tools: https://www.hunted.space/product/interioros , https://builtinbengaluru.in/company/emptycup
