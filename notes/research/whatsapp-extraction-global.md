# Global products that turn WhatsApp / messenger chats into structured project data (construction, fit-out, field services)

Research date: 2026-10-21. Public pages only. "Vendor claim" = stated by the company itself (website, press release); "third-party" = database or press; "independent" = not traceable to the vendor. Almost all traction and accuracy figures found are vendor claims.

## 1. Which companies do this, and what do they take in and put out?

### Takeaway
There are two families. (a) **WhatsApp-native "listener" products** that join existing site groups and turn messages, voice notes, photos and documents into reports and records: Sifu (Kodifly, Hong Kong), Banamind (UAE), Valoon (Germany), Pillar (Italy, the closest to "chat -> finance/ERP records"), Velora (India-based, see note). (b) **Own-app or incumbent platforms** that do the same extraction but inside their own app (Kraaft, OnSite, Benetics, Procore Daily Log Agent, Buildertrend / Houzz Pro receipt capture, Trunk Tools, Kojo). Almost none of the WhatsApp-native players publicly claim direct ERP/accounting write-back except Pillar; most stop at reports, dashboards, invoices-with-evidence and alerts.

### Cited Findings

**WhatsApp-native (reads existing groups)**

- **Sifu (getsifu.ai), built by Kodifly (Hong Kong)** — AI agent that "lives inside your existing site WhatsApp group" and captures every voice note, photo and message, turning them into daily progress reports and compliance alerts — [Sifu About](https://www.getsifu.ai/about)
  - Five background agents: chase missing updates, scan photos for safety issues, validate work against drawings/specs, write the daily report (PDF, ready by 7am in a dashboard), schedule updates, searchable photo/message archive — [Sifu homepage](https://www.getsifu.ai/en)
  - Languages listed: English, Arabic, Cantonese, Mandarin, Bahasa, Urdu "and more" — [Sifu homepage](https://www.getsifu.ai/en)
  - Only WhatsApp named as integration; replaces "three Excel sheets" — [Sifu homepage](https://www.getsifu.ai/en)
  - Security: AWS, regional data residency, "models never trained on project data", SOC 2 Type II "in progress" — [Sifu homepage](https://www.getsifu.ai/en)
  - Kodifly describes itself as a Hong Kong spatial-intelligence company with 5+ years deploying AI on live infrastructure projects — [Sifu search snippet / Kodifly](https://www.kodifly.com/)
  - Does not say whether it joins groups via official API, bot number or linked device; no human-review step described — [Sifu homepage](https://www.getsifu.ai/en)

- **Banamind (banamind.ai), Banamind LLC, UAE ("Made in UAE", Gulf/MENA focus)** — add Banamind to an existing project WhatsApp group; agent requests missing photos, sends scheduled reports, flags risks, runs checklist inspections in the group — [Banamind](https://banamind.ai/)
  - Inputs: WhatsApp messages, photos, video, voice notes, documents, plus email ingestion; document OCR and field extraction — [Banamind](https://banamind.ai/)
  - Outputs: daily/client progress reports (PDF or revocable links), risk register with severity scores, timelines and progress %, **invoices with attached proof-of-work and payment links**, priced estimates (labour, materials, markup), compliance records. No ERP/cost-entry sync mentioned — [Banamind](https://banamind.ai/)
  - Human review: tagged evidence confirmed "with one tap"; AI flags issues before task sign-off; reports editable — [Banamind](https://banamind.ai/)
  - Languages: "full Arabic support" plus AI translator for multinational crews — [Banamind](https://banamind.ai/)
  - Named customers (vendor): Pro Builders, AHC, Reliant Roofing, BK Restoration, Horizon Build Group; customer-reported 19% lower cost overruns, 25% less rework, 20 h/week saved (not verified) — [Banamind](https://banamind.ai/)

- **Valoon (valoon.chat), Valoon GmbH, Dortmund, Germany (KIT spin-off)** — crews keep using WhatsApp; office uses Valoon web platform (app.valoon.chat). Photo documentation filed to project, voice AI, real-time translation ("over 50 languages" in one place, "+20" in another), auto-generated reports, "Valoon Studio" for questions/dashboards on defects, hours, reports; digital timesheets; German servers — [Valoon](https://valoon.chat/)
  - Integrations "scoped individually"; none named — [Valoon](https://valoon.chat/)
  - Traction (vendor): 3,000+ construction projects in 10 countries — [Valoon](https://valoon.chat/)
  - Mechanism for reading WhatsApp not disclosed publicly; I found no source — (see Gaps)

- **Pillar (Milan, Italy, founded 2025)** — closest to the firstbriq use case (chat -> finance records). Contractors send **delivery notes, invoices, reports and site photos via WhatsApp** (or upload); AI processes them in real time. Platform pulls from accounting systems, bank feeds, job sites and WhatsApp; automates estimates, invoicing, site accounting, procurement, margin tracking — [Vestbee, May 2026](https://www.vestbee.com/insights/articles/pillar-raises-12-m)
  - Traction (company-reported): 500+ construction firms, 2,000+ projects, ~14 h/week admin saved — [Vestbee](https://www.vestbee.com/insights/articles/pillar-raises-12-m)

- **Velora (velora.ai)** — NOTE: appears to be India-based (Tracxn: Hyderabad, founded 2025 by Vikas Singhvi; +91 contact; INR-style testimonials). Covered briefly only because it was named as a starting point — [Tracxn](https://tracxn.com/d/companies/velora-ai/__1HZ6x1vS43aKGJoN_r2SpIbaNEBP2takduOjyNTL62g); [Velora](https://velora.ai/)
  - Inputs: WhatsApp text, photos, checklists, voice notes (auto-transcribed); BOQ, work order and contract docs; QR + GPS check-ins per work front. Languages: English, Hindi, Telugu, Spanish, Arabic — [Velora](https://velora.ai/)
  - Outputs: progress/blocker tracking, commitments tracked to closure, auto-drafted progress reports, **bill packaging (evidence filed against BOQ scope items, executed vs scoped quantities)**, contract-clause alerts (e.g. 7-day notice under GCC Cl. 8.5(e), LD exposure), audit trail linking each record to its source message. Explicitly "works alongside your PMIS and ERP, not instead of them" — [Velora](https://velora.ai/)
  - Human review: "You stay in control of every call"; items marked "Flagged for review"; reports "ready to review" — [Velora](https://velora.ai/)
  - Free "DPR Generator" desktop tool drafts Daily Progress Reports from WhatsApp groups — [Velora DPR Generator](https://velora.ai/desktop-app/index.html)

- **BRKZ (Saudi Arabia, construction procurement marketplace)** — raised $31M; its delivery agent reads delivery notes sent through WhatsApp and matches them to orders (bulk cement) — [Ventureburn](https://ventureburn.com/brkz-raises-31m-ai-construction-procurement/)

- **Heyloha (Covalore B.V., Utrecht, Netherlands)** — WhatsApp AI for construction firms, but customer-facing: answers client/subcontractor questions from a knowledge base, books meetings (Outlook), hands off to a PM. No ERP or data extraction — [Heyloha](https://www.heyloha.ai/en/whatsapp-voor/bouwbedrijven)

- **Adjacent (non-construction) WhatsApp extraction**: Galo AI reads WhatsApp messages, audio, images and PDFs from B2B buyers and turns them into orders ready for logistics/billing (food wholesale) — [Galo AI](https://www.soygalo.com/en-us). Duotach case study: a construction company's material orders received over WhatsApp, bot interprets them against the catalogue, checks stock and loads them — [Duotach](https://duotach.com/en/blog/bot-whatsapp-tomar-pedidos). Jelou (LATAM) raised $10M (Jan 2026) to build AI apps that "move money on WhatsApp" — [GlobeNewswire](https://www.globenewswire.com/news-release/2026/01/26/3225729/0/en/jelou-raises-10m-to-build-ai-apps-that-move-money-on-whatsapp.html)

**Own-app construction messengers (replace WhatsApp rather than read it)**

- **Kraaft (Paris)** — "super-messenger"/"WhatsApp for construction"; €13M Series A Jan 2025 led by Dawn Capital (with Brick & Mortar, Chalfen, Stride VC, OSS Ventures) for product and UK/Germany entry; €3.2M seed 2023. AI for tagging/reporting, photo geolocation, safety checks — [Kraaft](https://www.kraaft.co/en/articles/kraaft-raises-eu13m-series-a-to-scale-super-app-for-the-construction-industry); [Tech.eu](https://tech.eu/2025/01/21/kraaft-raises-13m-series-a-to-scale-super-app-for-the-construction-industry/). Users: 1,000 companies (2025 announcement) vs 30,000+ active users (Dealroom) — [Dealroom](https://app.dealroom.co/companies/kraaft)
- **OnSite (Singapore)** — standalone site-communication app, explicitly does not read WhatsApp; tags text, images, voice notes by project, location and timeline for documentation/disputes; 8 languages incl. Mandarin, Tamil, Bengali, Cantonese, Malay, handles code-switching; beta with design partners in Singapore and Hong Kong. Seed S$1.7M (US$1.3M), co-led by Tin Men Capital and Alter Global, ~April 2026. Mentions India as an opportunity, not a plan — [e27](https://e27.co/onsite-raises-us1-3m-to-fix-constructions-whatsapp-problem-20260408/); [Bricks & Bytes](https://bricks-bytes.com/funding-ma/onsite-raises-seed-round-ai-construction/)
- **Benetics (Zurich)** — voice assistant app: records, transcribes and turns speech into action plans, checklists, task assignments, photos, due dates; "powered by OpenAI"; WhatsApp used only to send tasks/reports to external partners via secure link — [Construction Management](https://constructionmanagement.co.uk/benetics-launches-ai-based-voice-assist-for-construction-workers/); [Benetics blog](https://www.benetics.ai/en/blog/ai-for-construction-workers-benetics-launches-first-digital-voice-assistant-for-the-construction-industry)

**Incumbent platforms with AI capture (in-app, not WhatsApp)**

- **Procore Daily Log Agent (Helix)** — turns field photos, emails, video and voice into completed daily logs; user "review, adjust, and approve" every draft; 150+ built-in actions let agents create/update records — [Procore AI Agents](https://www.procore.com/ai/agents); [Engineering.com](https://www.engineering.com/procore-expands-ai-tools-with-construction-workflow-agents/)
- **Buildertrend AI bill capture / Cost Inbox** — upload invoice/receipt, AI extracts details and creates a bill record; mobile receipts via OCR — [Buildertrend](https://buildertrend.com/?p=116501); [Cost Inbox](https://buildertrend.com/?p=110318)
- **Houzz Pro AutoMate AI expenses** — photo of receipt -> extracted, categorised expense under the project; batch scanning with per-file review — [ForConstructionPros](https://www.forconstructionpros.com/construction-technology/product/22948532/houzz-houzz-pro-ai-tools-automate-estimates-tasks-expenses); [Houzz Pro help](https://pro.houzz.com/pro-help/r/how-to-log-and-manage-expenses)
- **Trunk Tools (US)** — AI over project documents (drawings, specs, RFIs, schedules, submittals) with autonomous agents; $40M Series B 24 July 2025 led by Insight Partners, $70M total; "hundreds of projects", revenue 5x in six months (company-reported) — [Insight Partners](https://www.insightpartners.com/ideas/trunk-tools-closes-40m-series-b-to-lead-constructions-ai-transformation/); [Commercial Observer](https://commercialobserver.com/2025/07/trunk-tools-contech-series-b/)
- **Kojo (US)** — construction materials procurement; $10M from Wesco (Sept/Oct 2025) as Series C extension (Battery Ventures-led, $49M), ~$94M total; "Project POs" AI tool for long-lead purchase orders; 600+ contractors, $5B+ materials/year (vendor) — [Business Wire](https://www.businesswire.com/news/home/20251016530530/en/Kojo-Poised-to-Revolutionize-Construction-Materials-Management); [Axios](https://www.axios.com/pro/supply-chain-deals/2025/09/12/kojo-10m-wesco-data-center-materials)
- **Field Materials** — AI scans vendor quotes to remove PO data entry; suppliers notified by email/SMS, not WhatsApp — [Field Materials](https://www.fieldmaterials.com/)
- **YC**: no YC company found doing WhatsApp construction reporting; nearest is Opusense AI (P2025), voice+photo field inspection reports — [YC construction directory](https://ycombinator.com/companies/industry/construction)

### Inferences
- The "listener in the existing WhatsApp group" pattern is now crowded at the reporting layer (Sifu, Banamind, Valoon, Velora), mostly 2024-2026 startups with small or undisclosed funding. The finance/ERP layer (chat -> invoice, delivery note, cost entry, PO) is much thinner; Pillar (€15.2M total) and BRKZ (delivery notes only) are the main global examples. That is the gap firstbriq's "update the ERP" idea sits in.
- Incumbents (Procore, Buildertrend, Houzz Pro) do the same extraction from photos/voice/receipts but inside their own apps, with explicit human approval. Home-interiors/renovation in emerging markets, where crews live in WhatsApp, is under-served by them.
- Every product that describes review keeps a human approve/confirm step (Procore, Banamind one-tap confirm, Velora "flagged for review"); none publicly claims fully autonomous write-back to accounting.

### Gaps
- No public ERP connector list for Sifu, Banamind or Valoon. Pillar's accounting/ERP targets are not named.
- Raken and Fieldwire 2026 AI features: no current primary source found.
- Slate, Siteline: not researched for lack of tool budget; neither appeared as WhatsApp-based in searches.
- No WhatsApp-native construction-reporting startup found in LATAM or Africa (only generic WhatsApp AI vendors and pre-sales bots like Aurora Inbox).

## 2. How do they access WhatsApp, and what are the ban / ToS risks?

### Takeaway
The official Cloud API **cannot join a customer's existing WhatsApp groups**: its Groups API (Official Business Accounts only) lets a business *create* invite-only groups of at most **8 participants**. Products that "join your existing group" therefore either use an unofficial linked-device session (Velora documents a QR "Linked Devices" scan and says "no business API needed") or do not say how they do it. Unofficial access is against WhatsApp's terms on automated messaging and carries unpredictable ban risk.

### Cited Findings
- Meta Cloud API Groups API: available to businesses with an **Official Business Account**; not for WhatsApp Business app numbers; max **8 participants** per group; invite-link only; up to **10,000 groups** per business number; max 1 Cloud API business per group; text, media and template messages only (no interactive messages, calls, disappearing/view-once); per-message pricing — [Meta developer docs](https://developers.facebook.com/docs/whatsapp/cloud-api/groups)
- Meta's doc does not say a business number can join existing (user-created) groups — [Meta developer docs](https://developers.facebook.com/docs/whatsapp/cloud-api/groups)
- Third-party pages agree on the 8-person cap; one says there is no add-participant endpoint (invite only) — [Unipile](https://www.unipile.com/whatsapp-group-api/); [Omnichat](https://blog.omnichat.ai/whatsapp-groups-api/)
- Coexistence (same number on WhatsApp Business app + Cloud API): group chats stay in the app and are **not synced** to the API; automation applies only to 1:1 chats — [Wati](https://www.wati.io/en/blog/whatsapp-coexistence-solution/); [Seasalt.ai](https://seasalt.ai/en/blog/whatsapp-coexistence-technical-architecture-enterprise-use-and-the-future-of-hybrid-messaging)
- **Velora**: connects "through existing WhatsApp number (no business API needed)"; setup is scanning a QR code from WhatsApp > Linked Devices; recommends a dedicated number, notes WhatsApp's 4-linked-device limit; monitors only mapped groups; no mention of ban risk — [Velora setup guide](https://velora.ai/docs/velora-platform/velora-platform-setup/); [Velora](https://velora.ai/)
- Sifu ("joins the group and reads everything"), Banamind ("add Banamind to your group") and Valoon do not publicly state their mechanism — [Sifu](https://www.getsifu.ai/en); [Banamind](https://banamind.ai/); [Valoon](https://valoon.chat/)
- WhatsApp Help Center (as quoted by secondary sources): bulk and automated messaging violate the Terms; enforced with bans and in serious cases legal action — [Zylos research](https://zylos.ai/research/2026-01-26-whatsapp-api-automation/); [AdviseAI](https://www.adviseai.in/blog/whatsapp-automation-ban-risk)
- Anecdotal ban: Jan 2026 GitHub issue, Baileys account temporarily banned twice then permanently after bulk status uploads to 2,000-3,000 contacts from a server; commenters blamed sending pattern and server IP — [Baileys issue #2309](https://github.com/WhiskeySockets/Baileys/issues/2309)
- Reported ban signals (not confirmed by WhatsApp): robotic timing, datacentre/VPS IPs; ban timing reported from days to months with no reliable pattern — [AdviseAI](https://www.adviseai.in/blog/whatsapp-automation-ban-risk); [Kraya](https://blog.kraya-ai.com/whatsapp-automation-ban-risk)
- Meta policy, effective for new users 15 Oct 2025 and existing users **15 Jan 2026**: WhatsApp Business API terms bar **general-purpose AI chatbots** (ChatGPT, Perplexity, Luzia, Poke affected); business-specific bots (support, booking, order tracking) remain allowed; Meta decides what is a "primary use case" — [TechRadar](https://techradar.com/ai-platforms-assistants/meta-will-ban-rival-ai-chatbots-from-whatsapp); [respond.io](https://respond.io/blog/whatsapp-general-purpose-chatbots-ban)
- Pillar and BRKZ receive documents "via WhatsApp" (users send to a number), a pattern that works on the official 1:1 API — [Vestbee](https://www.vestbee.com/insights/articles/pillar-raises-12-m); [Ventureburn](https://ventureburn.com/brkz-raises-31m-ai-construction-procurement/)

### Inferences
- Three architectures exist: (1) **official 1:1 bot number** (forward photos/voice/invoices to the bot; compliant, but not a passive listener); (2) **official Groups API** (bot creates small groups of <=8; fits a client + PM + designer + site lead group for a home-interiors project, but not large existing site groups); (3) **linked-device listener** on a dedicated number (reads all existing groups passively; best UX, but ToS and ban exposure, and one ban can kill all project groups at once).
- A vertical project-data bot is a business-specific use case, so the Jan 2026 general-purpose chatbot ban should not apply, but this is an interpretation; Meta reserves the decision.
- For an interview: the honest design is official API for anything that sends messages, plus clear disclosure and consent if passively reading groups; human confirmation before ERP write.

### Gaps
- Valoon, Sifu and Banamind group-access mechanisms not publicly documented; could not confirm whether they use BSPs (Twilio, 360dialog) or linked devices.
- No official WhatsApp statement on ban rates for linked-device automation; the "68% of Indian businesses banned within 12 months" figure is a single vendor's unverified claim and should not be used.
- Launch date of the Groups API not on Meta's page.

## 3. Pricing, funding, team, traction (with dates)

### Takeaway
WhatsApp-native construction listeners are small and lightly funded (Valoon ~$0.05-0.16M plus grants; Velora unfunded; Sifu inside Kodifly; Banamind undisclosed). Prices where public sit around $100-400/month. The well-funded players (Trunk Tools $70M, Kojo ~$94M, Kraaft ~€16M, Pillar €15.2M) either own their app or focus on documents/procurement/finance.

### Cited Findings
| Company | Pricing | Funding | Traction (vendor unless noted) |
|---|---|---|---|
| Banamind (UAE) | Annual billing: Start $100/mo (1-5 users), Plus $200/mo (5-10), Scale $400/mo (10-20), Enterprise custom; 7-day free trial; all tiers same features — [Banamind pricing](https://banamind.ai/pricing) | Not disclosed — [Banamind](https://banamind.ai/) | 5 named customers — [Banamind](https://banamind.ai/) |
| Sifu / Kodifly (HK) | $399/site/month per third-party listing, not on Sifu's site — [SOTA2](https://www.sota2.com/products/kodifly-sifu); 30-day one-site pilot, no lock-in; "12 pilot slots remaining this quarter" — [Sifu](https://www.getsifu.ai/en) | Not found | Unnamed "major infrastructure project" PM testimonial — [Sifu](https://www.getsifu.ai/en) |
| Valoon (DE) | Tiered per-user licence, WhatsApp-only users (crews, subs) free; no prices — [Valoon](https://valoon.chat/) | Conflicting: $53K (PitchBook, 2023 accelerator + 2024 VC) — [PitchBook](https://pitchbook.com/profiles/company/541531-99); $161K incl. EXIST grant June 2025 — [Caplight](https://www.caplight.com/company/valoon); €25K NRW prize 2025 — [Valoon](https://valoon.chat/); undisclosed June 2026 round from Jaeger Gruppe — [Startup.eu](https://www.startup.eu/startup/valoon) | 3,000+ projects, 10 countries — [Valoon](https://valoon.chat/) |
| Pillar (IT) | Not found | €12M seed 12 May 2026 (Base10, Earlybird; Italian Founders Fund, Emblem); €3.2M pre-seed 2025 (Plug and Play, Kima, B Heroes); €15.2M total — [Vestbee](https://www.vestbee.com/insights/articles/pillar-raises-12-m) | 500+ firms, 2,000+ projects — [Vestbee](https://www.vestbee.com/insights/articles/pillar-raises-12-m) |
| Velora (India-based) | Per project, custom; discounted 3-month pilot; DPR Generator free — [Velora](https://velora.ai/) | Unfunded per Tracxn — [Tracxn](https://tracxn.com/d/companies/velora-ai/__1HZ6x1vS43aKGJoN_r2SpIbaNEBP2takduOjyNTL62g) | No named customers — [Velora](https://velora.ai/) |
| Kraaft (FR) | Not researched | €13M Series A Jan 2025; €3.2M seed 2023 — [Tech.eu](https://tech.eu/2025/01/21/kraaft-raises-13m-series-a-to-scale-super-app-for-the-construction-industry/) | 1,000 companies (2025) / 30,000+ users (Dealroom) — [Dealroom](https://app.dealroom.co/companies/kraaft) |
| OnSite (SG) | Not disclosed | S$1.7M / US$1.3M seed ~Apr 2026 — [e27](https://e27.co/onsite-raises-us1-3m-to-fix-constructions-whatsapp-problem-20260408/) | Beta, SG/HK design partners — [e27](https://e27.co/onsite-raises-us1-3m-to-fix-constructions-whatsapp-problem-20260408/) |
| Benetics (CH) | Not found | Conflicting: CHF 2M (Venture Lab) — [Venturelab](https://www.venturelab.swiss/Benetics-The-Venture-Leader-Technology-empowering-construction-professionals); "not raised" (Tracxn) — [Tracxn](https://tracxn.com/d/companies/benetics/__tyZg9uU6J0xNCL2oAw6uFsz_3Km5-4lXU30xJEyoeZo); bootstrapped + angels, first round planned end-2024 — [Roland Berger interview](https://www.benetics.ai/en/blog/roland-berger-interview-benetics) | Built with 15 trade companies — [Construction Management](https://constructionmanagement.co.uk/benetics-launches-ai-based-voice-assist-for-construction-workers/) |
| BRKZ (KSA) | — | $31M — [Ventureburn](https://ventureburn.com/brkz-raises-31m-ai-construction-procurement/) | — |
| Trunk Tools (US) | — | $40M Series B Jul 2025, $70M total — [Insight Partners](https://www.insightpartners.com/ideas/trunk-tools-closes-40m-series-b-to-lead-constructions-ai-transformation/) | Hundreds of projects; 5x revenue in 6 months — same |
| Kojo (US) | — | $10M Wesco extension Sept/Oct 2025; ~$94M total — [Business Wire](https://www.businesswire.com/news/home/20251016530530/en/Kojo-Poised-to-Revolutionize-Construction-Materials-Management) | 600+ contractors, $5B+ materials/yr — same |
| Procore Helix | Helix AI reportedly Premier tier only (third-party, unverified) — [Toarn](https://toarn.com/insights/procore) | Public company | — |

### Inferences
- Price anchors for an interview: about $100-400 per month per company or per site for WhatsApp-native reporting; per-project custom pricing in India-facing products.
- Low funding at the WhatsApp-listener layer suggests either early market or a structural limit (platform risk from unofficial access, hard to defend vs incumbents).

### Gaps
- Team sizes not found for any WhatsApp-native player.
- Sifu's $399/site/month comes only from a third-party listing.

## 4. Accuracy numbers, case studies, failure stories

### Takeaway
I found **no independent accuracy measurement** (extraction precision, wrong-entry rate) for any of these products. All numbers are vendor time-saved or adoption claims.

### Cited Findings
- Sifu: reporting time 60+ min -> under 10 min; field update completion ">80%", WhatsApp adoption ">70%" over 30 days; "40-60% of PM time lost to chasing updates", "25% of WhatsApp updates never followed up" — source: "time-tracking data collected across Sifu pilot sites, 2025-2026"; unclear if results or targets — [Sifu](https://www.getsifu.ai/en)
- Banamind: customer-reported 19% lower cost overruns, 25% less rework, 20 h/week saved — [Banamind](https://banamind.ai/)
- Pillar: ~14 h/week admin saved — [Vestbee](https://www.vestbee.com/insights/articles/pillar-raises-12-m)
- Velora: customer quotes cite "3 hours back every Friday" on reports and a "2-week pilot abandonment" (of a previous tool); cites 2024 Dodge study that coordination gaps erode an average 10% of annual profit margin — [Velora](https://velora.ai/)
- Procore keeps mandatory human review of every agent-drafted daily log — [Procore AI Agents](https://www.procore.com/ai/agents)
- Failure stories found only at the WhatsApp-access layer (account bans with unofficial libraries) — [Baileys issue #2309](https://github.com/WhiskeySockets/Baileys/issues/2309)

### Inferences
- In an interview, a credible differentiator is to measure and publish right / wrong / needs-review rates per field (amount, vendor, quantity, project) on held-out projects, and to design for "refuse and ask" rather than silent wrong ERP entries; none of the competitors show such numbers publicly.

### Gaps
- No independent reviews (G2/Capterra) or press investigations of extraction errors for any WhatsApp-native construction product.
- No public case study with before/after data audited by a third party.
