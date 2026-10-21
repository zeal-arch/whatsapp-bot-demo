# WhatsApp site bot: live demo

A clickable demo of a bot that sits in a home-interior project's WhatsApp group. It reads texts,
voice notes, bill photos and documents, and turns them into records in a project ERP. When it is not
sure, it asks the project manager or the sender instead of guessing.

Open `index.html` for the prep site, or `bot-demo.html` for the bot demo. No install or build is needed.

## What's in this repo

| Path | What it is |
|---|---|
| `index.html` | Interview prep site: the story, the bot design, ERP basics, lead management, product notes, companies, industry, practice questions |
| `bot-demo.html` | The WhatsApp bot demo (light and dark theme) |
| `img/` | Image used by the bot demo |
| `notes/round2-prep.md` | Full prep notes |
| `notes/similar-products.md` | Quick list of similar products |
| `notes/market-research-report.md` | Detailed research report with sources |
| `notes/research/` | The research notes behind the report |

## What you see

- **Phone:** a day of messages in the group "HSR 3BHK – Site": Hinglish and Kannada-English texts
  and voice notes, handwritten bills, a design drawing, a site photo, a PDF quote.
- **Bot console:** the steps the bot runs for each message (read, transcribe, extract, check, decide,
  call the API, reply) and the decision it takes.
- **ERP:** where the data lands: purchases, a PM review queue (with Approve / Reject), payments,
  progress log, documents, and budget against actual spend.

Click any message to see its full trace: the extracted record, the checks, the decision, and every API
call with its request and response. Click the bot card to see its rules, APIs, data map and settings.
Use the theme button to switch between light and dark.

## Important

This is a scripted mock-up of a design. The messages and bot outputs are prepared in advance; no real
AI model or WhatsApp account is connected. All names, shops and amounts are made up. The service
addresses in the API examples are placeholders, apart from the names of WhatsApp and Sarvam AI.

## Image credit

`img/site-kitchen-carcass.jpg`: "Kitchen renovation 9a assembling kitchen cabinet base unit with
countertop not on yet", Wikimedia Commons, released under CC0 (public domain).
https://commons.wikimedia.org/wiki/File:Kitchen_renovation_9a_assembling_kitchen_cabinet_base_unit_with_countertop_not_on_yet.JPG
