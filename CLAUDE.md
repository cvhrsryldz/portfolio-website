# Portfolio Website — Cevher Sarıyıldız

## Project Overview

Personal portfolio website for Cevher Sarıyıldız (Art Director & Prompt Engineer). Static single-page site deployed on **GitHub Pages**. No build system, no bundler, no package manager — pure HTML/CSS/JavaScript served directly.

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Markup | HTML5 (semantic) |
| Styling | Vanilla CSS (inline in `<style>` block) |
| Scripting | Vanilla JavaScript (inline `<script>` blocks) |
| Physics Engine | Matter.js v0.20.0 (CDN, SRI hash) |
| Fonts | Roc Grotesk (local WOFF2/WOFF), Space Mono (Google Fonts CDN) |
| Deployment | GitHub Pages (static) |

**No npm, no Node.js, no TypeScript, no framework.**

## File Structure

```
portfolio-website/
├── index.html          # Main portfolio site (all CSS/JS inline)
├── admin.html          # Admin panel for content management
├── README.md           # Minimal project description
├── CLAUDE.md           # This file
│
├── hero-bg.mp4         # Hero background video (~24MB)
├── about-video.mp4     # Scroll-synced about video
├── hero-audio.mp3      # Hero radio player audio — Daft Punk (5.5MB)
│
├── logo.svg            # Full logo
├── logomark.svg        # Icon-only logo mark (also used as favicon)
├── logotype.svg        # Text-only logotype
├── ai-hero.png         # AI section hero image
├── ai-*.svg            # AI tool icons (chatgpt, claude, midjourney, firefly, higgsfield, gemini)
├── physics-asset-[1-8].svg # Physics playground SVG assets (8 files)
│
├── fonts/              # Custom font files (Roc Grotesk family)
│   └── .gitkeep        # Font files not committed to repo
│
└── projects/           # Project assets (images, videos per project)
    ├── hayirlicumalar*  # Daha Hayırlı Cumalar
    ├── annelergunu*     # Bi'Talih - Mother's Day Run
    ├── nesine*          # Nesine.com
    ├── iit*             # Invest in Türkiye (DOOH)
    ├── tt*              # Turkish Technic
    ├── worldcup*        # Nesine.com - 2022 World Cup
    ├── fixo*            # Bi'Talih - Fixo
    ├── derbi*           # Bi'Talih - Derbies
    ├── ywa*             # Yes!WeAble
    ├── experimental*    # Experimental Typography
    ├── invest-sm*       # Invest in Türkiye (Social Media)
    ├── gametech*        # Gametech
    ├── informatif*      # What Is Design?
    ├── shadows*         # Shadows
    ├── yapali*          # Yapalı
    ├── aztec*           # Aztec Token
    ├── ram*             # Ram Robotics
    └── hb*              # Hepsiburada
```

## Architecture

### Single-File Approach
All CSS and JavaScript are **inline within `index.html`**. There are no external `.css` or `.js` files. When editing styles or scripts, work directly inside `index.html`.

### Admin Panel (`admin.html`)
Standalone content management interface (client-side only). Can export/import JSON and generate new `index.html` files.

### No Build Pipeline
- No `package.json`, `tsconfig`, `webpack`, `vite`, or any config files
- To run locally: `python3 -m http.server 8000`
- To deploy: push to GitHub, GitHub Pages serves from `main` branch

## Page Sections (index.html)

| Order | Section | ID/Class | Description |
|-------|---------|----------|-------------|
| 1 | Loader | `.loader` | Spinning logo animation, 2.2s delay, clip-path exit |
| 2 | Navigation | `nav` | Fixed top bar, logo + links, hamburger on mobile (`.nav-links.open` class toggle) |
| 3 | Hero | `.hero` | Fullscreen video bg, logotype image, subtitle, radio player, live clock (Istanbul TZ), scroll indicator |
| 4 | Back to Top | `.back-to-top` | Fixed bottom-right button, appears after 1vh scroll |
| 5 | Marquee | `.marquee-section` | Francis Bacon quote, 4 span copies, 30s animation |
| 6 | Gallery | `.gallery` | 18 project cards in 3-column grid, video rollover on hover |
| 7 | Project Modal | `.project-modal` | Fullscreen overlay with title, credits, gallery. Escape key to close |
| 8 | About | `#about` | Split layout: scroll-synced video + bio (7 paragraphs) + stats |
| 9 | Services | `#services` | 6 service cards in 2-column grid with descriptions |
| 10 | AI Section | `.ai-section` | 6 AI tool icons with tooltips, floating hero, scrolling code block |
| 11 | Physics | `.physics-section` | Matter.js interactive playground with 16 draggable SVGs, "Drag & Drop for Fun" label, accent divider to contact |
| 12 | Contact | `#contact` | CTA with email link and social profiles |
| 13 | Footer | `footer` | Copyright and credits |

## Gallery Projects (18 total)

