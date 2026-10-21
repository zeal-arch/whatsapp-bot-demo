# Similar products: research for firstbriq round 2

Done 2026-10-21, following the three areas in the interview mail:
1. WhatsApp group chats → structured data → ERP/SaaS (the round-1 problem)
2. AI-powered lead management (the extension they mentioned)
3. Companies in home interiors / home improvement (to compare with firstbriq)

Most sources are the companies' own websites or press releases, so treat numbers and claims as
*their* claims. Say "they claim" in the interview, not "they do".

---

## Headline for the interview

> "The idea is validated: several startups already turn WhatsApp site groups into reports and billing
> evidence, mostly for **large construction projects** in the Gulf, Europe and Indian infrastructure.
> Indian apps like Powerplay, Onsite and RDash take the other route: they try to **replace** WhatsApp
> with an app. What I did not find is a product built for **Indian residential interiors** that reads
> the WhatsApp chats, captures **material purchases and costs** from Hinglish voice notes and kacha
> bills, and shows the **homeowner** quote vs actual. That gap fits firstbriq."

(Say "I didn't find", not "it doesn't exist".)

---

## 1. WhatsApp → structured project data (closest to the round-1 problem)

### 1a. WhatsApp-native AI for construction sites (same pattern, different customer)
| Product | Where | What it does | Notes for you |
|---|---|---|---|
| **Velora** (velora.ai) | Appears India-aware (mentions crores, Hindi, Telugu) | Reads the team's existing WhatsApp groups; turns messages, voice notes and photos into progress, issues, deliveries, **billing evidence** matched to bill lines, and contract-delay alerts. Free "DPR Generator" (daily progress report) from group chats. Per-project pricing, 3-month pilot, paid import of old WhatsApp exports | **Closest match.** Says "no business API needed" (connects to an existing number). Aimed at big contractors, not homes |
| **Sifu** (getsifu.ai) | Gulf / global infrastructure | "Joins the group and reads everything." Five agents: daily report by 7am, chase missing updates, safety flags from photos, check work vs drawings, update schedule | Claims reporting time fell from 60 min to under 10. No expense/ERP output mentioned |
| **Banamind** (banamind.ai) | UAE / MENA | Add it to the project group; AI tags every photo, voice note and document by project, stage and zone; asks for missing photos; sends reports; risk scoring; invoicing; Arabic support | Claims 19% fewer cost overruns (vendor claim) |
| **Valoon** (valoon.chat) | Germany (Fraunhofer/KIT spin-off) | Works through messengers like WhatsApp; dictate-to-report, auto documentation | Small funding; says it was "first" to target messenger apps |
| **Benetics** | Switzerland/Germany | Voice assistant for site workers, 30+ languages | Voice-first app, not WhatsApp |
| Open-source example | GitHub (nsikakjon/WhatsApp-AI-Tool) | Bot logs texts, photos and voice notes per site; Claude writes a daily report; falls back to raw updates if AI fails | Good proof that a prototype is a weekend job; the hard part is accuracy and adoption |

**Lesson:** these products focus on *progress and reports*. The round-1 problem is about *who bought
what, at what cost*, which is money, so it needs stricter checks and PM approval.

### 1b. Indian construction / interior project apps (replace WhatsApp instead of reading it)
| Product | What it does | Notes |
|---|---|---|
| **Powerplay** | Construction PM app: daily logs, tasks, labour attendance, **material receipts (GRN) and consumption** | Says it "replaces WhatsApp and paper registers"; sends assignments via WhatsApp |
| **Onsite** (onsiteteams.com) | Construction **and interiors**: site tracking, invoicing, **expense management**, procurement; works with WhatsApp, Tally, Zoho | Claims 10,000+ contractors |
| **RDash** (rdash.ai) | Y Combinator-backed (2022); for construction and **interior fit-out**: BOQs, daily progress reports, snags, procurement, finance, **CRM for leads and quotations**, AI agents for anomaly detection | Lists WhatsApp as the problem it replaces. Claims 8–10% project cost savings |
| **Aasaan** | Construction site management with two-way WhatsApp workflows | Vendor's own comparison pages |
| **Zoho Projects** | General PM | Generic |

