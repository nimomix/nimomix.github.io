# Personal Site Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build and deploy Nimrod Bar's personal portfolio site to `https://nimomix.github.io`, linking out to his three apps (Parsee, Safeus, Bond) with a short bio and contact link.

**Architecture:** Single-page vanilla HTML/CSS site, no build step, no JS framework. Hosted via GitHub Pages from the user-pages repo `nimomix/nimomix.github.io`. Page served from `main` branch root. Matches the static-site approach already used by `Parsee-website` and `Safe/docs/website`.

**Tech Stack:** HTML5, CSS3 (custom properties, CSS Grid, Flexbox), system font stack (SF Pro on Apple), GitHub Pages.

**Spec:** `docs/superpowers/specs/2026-04-28-personal-site-design.md`

**Project root:** `/Users/nbar/Projects/nimomix.github.io/`

---

## File Structure

```
nimomix.github.io/
├── README.md
├── .gitignore
├── index.html
├── styles.css
├── images/
│   ├── parsee-icon.png        (192px, cropped from ParseeCube.icns)
│   ├── parsee-hero.jpg        (~1400px wide, JPEG q80, App Store hero)
│   ├── safeus-icon.png        (192px)
│   ├── safeus-screenshot.png  (~600px wide, home screen)
│   ├── bond-icon.png          (192px)
│   └── bond-onboarding.png    (~800px wide)
└── docs/
    └── superpowers/
        ├── specs/
        │   └── 2026-04-28-personal-site-design.md
        └── plans/
            └── 2026-04-28-personal-site.md  (this file)
```

Each file's responsibility:

- `index.html` — single page, four sections (hero, works, about, footer)
- `styles.css` — all styles, organized: tokens → reset → hero → sections → app cards → status pills → about → footer → responsive
- `images/` — six assets, all already produced as resized variants in `/Users/nbar/Projects/.superpowers/brainstorm/21085-1777376165/content/img/small/`
- `README.md` — short repo description
- `.gitignore` — `.DS_Store`, `.superpowers/`

---

## Task 1: Initialize repo structure

**Files:**
- Create: `/Users/nbar/Projects/nimomix.github.io/README.md`
- Create: `/Users/nbar/Projects/nimomix.github.io/.gitignore`
- Create: `/Users/nbar/Projects/nimomix.github.io/images/` (directory)

- [ ] **Step 1.1: Verify project root exists**

```bash
ls /Users/nbar/Projects/nimomix.github.io/docs/superpowers/specs/2026-04-28-personal-site-design.md
```

Expected: file path printed (the spec already exists from brainstorming).

- [ ] **Step 1.2: Create images directory**

```bash
mkdir -p /Users/nbar/Projects/nimomix.github.io/images
```

- [ ] **Step 1.3: Create `.gitignore`**

Write `/Users/nbar/Projects/nimomix.github.io/.gitignore` with this content:

```
.DS_Store
.superpowers/
```

- [ ] **Step 1.4: Create `README.md`**

Write `/Users/nbar/Projects/nimomix.github.io/README.md` with this content:

```markdown
# nimomix.github.io

Personal site for Nimrod Bar — iOS engineer & team lead.

Live at: https://nimomix.github.io

## Local preview

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploy

Push to `main`. GitHub Pages serves automatically.
```

- [ ] **Step 1.5: Verify the four files/dirs exist**

```bash
ls -la /Users/nbar/Projects/nimomix.github.io/
```

Expected output includes: `README.md`, `.gitignore`, `images/`, `docs/`.

---

## Task 2: Process and place assets

**Files:**
- Create: `/Users/nbar/Projects/nimomix.github.io/images/parsee-icon.png`
- Create: `/Users/nbar/Projects/nimomix.github.io/images/parsee-hero.jpg`
- Create: `/Users/nbar/Projects/nimomix.github.io/images/safeus-icon.png`
- Create: `/Users/nbar/Projects/nimomix.github.io/images/safeus-screenshot.png`
- Create: `/Users/nbar/Projects/nimomix.github.io/images/bond-icon.png`
- Create: `/Users/nbar/Projects/nimomix.github.io/images/bond-onboarding.png`

