# Portfolio Website — Cevher Sariyildiz

## Project Overview

Personal portfolio website for Cevher Sariyildiz (Graphic Designer & Art Director). Static single-page site deployed on **GitHub Pages**. No build system, no bundler, no package manager — pure HTML/CSS/JavaScript served directly.

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Markup | HTML5 (semantic) |
| Styling | Vanilla CSS (inline in `<style>` block) |
| Scripting | Vanilla JavaScript (inline `<script>` blocks) |
| Physics Engine | Matter.js v0.20.0 (CDN) |
| GIF Decoder | gifuct-js v2.1.2 (CDN, ES module) |
| Fonts | Roc Grotesk (local WOFF2/WOFF), Space Mono (Google Fonts CDN) |
| Deployment | GitHub Pages (static) |

**No npm, no Node.js, no TypeScript, no framework.**

## File Structure

```
portfolio-website/
├── index.html          # Main portfolio site (~50KB, all CSS/JS inline)
├── admin.html          # Admin panel for content management (~65KB)
├── README.md           # Minimal project description
├── CLAUDE.md           # This file
│
├── hero-video.mp4      # Hero background video (~24MB)
├── aboutme.gif         # Scroll-synced animated GIF (9.3MB)
├── around-the-world.mp3 # Hero radio player audio — Daft Punk (5.5MB)
│
├── Logo.svg            # Full logo
├── Logomark.svg        # Icon-only logo mark
├── Logotype.svg        # Text-only logotype
├── Asset1.svg          # Physics playground SVG assets (8 files)
├── Asset2.svg
├── Asset3.svg
├── Asset4.svg
├── Asset5.svg
├── Asset6.svg
├── Asset7.svg
├── Asset8.svg
│
├── fonts/              # Custom font files (Roc Grotesk family)
│   └── .gitkeep        # Font files not committed to repo
│
└── projects/           # Project assets directory (placeholder)
    └── .gitkeep
```

## Architecture

### Single-File Approach
All CSS and JavaScript are **inline within `index.html`**. There are no external `.css` or `.js` files. The CSS is minified; the JS is partially minified. When editing styles or scripts, work directly inside `index.html`.

### Admin Panel (`admin.html`)
Standalone content management interface. Features:
- Form-based editing of all site sections (hero, about, projects, services, contact)
- **Export/Import JSON** for saving/loading site data
- **Generate & Download** — produces a new `index.html` with updated content
- Live preview in new browser tab
- Dark theme UI with Turkish labels
- No backend — all client-side

### No Build Pipeline
- No `package.json`, `tsconfig`, `webpack`, `vite`, or any config files
- To run locally: open `index.html` in a browser (or use a local HTTP server for proper asset loading)
- To deploy: push to GitHub, GitHub Pages serves from `main` branch

## Page Sections (index.html)

| Order | Section | ID/Class | Description |
|-------|---------|----------|-------------|
| 1 | Loader | `.loader` | Spinning logo animation, 2.2s delay, clip-path exit |
| 2 | Navigation | `nav` | Fixed top bar, logo + links, hamburger on mobile |
| 3 | Hero | `.hero` | Fullscreen video background, title with stroke/accent text, radio audio player |
| 4 | Marquee | `.marquee-section` | Infinite horizontal scrolling text banner |
| 5 | Gallery | `.gallery` | 20 project cards in 3-column grid |
| 6 | Project Modal | `.project-modal` | Fullscreen overlay for project details |
| 7 | About | `#about` | Split layout: scroll-synced GIF + bio text + stats |
| 8 | Services | `#services` | 4-column service cards |
| 9 | Physics | `.physics-section` | Matter.js interactive playground with draggable SVGs |
| 10 | Contact | `#contact` | CTA with email link and social profiles |
| 11 | Footer | `footer` | Copyright and credits |

## CSS Conventions

