# Portfolio Design Specifications

## Design Philosophy

This site belongs to a humanist who builds. The design should embody that — warm, intentional, distinctive, accessible. Not a template. Not "developer portfolio." Not "academic homepage." The contrast between scholarly and technical IS the story, and the design should hold both.

Inspired by the Autograder4Canvas interface: warm amber, dusty rose, and steel blue on dark backgrounds. The portfolio draws from that palette selectively — it's not a CRT terminal, but it carries the same warmth and intentionality.

## What It Should Signal

To an anthropology hiring committee: "This person thinks about design as practice."
To a tech audience: "This person has scholarly depth behind the code."
To everyone: "This was made by someone who cares."

## Color Palette

Drawn from the Autograder4Canvas design system, adapted for web readability.

### Backgrounds (Warm Near-Black)
- `--bg-void`: #0E0A04 — page background, deepest layer
- `--bg-surface`: #1A1408 — content surface
- `--bg-card`: #241C0C — cards, elevated elements
- `--bg-elevated`: #2E2410 — hover states, active cards
- `--bg-input`: #120E06 — form inputs, recessed areas

### Text (Warm Off-White)
- `--text-primary`: #F0E6D0 — primary body text, headings
- `--text-secondary`: #C0B090 — secondary text, descriptions
- `--text-muted`: #8A7A60 — captions, metadata, timestamps

### Accent Colors
- `--amber`: #F0A830 — primary accent. Links, headings, active states
- `--amber-mid`: #C08820 — secondary amber. Hover text, subheadings
- `--amber-dim`: #7A5418 — muted amber. Borders, subtle elements
- `--rose`: #CC5282 — secondary accent. Decorative, highlights, key moments
- `--rose-hot`: #E8709E — rose hover states, emphasis
- `--rose-dim`: #7A3458 — muted rose. Subtle accents
- `--blue`: #6A9AB8 — tertiary accent. External links, research section
- `--blue-bright`: #90C8F0 — bright blue for high emphasis
- `--blue-dim`: #4A7090 — muted blue

### Borders
- `--border`: #3A2808 — default borders (warm, not gray)
- `--border-hover`: #6A4A12 — hover/focus borders

### Status
- `--green`: #72B85A — success/active indicators
- `--red`: #C04020 — error states

### Contrast Notes
- All body text (--text-primary on --bg-void) exceeds WCAG AAA (>15:1)
- Amber on dark backgrounds exceeds WCAG AA (>7:1)
- Rose is used for decorative/large text only (contrast ~3:1 on dark) — never for body text
- Blue on dark backgrounds meets WCAG AA (>4.5:1)

## Typography

Three typefaces, each serving a role:

### Fraunces (Display/Headings)
- Variable serif with optical sizing
- Warm, characterful, scholarly without being stuffy
- Used for: page titles, section headings, the name on the home page
- Weights: 400 (regular), 600 (semibold), 900 (black for the name)
- Google Fonts: `Fraunces:ital,opsz,wght@0,9..144,400;0,9..144,600;0,9..144,900`

### DM Sans (Body)
- Clean geometric sans-serif
- Excellent readability at body sizes
- Used for: paragraphs, descriptions, nav links, metadata
- Weights: 400, 500, 600
- Google Fonts: `DM+Sans:wght@400;500;600`

### JetBrains Mono (Code/Technical)
- Developer-standard monospace with ligatures
- Used for: project names in technical context, code snippets, repo links
- Weight: 400
- Google Fonts: `JetBrains+Mono:wght@400`

### Type Scale
- `--text-xs`: 0.75rem (12px) — metadata, timestamps
- `--text-sm`: 0.875rem (14px) — captions, small labels
- `--text-base`: 1rem (16px) — body text
- `--text-lg`: 1.125rem (18px) — lead paragraphs
- `--text-xl`: 1.5rem (24px) — section headings (h3)
- `--text-2xl`: 2rem (32px) — page titles (h2)
- `--text-3xl`: 3rem (48px) — hero heading (h1)
- `--text-4xl`: 4rem (64px) — name display on home

## Layout

### Grid
- Max content width: 1200px, centered
- Content padding: 2rem (mobile), 4rem (desktop)
- Card grid: CSS Grid, auto-fill, min 320px columns

### Spacing Scale
- `--space-xs`: 0.25rem (4px)
- `--space-sm`: 0.5rem (8px)
- `--space-md`: 1rem (16px)
- `--space-lg`: 2rem (32px)
- `--space-xl`: 4rem (64px)
- `--space-2xl`: 8rem (128px)

### Responsive Breakpoints
- Mobile: < 640px
- Tablet: 640px – 1024px
- Desktop: > 1024px

### Navigation
- Top bar: name left, links right
- Mobile: hamburger menu with slide-in panel
- Active page indicated with amber underline
- Links in DM Sans, 500 weight

### Footer
- Minimal: links to GitHub, Bluesky, LinkedIn, email
- Copyright notice
- "Humanist who builds" tagline

## Page Structure

### Home
- Hero: Name (Fraunces, large), identity statement, headshot (circle crop)
- Brief intro paragraph
- 3 feature cards linking to Research, Projects, Publications
- Warm, inviting, not overwhelming

### Research
- 5 research program sections
- Each with title, description, key publications/outputs
- Visual hierarchy through amber/rose section accents

### Publications
- Full publication list under "L. June Bloch"
- Earlier names (Lee Bloch, Leigh Bloch) noted with context: "Earlier publications appear under previous names."
- Grouped by type or journal
- Links to PDFs/DOIs where available

### Projects
- Cards for each built project (Reframe, Autograder4Canvas, EvalEye, Podcast-Editor, readthrough)
- What it does, why it matters, link to repo
- Monospace typography for project names

### Teaching
- Courses taught (Anthropology, Ethnic Studies, Native American Studies)
- Teaching philosophy
- Multiverse School participation (professional development)

### CV
- Downloadable PDF link (prominent)
- Web-rendered version of key CV sections

## Accessibility Requirements (Hard Constraints)

- WCAG 2.1 AA minimum, AAA where achievable
- Skip-to-main-content link
- Semantic HTML throughout (nav, main, article, section, aside, footer)
- All images have alt text
- Focus-visible styles on all interactive elements (amber outline)
- prefers-reduced-motion: disable all animations
- prefers-color-scheme: light mode option (future — design for dark-first, light-compatible palette)
- Keyboard navigable throughout
- No information conveyed by color alone
- Text resizable to 200% without layout breakage
- Link text is descriptive (no "click here")

## Visual Details

### Cards
- Background: --bg-card
- Border: 1px solid --border
- Border-radius: 8px
- Hover: border shifts to --border-hover, subtle amber glow shadow
- Padding: --space-lg

### Links
- Color: --amber
- Hover: --amber-mid, subtle underline
- External links: --blue, with subtle external-link indicator
- Focus: 2px solid --amber outline with 2px offset

### Subtle Effects
- Cards get a very subtle radial gradient (echoing Autograder phosphor bloom)
- Hero section: faint radial gradient from center, amber-tinted
- No heavy animations — respect reduced-motion universally
- Noise/grain texture overlay at <5% opacity for warmth (optional, test first)

## Future Considerations

- Light mode toggle (Phase 3+)
- Project demo screenshots/videos
- Blog/writing section (if Substack launches)
- Integration with Bluesky feed
- Visual art section (if June decides it fits)
