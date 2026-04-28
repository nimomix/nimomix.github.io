# Personal Site — Design Spec

**Date:** 2026-04-28
**Author:** Nimrod Bar
**Status:** Draft, pending review

A single-page personal site for Nimrod Bar that links out to his three apps (Parsee, Safeus, Bond), with a short bio and a contact link.

---

## 1. Purpose & Audience

The site has two audiences:

1. **Recruiters / hiring managers** — Nimrod is currently job-hunting. The site should signal "senior iOS professional, ships independently" without explicitly saying "looking for work" (his preference: quiet positioning; "open to opportunities" lives on LinkedIn, not here).
2. **Curious users / fellow indies** — people who land on the site from his apps, social media, or word of mouth and want to find his other work.

The site should reinforce both reads at once: a senior team lead who *also* ships indie apps is a stronger signal than either alone.

**Non-goals:**

- No blog, no RSS, no notes section. (Future: possible, but not part of this scope.)
- No "Hire me" / "Open to work" CTAs. Quiet positioning.
- No GitHub link (his repos are private; an empty-looking GitHub profile would hurt more than help).
- No LinkedIn link (user preference for now; can be added later).
- No analytics, no tracking, no cookies.

---

## 2. Site Structure

Single page, four sections in order:

1. **Hero** — name + role + short subtitle, plus two text links ("See the work ↓", "Get in touch")
2. **Works** — three app cards (Parsee, Safeus, Bond), one per row, each with status pill, icon, name, tagline, description, and CTA(s)
3. **About** — short two-paragraph bio
4. **Footer** — single contact link + copyright

No top nav, no separate pages, no overlay menus. Anchor links from the hero scroll to `#works` and `#about`.

---

## 3. Hosting & Repository

- **Repo name:** `nimomix.github.io` (GitHub user-pages special name)
- **GitHub account:** `nimomix` (personal)
- **Visibility:** public (required for free GitHub Pages)
- **URL:** `https://nimomix.github.io` (no `/repo-name` subpath)
- **Deployment:** push to `main` branch; GitHub Pages serves automatically. No build step.
- **Custom domain:** out of scope for v1; can be added later via a `CNAME` file.

---

## 4. Content

### 4.1 Hero

**Name:** Nimrod Bar

**Subtitle:**
> iOS engineer & team lead. Building iOS apps since 2012. These are my personal projects.

**Hero links (small, below subtitle):**
- "See the work ↓" → `#works`
- "Get in touch" → `mailto:NimoApps25@gmail.com`

### 4.2 Works section

Section eyebrow: `Works`
Section title: `Apps I'm building`

Three app cards in this order:

#### Parsee — *Available*

- **Tagline:** Parse. See. Understand.
- **Description:** Native macOS JSON viewer with smart filters, AI insights, JSON diff, and Xcode LLDB integration. Built because the browser-tab JSON viewers were never enough.
- **CTAs:**
  - `Visit site →` → `https://nimomix.github.io/Parsee-website/`
  - `Mac App Store` → `https://apps.apple.com/us/app/parsee-json-viewer/id6756983590`
- **Visual:** App Store hero shot (Parsee window + feature list on lavender background), edge-to-edge, no inset
- **Status pill:** green "Available"

#### Safeus — *Coming soon*

- **Tagline:** Let your loved ones know you're safe.
- **Description:** One-tap safety check-ins for iOS. Tell your contacts you're OK during emergencies, get notified when your group is accounted for. Phone-number based, privacy-first.
- **CTAs:**
  - `Visit site →` → `https://nimomix.github.io/safeus/`
  - (App Store link to be added when approved)
- **Visual:** iPhone home screenshot (`safeus_home_light.png`) on a soft green tinted background
- **Status pill:** amber "Coming soon" (covers "in App Store review" without internal-process language; can update text + add an App Store CTA when the app is approved)

#### Bond — *In development*

