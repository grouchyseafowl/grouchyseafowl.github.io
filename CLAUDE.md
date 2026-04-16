# Portfolio Site — Agent Instructions

Academic portfolio for Dr. L. June Bloch. Built with Astro, hosted on GitHub Pages.

**Global behavior instructions are in `~/.claude/CLAUDE.md`.** This file adds project-specific context for the portfolio site.

## Before Any Content Work

**Read the universal briefing first:** `/Users/june/Documents/GitHub/profile/JUNE_BLOCH_AGENT_BRIEFING.md`

This document contains June's full identity, story, publication record, research programs, and voice characteristics. Content on this site must reflect that document, not generic academic language.

**Also read the social media voice/story materials** in `/Users/june/Documents/GitHub/disabled_by_design/voice/` — especially `VOICE_DOCUMENT.md` and `STORY_PROMPT_RESPONSES/`. These contain framing devices, personal stories, and ways June talks about her work that should shape how projects, research, and teaching are described on the site. Don't just list or describe — frame through story.

## Design Constraints

Read `DESIGN_SPECS.md` for the full design system. Key rules:

- **Color palette** is drawn from the Autograder4Canvas interface. Warm amber + dusty rose + steel blue on dark backgrounds. Do not introduce new colors without updating the spec.
- **Typography**: Fraunces (headings), DM Sans (body), JetBrains Mono (code/technical). Do not change fonts.
- **Accessibility is a hard constraint.** WCAG 2.1 AA minimum. Test contrast ratios before changing any color usage. Never use rose (#CC5282) for body text — it doesn't meet contrast requirements.
- **No generic AI aesthetics.** If a design choice could appear on any template site, it's wrong.

## Content Sources

When updating content, pull from these primary sources:

- **Publications**: Scholar profile at `/Users/june/Documents/GitHub/profile/JUNE_BLOCH_AGENT_BRIEFING.md` (publications section)
- **Scholarship summary**: `/Users/june/Documents/Filing/Job Search/synthesis/Bloch_Scholarship_Summary_For_Agents.md`
- **Scholar profile**: `/Users/june/Documents/Filing/Job Search/Bloch_Scholar_Profile.md`
- **Research programs**: Agent briefing (5 research programs section)
- **Projects**: Read READMEs from `/Users/june/Documents/GitHub/Reframe/`, `/Users/june/Documents/GitHub/Autograder4Canvas/`, `/Users/june/Documents/GitHub/readthrough/`, `/Users/june/Documents/GitHub/Podcast-Editor/`
- **EvalEye**: `/Users/june/Documents/Filing/Job Search/Teaching Evals/EvalEye/`
- **Teaching**: `~/Documents/Teaching/2026courseplanning/`
- **Social media content & framing**: `/Users/june/Documents/GitHub/disabled_by_design/pipeline/content_queue/` and `/Users/june/Documents/GitHub/disabled_by_design/voice/` — use these as **framing devices** for how to talk about the work. The social media threads and story prompt responses contain June's voice explaining her research and projects in accessible, story-driven ways. Use that texture instead of dry descriptions or feature lists.
- **Consulting**: June has done transformative leadership consulting (formerly framed as DEI consulting). Get details from June for scope and framing.

## Earlier Names

June has published under Lee Bloch and Leigh Bloch. These are not hidden — include them with a note like "Earlier publications appear under previous names (Lee Bloch, Leigh Bloch)." The goal is legibility for readers tracing her publication record.

## Structure

- `src/pages/` — Astro page components (layout + content together for simple pages)
- `src/layouts/` — Base layout with nav, footer, meta
- `src/components/` — Reusable components (Nav, Footer, Card, etc.)
- `src/styles/global.css` — Design system (colors, typography, spacing)
- `content/` — Markdown content files (for pages that benefit from separating content from layout)
- `public/images/` — Headshot, project screenshots, static assets

## Build & Deploy

```bash
npm run dev      # local dev server
npm run build    # production build
npm run preview  # preview production build
```

Deployment is via GitHub Actions — push to main triggers build and deploy to GitHub Pages.

## Key Principles

1. **Story over list.** Research programs, projects, and teaching should be framed through narrative, not just described. Use the social media content and voice materials for framing inspiration.
2. **The contrast is the message.** The site holds scholarly depth and technical building together. The typography (serif headings + sans body + mono code) embodies this. Don't flatten it.
3. **Accessibility is non-negotiable.** June works on disability. The site must practice what it preaches.
4. **Specificity over generality.** If a description could appear on any academic's site, rewrite it.

## Maintenance Workflow

The site is fully populated as of 2026-04-09. Agents maintain it; June reviews and approves. Do not re-do work that's already done — read the current pages before editing.

**What triggers an update and what to change:**

| Trigger | What to update |
|---|---|
| Paper accepted (in press, no DOI yet) | `publications.astro` — add `<details class="pub-card">` with `In press` badge; no schema entry yet |
| Paper published (DOI assigned) | `publications.astro` — update year badge, add DOI links, add `ScholarlyArticle` entry to `publicationsJsonLd` array at top of file |
| In-press paper gets DOI | Same as above — promote from in-press card to full entry with schema |
| New project ships | `projects.astro` — read the project README first; frame through story not feature list |
| CV PDF changes | Replace `public/files/Bloch_CV.pdf` — no code changes needed |
| New job or affiliation | Update `BaseLayout.astro` Person schema `jobTitle` field + About page + homepage hero as needed |
| New headshot | Replace `public/images/headshot-rect.png` — target 560×700px, compress to <800KB |
| New research finding worth surfacing | `research.astro` — read primary sources first; see Content Sources above |

**Before editing any page:** read it first. Content is inline in `.astro` files. The publications page is the most complex — the `.astro` file is the source of truth, not any JSON data file.

**After any change:** `npm run build` to verify, then commit and push. GitHub Actions deploys automatically on push to main.

## SEO

SEO infrastructure was implemented 2026-04-09. Before making any changes, read the files listed below — don't guess at structure.

### What's implemented and where

**`src/layouts/BaseLayout.astro`** — all site-wide SEO lives here:
- `<meta name="description">` — per-page, passed as a prop
- `<link rel="canonical">` — auto-generated from `Astro.site` + current path
- Open Graph tags (`og:title`, `og:description`, `og:type`, `og:url`, `og:image`, `og:site_name`) — image is absolute URL
- Twitter/social card tags (`twitter:card`, `twitter:title`, `twitter:description`, `twitter:image`)
- `<meta name="author">` — "L. June Bloch"
- **Person JSON-LD schema** — name, job title, image, description, and `sameAs` links to ORCID, GitHub, Bluesky, LinkedIn, Google Scholar
- Optional `jsonld` prop — pass any JSON-LD object or array from a page to inject additional structured data into `<head>`

**`src/pages/publications.astro`** — page-level SEO:
- `ScholarlyArticle` JSON-LD for each published article with a DOI — title, author (with ORCID), journal, date, DOI
- Passed to `BaseLayout` via the `jsonld` prop

**`public/robots.txt`** — allows all crawlers, points to sitemap

**`astro.config.mjs`** — `@astrojs/sitemap` integration generates `sitemap-index.xml` at build time; all 8 pages included automatically

### How to maintain

**Adding a new published article:**
1. Add the `<details class="pub-card">` block to `publications.astro` (inline HTML — the `.astro` file is the source of truth, not any JSON data file)
2. Add a corresponding `ScholarlyArticle` entry to the `publicationsJsonLd` array at the top of the same file
3. Include `datePublished`, `isPartOf.name` (journal), `url` (DOI link), and `identifier.value` (DOI string)

**Updating the Person schema** (job title, affiliations, social links):
- Edit the `sameAs` array and `jobTitle` field in `BaseLayout.astro` (around line 55–68)
- ORCID: `https://orcid.org/0000-0001-6805-0192`

**Adding a new page:**
- The sitemap auto-updates on build — no manual work needed
- Canonical URL auto-generates — no manual work needed
- Pass a custom `description` prop to `BaseLayout` — don't rely on the default

**Google Search Console:**
- Domain verified as of 2026-04-09
- Sitemap submitted: `https://ljunebloch.com/sitemap-index.xml`
- Check Search Console for crawl errors if something seems off

### What's NOT implemented (deliberate)

- No `ScholarlyArticle` schema for articles without DOIs (Academic Precarity 2020, Archaeologies 2014) or in-press/manuscripts — add when DOIs exist
- No Article schema for book chapters, public scholarship, or zines — not worth the noise
- No image srcset/WebP variants — headshot is 560×700px at 703KB, acceptable for now

## Domain

`ljunebloch.com` — live as of 2026-04-09. DNS on Cloudflare. Email forwarding via Cloudflare Email Routing: `june@ljunebloch.com` → Gmail.

## Repo

GitHub repo: `grouchyseafowl/grouchyseafowl.github.io`
Deploy: GitHub Actions on push to main (`.github/workflows/deploy.yml`)

## graphify

This project has a graphify knowledge graph at graphify-out/.

Rules:
- Before answering architecture or codebase questions, read graphify-out/GRAPH_REPORT.md for god nodes and community structure
- If graphify-out/wiki/index.md exists, navigate it instead of reading raw files
- After modifying code files in this session, run `python3 -c "from graphify.watch import _rebuild_code; from pathlib import Path; _rebuild_code(Path('.'))"` to keep the graph current