The brainstorming session already produced resized versions of all six assets at `/Users/nbar/Projects/.superpowers/brainstorm/21085-1777376165/content/img/small/`. Copy them with their final names.

- [ ] **Step 2.1: Verify the source assets still exist**

```bash
ls /Users/nbar/Projects/.superpowers/brainstorm/*/content/img/small/ 2>/dev/null
```

Expected output should include: `parsee-cube-cropped.png`, `parsee-appstore.jpg`, `safeus-icon.png`, `safeus_home_light.png`, `bond-icon.png`, `bond-onboarding.png`.

If those paths don't exist (the brainstorm dir was cleaned up), regenerate them:

```bash
# Re-extract Parsee icon from the .app bundle
mkdir -p /tmp/parsee-rebuild && cd /tmp/parsee-rebuild
unzip -q "/Users/nbar/Projects/Parsee/PARSEE New icon/PARSEE_2025.zip"
iconutil -c iconset PARSEE.app/Contents/Resources/ParseeCube.icns -o /tmp/parsee.iconset
sips -c 200 200 /tmp/parsee.iconset/icon_128x128@2x.png --out /tmp/parsee-icon.png
sips -Z 1400 /Users/nbar/Downloads/parsee.png --out /tmp/parsee-hero-large.png
sips -s format jpeg -s formatOptions 80 /tmp/parsee-hero-large.png --out /tmp/parsee-hero.jpg
sips -Z 192 /Users/nbar/Projects/Safe/Safe/Safe/SafeusIcon1024.png --out /tmp/safeus-icon.png
sips -Z 600 /Users/nbar/Projects/Safe/images/safeus_home_light.png --out /tmp/safeus-screenshot.png
sips -Z 192 /Users/nbar/Projects/Bond/images/Bond-icon-iOS-Default-512x512@1x.png --out /tmp/bond-icon.png
sips -Z 800 /Users/nbar/Projects/Bond/images/BondOnboarding.png --out /tmp/bond-onboarding.png
```

- [ ] **Step 2.2: Copy assets into `images/`**

If brainstorm dir is intact, copy from there with renames:

```bash
SRC=$(ls -d /Users/nbar/Projects/.superpowers/brainstorm/*/content/img/small | head -1)
DST=/Users/nbar/Projects/nimomix.github.io/images
cp "$SRC/parsee-cube-cropped.png" "$DST/parsee-icon.png"
cp "$SRC/parsee-appstore.jpg"     "$DST/parsee-hero.jpg"
cp "$SRC/safeus-icon.png"          "$DST/safeus-icon.png"
cp "$SRC/safeus_home_light.png"    "$DST/safeus-screenshot.png"
cp "$SRC/bond-icon.png"            "$DST/bond-icon.png"
cp "$SRC/bond-onboarding.png"      "$DST/bond-onboarding.png"
```

If brainstorm dir is gone, copy from `/tmp/`:

```bash
DST=/Users/nbar/Projects/nimomix.github.io/images
cp /tmp/parsee-icon.png "$DST/"
cp /tmp/parsee-hero.jpg "$DST/"
cp /tmp/safeus-icon.png "$DST/"
cp /tmp/safeus-screenshot.png "$DST/"
cp /tmp/bond-icon.png "$DST/"
cp /tmp/bond-onboarding.png "$DST/"
```

- [ ] **Step 2.3: Verify all six assets exist with reasonable sizes**

```bash
ls -la /Users/nbar/Projects/nimomix.github.io/images/
```

Expected:
- `parsee-icon.png` ≈ 50 KB
- `parsee-hero.jpg` ≈ 230 KB
- `safeus-icon.png` ≈ 50 KB
- `safeus-screenshot.png` ≈ 40 KB
- `bond-icon.png` ≈ 55 KB
- `bond-onboarding.png` ≈ 40 KB

If any file is 0 bytes or missing, retry the copy step.

- [ ] **Step 2.4: Visual verification of icons** (open Finder, glance at the three icons to confirm they look right)