- **Tagline:** Agreements made simple.
- **Description:** Create, share, sign, and track personal agreements with the people who matter most. Coffee owed, freelance contract, or anything in between — iOS first, Hebrew & English.
- **CTAs:** none (intentional — no dead "Notify me" button)
- **Visual:** Bond onboarding screenshot on a cream/parchment background (so the dark iPhone reads clearly and ties to Bond's gold accent)
- **Status pill:** gold "In development"

### 4.3 About

Section eyebrow: `About`
Section title: `Hi, I'm Nimrod.`

Two paragraphs:
> 14+ years building iOS apps, the last 8 leading teams. I care about thoughtful interfaces, performance, and code that ages well.
>
> The apps above are ones I cared enough about to ship on my own. Say hi if you'd like to talk shop or work together — my inbox is open.

Company name (Shutterfly) is intentionally NOT mentioned anywhere on the site.

### 4.4 Footer

- Single link: `Contact` → `mailto:NimoApps25@gmail.com`
- Copyright: `© 2026 Nimrod Bar`

---

## 5. Visual Design

### 5.1 Aesthetic direction

Apple-style polish, matching the visual language of the existing Parsee marketing site. SF Pro Display (system stack), generous whitespace, light/dark mixed layout, subtle shadows.

### 5.2 Hero

- **Background:** dark — radial gradient from `#1a1d24` to `#0a0a0c`
- **Accent:** soft blue glow at top center (`rgba(10,132,255,0.18)`) — visually echoes Apple-style hero treatments and the Parsee site
- **Name:** `clamp(56px, 7vw, 88px)`, weight 700, `letter-spacing: -0.025em`
- **Subtitle:** 22px, `#a1a1a6`, max-width 580px
- **Hero link row:** 14px, muted with white-on-hover

### 5.3 Section headers (Works, About)

- **Eyebrow:** 12px uppercase, letter-spacing 0.2em, `#86868b`
- **Title:** `clamp(34px, 4vw, 44px)`, weight 700, `letter-spacing: -0.022em`

### 5.4 App cards

- **Layout:** two columns on desktop (`1fr 1fr`), text on left, visual on right; stacks to single column on mobile (≤ 720px) with visual on top
- **Container:** 22px border-radius, subtle shadow + 1px hairline, white background
- **Padding (text side):** 44px vertical, 36px horizontal
- **Icon:** 64×64, 14px border-radius, soft shadow
- **App name:** 30px, weight 700, `letter-spacing: -0.02em`
- **Tagline:** 18px, muted (`#6e6e73`)
- **Description:** 15px, line-height 1.55
- **CTAs:** pill buttons (`border-radius: 980px`); primary is dark (`#1d1d1f`), secondary is light (`rgba(0,0,0,0.06)`)

### 5.5 Status pills

Small rounded pill, top-right of each card. Colored dot + uppercase tracked text. Three states:

| State | Color (text + dot) | Background | Text |
|---|---|---|---|
| Available | `#1f8a3b` | `rgba(52,199,89,0.10)` | `Available` |
| Coming soon | `#b46500` | `rgba(255,159,10,0.12)` | `Coming soon` |
| In development | `#a07a1f` (gold) | `rgba(212,175,80,0.18)` | `In development` |

### 5.6 Per-app tinted visual backgrounds

Each app's "visual cell" gets a tinted background that ties to its identity:

- **Parsee:** lavender gradient `#ece8f7 → #d4cdef`. Image fills edge-to-edge.
- **Safeus:** soft green gradient `#e9f5ee → #d1ead9`. Phone screenshot centered with shadow.
- **Bond:** cream gradient `#f4ebd4 → #e8d9b7`. Phone screenshot centered with warm shadow. *(Cream background chosen so the dark iPhone frame is visible — pure black against black hid the device.)*

### 5.7 About section

- Background: `#fafafa` (subtle separation from white)
- Prose max-width: 620px
- Body size: 19px

### 5.8 Footer

- Border-top hairline (`rgba(0,0,0,0.06)`)
- Single link, centered
- Copyright in muted text (13px, `#86868b`)

### 5.9 Typography stack

```
font-family: -apple-system, "SF Pro Display", "SF Pro Text", system-ui, sans-serif;
```

For non-Apple platforms, optionally fall back to self-hosted Inter (matching the Parsee site approach) — out of scope for v1; system fallback is fine.

### 5.10 Light/dark mode

v1 is light-only with a dark hero (mixed). Full dark-mode parity is a future enhancement.

---

## 6. Assets

All assets need to live in the repo at `images/` (matching Parsee-website convention).

| Asset | Source | Notes |
|---|---|---|
| `parsee-icon.png` | `Parsee/PARSEE.app/Contents/Resources/ParseeCube.icns` (extract via `iconutil`) | Center-crop to remove macOS safe-area padding |
| `parsee-hero.jpg` | `~/Downloads/parsee.png` (App Store screenshot) | Resize to ~1400px wide, JPEG q80 |
| `safeus-icon.png` | `Safe/Safe/Safe/SafeusIcon1024.png` | Resize to 192px |
| `safeus-screenshot.png` | `Safe/images/safeus_home_light.png` | Resize to ~600px wide |
| `bond-icon.png` | `Bond/images/Bond-icon-iOS-Default-512x512@1x.png` | Resize to 192px |
| `bond-onboarding.png` | `Bond/images/BondOnboarding.png` | Resize to ~800px wide |
| `favicon.ico`, `favicon-32.png`, `favicon-180.png` | Out of scope for v1; ship without a custom favicon and add later | — |

Open-graph image (1200×630) for link previews — out of scope for v1; can be added later.

---

## 7. Technology

Match the Parsee-website setup: vanilla HTML/CSS/JS, no build step, no framework, no package manager.

- One `index.html`
- One `styles.css` (could inline initial render-blocking CSS in `<head>` if needed; not required for v1)
- Optional `app.js` for the hero `fade-in` reveal animation if used
- Self-host fonts only if a non-Apple-platform fallback is needed (out of scope for v1)

Page weight target: under 400 KB total including the App Store hero image (acceptable for a personal site that loads once).

---

## 8. Accessibility & Responsiveness

- All images have meaningful `alt` text (or empty `alt=""` for purely decorative ones like icons that have a visible text label next to them)
- Semantic HTML: `<header>`, `<section>`, `<footer>`, headings in correct order
- Color contrast: status pills, hero subtitle, and footer text all meet WCAG AA (verified against background)
- Mobile breakpoint at 720px: app cards stack to single column, visual moves above text
- Touch targets ≥ 44px for all links and CTAs

---

## 9. Out of Scope (v1)

- Custom domain mapping
- Open-graph / Twitter card meta
- Blog, notes, RSS
- Light/dark mode parity (currently mixed by design)
- GitHub link, LinkedIn link, social icons
- Bond "notify me" email-capture form
- Hebrew (RTL) version of the site
- Analytics

---

## 10. Future Considerations

- Map a custom domain (e.g., `nimrodbar.com`) when desired — single `CNAME` file change
- Add LinkedIn / GitHub later if context changes
- Add a fourth app card when Nimrod ships another app — current layout scales naturally
- Replace Bond's onboarding screenshot with a polished marketing shot once Bond's marketing materials are ready
- Add an App Store CTA + flip Safeus's status pill from "Coming soon" to "Available" when Safeus passes review

---

## 11. Implementation Plan (handoff)

After this spec is approved:

1. Initialize the repo at `/Users/nbar/Projects/nimomix.github.io/`
2. Create `index.html`, `styles.css`, `images/` from the locked v12 mockup
3. Process and copy the assets listed in §6
4. Local preview (open `index.html` directly or run `python3 -m http.server`)
5. Push to `github.com/nimomix/nimomix.github.io` and verify the site at `https://nimomix.github.io`

The implementation plan itself will be drafted via the writing-plans skill once this spec is approved.
