# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static portfolio website built with Astro, deployed on Vercel. The site showcases personal projects with a clean, responsive design featuring dark mode support.

**Live Site**: https://astro-site-nine-puce.vercel.app

## Architecture

### Tech Stack

- **Framework**: Astro (static site generator)
- **Styling**: CSS with custom properties for theming
- **Deployment**: Vercel (static hosting with global CDN)
- **Transitions**: Astro View Transitions (ClientRouter)

### Project Structure

```
astro-site/
├── src/
│   ├── components/          # Reusable UI components
│   │   └── ThemeToggle.astro  # Dark mode toggle button
│   ├── data/
│   │   └── projects.json    # Project metadata
│   ├── layouts/
│   │   └── BaseLayout.astro # Main layout with nav/footer
│   ├── pages/
│   │   ├── index.astro      # Homepage (/)
│   │   ├── about.astro      # About page (/about)
│   │   ├── 404.astro        # Error page
│   │   └── projects/
│   │       └── movie-tracking.astro  # Project detail page
│   └── styles/              # Additional stylesheets
├── public/
│   ├── css/styles.css       # Global stylesheet
│   ├── img/                 # Images (thumbnails, heroes)
│   └── Resume.pdf           # Downloadable resume
├── astro.config.mjs         # Astro configuration
├── package.json             # Node.js dependencies
└── vercel.json              # Vercel deployment config
```

### Key Design Patterns

**Project System**: Projects are stored in `src/data/projects.json`:
```json
{
  "name": "Project Name",
  "thumb": "img/thumbnail.svg",
  "hero": "img/hero.png",
  "categories": ["category1", "category2"],
  "slug": "project-slug"
}
```

Each project has a corresponding page at `src/pages/projects/{slug}.astro`.

**Layout System**: All pages use `BaseLayout.astro` which provides:
- HTML document structure with meta tags
- Navigation with active link highlighting
- Footer
- Theme toggle component
- View transitions (ClientRouter)

**Theming**: Dark/light mode implemented via:
- CSS custom properties (`:root` and `:root[data-theme="dark"]`)
- localStorage for persistence
- Inline script to prevent flash on page load

## Development Commands

```bash
# Navigate to Astro project
cd astro-site

# Install dependencies
npm install

# Start development server (http://localhost:4321)
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## Deployment

```bash
# Deploy to Vercel production
cd astro-site
vercel --prod --yes
```

See `.claude/skills.md` for detailed deployment procedures.

## Adding New Projects

1. Add project metadata to `src/data/projects.json`
2. Create page at `src/pages/projects/{slug}.astro`
3. Import and use `BaseLayout` component
4. Place images in `public/img/`

Example project page structure:
```astro
---
import BaseLayout from '../../layouts/BaseLayout.astro';
---

<BaseLayout title="Project Name | Portfolio">
  <main class="main main--project">
    <!-- Project content here -->
  </main>
</BaseLayout>
```

## Important Files

| File | Purpose |
|------|---------|
| `src/layouts/BaseLayout.astro` | Main layout with nav, footer, theming |
| `src/components/ThemeToggle.astro` | Dark mode toggle button |
| `src/data/projects.json` | Project metadata |
| `public/css/styles.css` | Global styles with CSS variables |
| `vercel.json` | Vercel build configuration |

## CSS Custom Properties

Theme colors are defined in `public/css/styles.css`:
- `--color-bg` - Background color
- `--color-text` - Text color
- `--color-accent` - Accent color
- `--color-link` - Link color
- `--color-card-bg` - Card background
- `--color-footer-bg` - Footer background
