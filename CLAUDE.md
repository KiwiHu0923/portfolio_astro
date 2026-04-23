# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static portfolio website for ChiWei Hu (William) built with Astro, deployed on Vercel. The site features an academic-style design inspired by [pbb.sh](https://pbb.sh), with a global profile sidebar and timeline-style experience page.

**Live Site**: https://astro-site-nine-puce.vercel.app

## Architecture

### Tech Stack

- **Framework**: Astro (v6.1.8, static site generator)
- **Styling**: CSS with custom properties for theming (light/dark mode)
- **Deployment**: Vercel (static hosting with global CDN)
- **Transitions**: Astro View Transitions (ClientRouter)

### Project Structure

```
astro-site/
├── src/
│   ├── components/
│   │   └── ThemeToggle.astro      # Dark mode toggle button
│   ├── data/
│   │   └── projects.json          # Legacy project metadata (unused by new pages)
│   ├── layouts/
│   │   └── BaseLayout.astro       # Main layout — includes profile sidebar
│   └── pages/
│       ├── index.astro            # Homepage — bio content (About + Experience summary)
│       ├── experience.astro       # Timeline view: Education / Work / Projects
│       ├── 404.astro              # Error page
│       └── projects/
│           ├── index.astro        # Projects list page
│           └── movie-tracking.astro  # Legacy project detail page
├── public/
│   ├── css/styles.css             # Global stylesheet
│   ├── img/                       # Images (headshot, thumbnails, etc.)
│   └── Resume.pdf                 # Downloadable resume
├── astro.config.mjs
├── package.json
└── vercel.json
```

### Key Design Patterns

**Global Layout (two visually-matching cards)**: `BaseLayout.astro` renders a `.layout` wrapper (no background of its own, `max-width: 1100px`). Inside it:
- **Left**: `.profile-sidebar__inner` — headshot, name, Chinese name, social icons. On desktop (≥768px), the outer `.profile-sidebar` is `position: fixed; top: 50%; transform: translateY(-50%)`, so the card stays pinned to the vertical center of the viewport while only the right column scrolls. `left` uses `max(1.5rem, calc((100vw - 1100px) / 2 + 1.5rem))` so it aligns with the layout container on large viewports but stays 1.5rem from the edge on small ones.
- **Right**: `.page-content` — slot for per-page content. Uses `margin-left` equal to `sidebar_width + gap` to leave room for the fixed sidebar.

Both cards share identical styling (`--color-card-bg`, border, `border-radius: 16px`, padding) so they read as a matched pair. On mobile the two stack vertically.

Page-level files (`index.astro`, `experience.astro`, `projects/index.astro`) therefore only render their main content; they do not repeat the sidebar.

**Header**: `BaseLayout.astro` renders only the nav (About / Experience / Projects). The name "ChiWei Hu (William)" lives in the profile sidebar only — don't add a page-level `<h1>` with the name again.

**Nested card backgrounds**: Because `.page-content` uses `--color-card-bg`, any nested card on top of it (e.g. `.project-item`) uses `--color-bg` so it contrasts with the surrounding surface. Keep this rule in mind when adding new card-like elements.

**Timeline Pattern** (`experience.astro`): Each section (Education, Work Experience, Projects) uses:
```
.timeline-section
  .timeline__heading
  .timeline
    .timeline__item
      .timeline__node        ← circle sitting on the vertical line
      .timeline__content
        .timeline__title     ← bold title
        .timeline__org       ← accent-colored pill badge
        .timeline__date      ← monospace date
```
A vertical line is drawn via `.timeline__item::before`; the last item in each section omits it.

**Theming**: Dark/light mode implemented via:
- CSS custom properties on `:root` and `:root[data-theme="dark"]`
- `localStorage` for persistence
- Inline script in `<head>` to prevent flash on page load

### Navigation

`BaseLayout.astro` nav links (active state tracked by `currentPath`):
- `/` → About
- `/experience` → Experience
- `/projects` → Projects

## Development Commands

```bash
cd astro-site

npm install
npm run dev       # Dev server, usually http://localhost:4321
npm run build     # Production build to dist/
npm run preview   # Preview built output
```

## Deployment

Vercel auto-deploys from the `main` branch. To deploy manually:

```bash
cd astro-site
vercel --prod --yes
```

To push changes **without** triggering auto-deploy, push to a non-main branch (e.g. `dev/redesign`).

See `.claude/skills.md` for detailed deployment procedures.

## Adding / Editing Content

| Change | File |
|--------|------|
| Bio / About text | `src/pages/index.astro` |
| Education, Work, Project timeline entries | `src/pages/experience.astro` |
| Project list + repo links + descriptions | `src/pages/projects/index.astro` |
| Navigation links | `src/layouts/BaseLayout.astro` |
| Profile sidebar (headshot, name, socials) | `src/layouts/BaseLayout.astro` |
| Theme colors, layout, timeline styles | `public/css/styles.css` |

## Bio Styling Conventions (`index.astro`)

Inside `.bio-content`, inline spans are styled with one of two classes:
- `.bio__link` — hyperlinks to external orgs (bold, accent color, underline on hover).
- `.bio__keyword` — non-link highlights for technical terms or orgs without a URL (bold + accent color only; no background, no hover effect). Use this for tech stack (C++, Rust, Apache Thrift…) and for organizations that should be emphasized but not linked.

Block rhythm: `.bio__heading` has `margin-top: 2.25rem` (with `:first-child` reset) to give each section clear breathing room. Don't remove the `:first-child` reset or the first heading will have a phantom gap above it.

## Fonts

Loaded from Google Fonts in `BaseLayout.astro` `<link>`:
- **Lato** (400, 700) — body/UI font, assigned via `--font-sans`.
- **Ma Shan Zheng** — kaiti-style Chinese calligraphy, used only for `.profile__name-chinese`. Fallback stack includes `BiauKai`, `DFKai-SB`, `標楷體`, `Kaiti`, `serif`, so the Chinese name still renders in a kaiti family if the Google Font fails to load.

## CSS Custom Properties

Theme colors are defined in `public/css/styles.css`:
- `--color-bg`, `--color-text`, `--color-text-secondary`, `--color-heading`
- `--color-accent`, `--color-accent-hover`
- `--color-link`, `--color-link-hover`
- `--color-card-bg`, `--color-card-border`, `--color-border`
- `--color-footer-bg`, `--color-footer-text` (footer removed, vars retained)
- Transitions: `--transition-fast` (180ms), `--transition-normal` (250ms)

Current palette is tuned for the single-card layout (light: bg `#e5e7ee` / card `#ffffff`; dark: bg `#0a0b14` / card `#1b1e2a`). Nested elements like `.project-item` use `--color-bg` so they contrast on top of the card surface. If you touch these values, preserve the three-tier relationship: page-bg (darkest/lightest) → card-bg (the big layout card) → nested cards use page-bg again.

## Working Conventions

- **Always update `CLAUDE.md` and `TODO.md` after any code change** so they stay in sync with the implementation.
- When making changes that should *not* trigger a Vercel production deploy, push to a branch other than `main`.
