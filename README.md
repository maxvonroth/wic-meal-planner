# Maine WIC Meal Planner

A personal web app built to help my family make the most of our Maine WIC food benefits. It combines a recipe library, a weekly meal planner, and a smart shopping list — all organized around what WIC will actually cover.

**Live app:** [maxvonroth.github.io/wic-meal-planner](https://maxvonroth.github.io/wic-meal-planner)

---

## Background

WIC (Women, Infants, and Children) is a federal nutrition assistance program. Our household — two infants, a toddler, and a postpartum mom — participates in Maine's program, which covers specific categories of food: fresh produce, dairy, whole grains, legumes, eggs, and a few others. The tricky part is figuring out which of our favorite recipes actually align with those categories, and then building a shopping list that separates what WIC pays for from what we buy ourselves.

I built this app from scratch with no prior coding experience, using Claude (Anthropic's AI assistant) as a collaborative development partner across multiple sessions.

---

## What It Does

### Recipe Library
- Holds 63 family recipes, imported in bulk from the Paprika recipe app
- Each recipe is automatically analyzed to estimate how "WIC-friendly" it is based on its ingredients
- Recipes can be searched, filtered, and opened for editing — ingredients, directions, notes, and recipe name are all editable
- Vegetarian-adaptable recipes are automatically flagged with a badge

### WIC Scoring
- A custom scoring engine reads each recipe's ingredient list and runs it through two checks: first for disqualifiers (spices, oils, condiments, heavily processed items), then for WIC-eligible categories
- Scores are shown visually per recipe so it's easy to see at a glance what fits well with our benefits

### Weekly Meal Planner
- A 7-day grid for planning meals
- You can designate "anchor" recipes for the week, and the app will suggest other recipes that share ingredients — reducing food waste and shopping complexity

### Shopping List
- Pulls ingredients from the week's planned meals
- Automatically sorts items into two columns: what WIC covers vs. what to buy out of pocket
- Can also be viewed organized by grocery section (produce, dairy, pantry, etc.)
- AI-powered consolidation cleans up the list: combining duplicates, standardizing quantities, and stripping redundant entries

### URL Recipe Import
- Paste a link to any recipe webpage and the app will attempt to extract and import it automatically
- Uses AI to parse the page content when standard extraction isn't enough

---

## How It's Built

This is a single HTML file — no frameworks, no build process. The entire app lives in one file that's hosted for free on GitHub Pages. Here's what's running behind the scenes:

### GitHub Pages
Hosts the app at a public URL for free. Every time the source file is updated and pushed to GitHub, the live site updates automatically.

### Firebase Firestore (Google)
A cloud database that stores recipes, notes, and the weekly meal plan. This is what allows the app to sync in real time across multiple devices — my wife and I can both open it on our phones and see the same data.

### Cloudflare Workers
A small server-side script that acts as a secure go-between for the app and external services. It handles two things the browser can't do directly for security reasons: calling the AI API and fetching recipes from other websites. It's protected by a password so only our household can use it.

### Anthropic Claude API
The AI layer. It powers the shopping list consolidation (cleaning up and combining ingredients intelligently) and recipe extraction from URLs (reading a webpage and pulling out the actual recipe).

### Google Cloud Console
Used only for one thing: locking down the Firebase API key so it can only be called from our app's domain — a basic security measure to prevent misuse.

---

## Security

The app has a PIN-based lock screen. The PIN is never stored anywhere — only a one-way cryptographic hash of it is kept in the source code. If no PIN has been set (as in this portfolio version), the app opens freely without any prompt.

The Cloudflare Worker that handles AI calls is separately password-protected and only accepts requests that include the correct credential.

---

## Notable Technical Challenges

A few problems that came up during development that are worth highlighting:

**CORS restrictions** — Browsers block web apps from calling certain APIs directly for security reasons. The Anthropic API is one of them. The solution was routing those calls through a Cloudflare Worker, which acts as a trusted server-side intermediary.

**Firebase module scope** — Firebase loads as a JavaScript "module," which runs in an isolated scope. Any functions that needed to respond to button clicks had to be explicitly attached to the `window` object, or the browser couldn't find them.

**Firestore nested arrays** — Firebase's database doesn't support arrays-within-arrays. The weekly meal plan grid (7 days × multiple meals) had to be flattened into a single list before saving, and rebuilt into a grid when loaded back.

**Paprika export quirks** — The bulk recipe import had to account for how Paprika structures its HTML exports. Section headers (like "For the sauce:") were being parsed as ingredients and had to be filtered out.

---

## What's Next

Features planned for future development:

- **Maine WIC Approved Product List integration** — Maine WIC publishes a public CSV of every approved product with UPC codes, brand names, and categories. The plan is to build a searchable version into the app, let users star their preferred products in each category, and surface only those starred items on the shopping list.
- **Printable shopping list** — A clean print or PDF export of the week's shopping list
- **Vegetarian recipe filter**
- **Firebase Authentication** — A more robust multi-user login system for the long term

---

## Project Context

Built over several weeks in early 2026. All development was done collaboratively with Claude — I described what I wanted in plain language, and we worked through the implementation together session by session. This project represents my first experience building and shipping a web application.