```bash
open /Users/nbar/Projects/nimomix.github.io/images/
```

Expected: Parsee icon shows a 3D translucent purple cube; Safeus icon shows a green safety symbol; Bond icon shows a gold cursive "B" on black.

---

## Task 3: Build `index.html`

**Files:**
- Create: `/Users/nbar/Projects/nimomix.github.io/index.html`

- [ ] **Step 3.1: Write the complete `index.html`**

Write `/Users/nbar/Projects/nimomix.github.io/index.html` with this exact content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="#0a0a0c">

  <title>Nimrod Bar — iOS engineer &amp; team lead</title>
  <meta name="description" content="iOS engineer &amp; team lead. Building iOS apps since 2012. Personal projects: Parsee, Safeus, Bond.">

  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <!-- HERO -->
  <header class="hero">
    <h1 class="hero-name">Nimrod Bar</h1>
    <p class="hero-role">iOS engineer &amp; team lead. Building iOS apps since 2012. These are my personal projects.</p>
    <div class="hero-meta">
      <a href="#works">See the work ↓</a>
      <span class="dot">·</span>
      <a href="mailto:NimoApps25@gmail.com">Get in touch</a>
    </div>
  </header>

  <!-- WORKS -->
  <section class="section works" id="works">
    <p class="section-eyebrow">Works</p>
    <h2 class="section-title">Apps I'm building</h2>

    <div class="apps">

      <!-- Parsee -->
      <article class="app parsee">
        <div class="app-text">
          <span class="status status-live">Available</span>
          <img class="app-icon" src="images/parsee-icon.png" alt="" width="64" height="64">
          <h3 class="app-name">Parsee</h3>
          <p class="app-tag">Parse. See. Understand.</p>
          <p class="app-desc">Native macOS JSON viewer with smart filters, AI insights, JSON diff, and Xcode LLDB integration. Built because the browser-tab JSON viewers were never enough.</p>
          <div class="app-cta">
            <a class="btn btn-primary" href="https://nimomix.github.io/Parsee-website/">Visit site →</a>
            <a class="btn btn-secondary" href="https://apps.apple.com/us/app/parsee-json-viewer/id6756983590">Mac App Store</a>
          </div>
        </div>
        <div class="app-visual app-visual-parsee">
          <img src="images/parsee-hero.jpg" alt="Parsee on the App Store: macOS window showing JSON tree, with feature list">
        </div>
      </article>

      <!-- Safeus -->
      <article class="app safeus">
        <div class="app-text">
          <span class="status status-soon">Coming soon</span>
          <img class="app-icon" src="images/safeus-icon.png" alt="" width="64" height="64">
          <h3 class="app-name">Safeus</h3>
          <p class="app-tag">Let your loved ones know you're safe.</p>
          <p class="app-desc">One-tap safety check-ins for iOS. Tell your contacts you're OK during emergencies, get notified when your group is accounted for. Phone-number based, privacy-first.</p>
          <div class="app-cta">
            <a class="btn btn-primary" href="https://nimomix.github.io/safeus/">Visit site →</a>
          </div>
        </div>
        <div class="app-visual app-visual-safeus">
          <img src="images/safeus-screenshot.png" alt="Safeus iPhone home screen showing the I'm Safe button">
        </div>
      </article>

      <!-- Bond -->
      <article class="app bond">
        <div class="app-text">
          <span class="status status-dev">In development</span>
          <img class="app-icon" src="images/bond-icon.png" alt="" width="64" height="64">
          <h3 class="app-name">Bond</h3>
          <p class="app-tag">Agreements made simple.</p>
          <p class="app-desc">Create, share, sign, and track personal agreements with the people who matter most. Coffee owed, freelance contract, or anything in between — iOS first, Hebrew &amp; English.</p>
        </div>
        <div class="app-visual app-visual-bond">
          <img src="images/bond-onboarding.png" alt="Bond iPhone onboarding screen">
        </div>
      </article>

    </div>
  </section>

  <!-- ABOUT -->
  <section class="section about" id="about">
    <p class="section-eyebrow">About</p>
    <h2 class="section-title">Hi, I'm Nimrod.</h2>
    <div class="about-prose">
      <p>14+ years building iOS apps, the last 8 leading teams. I care about thoughtful interfaces, performance, and code that ages well.</p>
      <p class="muted">The apps above are ones I cared enough about to ship on my own. Say hi if you'd like to talk shop or work together — my inbox is open.</p>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    <a class="footer-link" href="mailto:NimoApps25@gmail.com">Contact</a>
    <p class="copyright">© 2026 Nimrod Bar</p>
  </footer>

