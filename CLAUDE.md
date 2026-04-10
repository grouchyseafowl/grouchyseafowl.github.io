# Portfolio Site — Agent Instructions

Academic portfolio for Dr. L. June Bloch. Built with Astro, hosted on GitHub Pages.

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
4. **Specificity over generality.** Named scholars, concrete findings, particular tensions. If a description could appear on any academic's site, rewrite it.
5. **Low friction for June.** She reviews and approves. Agents maintain. The system should not require her initiative to stay current.

## Phase 2 Content Notes

Phase 2 populates the placeholder content. The agent doing Phase 2 must:

1. **Read the full `JUNE_BLOCH_AGENT_BRIEFING.md`** — the entire document, not excerpts
2. **Read the social media voice/story materials** — these provide framing devices (how June talks about her work in accessible, story-driven ways)
3. **Frame through story, not lists.** Research programs should read like "here's the question that keeps me up at night" not "this research program examines..."
4. **Include Multiverse School** on Teaching page under Professional Development
5. **Include Transformative Leadership consulting** on Teaching page (get details from June)
6. **Earlier names** (Lee Bloch, Leigh Bloch) are listed openly with context for readers
7. **Populate publications** from agent briefing + scholar profile + Zotero MCP if available
8. **"Disabled by Design" explainer** — add a section on the home page (below the hero) explaining the concept: systems are designed in ways that produce disability, and redesigning them requires interrogating constitutive power relations. Connect it to the Bluesky handle (@disabledbydesign.bsky.social) and the scholarly work. This is the site's framing concept, not just a brand name.
9. **Add RoboStripper and CGT Skill** to Projects page. CGT skill source: `/Users/june/Documents/Teaching/2026courseplanning/cgt_skill/`. RoboStripper: `/Users/june/Documents/GitHub/RoboStripper/`
10. **Clean headshot needed** — current images have "DISABLED BY DESIGN" text overlay. Either get a clean version from June or CSS-crop the existing one. A clean professional headshot is better for job search contexts.

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

Target domain: `ljunebloch.com` (Cloudflare Registrar, ~$10.46/yr). Currently deploying to `grouchyseafowl.github.io`. When domain is purchased, update `astro.config.mjs` site URL and add CNAME file to `public/`.

## Repo

GitHub repo: `grouchyseafowl/grouchyseafowl.github.io`
Deploy: GitHub Actions on push to main (`.github/workflows/deploy.yml`)