### Custom Properties (`:root`)
```css
--black: #191919;
--white: #E6E6E6;
--cream: #AAA239;
--accent: #FFEF00;       /* Primary yellow */
--accent2: #807B40;      /* Olive gold */
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

### Typography
- Fluid sizing with `clamp()` — e.g., `clamp(3.5rem, 10vw, 9rem)` for hero title
- Display font: Roc Grotesk Wide (700, 800)
- Body font: Roc Grotesk (400, 500, 700, 800)
- Monospace: Space Mono (400, 700) — used for labels, nav, metadata

### Key CSS Patterns
- `mix-blend-mode: difference` on nav and cursor (nav switches to `normal` on marquee and AI sections via `nav-dark` class)
- `cursor: none` globally (custom cursor replaces default)
- `backdrop-filter: blur()` on modal close button
- `-webkit-text-stroke` for outlined hero text
- CSS Grid for gallery (`repeat(3, 1fr)`) and service cards
- `aspect-ratio: 3/4` for gallery items

## JavaScript Features

### Custom Cursor
- 12px accent-colored dot + 40px border follower circle
- Follower uses `requestAnimationFrame` with easing (`lerp`)
- Expands on hover over clickable elements
- Hidden on mobile (`@media max-width: 768px`)

### Scroll Animations (IntersectionObserver)
- `.reveal` and `.gallery-item` elements observed
- Threshold: `0.15`, root margin: `0px 0px -50px 0px`
- Adds `.visible` class triggering CSS `opacity` + `translateY` transitions
- Staggered delays via `.reveal-delay-1`, `-2`, `-3`

### GIF Scroll Sync (gifuct-js)
- Fetches `aboutme.gif`, decodes all frames into ImageData array
- Renders frames to a `<canvas>` based on scroll position
- Frame index: `Math.floor(-scrollOffset * (totalFrames / pixelsPerCycle))`
- Initialized lazily via IntersectionObserver

### Matter.js Physics Playground
- Lazy-initialized when section scrolls into view
- Creates engine with `gravity.y = 1.5`
- 8 SVG assets as physics bodies (rectangle collision shapes)
- Mouse constraint for drag interaction
- Touch events supported (passive listeners)
- Canvas rendering synced with DOM transforms via `requestAnimationFrame`
- Resizes and reinitializes on window resize
- Cleans up when scrolled out of view

### Project Modal
- Click gallery item opens fullscreen modal
- Reads project data from `data-*` attributes on gallery items
- Color-shifted hero background using `shiftColor()` utility
- Generated credits grid and gallery images
- Scroll lock on body when open

### Hero Radio Player
- `<audio>` element with `loop` plays `around-the-world.mp3` (Daft Punk — Around The World)
- Audio is **paused by default** — user clicks `.radio-btn` to toggle play/pause
- Pulsing double-ring indicator (`@keyframes radioPulse`) draws attention when paused
- 3 equalizer bars (`@keyframes eqBounce`) animate when playing
- `.radio-btn.playing` class toggles visual state (accent border, animated bars, pulse stops)
- Positioned in `.hero-bottom` between hero-info and hero-scroll

### Navigation
- Smooth scroll via `scrollIntoView({ behavior: 'smooth' })`
- Mobile hamburger toggle (`.nav-links.open` class)
- `nav-dark` class applied via IntersectionObserver on marquee and AI sections (switches blend mode to normal)

## Key JavaScript Functions

| Function | Purpose |
|----------|---------|
| `animateFollower()` | Cursor follower animation loop |
| `shiftColor(hex, amount)` | Shift hex color for modal hero |
| `showFrame(idx)` | Render specific GIF frame to canvas |
| `onScroll()` | Calculate and display scroll-synced GIF frame |
| `init()` | Initialize Matter.js physics engine |
| `cleanup()` | Destroy physics engine and remove bodies |
| `updatePositions()` | Sync physics body positions to DOM elements |

## Contact Info (Hardcoded)

- Email: `cvhrsryldz96@gmail.com`
- GitHub: `https://github.com/cvhrsryldz`
- Social links: Behance, Instagram (in contact section)

## Development Notes

### Local Development
```bash
# Option 1: Python HTTP server
python3 -m http.server 8000

# Option 2: Open directly
open index.html
```
A local HTTP server is recommended for proper CORS handling of assets (GIF fetch, SVG loading).

### Content Updates
1. Open `admin.html` in browser
2. Edit sections via the form UI
3. Click "Generate & Download" to get updated `index.html`
4. Replace existing `index.html` with the downloaded version

### Important Caveats
- **CSS/JS are minified inline** — edits to `index.html` styles require working with minified code
- **Font files not in repo** — `fonts/` directory has only `.gitkeep`; Roc Grotesk WOFF2/WOFF files must be added separately
- **Large media files** — `hero-video.mp4` (~24MB), `aboutme.gif` (9.3MB), and `around-the-world.mp3` (5.5MB) are committed to repo
- **No `.gitignore`** — all files are tracked
- **Admin panel generates full HTML** — changes made directly to `index.html` may be overwritten if admin panel is used to regenerate
- **No testing framework** — manual browser testing only
- **Gallery projects use color blocks** — no actual project images; visual differentiation is via CSS gradient backgrounds with `data-color` attributes
