# mattstraub.com — Redesign Documentation

**Version:** 2.0 (Interactive Update)
**Last Updated:** February 24, 2026
**Author:** Matt Straub
**Status:** Concept / Pre-Launch

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Architecture & File Structure](#2-architecture--file-structure)
3. [Design System](#3-design-system)
4. [Page Sections](#4-page-sections)
5. [Interactive Features](#5-interactive-features)
6. [Responsive Behavior](#6-responsive-behavior)
7. [Content Guide](#7-content-guide)
8. [Deployment & Migration](#8-deployment--migration)
9. [Maintenance & Future Enhancements](#9-maintenance--future-enhancements)

---

## 1. Project Overview

### Purpose

A personal portfolio and professional identity site for Matt Straub, Customer Success Manager at Meta. The site communicates Matt's "Tech × People" brand positioning — bridging technical expertise in customer success with a creative background in sound design and digital preservation.

### Previous Site

The existing mattstraub.com is a WordPress.com-hosted site with a single About page, a `/remember/` project subpage, a Dropbox file upload link, and a contact page. The content is presented as a long text block with minimal visual hierarchy or interactivity.

### Redesign Goals

- Elevate the visual identity with a modern, editorial dark-theme aesthetic
- Organize content into clear, scannable sections (About, Expertise, Projects, Passions, Contact)
- Add subtle cursor-driven interactive elements that reward exploration
- Maintain all existing content and navigation destinations (LinkedIn, Dropbox Send Files, Contact, remember project)
- Deliver as a single static HTML file with zero external dependencies beyond Google Fonts
- Make migration off WordPress straightforward

---

## 2. Architecture & File Structure

The site is a single self-contained HTML file. All CSS is inline in a `<style>` block and all JavaScript is inline in a `<script>` block at the end of the `<body>`. There are no external CSS or JS dependencies.

### External Dependencies

| Resource | Purpose | CDN |
|----------|---------|-----|
| Instrument Serif | Display/headline font | Google Fonts |
| DM Sans | Body text font | Google Fonts |
| JetBrains Mono | Monospace labels, nav, tags | Google Fonts |

### If Expanding to Multiple Pages

If the site grows beyond a single page (e.g., a dedicated `/remember/` page, a blog), consider restructuring into:

```
mattstraub.com/
├── index.html
├── remember/
│   └── index.html
├── assets/
│   ├── css/
│   │   └── style.css      (extracted from inline)
│   ├── js/
│   │   └── interactions.js (extracted from inline)
│   └── images/
│       ├── headshot.jpg
│       └── remember/
└── favicon.ico
```

At that point, a static site generator like Astro or Eleventy would help manage shared navigation and styles across pages without adding runtime complexity.

---

## 3. Design System

### Color Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `--bg` | `#0c0b0f` | Page background |
| `--bg-elevated` | `#141319` | Card backgrounds, project section |
| `--surface` | `#1c1b22` | Portrait placeholder, project visual |
| `--text-primary` | `#f0ede6` | Headlines, primary text |
| `--text-secondary` | `#8e8a9a` | Body text, descriptions |
| `--text-muted` | `#5a5668` | Labels, section markers, footer |
| `--accent` | `#c8ff3c` | Primary accent — CTAs, highlights, cursor, interactive glow |
| `--warm` | `#ff7a52` | Secondary accent — About section heading emphasis |
| `--cool` | `#6e8cff` | Tertiary accent — Project heading emphasis, hover state on sound bars |

### Typography

| Element | Font | Weight | Size | Notes |
|---------|------|--------|------|-------|
| Hero headline | Instrument Serif | 400 | `clamp(3.5rem, 8vw, 8rem)` | Italic variant used for `<em>` accented words |
| Section headings | Instrument Serif | 400 | `clamp(2rem–2.5rem, 3.5–5vw, 3–4.5rem)` | Varies by section |
| Card titles | Instrument Serif | 400 | 1.1–1.4rem | |
| Body text | DM Sans | 300 | 0.9–1.15rem | Light weight for readability on dark backgrounds |
| Nav links | JetBrains Mono | 300 | 0.72rem | Uppercase, letter-spaced |
| Section labels | JetBrains Mono | 300 | 0.65rem | Uppercase, wide letter-spacing (0.25em) |
| Buttons | JetBrains Mono | 400 | 0.72rem | Uppercase, pill-shaped |
| Detail labels | JetBrains Mono | — | 0.6rem | Uppercase, small caps style |
| Detail values | Instrument Serif | — | 1.15rem | Warm serif for contrast |

### Spacing & Layout

- Page max-width: Content grids are capped at `max-width: 1200px`
- Section padding: `8rem` vertical, `3rem` horizontal (desktop); `5rem` / `1.5rem` (tablet)
- Card border-radius: 16–20px
- Button border-radius: 100px (full pill)
- Grid gaps: 1.25–6rem depending on section density

### Visual Texture

- **Grain overlay:** SVG noise filter applied via `body::before` as a fixed layer at 4% opacity. Creates subtle film grain across the entire page.
- **Ambient orbs:** Three large blurred circles (`filter: blur(100px)`) in accent, cool, and warm colors float behind the hero with a slow `orbFloat` animation. Opacity is 15%.
- **Grid backdrop:** Faint green grid lines in the hero, masked with a radial gradient so they fade toward the edges.

---

## 4. Page Sections

### Navigation (fixed)

- Logo: "matt." with accent-colored period
- Links: About, What I Do, Projects, Contact
- Frosted glass effect with `backdrop-filter: blur(20px)`
- Underline animation on hover (accent-colored, expands left-to-right)
- Collapses to logo-only on mobile (`< 550px`)

### Hero

- Tagline: "Customer Success Manager — Meta"
- Headline: "Where *technology* meets the *human* experience" (italic accent words)
- Subtext paragraph
- Two CTAs: "Get in Touch →" (primary) and "View Work" (outline)
- "Scroll to explore" hint at bottom-left with animated pulse line
- Background: grid, floating orbs, cursor-reactive glow

### About

- Two-column grid: portrait placeholder (left) + text content (right)
- Portrait area has gradient placeholder with "MS" initials and "NYC Based" tag — **replace with actual headshot**
- Heading: "Obsessed with the intersection of *tech & people*"
- Three body paragraphs covering role, education, and origins
- Detail grid: Based In, Currently, Education, Focus

### What I Do (Expertise)

- Three-column card grid
- Cards: Customer Success (⚡), Creative Problem Solving (🎨), Digital Preservation (🔬)
- Each card has an icon in a tinted container, title, and description
- Cursor-reactive radial glow on hover (see Interactive Features)

### Featured Project: remember

- Two-column layout: animated sound wave visual (left) + project info (right)
- Sound wave: 15 animated bars with staggered delays
- Project description covering the installation concept, inspiration, and context
- Tag pills: Sound Design, Installation Art, Immersive Audio, Spatial Sound
- Sound bars shift from green to blue on hover

### Beyond Work (Passions)

- Four-column card grid
- Cards: Audio & Sound (🎙), Family Archives (📼), Hometown Roots (🏔), Disc Golf (🥏)
- 3D tilt effect on hover (see Interactive Features)

### Contact

- Centered layout with large serif heading: "Let's build something *together*"
- Subtext paragraph
- Three CTAs: Say Hello (mailto), LinkedIn, Send Files

### Footer

- Left: © 2026 Matt Straub · NYC
- Right: LinkedIn, Email, Dropbox links

---

## 5. Interactive Features

All interactive features are implemented in vanilla JavaScript at the bottom of the HTML file. They are purely cosmetic and the site remains fully functional with JavaScript disabled (just without the effects).

### Custom Cursor

- **Elements:** `.cursor-dot` (8px accent dot) and `.cursor-ring` (36px hollow ring)
- **Behavior:** Dot follows mouse instantly; ring follows with a smooth lag (`0.15` lerp factor via `requestAnimationFrame`)
- **Hover expansion:** Ring expands to 56px and increases border opacity when hovering over links, buttons, cards, and tags
- **Disabled on:** screens ≤ 900px or touch devices (`pointer: coarse`)
- **Blend mode:** `mix-blend-mode: difference` on the dot for visibility against any background

### Hero Glow (Cursor-Reactive)

- **CSS:** `.hero-glow` div with `radial-gradient(600px circle at var(--mouse-x) var(--mouse-y), ...)`
- **JS:** Updates `--mouse-x` and `--mouse-y` CSS custom properties on hero `mousemove`
- **Effect:** Soft green glow (6% opacity) follows cursor across the hero section

### Headline Letter Proximity Glow

- **Setup:** On page load, the hero `<h1>` content is split into individual `<span class="char">` elements while preserving `<em>` tag structure. Words are wrapped in `<span class="word">` to prevent line-break issues.
- **Behavior:** On `mousemove` within the hero, each character's center position is compared to the cursor. Characters within 80px radius receive the `.glow` class.
- **Effect:** Glowing characters turn accent green with `text-shadow` and lift 2px. Characters inside `<em>` tags glow brighter (`#e0ff80`).
- **Cleanup:** All `.glow` classes removed on `mouseleave`.
- **Performance note:** This iterates over ~50 character spans on every mouse move. Performance is fine for this count, but if the headline text were significantly longer, consider using a throttle or spatial index.

### Expertise Card Radial Glow

- **CSS:** Each `.expertise-card` has a `::after` pseudo-element with a radial gradient positioned at `var(--card-mouse-x)` / `var(--card-mouse-y)`. Opacity transitions from 0 to 1 on hover.
- **JS:** Updates the card's CSS custom properties on `mousemove` within each card.
- **Effect:** A soft green spotlight (6% opacity, 250px radius) follows the cursor inside the card.

### Passion Card 3D Tilt

- **JS:** On `mousemove`, calculates cursor position relative to card center as a -0.5 to 0.5 range, then applies `rotateX` and `rotateY` transforms (±8°) with `perspective(600px)`.
- **Reset:** Transform smoothly resets to flat on `mouseleave`.

### Contact Section Glow

- Same implementation as the hero glow, applied to the contact section container.

### Sound Wave Color Shift

- **CSS-only:** `.project-visual:hover .sound-bar` transitions `background` from `var(--accent)` to `var(--cool)`.

### Scroll Reveal Animations

- **Implementation:** `IntersectionObserver` with 15% threshold
- **Elements:** All `.reveal` elements fade up (30px translate + opacity) with a cubic-bezier easing
- **Stagger:** Multiple elements appearing at the same time are staggered with `setTimeout` at 100ms intervals
- **One-shot:** Observer disconnects after each element reveals

---

## 6. Responsive Behavior

### Breakpoints

| Breakpoint | Changes |
|------------|---------|
| `≤ 900px` | Nav padding reduces. Hero/section padding decreases. About grid stacks to single column. Expertise grid stacks. Project layout stacks. Passions grid → 2 columns. Footer stacks vertically. **Custom cursor hidden.** |
| `≤ 550px` | Nav links hidden (logo only). Passions grid → 1 column. About detail row → 1 column. Contact section padding reduced. |
| `pointer: coarse` | Custom cursor hidden regardless of screen size (touch devices). |

### Touch Considerations

- All hover effects are progressive enhancements — cards and elements remain fully visible and readable without hover states
- The 3D tilt on passion cards won't fire on touch devices (no mousemove)
- Button hover states still work via `:hover` pseudo-class on devices that support it

---

## 7. Content Guide

### Placeholder Content to Replace Before Launch

| Element | Current State | Action Needed |
|---------|---------------|---------------|
| Portrait image | "MS" initials placeholder | Replace with actual headshot (recommend 600×800px minimum, will be displayed in 3:4 aspect ratio with grayscale filter) |
| Email address | `hello@mattstraub.com` | Verify this is the correct contact email |
| LinkedIn URL | `#` placeholder | Replace with actual LinkedIn profile URL |
| Send Files link | `#` placeholder | Replace with Dropbox file request URL (`https://www.dropbox.com/request/yCidkbsHprXzoK4mna43`) |
| Footer links | `#` placeholders | Same as above — update LinkedIn, Email (mailto), Dropbox |

### Adding a Headshot

Replace the `.about-portrait-placeholder` div with an `<img>` tag:

```html
<!-- Remove this -->
<div class="about-portrait-placeholder"><span>MS</span></div>

<!-- Replace with -->
<img src="assets/images/headshot.jpg" alt="Matt Straub" 
     style="width:100%;height:100%;object-fit:cover;filter:grayscale(30%) contrast(1.05);">
```

The grayscale filter is intentional — it shifts to full color on hover via the existing `.about-portrait:hover` rule.

### Editing Copy

All text content is directly in the HTML. Key sections to update over time:

- **Hero tagline** (`hero-tag`): Update if role/company changes
- **Hero headline and subtext**: Core brand message
- **About paragraphs**: Bio content
- **About detail values**: Location, role, education, focus area
- **Expertise card descriptions**: Evolve as professional focus shifts
- **Project info**: Could be expanded or swapped for a newer featured project
- **Passion cards**: Update interests as they change

### Adding the remember Page

The current site has a dedicated `/remember/` page. To preserve this:

1. Create a `remember/index.html` file with the same nav, footer, and design system
2. Add the installation photos (currently hosted on WordPress)
3. Include the audio player for the promotional track
4. Link from the main site's project section ("Learn More →" button)

---

## 8. Deployment & Migration

### Recommended Hosting

| Platform | Pros | Free Tier |
|----------|------|-----------|
| **Netlify** | Simplest setup, form handling, instant deploys from Git | Yes |
| **Vercel** | Fast, great developer experience, preview deploys | Yes |
| **Cloudflare Pages** | Fastest CDN, unlimited bandwidth | Yes |
| **GitHub Pages** | Free, integrated with repo | Yes |

All of these are well-suited for a static HTML site and support custom domains with automatic SSL.

### Deployment Steps

1. **Create a GitHub repository** for the site files
2. **Push the HTML file** (and any assets like images) to the repo
3. **Connect the repo** to your chosen hosting platform (Netlify/Vercel/Cloudflare Pages)
4. **Configure the custom domain:**
   - In the hosting platform, add `mattstraub.com` as a custom domain
   - At the domain registrar, update DNS records as directed (usually a CNAME or A record)
   - Wait for DNS propagation (typically 15 minutes to 24 hours)
5. **SSL certificate** will be provisioned automatically by the hosting platform
6. **Set up redirects** for any old WordPress URLs that should still work:
   - `/remember/` → new remember page (or section anchor)
   - `/contact/` → `/#contact`

### WordPress Migration Checklist

- [ ] Download all images currently hosted on WordPress (headshot, remember installation photos)
- [ ] Export the Dropbox file request URL from the current site
- [ ] Note any WordPress.com analytics (StatCounter) — consider replacing with a privacy-friendly alternative like Plausible or Fathom, or simply removing analytics
- [ ] Test all links on the new site before switching DNS
- [ ] After DNS switch, verify the old WordPress site is no longer resolving
- [ ] Cancel WordPress.com plan if applicable

---

## 9. Maintenance & Future Enhancements

### Regular Maintenance

- **Content updates:** Edit HTML directly — all copy is inline, no CMS required
- **Font loading:** Google Fonts are loaded via CDN; no maintenance needed unless fonts are deprecated
- **Browser testing:** Periodically verify in Chrome, Safari, Firefox, and Edge. The CSS uses standard properties with `-webkit-` prefixes where needed.

### Potential Future Enhancements

| Enhancement | Complexity | Notes |
|-------------|------------|-------|
| Dedicated remember page | Low | Duplicate the layout, add installation photos and audio |
| Blog or writing section | Medium | Would benefit from a static site generator (Astro, Eleventy) |
| Dark/light theme toggle | Medium | Add a light-mode color set and toggle logic; would need redesigning the ambient effects |
| Project gallery | Medium | If adding more projects beyond remember |
| Contact form | Low | Use Formspree or Netlify Forms — no backend needed |
| Analytics | Low | Add Plausible or Fathom script tag |
| Open Graph / social meta | Low | Add `<meta property="og:...">` tags and a preview image for link sharing |
| Favicon | Low | Add a favicon.ico and Apple touch icon |
| Performance: font subsetting | Low | Self-host subsetted fonts to reduce load time |
| Accessibility audit | Medium | Add skip-to-content link, verify ARIA roles, test with screen reader, ensure all interactive elements are keyboard-navigable |

### Known Limitations

- **No CMS:** Content changes require editing HTML directly. This is fine for a personal site but would need a CMS if someone else manages content.
- **Single-file architecture:** Works well now but would need restructuring if the site grows to 3+ pages.
- **Custom cursor:** Not visible on touch devices (by design). The cursor is hidden but the default cursor is restored — no functionality is lost.
- **Letter proximity effect:** Iterates over all character spans on every mouse move. Acceptable for the current headline length (~50 characters) but should be revisited if the headline grows significantly.
- **No offline support:** No service worker. Could be added if desired.