**Lesson:** these require contractors and suppliers to adopt an app. That is the adoption problem the
round-1 bot avoids. Strong interview point: *"Their weak spot is the vendor who never opens the app;
a WhatsApp reader removes that step."*

### 1c. Bill / expense extraction on WhatsApp (the "who bought what" piece)
| Product | What it does | Notes |
|---|---|---|
| **Zoffer Bills** | Forward vendor bills on WhatsApp (handwritten too) → vendor, date, line items, tax, amount pulled into **Zoho Books**; **nothing posts until the user approves** | ₹999/month; new (Product Hunt). Same human-approval idea as your design |
| **Blipko** | AI bookkeeper inside WhatsApp for Indian small businesses; reads images and voice notes; **understands Hinglish**; UPI | Early-stage project |
| **Khata Bhai**, **KhataBuddy** | WhatsApp billing / GST invoicing assistants (Hindi, English, Hinglish) | Create invoices; they don't read incoming bills |
| **Houzz Pro** (US) | Logs expenses from **receipt photos**, drafts change orders and invoices with AI | Big global player already doing the money part |

### 1d. WhatsApp group tooling (infrastructure you could build on)
| Product | What it does | Notes |
|---|---|---|
| **Periskope** | "CRM for WhatsApp groups": manage many groups, AI chat summaries (uses Gemini), flag messages as tickets, sync to HubSpot / Zoho / Google Sheets / Freshdesk | Connects by **scanning a QR code** (no official API) |
| Official **WhatsApp Cloud API Groups** | Business number can create and post in groups | Reported limits: Official Business Account needed, small groups, invite-link join only |

**Talking point on access:** many of these products connect "without the business API", meaning a
linked device. That is easy to adopt, but WhatsApp can ban the number and it breaks their terms. Say you
would weigh that risk openly: pilot fast, but plan for the official API.

---

## 2. AI lead management

| Product | Market | What it does |
|---|---|---|
| **Sell.do** | Indian real estate | Says it has AI lead scoring, auto-logged calls, follow-ups, a WhatsApp agent that replies, qualifies and **books site visits** (a competitor says its AI is weaker, so the sources conflict) |
| **TeleCRM** | Indian sales teams | Calling + WhatsApp-first CRM, WhatsApp chatbot, bulk messages, AI call analysis |
| **Kylas** | India | CRM with automatic lead distribution (routing) |
| **Realatic**, **Leadrat**, **Propflo** | Indian real estate | CRMs claiming AI auto-qualification over WhatsApp |
| **RDash CRM** | Indian construction / interiors | Lead → quotation → project in one flow |
| **Houzz Pro CRM** | US | Leads from the Houzz marketplace + AI insights, straight into estimates |
| AI voice receptionists (Solvea, Hatch, CallSphere, Open.cx, Signpost, Workiz) | US home services | Answer every call 24/7, ask qualifying questions, check service area, book jobs into the calendar; ~$30–400/month |
| **Thumbtack**, **Angi** | US | Marketplace lead matching; pros pay per lead (complaints about lead quality are common) |

**Lessons for firstbriq's lead system**
- The pitch abroad is **speed to lead**: the first business to reply usually wins.
- Indian tools are mostly **real estate CRMs**; I found nothing built for **interior designers
  receiving leads from a marketplace**. That gap fits firstbriq: qualify the homeowner once (BHK,
  budget, possession date, pincode, style) in their language on WhatsApp, then route to the 2–3 best-fit
  designers with a summary.
- Marketplace risk (Thumbtack/Angi): if designers pay for poor leads, they leave. Qualification
  quality is the product.

---

## 3. Home interiors platforms (compare with firstbriq)

### India
| Company | Model | Compared with firstbriq |
|---|---|---|
| **Livspace**, **HomeLane** (bought **DesignCafe** in 2024), **Bonito Designs** | Full-stack: own designers, factories, execution, warranty | Trust by owning everything. firstbriq: trust by **verifying independent designers** |
| **My Interior Designers** | **Bengaluru-first** designer discovery platform, launched May 2026, plans for 10+ cities and Dubai | **Direct competitor** in the same city. Its press release does not say how it verifies designers. firstbriq's verified costs and timelines are the differentiator |
| **Interiors by Verified.RealEstate** | Chennai / Tamil Nadu; itemised **fixed-price quotes**, verified materials, **penalty for delays**, NRI-friendly remote execution | Shows homeowners value guarantees and comparable quotes |
| **Foyr, EmptyCup, Zeyka, InteriorOS** | Software for Indian designers (3D, quotes, leads) | Supply-side tools firstbriq could integrate with |

