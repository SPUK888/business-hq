# Business HQ

**[⬇ Download business-hq.zip](https://github.com/SPUK888/business-hq/releases/latest/download/business-hq.zip)**: unzip it and double-click `business_hq.html`.

A live 3D office for a trade business. Every desk is one part of the business, and each shows its own numbers:

| Desk | What it shows |
|---|---|
| **MyElliot** (reception) | Calls answered and missed. MyElliot is an AI receptionist that answers every call 24/7 and books the job in: [myelliot.uk](https://myelliot.uk/) |
| **Enquiries** | Every enquiry from the website, quote quiz, WhatsApp and phone, and where it came from |
| **Website** | Pages, pages in Google, visits |
| **SEO desk** | Local searches, times shown in Google, clicks, best position |
| **Reviews** | Google reviews, rating, new this month |
| **Jobs** | Quotes sent, jobs won, win rate |
| **Customers** | Customers and follow-ups due |
| **Email desk** | Emails in, answered, sorted automatically |
| **Ads desk** | Ad spend and leads from ads |

## Open it

Download `business_hq.html` and double-click it. It opens in any modern browser; there's nothing to install.

- **Present** (top right) walks through every desk full screen. Use the arrow keys to move and Esc to stop.
- Click any desk, or press 1-9, to open it.

## Your numbers

The numbers shown are sample data. Open the file in a text editor and find `YOUR NUMBERS GO HERE` near the top.
Replace each value with your own: your business name, time zone, calls, enquiries, reviews and so on.

The desks can be connected to update automatically (website analytics, Google Search Console, your
inbox, call answering). Ask about setting that up.

## Inbox Sorter (n8n workflow)

`inbox_sorter_workflow.json` is an [n8n](https://n8n.io) workflow behind the **Email desk**. Every minute it:

1. reads new emails sent to your enquiry address
2. sorts each one with AI: sales enquiry, booking request, question, complaint, spam or other
3. writes a one-line summary, an urgency level and a confidence score
4. logs it to a Google Sheet, skipping any email it has already logged

It **never changes, moves or deletes an email**. Complaints, and anything the AI is less than 80% sure about,
are always marked **Needs Human**.

**Setup:** in n8n, go to *Workflows → Import from file* and pick `inbox_sorter_workflow.json`. The yellow
**Setup** note inside the workflow lists the five steps: your email address, Gmail, a Google AI Studio key,
your Google Sheet, then switch it on. It comes with no logins or accounts attached; you connect your own.
