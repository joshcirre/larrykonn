# Let's create an actual landing page

## Goal

Turn the current public `/` page into a real product landing page for **Larrykonn** — a minimal demo app that showcases what’s possible with the Laravel AI SDK — so visitors understand the product story before they log in or register.

This doc is the brief for that work. Implementation should follow this context rather than inventing a generic SaaS marketing page.

---

## What Larrykonn is

Larrykonn is a **Laravel AI SDK demonstration app**, not a general productivity SaaS.

It shows a working research workflow:

1. **Capture** research materials (images, documents, URLs)
2. **Analyze** them with AI agents (summaries, categorization, vision)
3. **Index** them into a per-user vector store
4. **Chat** with a research agent that searches the user’s knowledge base first, then the web

Primary stack signals (already in the product):

- Laravel + Inertia React + Fortify auth
- `laravel/ai` agents, streaming, tools, vector stores
- Reverb/Echo for realtime demo affordances
- Deployed on Laravel Cloud
- Repo: `joshcirre/larrykonn`

Public positioning already used in-app:

> Built with Laravel & Laravel AI SDK. Deployed on Laravel Cloud.

External anchors from README:

- Laravel AI SDK: https://laravel.com/ai
- Laravel Cloud: https://laravel.com/cloud
- Live demo: https://larrykonn.laravel.cloud

---

## Current state (baseline)

Route: `GET /` → Inertia `welcome` (`routes/web.php` → `resources/js/pages/welcome.tsx`)

Today the welcome page is a **minimal centered shell**:

- App logo
- “Larrykonn” title
- Log in / Register (or Dashboard if authenticated)

There is no product explanation, feature story, demo framing, or docs/SDK CTA.

Meanwhile, the authenticated product already has a strong demo voice:

- Research library + capture form
- Research chat with streaming agent responses
- Toggleable **feature hint badges** that point at real source files (`FeatureBadge` / `useHints`) for SDK capabilities: streaming, agents, FileSearch, WebSearch, vector stores, conversations, vision, broadcasting, categorization

The landing page should feel like the public front door to that same demo story — not a separate brand.

---

## Audience

Primary:

- Developers evaluating the Laravel AI SDK
- Laravel/Cloud visitors opening the live demo

Secondary:

- People who registered and need a clear “what is this?” reminder before entering Research

Not the audience:

- Generic end-users looking for a research product to buy
- Enterprise marketing buyers needing pricing/plans

---

## Landing-page job

In one viewport (and a short scroll), the page should answer:

1. **What is this?** — Larrykonn, a Laravel AI SDK demo
2. **What can I do here?** — save research, let AI summarize/index it, chat over your knowledge base
3. **Why should I care?** — see agents, streaming, tools, and vector stores in a real Laravel app
4. **What do I do next?** — Register / Log in to try the demo, plus optional links to Laravel AI docs / Cloud / GitHub

---

## Messaging draft (starting point)

**Brand:** Larrykonn (hero-level — do not bury it as nav-only text)

**Headline options (pick one tone and stick to it):**

- “A Laravel AI SDK demo you can actually click through”
- “Research capture, vector search, and agent chat — built with Laravel AI”
- “See Laravel AI agents, streaming, and vector stores in one small app”

**Supporting sentence:**

- “Larrykonn is a minimal demo that captures images, documents, and URLs, analyzes them with AI, and lets you chat across your personal knowledge base.”

**Primary CTA:**

- Authenticated → Dashboard / Research
- Guest → Register (primary) + Log in (secondary)

**Secondary links (footer or quiet tertiary):**

- Laravel AI docs
- GitHub repo
- Laravel Cloud (optional)

Avoid inventing product claims the app does not demonstrate (pricing, teams, sync, mobile apps, etc.).

---

## Suggested page structure

Keep it one composition, not a dashboard.

1. **Hero**
   - Brand name dominant
   - One headline + one short supporting sentence
   - CTA group (Register / Log in or Dashboard)
   - Prefer a product-real visual anchor (research capture, chat, or feature-hint UI) over abstract decoration
2. **How it works** (short, 3 steps max)
   - Capture → Analyze / index → Chat with your knowledge base
3. **SDK capabilities shown in this demo**
   - Mirror the existing feature vocabulary: Agents, Streaming, FileSearch, WebSearch, Vector stores, Conversations, Vision, Broadcasting, Categorization
   - Prefer concrete “you’ll see this in the app” language over buzzword grids
4. **Footer**
   - Reuse the existing product line: Laravel + Laravel AI SDK + Laravel Cloud + GitHub

Optional later (not required for first pass):

- Tiny code snippet from `ResearchAgent` or the stream controller (only if it stays secondary to the product story)
- Link into docs/LARAVEL_AI_GUIDE.md concepts without dumping the whole guide onto the page

---

## Design / implementation constraints

- Implement on the existing Inertia welcome page (`resources/js/pages/welcome.tsx`), keep Fortify registration flag behavior (`canRegister`)
- Match existing app visual language (Tailwind v4, current UI components, logo) rather than introducing a disconnected marketing theme
- Preserve auth CTAs; do not require login to understand the story
- Do not turn the first viewport into a stats/dashboard collage
- Feature badges / hint system already teach SDK details inside the app — the landing page should tease that story, not duplicate every tooltip
- Respect frontend design rules for branded surfaces: brand-first hero, one job per section, real product imagery when possible

---

## Success criteria

- A first-time visitor can explain what Larrykonn demonstrates without opening Research
- The page clearly positions Larrykonn as an **SDK demo**, not a standalone research SaaS
- CTAs still get people into auth → Research quickly
- Messaging aligns with README, in-app footer, and existing feature-hint vocabulary

---

## Out of scope (for this todo’s first landing pass)

- Reworking authenticated Research UX
- New backend routes beyond `/` welcome props
- Full docs site / blog
- Pricing, waitlist, or marketing analytics stack

---

## Implementation notes for the next agent

- Start from `resources/js/pages/welcome.tsx`
- Reuse `@/components/ui/button`, logo, and Wayfinder `login` / `register` / `dashboard` routes
- Consider lightly surfacing the same feature labels already defined in `resources/js/components/demo/feature-badge.tsx`
- After UI lands, verify guest and authenticated states on `/`
- Live reference: https://larrykonn.laravel.cloud
