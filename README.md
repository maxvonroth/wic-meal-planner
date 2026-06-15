# Maine WIC Meal Planner

A working web application built to help my family maximize our Maine WIC food benefits — designed, scoped, and shipped without writing a single line of code.

**Live app:** [maxvonroth.github.io/wic-meal-planner](https://maxvonroth.github.io/wic-meal-planner)

---

## What This Project Actually Demonstrates

This app exists because I had a real problem and figured out how to solve it using AI as the primary tool. I'm not a developer. I don't have a technical background. What I do have is the ability to identify a problem worth solving, break it into pieces, choose the right tools, and iterate until something useful ships.

Every feature in this app started as a plain-language description of what I needed. I worked with Claude (Anthropic's AI assistant) as a development partner across multiple sessions — scoping requirements, troubleshooting when things broke, making tradeoffs, and continuously refining based on how my wife (the primary user) actually interacted with it.

That process — translating real-world needs into working AI-powered solutions — is what I'm looking to do professionally.

---

## The Problem

WIC (Women, Infants, and Children) is a federal nutrition assistance program. Our household — two infants, a toddler, and a postpartum mom — participates in Maine's program. WIC covers specific food categories: fresh produce, dairy, whole grains, legumes, eggs, and a few others. The challenge is knowing which of your recipes align with those categories, and at the store, knowing exactly what goes on which part of the bill.

There's no good tool for this. So I built one.

---

## What It Does

### Recipe Library
63 family recipes imported in bulk from our existing recipe app, each automatically analyzed for WIC alignment. Searchable, filterable, and fully editable. Vegetarian-adaptable recipes are auto-flagged.

### WIC Scoring Engine
A custom two-step scoring system: first it checks for disqualifiers (oils, spices, condiments, heavily processed items), then scores against WIC-eligible categories. Every recipe gets a visual score so it's easy to plan around our benefits.

### Weekly Meal Planner
A 7-day planning grid. Designate anchor recipes for the week and the app suggests others that share ingredients — reducing both food waste and shopping complexity.

### Shopping List
Pulls from the week's meals and splits automatically into what WIC covers vs. what we pay for ourselves. Can also be sorted by grocery section. An AI layer consolidates the list — combining duplicates, standardizing quantities, removing redundant entries.

### URL Recipe Import
Paste any recipe link and the app extracts and imports it. AI handles the parsing when standard extraction isn't enough.

---

## How It's Built

A single HTML file hosted on GitHub Pages, with four external services wired together:

| Service | Role |
|---|---|
| **GitHub Pages** | Free hosting — updates automatically when the file changes |
| **Firebase (Google)** | Cloud database for real-time sync across devices |
| **Cloudflare Workers** | Secure server-side middleman for AI calls and external requests |
| **Anthropic Claude API** | Powers shopping list consolidation and recipe extraction |

Choosing this stack was itself a design decision: free or near-free tiers across the board, no backend to maintain, and enough capability to handle everything the app needs.

---

## AI Integration Points

Rather than using AI as a novelty, each integration solves a specific problem where rules-based logic would fall short:

**Shopping list consolidation** — Ingredient lists from multiple recipes contain duplicates, inconsistent units, and redundant entries ("1 cup flour" and "2 cups flour" from different recipes). A rules-based deduplicator would need to anticipate every possible phrasing. AI handles the variation naturally.

**Recipe extraction from URLs** — Recipe websites structure their content differently. Rather than writing scrapers for individual sites, AI reads the page and pulls out the relevant content regardless of how it's laid out.

**WIC ingredient scoring** — Determining whether "low-sodium chicken broth" is a WIC-eligible protein or a disqualifying processed ingredient requires judgment, not just a keyword match. The scoring engine uses categorical logic informed by that kind of reasoning.

---

## Real-User Feedback Loop

My wife does the actual grocery shopping, which makes her the most important user of this app. A core principle of the project has been to gather her feedback on friction points and missing features before building further — rather than adding features speculatively. That discipline shapes what gets prioritized next.

---

## What's Next

- **Maine WIC Approved Product List** — Maine WIC publishes a public database of every approved product with UPC codes and categories. The plan is to make it searchable in the app, let users star preferred products per category, and surface only those on the shopping list — solving the hardest part of in-store WIC shopping.
- **Printable shopping list** — Clean print/PDF export
- **Firebase Authentication** — More robust multi-user login for the long term

---

## Project Context

Built over several weeks in early 2026. I have no programming background. This was conceived, scoped, and shipped entirely through AI-assisted development — which I think of less as a workaround and more as the point.
