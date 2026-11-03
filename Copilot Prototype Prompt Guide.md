# Using GitHub Copilot to build an interactive dashboard prototype

This guide shows how to get Copilot to produce a clickable, Power BI-style dashboard mockup from a plain-English description. The prototype is a single HTML file that opens in any browser. It uses dummy data, so it needs no data connection and is safe to share for feedback before any Power BI build work.

## Process

1. **Start with a clear brief.** Use the example prompt below as a template. Replace the bracketed items with your own business context.
2. **Let Copilot build a first version, then review it in the browser.** Click through every page, slicer and layout toggle.
3. **Iterate in small, specific requests.** For example, "make the funnel bars log-scaled and say so in the header". Asking for one change at a time makes problems easier to spot.
4. **Ask Copilot to explain any number you don't trust.** For example, "how is VNB calculated?" or "how are the campaign NAP goals derived?". Prototype logic should be visible and easy to defend.
5. **Export the dummy data.** Ask for an Excel file with every dataset and assumption behind the visuals. Your data team can use it to map real sources.
6. **Split or repackage as needed.** For example, "create a separate version with each section as its own page, plus a launch page that links to them".

## Example prompt

```text
Create an interactive dashboard prototype that mimics a Power BI report. Deliver it as a
single self-contained HTML file that works offline in a browser, with no data connection.
Use realistic dummy data that I can explain.

CONTEXT
- Audience: [e.g., marketing leadership and campaign managers]
- Business: [e.g., direct-to-consumer insurance marketing]
- Programs: [e.g., 3 Cross-Sell and 5 Retention campaigns]
- Media tactics: [e.g., Email, Direct Mail, Outbound Calls]
- Reporting period: [e.g., 8 weeks of weekly data, rolled up to monthly and YTD]

CANVAS
- Fixed 1280 x 720 report canvas on a neutral grey page, with Power BI-style look:
  dark navy title bar, slicer row, content area, and page tabs at the bottom
  with "Page X of Y".

PAGES (one tab each)
1. Executive Summary: KPI cards (value, % vs goal, % vs prior period, sparkline), a trend chart
   vs goal that switches metric when a KPI card is clicked, and NAP by media tactic and by
   campaign type, plus a campaign performance table.
2. Full Funnel: stages from [Contacts] to [Buys] with stage-to-stage conversion, a
   conversion-channel breakdown, and a campaign-by-stage heatmap where clicking a row
   filters the page.
3. Journey Analytics: touch-by-touch sequence for a selected campaign, top touch sequences,
   media tactic overlap, and combination lift.
4. Weekly Optimization: a feed of recommended actions with estimated impact, confidence,
   evidence, and Accept/Dismiss buttons.
5. Metric Definitions: searchable table of metric, synonyms, business definition, and
   calculation. Include these metrics: [list your metrics].

INTERACTIVITY
- Slicers: campaign type, campaign, media tactic, conversion channel, and date range
  (with a "Clear filters" button). All visuals respond to the slicers.
- A Layout A / Layout B toggle on each page so I can compare two design options.
- Click behavior: KPI cards change the trend metric; table rows filter the page.

DATA
- Generate dummy data with a seeded random generator so numbers are the same on every load.
- Use realistic funnel rates, week-to-week variation, and campaign-level trends.
- Build all totals, rates, goals, and percentages from one underlying table. Do not hardcode
  display values, so every number reconciles across pages.
- Goals should be derived from the data (state how), not typed in.

STYLE
- Font: Segoe UI. Navy (#1A2B4C) for headers; consistent colors for each campaign type and media tactic.
- Dense but readable, with small fonts (10-13px), tabular numerals, and subtle borders.

When finished, summarize the page list, the data assumptions, and how goals and any
derived metrics are calculated.
```

## Example prompt: simple one-page dashboard

Use this shorter version for a first attempt or a single-topic view. Add pages and features with follow-up prompts.

```text
Create a one-page interactive dashboard prototype that looks like a Power BI report.
Deliver a single self-contained HTML file that works offline in a browser.

CONTEXT
- Audience: [e.g., campaign managers]
- Topic: [e.g., weekly email campaign performance]
- Dimensions: [e.g., campaign, week]
- Metrics: [e.g., sends, clicks, click rate, applications, premium]

LAYOUT (1280 x 720 canvas, navy title bar, slicer row, content area)
- Row of 4-6 KPI cards, each with value, % vs goal, % vs prior period and a sparkline
- One trend chart by week with a goal line
- One breakdown bar chart by [campaign]
- One detail table sorted by [premium], with a variance column
- Slicers for [campaign] and [date range], plus a "Clear filters" button

DATA
- Seeded dummy data (same numbers every load), built from one underlying table
- Every total, rate, and goal is calculated from that table, not typed in
- Goals are derived from the data (explain how)

When finished, summarize the metrics shown and how each is calculated.
```

## Tips for better results

- **Be specific about metrics and their relationships.** Name each metric and say how it rolls up. Copilot will invent a definition if you don't give one.
- **Ask for reconciled data.** The line "build everything from one underlying table" stops numbers from disagreeing between pages.
- **Give one change per follow-up.** Combining many edits in one message makes it hard to tell what changed.
- **Test the interactions yourself.** Try every slicer combination, especially ones that return no data.
- **Ask for the assumptions.** Ask Copilot to list every made-up number (unit costs, margins, goals) so you can replace them with real values.
- **Label it as a mockup.** Dummy data can be mistaken for real results when shared. Keep a "mockup" caption on the canvas.
- **Keep prompts free of sensitive data.** Use fabricated numbers and generic campaign names. Don't paste real customer or financial data into prompts.

## Follow-up prompts that worked well for this prototype

- "Create a separate version that splits the Executive Summary, Full Funnel, and Journey/Weekly Optimization tabs into separate pages, and add a launch page with a short summary of each and links."
- "Create an Excel file that contains all of the dummy data used in this prototype."
- "How are the campaign-level NAP goals on the Executive Summary derived?"
- "Explain how the bars are scaled on the Full Funnel card."
- "How is VNB calculated?"