</body>
</html>
```

- [ ] **Step 3.2: Verify HTML written**

```bash
wc -l /Users/nbar/Projects/nimomix.github.io/index.html
```

Expected: ~80 lines.

```bash
grep -c "Nimrod Bar" /Users/nbar/Projects/nimomix.github.io/index.html
```

Expected: 2 (in `<title>` and `<h1>`) plus 1 in copyright = 3.

```bash
grep -c "NimoApps25@gmail.com" /Users/nbar/Projects/nimomix.github.io/index.html
```

Expected: 2 (hero meta + footer).

---

## Task 4: Build `styles.css`

**Files:**
- Create: `/Users/nbar/Projects/nimomix.github.io/styles.css`

- [ ] **Step 4.1: Write the complete `styles.css`**

Write `/Users/nbar/Projects/nimomix.github.io/styles.css` with this exact content:

```css
/* Personal site — Nimrod Bar
   Vanilla CSS, no build step. */

:root {
  /* Color tokens */
  --bg: #ffffff;
  --bg-alt: #fafafa;
  --text: #1d1d1f;
  --text-muted: #6e6e73;
  --text-faint: #86868b;
  --accent: #007AFF;
  --hairline: rgba(0, 0, 0, 0.06);

  --shadow-card: 0 1px 0 rgba(0,0,0,0.04),
                 0 8px 24px -8px rgba(0,0,0,0.12),
                 0 0 0 1px rgba(0,0,0,0.06);

  /* Type scale */
  --fs-hero: clamp(56px, 7vw, 88px);
  --fs-section: clamp(34px, 4vw, 44px);
  --fs-app-name: 30px;
  --fs-app-tag: 18px;
  --fs-body: 17px;
  --fs-small: 14px;

  --lh-display: 1;
  --lh-body: 1.5;

  --ls-display: -0.025em;
  --ls-section: -0.022em;
  --ls-app: -0.02em;
}

/* Reset */
*, *::before, *::after { box-sizing: border-box; }
* { margin: 0; }
html { -webkit-text-size-adjust: 100%; scroll-behavior: smooth; }
body {
  font-family: -apple-system, BlinkMacSystemFont, "SF Pro Display", "SF Pro Text", system-ui, sans-serif;
  font-size: var(--fs-body);
  line-height: var(--lh-body);
  color: var(--text);
  background: var(--bg);
  -webkit-font-smoothing: antialiased;
  text-rendering: optimizeLegibility;
}
img { display: block; max-width: 100%; height: auto; }
a { color: var(--accent); text-decoration: none; }

