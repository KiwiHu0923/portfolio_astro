# Portfolio Website TODO

Redesign inspired by [pbb.sh](https://pbb.sh) — clean, academic-style portfolio on Astro.

---

## Phase 1: Layout & Navigation ✅ COMPLETED

- [x] Page structure: About (`/`) | Experience (`/experience`) | Projects (`/projects`)
- [x] Nav updates in `BaseLayout.astro` with active-link highlighting
- [x] Astro View Transitions (ClientRouter)
- [x] Profile section on homepage with headshot, name "ChiWei Hu (William)", Chinese name 胡齊崴
- [x] Social links row: Resume / GitHub / LinkedIn / Email (icons only)

---

## Phase 2: Global Profile Sidebar ✅ COMPLETED

- [x] Profile sidebar moved into `BaseLayout.astro` — appears on every page
- [x] Two-column layout (`.layout` → `.profile-sidebar` + `.page-content`)
- [x] Desktop (≥768px): sidebar is `position: fixed` and vertically centered (`top: 50%; translateY(-50%)`)
- [x] Mobile: stacked layout (sidebar on top, content below)
- [x] Large-screen (≥1200px) centering tweak
- [x] Removed old footer section
- [x] Removed duplicate "William Hu" `<h1>` from header (name lives in sidebar only)
- [x] `.page-content` now renders as a subtle surface card (card-bg + border + radius); nested `.project-item` flipped to page-bg to keep contrast
- [x] `.profile-sidebar__inner` also rendered as a matching surface card so bio + content look symmetric
- [x] Bumped `--color-bg` / `--color-card-bg` contrast so the cards are distinguishable at first glance
- [x] Palette retuned to blue-tinted dark for the card lift (light: `#e5e7ee` / `#ffffff`; dark: `#0a0b14` / `#1b1e2a`)
- [x] Reverted sidebar to `position: fixed` + vertically centered in viewport — only the right column scrolls. Both profile and content still styled as matching cards (not one shared card)
- [x] Added anchor IDs (`#multimedia`, `#weenix`) to `projects/index.astro` and linked them from the "operating system kernel" / "multimedia processing pipelines" keywords in `index.astro` Experience section
- [x] `.project-item:target` highlight: accent border + 3px glow + brief tinted-bg pulse (`project-target-pulse` keyframes); added `scroll-margin-top` + `html { scroll-behavior: smooth }` for a clean anchor jump
- [x] Bio vertical rhythm fixed: `.bio__heading` now has `margin-top: 2.25rem` (reset for `:first-child`), removed orphan `flex: 1` on `.bio-content`
- [x] "胡齊崴" now uses **Ma Shan Zheng** (Google Font, kaiti-style calligraphy) with fallback to `BiauKai` / `DFKai-SB` / `標楷體` / `Kaiti`
- [x] Added `text-align: center` to `.profile-sidebar__inner` so the "ChiWei Hu (William)" name (and any wrapping text) stays centered inside the sidebar card

---

## Phase 3: Styling Overhaul ✅ COMPLETED

- [x] Light palette: `#fafafa` bg / `#2563eb` accent
- [x] Dark palette: `#0f0f0f` bg / `#60a5fa` accent
- [x] Added `--color-heading`, `--color-accent-hover`, `--color-link-hover`
- [x] Transitions: 180ms / 250ms cubic-bezier
- [x] Project card hover (translateY, shadow, border)
- [x] Category tags with accent background
- [x] Social icon hover states
- [x] Typography scale (h1–h4) + responsive font sizing

---

## Phase 4: Content Alignment with Resume ✅ COMPLETED

### `experience.astro` — Timeline Redesign
- [x] Removed all bullet-point details; each node shows only title / org / date
- [x] Education nodes: USC MS CS, NTU MS Biochemistry, NCKU BA Life Science
- [x] Work nodes: Meta SWE Intern (WhatsApp), Strong Electro-Mechanical SWE (CIM)
- [x] **Projects timeline node added** (Multimedia Processing, Weenix, Portfolio)
- [x] Timeline visual: circular nodes on a vertical line, accent pill for organization, monospace date

### `projects/index.astro`
- [x] Three projects with repo links (GitHub / Bitbucket), tags, bullet descriptions
- [x] Dates added: Multimedia (Mar 2026), Weenix (Dec 2025), Portfolio (Sep 2024)
- [x] Descriptions aligned with resume wording

### `index.astro`
- [x] Bio covers USC, Meta, Strong, NTU, NCKU with correct hyperlinks
- [x] Separate "About" and "Experience" headings
- [x] Technical keywords in Experience section highlighted with `.bio__keyword` (tinted accent pill)
- [x] "Strong Electro-Mechanical" in About switched from hyperlink to `.bio__keyword` highlight

---

## Phase 5: Future Enhancements (Optional)

### Content / Features
- [ ] Add school/company logos next to each timeline node (icon column)
- [ ] "Selected Projects" preview on homepage
- [ ] News / updates timeline
- [ ] Expand individual project pages (more detail than the list view)

### Accessibility
- [ ] ARIA label audit
- [ ] Keyboard navigation pass
- [ ] Screen-reader pass
- [ ] Color contrast verification

### Performance
- [ ] Switch `<img>` to Astro `<Image>` component
- [ ] Lazy-load hero/thumbnail images
- [ ] CSS bundle size audit

### SEO
- [ ] Meta descriptions per page
- [ ] Open Graph tags
- [ ] JSON-LD structured data
- [ ] Sitemap

### Infra / Housekeeping
- [x] Removed unused headshot backups from `public/` (`headshot.jpg`, `headshot3.png`, `headshot4.png`, `headshot2-removebg-preview.png`, `public/headshot2.jpg`)
- [x] Switched profile photo source in `BaseLayout.astro` to new `/img/headshot.jpg` (renamed from `headshot.JPG` to lowercase for cross-platform safety on Linux/Vercel)
- [x] Moved misplaced `public/img/Resume.pdf` back to `public/Resume.pdf` (where the `/Resume.pdf` link in `BaseLayout.astro` expects it)
- [ ] Decide whether to keep `src/data/projects.json` and `projects/movie-tracking.astro` (currently orphaned by new list page)
- [ ] Add Vercel Web Analytics (optional)

---

## Reference

- **Target Design**: [pbb.sh](https://pbb.sh)
- **Repo (GitHub)**: https://github.com/KiwiHu0923/portfolio_astro
- **Active branch**: `dev/redesign` (pushed; main untouched to avoid auto-deploy)
