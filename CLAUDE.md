# ViFOUNDATION website: instructions for Claude

This repo is the public website vifoundation.ch. **The repository is public. Everything committed here becomes visible to the world.** Read the rules below before every change.

## Rules, in order of importance

1. **Publish only what has been approved.** The user may have access to board minutes, candidate shortlists, internal budgets and correspondence. None of that belongs here. Only text the user has explicitly said is for the website may be committed. If unsure, ask.
2. **Show before you commit.** Before committing, show the user the exact new public text and wait for an OK.
3. **Never push to `main`.** Work on a branch and open a pull request. Vercel builds a preview link for each branch. The user checks the preview and merges. Merging to `main` publishes the site.
4. **Never add bank or account details, IBANs, passwords, tokens, personal phone numbers or private email addresses.** The Support section is email-only by decision of the COO. An earlier version showed an IBAN, which was removed. Do not reintroduce it.
5. **No invented numbers.** If a figure, date or budget is unconfirmed, write "To confirm". Name the source of every figure in the commit message (for example "per Pascal Herzog email, 24 Sep 2026").
6. **Respect strikethrough.** In documents the user supplies, struck-through text means "remove".

## How the site is built

- Static site. `index.html` is the whole site (HTML, CSS and JavaScript). Other files: `llms.txt`, `robots.txt`, `sitemap.xml`, `images/`.
- Project texts live in the `PROJECTS` object inside `<script>` in `index.html` (keys such as `mosan`, `orangutan`, `cachoeira`). The display order is the `ORDER` array.
- A project change usually needs edits in several places: the `PROJECTS` entry, the homepage card or feature box, the JSON-LD block at the top, and `llms.txt`. Search for the project name to find them all.
- Style conventions: British spelling; budgets as `USD 15'000`; en dash for ranges (2026–2029); status labels such as "Active · since 2025", "Closed · 2024–25".

## After every edit, run this check

A stray quote or comma in `PROJECTS` breaks every project page. Run:

```
node -e "
const fs=require('fs');const s=fs.readFileSync('index.html','utf8');
const m=s.match(/const PROJECTS = (\{[\s\S]*?\n\});/);
const P=eval('('+m[1]+')');console.log('projects:',Object.keys(P).length);
for(const b of s.matchAll(/<script type=\"application\/ld\+json\">([\s\S]*?)<\/script>/g))JSON.parse(b[1]);
console.log('JSON-LD ok');"
```

The project count must match the number of cards on the page. Open the branch's preview link and click every project that was changed.

## Open items (as of 5 Nov 2026)

- **Partners:** remove Zurich, Eversys and Coffema by 31 Dec 2026. Add the City of Basel only if its proposal is accepted.
- **Learning Cachoeira:** budget is USD 11'716. The improved project text promised by Pascal Herzog has not arrived. The old text is still live.
- **Orang Utan Coffee:** the Aug 2026 report headline says "603 Farmers", while the site says "350+". Ask what 603 counts before changing either. ViFOUNDATION is listed as funder of USD 15'000; Pascal has not confirmed this.
- **Coffee Value Chain for Climate Action (Guatemala):** budget and funder still say "To confirm".
- **Audited report:** the button opens an email request. Pascal does not want the "Verfügung" published online.
- **Domain and hosting:** vifoundation.ch DNS is still with SELISE, which ends on 31 Mar 2027. The domain must move to an account the foundation controls before then.

## Who decides

Pascal Herzog (COO and Impact, ViCOLLECTIVE; ViFOUNDATION board member) owns the website content. Kurt Lambert (Chairman) has stepped back from day-to-day edits. When content is disputed, ask Pascal.
