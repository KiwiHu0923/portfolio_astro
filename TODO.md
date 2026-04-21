# Portfolio Website Redesign TODO

Redesign portfolio to visually match [pbb.sh](https://pbb.sh) - a clean, academic-style portfolio.

> **Note**: This focuses on visual similarity, not architectural changes. Your current Astro + JSON setup works fine.

---

## Phase 1: Layout & Navigation Redesign ✅ COMPLETED

### New Page Structure
- [x] **About** (`/`) - Make this the homepage with profile section
- [x] **Experience** (`/experience`) - Professional background and positions
- [x] **Projects** (`/projects`) - Expanded project showcase (replaces current home)

### Navigation Updates
- [x] Update `BaseLayout.astro` navigation to: About | Experience | Projects
- [x] Add smooth view transitions between sections (ClientRouter already implemented)
- [x] Implement tab-style navigation highlighting (nav__link--active)

### Profile Section (Homepage)
- [x] Add profile avatar/headshot (circular, prominent placement)
- [x] Display name with secondary text: "ChiWei Hu (William)" / 胡齊崴
- [ ] ~~Add location/affiliation line~~ (skipped per user request)
- [x] Create social links row:
  - [x] CV/Resume link
  - [x] GitHub
  - [x] LinkedIn
  - [x] Email
- [ ] Add affiliation logos section (universities, companies)

---

## Phase 2: Component Development ✅ (Basic Implementation Done)

> **Note**: Profile and social links were integrated directly into `index.astro` for simplicity. These can be extracted into separate components later if needed.

### Components Status
- [x] Profile section - Integrated in `index.astro`
- [x] Social links with SVG icons - Integrated in `index.astro`
- [x] Experience entries - Integrated in `experience.astro`
- [x] Project cards - Already exists (reused from original)
- [ ] `NewsTimeline.astro` - Scrollable timeline (future enhancement)
- [ ] `AffiliationLogos.astro` - Row of organization logos (future enhancement)

### Enhanced Existing Components
- [x] `ThemeToggle.astro` - Working with sun/moon icons
- [x] System preference detection - Already implemented

---

## Phase 3: Styling Overhaul ✅ COMPLETED

### Design System Updates
- [x] Update CSS custom properties for new color palette:
  - Light mode: Clean academic palette (#fafafa bg, #2563eb accent)
  - Dark mode: Softer dark theme (#0f0f0f bg, #60a5fa accent)
  - Added --color-heading, --color-accent-hover, --color-link-hover
- [x] Add accent color highlighting for keywords and links
- [x] Implement smoother transitions (180ms cubic-bezier)

### Layout Improvements
- [x] Project cards with hover effects (translateY, shadow, border color)
- [x] Category tags with accent background
- [x] Experience items with left border indicator
- [x] Social links with hover states

### Typography
- [x] Added typography scale (h1-h4)
- [x] Proper heading hierarchy with --color-heading
- [x] Responsive font sizing (@media max-width: 640px)
- [x] Font smoothing for better rendering

---

## Phase 4: Content & Pages

### Homepage Content
- [ ] Write compelling bio/introduction
- [ ] Add "Research Focus" or "What I Do" section with 2-3 key areas
- [ ] Create news/updates timeline with recent achievements
- [ ] Add "Selected Projects" preview section

### Experience Page
- [ ] Create timeline of professional experience
- [ ] Add education section
- [ ] Include skills/technologies section

### Projects Page
- [ ] Keep existing movie-tracking project
- [ ] Add additional projects to `projects.json`
- [ ] Create new project detail pages in `src/pages/projects/`
- [ ] Implement filtering by category/tag (optional)

---

## Phase 5: Polish (Optional)

### Accessibility
- [ ] Audit and improve ARIA labels
- [ ] Ensure keyboard navigation works
- [ ] Test with screen reader
- [ ] Verify color contrast ratios

### Performance
- [ ] Optimize images (use Astro Image component)
- [ ] Implement lazy loading for cards/images
- [ ] Minimize CSS bundle size
- [ ] Add proper caching headers

### SEO
- [ ] Add meta descriptions to all pages
- [ ] Implement Open Graph tags
- [ ] Add structured data (JSON-LD)
- [ ] Create sitemap

### Analytics (Optional)
- [ ] Add Vercel Web Analytics
- [ ] Set up basic event tracking

---

## File Structure Target

```
astro-site/
├── src/
│   ├── components/
│   │   ├── ProfileCard.astro      # NEW: Avatar, name, bio
│   │   ├── SocialLinks.astro      # NEW: Social icons row
│   │   ├── NewsTimeline.astro     # NEW: Recent updates
│   │   ├── ProjectCard.astro      # NEW: Enhanced project card
│   │   ├── ExperienceCard.astro   # NEW: Work/education entry
│   │   └── ThemeToggle.astro      # EXISTS: Dark mode toggle
│   ├── data/
│   │   ├── projects.json          # EXISTS: Project data
│   │   └── experience.json        # NEW: Work/education data
│   ├── layouts/
│   │   └── BaseLayout.astro       # EXISTS: Update nav
│   ├── pages/
│   │   ├── index.astro            # MODIFY: Profile/About page
│   │   ├── experience.astro       # NEW: Experience page
│   │   ├── projects/
│   │   │   ├── index.astro        # NEW: Projects list
│   │   │   └── [existing].astro   # EXISTS: Project details
│   │   └── 404.astro              # EXISTS
│   └── styles/                    # OPTIONAL: Move styles here
├── public/
│   ├── css/styles.css             # EXISTS: Update styles
│   ├── img/
│   └── Resume.pdf
└── package.json
```

---

## Quick Wins ✅ COMPLETED

1. [x] Update navigation in `BaseLayout.astro` (About | Experience | Projects)
2. [x] ~~Create `ProfileCard.astro` component~~ (integrated directly in index.astro)
3. [x] Redesign `index.astro` as About/Profile page
4. [x] Add social links row with icons
5. [x] Create `experience.astro` page

---

## Reference

- **Target Design**: [pbb.sh](https://pbb.sh)
- **Source Repo**: [github.com/sleepymalc/pbb.sh](https://github.com/sleepymalc/pbb.sh)