| # | Title | Category | Slug |
|---|-------|----------|------|
| 1 | Daha Hayırlı Cumalar | Art Project | hayirlicumalar |
| 2 | Bi'Talih - Mother's Day Run | Brand Activation | annelergunu |
| 3 | Nesine.com | Social Media Design | nesine |
| 4 | Invest in Türkiye | DOOH Campaign | iit |
| 5 | Turkish Technic | Brand Communication | tt |
| 6 | Nesine.com - 2022 World Cup | Campaign Design | worldcup |
| 7 | Bi'Talih - Fixo | Character Design | fixo |
| 8 | Bi'Talih - Derbies | Brand Activation | derbi |
| 9 | Yes!WeAble | Brand Identity | ywa |
| 10 | Experimental Typography | Academic Project | experimental |
| 11 | Invest in Türkiye | Social Media Design | invest-sm |
| 12 | Gametech | Brand Identity | gametech |
| 13 | What Is Design? | Content Design | informatif |
| 14 | Shadows | Cover Art | shadows |
| 15 | Yapalı | Brand Identity | yapali |
| 16 | Aztec Token | NFT Project | aztec |
| 17 | Ram Robotics | Brand Identity | ram |
| 18 | Hepsiburada | Social Media Design | hb |

Projects with video covers: annelergunu, iit, worldcup, derbi, aztec, hb (use `data-video` attribute).
Projects with static covers: all others (use `data-cover` + `<img>` in `.gallery-cover`).

## CSS Conventions

### Custom Properties (`:root`)
```css
--black: #191919;
--white: #E6E6E6;
--cream: #AAA239;
--accent: #FFEF00;
--accent2: #807B40;
--gray: #807B40;
--olive: #555339;
--gold: #D5C923;
--font-display: 'Roc Grotesk Wide', 'Roc Grotesk', sans-serif;
--font-body: 'Roc Grotesk', sans-serif;
--font-mono: 'Space Mono', monospace;
```

### Responsive Breakpoints
| Breakpoint | Target |
|-----------|--------|
| Default | Desktop (1200px+) |
| `max-width: 1024px` | Small desktop / tablet |
| `max-width: 768px` | Tablet / mobile |
| `max-width: 480px` | Small mobile |

### Accessibility
- `@media (prefers-reduced-motion: reduce)` disables all animations
- `-webkit-backdrop-filter` prefix on blur elements for Safari
- `loading="lazy"` on all gallery cover images
- Escape key closes project modal
- `aria-label` on icon buttons

## JavaScript Features

### Hero Section
- **Live Clock**: Shows Istanbul time (Europe/Istanbul timezone), updates every second
- **Radio Player**: Audio toggle with equalizer animation, paused by default
- **Back to Top**: Fixed button appears after scrolling past 1 viewport height

### Gallery & Modal
- **Video Rollover**: Items with `data-video` get `<video>` elements created via JS, play on hover
- **Video preload**: `auto` for thumbnail frame visibility at timecodes
- **Project Modal**: Reads `data-*` attributes, shows title, category, description, credits grid, gallery images/videos
- **View More**: First 6 items visible, rest shown on click

### About Section
- Scroll-synced `<video>` (about-video.mp4) using `currentTime` based on scroll position
- Lazy-initialized via IntersectionObserver

### Matter.js Physics
- Lazy-initialized when section scrolls into view
- 16 bodies (8 original + 8 recolored SVGs) spawned simultaneously above viewport
- Each body gets randomized angle, velocity, angular velocity, and physics properties (restitution, friction, frictionAir)
- Gravity: 0.9 (softer fall)
- Mouse/touch drag interaction
- "Drag & Drop for Fun" label with hand icon (radio-style) at bottom-right
- Accent yellow border-bottom separates physics from contact section
- Fixed timestep physics loop via requestAnimationFrame

### Navigation
- Smooth scroll via `scrollIntoView`
- Mobile menu: CSS class toggle (`.nav-links.open`)
- `nav-dark` class via IntersectionObserver on marquee/AI sections

## SEO & Meta

- `<meta name="description">` for search engines
- Open Graph tags (`og:title`, `og:description`, `og:image`, `og:url`)
- Twitter Card meta tags
- `<link rel="icon">` using Logomark.svg
- `<link rel="canonical">`
- Matter.js CDN loaded with `integrity` (SRI hash)
- Download protection: `controlsList="nodownload"` on videos, context menu blocked on media, drag prevention on images

## Contact Info (Hardcoded)

- Email: `cvhrsryldz96@gmail.com`
- GitHub: `https://github.com/cvhrsryldz`
- Behance: `https://www.behance.net/cvhrsryldz`
- Instagram: `https://www.instagram.com/cevherderler/`

## Development Notes

### Local Development
```bash
python3 -m http.server 8000
```
A local HTTP server is required for proper CORS handling of video/SVG assets.

### Important Caveats
- **CSS/JS are inline** — edits require working directly in `index.html`
- **Font files not in repo** — `fonts/` has only `.gitkeep`; Roc Grotesk files must be added separately
- **Large media files** — hero-bg.mp4 (~24MB), about-video.mp4, hero-audio.mp3 are in repo
- **No `.gitignore`** — all files are tracked
- **Admin panel generates full HTML** — direct `index.html` edits may be overwritten by admin regeneration
- **No testing framework** — manual browser testing only