/* HERO */
.hero {
  background: radial-gradient(ellipse at 50% 0%, #1a1d24 0%, #0a0a0c 70%);
  color: #f5f5f7;
  padding: 96px 32px 72px;
  text-align: center;
  position: relative;
  overflow: hidden;
}
.hero::before {
  content: "";
  position: absolute;
  inset: 0;
  background: radial-gradient(600px 240px at 50% 0%, rgba(10,132,255,0.18), transparent 70%);
  pointer-events: none;
}
.hero-name {
  font-size: var(--fs-hero);
  font-weight: 700;
  letter-spacing: var(--ls-display);
  line-height: var(--lh-display);
}
.hero-role {
  font-size: 22px;
  color: #a1a1a6;
  margin: 22px auto 0;
  max-width: 580px;
  line-height: 1.45;
}
.hero-meta {
  margin-top: 36px;
  font-size: var(--fs-small);
  color: var(--text-faint);
  display: flex;
  gap: 18px;
  justify-content: center;
  flex-wrap: wrap;
}
.hero-meta a {
  color: #f5f5f7;
  border-bottom: 1px solid rgba(255,255,255,0.2);
  padding-bottom: 1px;
}
.hero-meta a:hover { border-color: #f5f5f7; }
.hero-meta .dot { color: #444; }

/* SECTIONS */
.section { padding: 96px 32px 72px; }
.section-eyebrow {
  text-align: center;
  font-size: 12px;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--text-faint);
  margin-bottom: 12px;
}
.section-title {
  text-align: center;
  font-size: var(--fs-section);
  font-weight: 700;
  letter-spacing: var(--ls-section);
  margin-bottom: 56px;
}

/* APP CARDS */
.apps {
  display: grid;
  grid-template-columns: 1fr;
  gap: 28px;
  max-width: 1040px;
  margin: 0 auto;
}
.app {
  display: grid;
  grid-template-columns: 1fr 1fr;
  border-radius: 22px;
  overflow: hidden;
  box-shadow: var(--shadow-card);
  background: #fff;
}
.app-text {
  padding: 44px 36px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
}
.app-icon {
  width: 64px;
  height: 64px;
  border-radius: 14px;
  box-shadow: 0 4px 14px rgba(0,0,0,0.08);
  margin-bottom: 18px;
}
.app-name {
  font-size: var(--fs-app-name);
  font-weight: 700;
  letter-spacing: var(--ls-app);
}
.app-tag {
  font-size: var(--fs-app-tag);
  color: var(--text-muted);
  margin: 6px 0 18px;
}
.app-desc {
  font-size: 15px;
  line-height: 1.55;
  margin-bottom: 24px;
}
.app-cta {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}

/* Buttons */
.btn {
  font-size: var(--fs-small);
  font-weight: 500;
  padding: 9px 16px;
  border-radius: 980px;
  display: inline-flex;
  align-items: center;
  gap: 6px;
  transition: opacity 0.15s;
}
.btn-primary { background: #1d1d1f; color: #fff; }
.btn-secondary { background: rgba(0,0,0,0.06); color: #1d1d1f; }
.btn:hover { opacity: 0.85; }

/* Status pills */
.status {
  position: absolute;
  top: 24px;
  right: 24px;
  font-size: 11px;
  font-weight: 600;
  padding: 5px 11px;
  border-radius: 980px;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  display: inline-flex;
  align-items: center;
  gap: 6px;
}
.status::before {
  content: "";
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: currentColor;
}
.status-live { background: rgba(52,199,89,0.10); color: #1f8a3b; }
.status-soon { background: rgba(255,159,10,0.12); color: #b46500; }
.status-dev  { background: rgba(212,175,80,0.18); color: #a07a1f; }

/* App visuals */
.app-visual {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 40px;
  min-height: 320px;
}
.app-visual img {
  max-width: 100%;
  max-height: 280px;
  border-radius: 8px;
  box-shadow: 0 12px 30px -8px rgba(0,0,0,0.18);
}

/* Parsee — App Store hero fills the cell edge-to-edge */
.app-visual-parsee {
  background: linear-gradient(135deg, #ece8f7 0%, #d4cdef 100%);
  padding: 0;
  overflow: hidden;
  min-height: 0;
}
.app-visual-parsee img {
  width: 100%;
  height: 100%;
  max-width: none;
  max-height: none;
  object-fit: cover;
  border-radius: 0;
  box-shadow: none;
}

/* Safeus — soft green, screenshot centered with rounded corners */
.app-visual-safeus {
  background: linear-gradient(135deg, #e9f5ee 0%, #d1ead9 100%);
}
.app-visual-safeus img {
  max-height: 320px;
  border-radius: 24px;
}

/* Bond — cream so dark phone reads against it */
.app-visual-bond {
  background: linear-gradient(135deg, #f4ebd4 0%, #e8d9b7 100%);
  padding: 32px;
}
.app-visual-bond img {
  max-height: 380px;
  border-radius: 28px;
  box-shadow: 0 18px 44px -12px rgba(60,40,10,0.35);
}

/* ABOUT */
.about { background: var(--bg-alt); text-align: center; }
.about-prose {
  max-width: 620px;
  margin: 0 auto;
  font-size: 19px;
  line-height: 1.6;
}
.about-prose p { margin-bottom: 18px; }
.about-prose p:last-child { margin-bottom: 0; }
.about-prose .muted { color: var(--text-muted); }

/* FOOTER */
.footer {
  padding: 56px 32px 64px;
  text-align: center;
  border-top: 1px solid var(--hairline);
}
.footer-link {
  color: var(--text);
  font-size: 15px;
  font-weight: 500;
  display: inline-block;
  margin-bottom: 16px;
}
.footer-link:hover { color: var(--accent); }
.copyright {
  color: var(--text-faint);
  font-size: 13px;
}

/* RESPONSIVE — stack app cards on narrow viewports */
@media (max-width: 720px) {
  .app {
    grid-template-columns: 1fr;
  }
  .app-visual {
    order: -1;
    min-height: 280px;
  }
  .status {
    top: 16px;
    right: 16px;
  }
}
```

- [ ] **Step 4.2: Verify CSS written**

```bash
wc -l /Users/nbar/Projects/nimomix.github.io/styles.css
```

Expected: ~230 lines.

```bash
grep -c "^[a-zA-Z\.]" /Users/nbar/Projects/nimomix.github.io/styles.css
```

Expected: at least 30 (CSS rule openers).

---

## Task 5: Local preview & visual verification

**Files:** none modified — verification only.

- [ ] **Step 5.1: Start a local server**

```bash
cd /Users/nbar/Projects/nimomix.github.io && python3 -m http.server 8000
```

Run in background. Server prints "Serving HTTP on 0.0.0.0 port 8000".

- [ ] **Step 5.2: Verify the page loads**

```bash
curl -s -o /dev/null -w "HTTP: %{http_code}\n" http://localhost:8000/
```

Expected: `HTTP: 200`.

- [ ] **Step 5.3: Verify all six images load**

```bash
for img in parsee-icon.png parsee-hero.jpg safeus-icon.png safeus-screenshot.png bond-icon.png bond-onboarding.png; do
  curl -s -o /dev/null -w "$img: %{http_code} (%{size_download} bytes)\n" "http://localhost:8000/images/$img"
done
```

Expected: all six return `200` with non-zero byte count.

- [ ] **Step 5.4: Open in default browser**

```bash
open http://localhost:8000/
```

Visual checklist (the engineer must look at the rendered page and confirm each):
- Hero renders with dark background, large "Nimrod Bar", subtitle visible, two text links underneath
- Parsee card: green "Available" pill, 3D cube icon, App Store hero fills the right side edge-to-edge on lavender, two CTA buttons
- Safeus card: amber "Coming soon" pill, Safeus icon, phone screenshot on soft green, single CTA button
- Bond card: gold "In development" pill, gold-on-black B icon, dark phone visible against cream background, no CTA button
- About section on grey background, "Hi, I'm Nimrod." title, two paragraphs
- Footer: "Contact" link, copyright

- [ ] **Step 5.5: Verify responsive at 720px**

In the browser, resize the window narrower than 720px (or use DevTools device emulation). App cards should stack vertically with the visual on top of the text.

- [ ] **Step 5.6: Click each link to verify destinations**

- "See the work ↓" → smooth-scrolls to Works section
- "Get in touch" → opens mail client to `NimoApps25@gmail.com`
- Parsee "Visit site →" → opens `https://nimomix.github.io/Parsee-website/`
- Parsee "Mac App Store" → opens App Store listing
- Safeus "Visit site →" → opens `https://nimomix.github.io/safeus/`
- Footer "Contact" → opens mail client

- [ ] **Step 5.7: Stop the local server**

Kill the background server process.

---

## Task 6: Initialize Git and first commit

**Files:** none — git operations only.

- [ ] **Step 6.1: Initialize the repo**

```bash
cd /Users/nbar/Projects/nimomix.github.io && git init -b main
```

Expected output: `Initialized empty Git repository in /Users/nbar/Projects/nimomix.github.io/.git/`.

- [ ] **Step 6.2: Stage all files**

```bash
git -C /Users/nbar/Projects/nimomix.github.io add .
```

- [ ] **Step 6.3: Verify what will be committed**

```bash
git -C /Users/nbar/Projects/nimomix.github.io status
```

Expected: untracked files now staged. You should see `index.html`, `styles.css`, `README.md`, `.gitignore`, six files in `images/`, the spec, and this plan. **You should NOT see** `.DS_Store` or anything in `.superpowers/`.

- [ ] **Step 6.4: Make the first commit**

```bash
git -C /Users/nbar/Projects/nimomix.github.io commit -m "$(cat <<'EOF'
Initial commit: personal site v1

Single-page portfolio site at nimomix.github.io.
Hero + works (Parsee/Safeus/Bond) + about + footer.
Vanilla HTML/CSS, no build step.

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>
EOF
)"
```

Expected output: commit hash and summary line printed.

---

## Task 7: Create GitHub repo and push

**Pre-requisite:** `gh` CLI installed and authenticated against the `nimomix` account.

- [ ] **Step 7.1: Verify `gh` is authenticated as `nimomix`**

```bash
gh auth status
```

Expected: shows the user is logged in to github.com. If the active account is NOT `nimomix`, switch with:

```bash
gh auth switch --user nimomix
```

If `nimomix` is not yet logged in, run `gh auth login` and follow prompts.

- [ ] **Step 7.2: Create the public repo (BLOCKING — confirm with user before running)**

This is a destructive/visible action: it creates a new public GitHub repository. **Confirm with the user before executing.** Once approved:

```bash
gh repo create nimomix/nimomix.github.io \
  --public \
  --description "Personal site for Nimrod Bar" \
  --source /Users/nbar/Projects/nimomix.github.io \
  --remote origin \
  --push
```

This single command: creates the repo, adds the remote as `origin`, and pushes the `main` branch.

Expected output: confirms repo creation and push.

- [ ] **Step 7.3: Verify the remote is set**

```bash
git -C /Users/nbar/Projects/nimomix.github.io remote -v
```

Expected: `origin  https://github.com/nimomix/nimomix.github.io.git (fetch)` and `(push)`.

---

## Task 8: Verify GitHub Pages deployment

**Files:** none — verification only. GitHub Pages auto-enables for `<user>.github.io` repos.

- [ ] **Step 8.1: Wait for the first Pages build**

GitHub builds the page within ~30-60 seconds of the first push to `main`. Poll:

```bash
for i in 1 2 3 4 5 6 7 8 9 10; do
  CODE=$(curl -s -o /dev/null -w "%{http_code}" -L https://nimomix.github.io/)
  echo "attempt $i: HTTP $CODE"
  [ "$CODE" = "200" ] && break
  sleep 15
done
```

Expected: eventually `HTTP 200` (may need a few attempts).

- [ ] **Step 8.2: Verify the live page contains the right content**

```bash
curl -s -L https://nimomix.github.io/ | grep -c "Nimrod Bar"
```

Expected: 3 or more (title, h1, copyright).

```bash
curl -s -L https://nimomix.github.io/ | grep -c "NimoApps25@gmail.com"
```

Expected: 2.

- [ ] **Step 8.3: Verify all six images load on the live site**

```bash
for img in parsee-icon.png parsee-hero.jpg safeus-icon.png safeus-screenshot.png bond-icon.png bond-onboarding.png; do
  curl -s -o /dev/null -w "$img: %{http_code}\n" "https://nimomix.github.io/images/$img"
done
```

Expected: all six return `200`.

- [ ] **Step 8.4: Open the live site**

```bash
open https://nimomix.github.io/
```

Final visual check: confirm the live site looks identical to the local preview from Task 5.

---

## Done

Site is live at `https://nimomix.github.io`. Future updates: edit files, commit, push to `main` — Pages rebuilds automatically.