### Global
| Company | Model | Lesson |
|---|---|---|
| **Houzz + Houzz Pro** (US) | Inspiration + directory + SaaS for pros with AI estimates and receipt capture | Marketplace + pro software is a proven combination |
| **Sweeten** (US) | Free matching with vetted contractors, stays involved during the project | Support after the match builds trust |
| **Block Renovation** (US) | Standardised scopes, comparable bids, milestone payments with oversight | Comparable quotes = firstbriq "quote comparison" idea |
| **Checkatrade** (UK), **hipages** (Australia) | Vetted trades + reviews; hipages also sells job software to trades | Vetting + reviews + supply-side software |
| **Thumbtack / Angi** (US) | Pay-per-lead marketplaces | Lead quality decides whether pros stay |

---

## 4. Three things to say that show you researched

1. "Velora, Sifu and Banamind prove that reading WhatsApp groups works for big construction. They report
   progress; your problem is **money**, so I'd add Zoffer-style approval before anything posts."
2. "Powerplay, Onsite and RDash try to **replace** WhatsApp. The round-1 approach **reads** it, so
   suppliers and carpenters don't have to change anything."
3. "Lead tools in India are built for real estate. A marketplace like firstbriq can own **qualify once,
   match to the right designers**, and later show the homeowner quote vs actual from the WhatsApp bot,
   one journey from lead to handover."

---

## Sources
WhatsApp construction AI: https://velora.ai/ · https://www.getsifu.ai/en · https://banamind.ai/ ·
https://valoon.chat/en/funktionen/speech-to-report/ · https://valoon.chat/en/company/ ·
https://www.venturelab.swiss/Benetics-The-Venture-Leader-Technology-empowering-construction-professionals ·
https://github.com/nsikakjon/WhatsApp-AI-Tool/pull/7

Indian construction/interior apps: https://www.getpowerplay.in/resources/blogs/best-construction-apps-for-site-management/ ·
https://onsiteteams.com/ · https://play.google.com/store/apps/details?id=com.app.onsite&hl=en_IN ·
https://rdash.ai/blog/top-interior-project-management-software-in-india/ · https://www.getapp.com/construction-software/a/rdash/ ·
https://aasaan.co/best-construction-project-management-software-in-india/

Bill extraction: https://www.producthunt.com/products/zoffer-bills · https://peerlist.io/sadikkp/project/blipko ·
https://www.capterra.in/software/1092751/Khata-Bhai · https://webcatalog.io/en/apps/khatabuddy

WhatsApp groups: https://periskope.app/blog/summarize-whatsapp-group-chats-with-ai ·
https://periskope.app/blog/how-to-add-an-ai-chatbot-to-whatsapp-business-groups-no-api ·
https://kapso.ai/blog/whatsapp-groups-api-state-2026 · https://www.unipile.com/whatsapp-group-api/

Lead management: https://www.sell.do/blog/best-real-estate-crm-software-for-agents-in-india ·
https://telecrm.in/blog/top-10-crm-software/ · https://realatic.com/blog/best-crm-real-estate-india/ ·
https://leadrat.com/top-17-real-estate-crm-in-india-in-2026/ · https://solvea.cx/blog/ai-lead-qualification-for-home-services ·
https://www.open.cx/voice/for-contractors

Interiors platforms: https://thedailyguardian.com/business/my-interior-designers-enters-indias-interior-discovery-space-with-a-more-structured-and-trust-led-approach20260525181504-698072/ ·
https://interiors-vre.centralindia.cloudapp.azure.com/compare · https://inc42.com/?p=566464 ·
https://www.newyorkbuildexpo.com/industry-news-1/houzz-pro-highlights-year-ai-powered-workflows-ahead-ny-build-2026
