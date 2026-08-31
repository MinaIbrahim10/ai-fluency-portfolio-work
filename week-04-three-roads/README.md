# Week 4 — Three Roads: Choose Your Stack with AI

General AI Fluency — Build

## Context

I already have a working AI engineering portfolio, so I treated this assignment as a retrospective stack decision rather than rebuilding the site from scratch.

Portfolio:

https://minaibrahim.tech/

My goal is to keep the site free, easy to maintain, and strong enough to present technical case studies, open-source work, research, live projects, diagrams, and long-form engineering content.

---

# 1. My Constraints

## Cost

Free only.

## Skill Level

Comfortable with:

- HTML
- CSS
- JavaScript
- React
- Vite
- Git / GitHub
- basic deployment workflows
- APIs and backend engineering

I do not need a no-code tool.

## What the Portfolio Needs to Do

The portfolio needs to show:

- a strong AI engineering claim
- selected AI systems
- Generative AI / LLM work
- RAG and agentic systems
- TensorFlow open-source work
- research
- production software
- technical skills
- professional experience
- clear contact actions

## How the Work Must Be Displayed

The portfolio needs to support:

- technical diagrams
- project visuals
- GitHub repository links
- live project links
- research / publication links
- long-form technical descriptions
- runtime metrics
- engineering evidence
- responsive layout

## Dynamic Requirements

No backend is required yet.

The current portfolio is primarily informational and evidence-focused.

A backend would only become useful later if I add features such as:

- authenticated content management
- dynamic project data
- analytics dashboards
- a contact API
- user accounts
- personalized experiences

For the current version, adding a backend would create unnecessary complexity.

---

# 2. Three Stack Options

## Option 1 — Plain HTML / CSS / JavaScript

### Build

Create the site with:

- semantic HTML
- CSS
- small amounts of JavaScript

### Free Hosting

- Cloudflare Pages
- GitHub Pages
- Netlify

### Backend

No.

### Strengths

- simplest option
- very fast
- almost no tooling overhead
- easy to deploy
- easy to host for free
- minimal maintenance

### Trade-Off

As the portfolio grows, reusable sections, project cards, and larger content structures become harder to maintain manually.

Adding richer interactions also becomes less organized than using a component-based framework.

---

## Option 2 — React + Vite

### Build

Use:

- React
- Vite
- reusable components
- static project/content data
- CSS or a lightweight styling system

### Free Hosting

- Cloudflare Pages
- Vercel
- Netlify

### Backend

Not yet.

### Strengths

- component-based structure
- easy to maintain as the portfolio grows
- good support for interactive sections
- simple static deployment
- fast development
- strong ecosystem
- enough power without unnecessary infrastructure

### Trade-Off

It introduces more tooling and JavaScript than a plain static site.

However, the complexity is still small enough to manage comfortably.

---

## Option 3 — Next.js

### Build

Use:

- Next.js
- React
- routing
- static generation
- optional server features

### Free Hosting

Vercel.

### Backend

Not required initially, but server features are available.

### Strengths

- powerful routing
- static generation
- strong SEO tools
- server-side capabilities
- easy path to dynamic functionality later
- useful for larger content-driven applications

### Trade-Off

It introduces additional framework concepts and maintenance that the current portfolio does not need.

The portfolio does not currently require:

- server rendering
- authentication
- server actions
- database-backed content
- complex dynamic routes

Using Next.js now would be more infrastructure than the problem requires.

---

# 3. Pressure Test

## What breaks if I choose the simplest option?

Plain HTML/CSS/JS would still work for the current portfolio.

Nothing critical would break.

The main limitation would appear later when:

- the number of projects grows
- project layouts need to stay consistent
- components are reused across sections
- more interaction is added

I would begin repeating markup and maintaining similar sections manually.

---

## What do I maintain if I choose the most powerful option?

With Next.js I would need to maintain:

- framework upgrades
- routing conventions
- build configuration
- larger dependency surface
- deployment-specific behavior
- potentially server/client component decisions

Those features are useful for a larger application, but they do not currently improve the proof in my portfolio.

---

## Can I finish in two weeks?

### Plain HTML / CSS / JS

Yes, easily.

### React + Vite

Yes.

It provides enough structure without slowing the build down.

### Next.js

Yes technically, but I would spend more time on framework structure than the portfolio actually requires.

---

## Does each option show my work properly?

### Plain HTML / CSS / JS

Yes, but maintaining a growing set of technical cases becomes less convenient.

### React + Vite

Yes.

It handles technical case sections, diagrams, project cards, research links, metrics, and responsive layouts cleanly.

### Next.js

Yes, but most of its additional capabilities would currently go unused.

---

# 4. My Decision

## Chosen Stack

React + Vite with static hosting.

Preferred free hosting:

Cloudflare Pages.

## Why I Chose It

I chose React + Vite because it gives me a clean component-based structure without adding backend or framework complexity that the portfolio does not need.

It is powerful enough to present:

- AI engineering projects
- Generative AI / LLM work
- RAG and agentic systems
- technical diagrams
- TensorFlow runtime evidence
- open-source contributions
- research
- live project links
- long-form technical content

while remaining simple to deploy and maintain.

---

# 5. Why I Did Not Choose the Other Two

## Plain HTML / CSS / JavaScript

I did not choose it as the main long-term stack because the portfolio already contains multiple repeated project and engineering sections.

As the site grows, maintaining those patterns manually would become less convenient.

It is still a good choice for very small static pages, including the Week 4 "Empty but Live" milestone.

---

## Next.js

I did not choose Next.js because the current portfolio does not need server-side features or a backend.

Using it now would add framework complexity without improving how my work is presented.

If the portfolio later becomes a larger dynamic application, I could reconsider it.

---

# 6. Can I Maintain This?

Yes.

I can maintain React + Vite comfortably because:

- the architecture is simple
- the site can remain mostly static
- there is no backend to operate
- deployments are straightforward
- reusable components reduce repeated work
- the dependency surface is manageable

This is important because the best stack is not only one I can build once, but one I can continue updating.

---

# 7. Does It Show My Work Well?

Yes.

React + Vite gives enough flexibility to present technical evidence clearly without making the technology itself the focus.

The stack supports the real goal:

> show strong AI engineering proof and make it easy for visitors to contact me.

---

# Final Rationale

I considered three genuine options: plain HTML/CSS/JavaScript, React + Vite, and Next.js.

I chose React + Vite with free static hosting because it gives the best balance between simplicity, maintainability, and flexibility.

I can maintain this stack, it displays my technical work well, and it does not introduce a backend before one is actually needed.

The backend decision is:

> Not yet.
