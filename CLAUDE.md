# Business HQ

A 3D "office" dashboard for a trade business (one desk per part of the business), plus an n8n
workflow that feeds the Email desk. Audience is non-technical business owners; see README.md.

## Files
- `business_hq.html`: the whole app in one file (~700 lines). Don't read it all; jump to the part you need:
  - lines ~9-165: `<style>` (CSS)
  - lines ~169-196: `window.BUSINESS_DATA`, the **`YOUR NUMBERS GO HERE`** block. All numbers the page shows
    come from here (`totals`, `sites`, `enquiries`, `jobs`, `events`). `"sample": true` marks sample data.
  - `const PODS = [...]` (~line 226): the 9 desks (id, name, color, big number, rows, roles, blurb, links).
    Add, remove or rename desks here.
  - `const TOUR` (~line 494): the Present mode walkthrough order. `renderPanel` / `renderCards`: the side
    panel and desk cards. `tick` / `nextEvent`: the live event feed driven by `events`.
- `inbox_sorter_workflow.json`: n8n workflow (nodes: Setup, Every minute, Config, Get enquiry emails,
  Normalize, Build AI request, Classify with Gemini, Check AI answer, Log to Google Sheets, Read logged IDs).
- `README.md`: user-facing instructions and the release download link.

## Rules
- The page must keep working when double-clicked (`file://`) with nothing to install: no build step,
  no bundler, no `fetch()` of local files. Keep it one self-contained HTML file.
- External loads are only three.js r128 from cdnjs and Google Fonts. Don't add other dependencies.
- Keep the `BUSINESS_DATA` keys stable; the README tells users to edit them by hand. If you add a key,
  give it a sample value and make the page cope with it missing.
- Escape any data put into HTML with the existing `esc()` helper.
- The n8n workflow must never change, move or delete emails, and must ship with no credentials,
  email addresses or API keys in it. Complaints and AI confidence below 80% stay "Needs Human".
- Write user-facing text (README, blurbs) in plain English for a tradesperson, not a developer.
- If you change desks, keyboard keys (1-9, arrows, Esc) or setup steps, update README.md to match.

## Checking changes
- Validate the workflow JSON: `python3 -c "import json; json.load(open('inbox_sorter_workflow.json'))"`
- Open the page in headless Chromium (Playwright is preinstalled in cloud sessions) and check there are
  no console errors and the desks render.
