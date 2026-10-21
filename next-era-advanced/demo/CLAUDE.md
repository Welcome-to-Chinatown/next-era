# Restaurant Reorder Dashboard

## What we are building
A simple website for a neighborhood restaurant. The owner picks this week's inventory CSV
with a file picker and instantly sees what is running low, what to order, and what it costs.
Before a file is chosen, the page shows a friendly empty state that points to the file picker.

## Tech stack
- Next.js (App Router) with React and TypeScript
- Chart.js with react-chartjs-2 for charts
- PapaParse to read the CSV
- Plain CSS in app/globals.css. No other UI libraries.
- Use the latest stable versions (install with @latest). Lint uses eslint (`next lint` was
  removed in Next.js 16).

## Data and cleaning rules
Columns: item, category, supplier, unit, on_hand, par_level, unit_cost, weekly_usage,
lead_time_days. Put all cleaning in lib/clean.ts.
- Trim extra spaces and ignore letter case in item, category, and supplier. "produce" and
  "Produce" are the same category. "greenmarket produce co." is "Greenmarket Produce Co."
  Show clean, title-style names.
- An item is BELOW PAR when on_hand is less than par_level. Equal to par is fine.
- Units to order = par_level minus on_hand.
- Reorder cost = units to order times unit_cost.
- An item is URGENT when days of cover is less than lead_time_days, where days of cover =
  on_hand divided by (weekly_usage divided by 7).
- Do the money math in whole cents so totals add up exactly.

## Features
- File picker. Parse and clean in the browser. Show a clear message if columns are missing.
- Four number cards: items tracked, items below par, total reorder cost, items out of stock.
- Bar chart: reorder cost by supplier.
- Table: every below-par item with supplier, on hand, par, units to order, cost, and an
  URGENT badge. Sort by urgent first, then by cost.
- Filters: supplier and category. They change every number, chart, and table.
- A "Copy order list" button for each supplier that copies a plain-text list of what to order.
- Look: clean and simple. Navy #111f75 and yellow #e5e138 on a light grey page. Works on phones.

## Rules
- The user uploads the CSV in the browser. All parsing and math happen in the browser.
- No database, no login, no API routes. Nothing is stored or sent anywhere.
- Do not put the CSV in the public folder. The page must start empty.
- It must pass `npm run build` (and `npm run lint`) and be ready to deploy on Vercel.
- Keep cleaning code in lib/, separate from components in components/.
- This folder already holds CLAUDE.md and the sample CSV. Never delete or overwrite them.
  If create-next-app refuses because the folder is not empty, write the files by hand.
- Explain changes in plain language. Ask before adding new libraries.

## Commands
- `npm install` then `npm run dev` and open http://localhost:3000
- `npm run build` must finish with no errors before every commit
- `npm run lint` to check the code
