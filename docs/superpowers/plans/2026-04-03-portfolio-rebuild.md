# Portfolio Site Rebuild — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild Najeem Takiyu-Deen's portfolio as a polished single-page HTML/CSS/JS site with sections for Hero, About, Skills, Projects, Experience, Credentials, and Contact.

**Architecture:** Single `index.html` file containing all HTML structure, embedded `<style>` block with all CSS, and an embedded `<script>` block at the bottom for interactivity. Photo copied to `assets/photo.webp`. No build step, no framework — deploys directly to GitHub Pages.

**Tech Stack:** HTML5, CSS3 (custom properties, Grid, Flexbox), Vanilla JS (IntersectionObserver, scroll events), Google Fonts (Cormorant Garamond + DM Sans)

---

## File Map

| File | Action | Responsibility |
|---|---|---|
| `index.html` | Create (replaces `index.html.html`) | Full site — HTML + CSS + JS |
| `assets/photo.webp` | Copy from `C:\Users\najee\Desktop\preview.webp` | Profile photo |
| `index.html.html` | Delete after `index.html` is verified | Old file |

---

### Task 1: Setup — copy photo and create HTML skeleton

**Files:**
- Create: `assets/photo.webp` (copy)
- Create: `index.html`

- [ ] **Step 1: Create the assets folder and copy the photo**

```bash
mkdir -p C:/Users/najee/portfolio/assets
cp "C:/Users/najee/Desktop/preview.webp" "C:/Users/najee/portfolio/assets/photo.webp"
```

Verify: `ls C:/Users/najee/portfolio/assets/` shows `photo.webp`

- [ ] **Step 2: Create `index.html` with the full boilerplate skeleton**

Create `C:/Users/najee/portfolio/index.html` with this content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Najeem Takiyu-Deen — Data Analyst Portfolio</title>
<meta name="description" content="Portfolio of Najeem Takiyu-Deen — Global CRM Insights & Customer Data Analyst based in Zürich, Switzerland.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
/* ── CSS GOES HERE (added task by task) ── */
</style>
</head>
<body>

<!-- NAV -->
<!-- HERO -->
<!-- ABOUT -->
<!-- SKILLS -->
<!-- PROJECTS -->
<!-- EXPERIENCE -->
<!-- CREDENTIALS -->
<!-- CONTACT -->
<!-- FOOTER -->

<script>
/* ── JS GOES HERE (Task 11) ── */
</script>
</body>
</html>
```

- [ ] **Step 3: Open in browser to confirm it loads (blank white page is correct)**

Open `C:/Users/najee/portfolio/index.html` in your browser. It should show a blank page with no errors in the console.

- [ ] **Step 4: Commit**

```bash
cd C:/Users/najee/portfolio
git add assets/photo.webp index.html
git commit -m "chore: add photo asset and HTML skeleton for portfolio rebuild"
```

---

### Task 2: CSS Foundation — variables, reset, base styles

**Files:**
- Modify: `index.html` — fill in the `<style>` block

- [ ] **Step 1: Replace the `/* ── CSS GOES HERE ── */` comment with the full CSS foundation**

Inside the `<style>` block in `index.html`, add:

```css
/* ── VARIABLES ───────────────────────────────────────── */
:root {
  --navy: #1B1B2F;
  --navy-deep: #111120;
  --crystal: #3A6186;
  --crystal-light: #89A0B4;
  --gold: #C4A35A;
  --gold-light: #E8D5A3;
  --cream: #FAF8F4;
  --white: #FFFFFF;
  --text: #2C2C3E;
  --muted: #6B7280;
  --border: rgba(58,97,134,0.15);
}

/* ── RESET ───────────────────────────────────────────── */
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
img { display: block; max-width: 100%; }
a { text-decoration: none; color: inherit; }
ul { list-style: none; }
button { cursor: pointer; border: none; background: none; font-family: inherit; }

/* ── BASE ────────────────────────────────────────────── */
html { scroll-behavior: smooth; }

body {
  font-family: 'DM Sans', sans-serif;
  background: var(--cream);
  color: var(--text);
  overflow-x: hidden;
}

/* ── SHARED SECTION STYLES ───────────────────────────── */
.section-inner {
  max-width: 1100px;
  margin: 0 auto;
  padding: 80px 40px;
}

.section-label {
  font-size: 10px;
  font-weight: 500;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--crystal);
  margin-bottom: 12px;
}

.section-label--gold { color: var(--gold); }

.section-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 44px;
  font-weight: 300;
  color: var(--navy);
  margin-bottom: 48px;
  line-height: 1.15;
}

.section-title--white { color: var(--white); }

/* ── SCROLL ANIMATION ────────────────────────────────── */
.fade-in {
  opacity: 0;
  transform: translateY(28px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.fade-in.visible {
  opacity: 1;
  transform: translateY(0);
}

/* ── BUTTONS ─────────────────────────────────────────── */
.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 11px 24px;
  border-radius: 4px;
  font-size: 13px;
  font-weight: 500;
  letter-spacing: 0.5px;
  transition: opacity 0.2s, transform 0.15s;
  cursor: pointer;
}
.btn:hover { opacity: 0.85; transform: translateY(-1px); }

.btn-gold {
  background: var(--gold);
  color: var(--navy);
  font-weight: 600;
}

.btn-outline-gold {
  border: 1px solid rgba(196,163,90,0.5);
  color: var(--gold);
}

.btn-outline-crystal {
  border: 1px solid rgba(58,97,134,0.4);
  color: var(--crystal);
}

/* ── RESPONSIVE HELPERS ──────────────────────────────── */
@media (max-width: 768px) {
  .section-inner { padding: 60px 24px; }
  .section-title { font-size: 32px; }
}
```

- [ ] **Step 2: Verify in browser — page still blank, no console errors**

Refresh `index.html` in the browser. Still a blank cream page, no errors.

- [ ] **Step 3: Commit**

```bash
cd C:/Users/najee/portfolio
git add index.html
git commit -m "style: add CSS variables, reset, base styles, and utility classes"
```

---

### Task 3: Sticky Navigation

**Files:**
- Modify: `index.html` — add nav HTML and CSS

- [ ] **Step 1: Replace `<!-- NAV -->` comment with the nav HTML**

```html
<!-- ── NAV ────────────────────────────────────────────── -->
<header class="site-header" id="site-header">
  <nav class="nav-inner">
    <a href="#hero" class="nav-logo">NT</a>

    <button class="nav-hamburger" id="nav-hamburger" aria-label="Toggle menu">
      <span></span><span></span><span></span>
    </button>

    <ul class="nav-links" id="nav-links">
      <li><a href="#about" class="nav-link">About</a></li>
      <li><a href="#skills" class="nav-link">Skills</a></li>
      <li><a href="#projects" class="nav-link">Projects</a></li>
      <li><a href="#experience" class="nav-link">Experience</a></li>
      <li><a href="#credentials" class="nav-link">Credentials</a></li>
      <li><a href="#contact" class="nav-link">Contact</a></li>
    </ul>
  </nav>
</header>
```

- [ ] **Step 2: Add nav CSS inside the `<style>` block (before the closing `</style>`)**

```css
/* ── NAV ─────────────────────────────────────────────── */
.site-header {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  background: transparent;
  transition: background 0.3s ease, box-shadow 0.3s ease;
}

.site-header.scrolled {
  background: rgba(27, 27, 47, 0.97);
  box-shadow: 0 1px 0 rgba(196,163,90,0.15);
}

.nav-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 40px;
  height: 64px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-logo {
  font-family: 'DM Sans', sans-serif;
  font-size: 15px;
  font-weight: 600;
  letter-spacing: 3px;
  color: var(--gold);
}

.nav-links {
  display: flex;
  gap: 4px;
}

.nav-link {
  padding: 8px 16px;
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: rgba(255,255,255,0.6);
  border-bottom: 2px solid transparent;
  transition: color 0.2s, border-color 0.2s;
}

.nav-link:hover,
.nav-link.active {
  color: var(--gold);
  border-bottom-color: var(--gold);
}

/* Hamburger */
.nav-hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  padding: 4px;
}

.nav-hamburger span {
  display: block;
  width: 22px;
  height: 2px;
  background: var(--gold);
  border-radius: 2px;
  transition: transform 0.3s, opacity 0.3s;
}

.nav-hamburger.open span:nth-child(1) { transform: translateY(7px) rotate(45deg); }
.nav-hamburger.open span:nth-child(2) { opacity: 0; }
.nav-hamburger.open span:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

@media (max-width: 768px) {
  .nav-inner { padding: 0 24px; }
  .nav-hamburger { display: flex; }
  .nav-links {
    display: none;
    position: absolute;
    top: 64px; left: 0; right: 0;
    background: rgba(27,27,47,0.98);
    flex-direction: column;
    padding: 16px 24px 24px;
    border-top: 1px solid rgba(196,163,90,0.15);
    gap: 0;
  }
  .nav-links.open { display: flex; }
  .nav-link { padding: 14px 0; border-bottom: 1px solid rgba(255,255,255,0.06); }
  .nav-link:last-child { border-bottom: none; }
}
```

- [ ] **Step 3: Verify — open in browser, a transparent nav bar should appear at the top**

Refresh `index.html`. You should see the "NT" logo and nav links at the top in gold/muted white. No hamburger visible on desktop.

- [ ] **Step 4: Commit**

```bash
cd C:/Users/najee/portfolio
git add index.html
git commit -m "feat: add sticky navigation with hamburger menu"
```

---

### Task 4: Hero Section

**Files:**
- Modify: `index.html` — add hero HTML and CSS

- [ ] **Step 1: Replace `<!-- HERO -->` comment with hero HTML**

```html
<!-- ── HERO ───────────────────────────────────────────── -->
<section class="hero" id="hero">
  <div class="hero-bg-orb hero-bg-orb--1"></div>
  <div class="hero-bg-orb hero-bg-orb--2"></div>

  <div class="hero-left">
    <p class="hero-eyebrow">Portfolio · Data Analytics</p>
    <h1 class="hero-name">Najeem<br><em>Takiyu-Deen</em><br>BSc.</h1>
    <p class="hero-title">
      Global CRM Insights &amp; Customer Data Analyst<br>
      SQL · Python · Power BI · Agile / Scrum Certified
    </p>
    <div class="hero-contact">
      <div class="contact-item"><span class="contact-dot"></span>njmtdeen@gmail.com</div>
      <div class="contact-item"><span class="contact-dot"></span>+41 78 744 76 75</div>
      <div class="contact-item"><span class="contact-dot"></span>Zürich, Switzerland</div>
    </div>
    <div class="hero-badges">
      <span class="hero-badge">SQL</span>
      <span class="hero-badge">Python</span>
      <span class="hero-badge">Power BI</span>
      <span class="hero-badge">Scrum Certified</span>
    </div>
    <div class="hero-ctas">
      <a href="#projects" class="btn btn-gold">View Projects</a>
      <a href="#contact" class="btn btn-outline-gold">Get in Touch</a>
    </div>
  </div>

  <div class="hero-right">
    <div class="photo-frame">
      <img src="assets/photo.webp" alt="Najeem Takiyu-Deen" class="photo-circle" />
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add hero CSS in the `<style>` block**

```css
/* ── HERO ────────────────────────────────────────────── */
.hero {
  min-height: 100vh;
  background: var(--navy);
  display: grid;
  grid-template-columns: 1fr 1fr;
  align-items: center;
  position: relative;
  overflow: hidden;
  padding-top: 64px; /* nav height */
}

.hero-bg-orb {
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
}
.hero-bg-orb--1 {
  width: 600px; height: 600px;
  background: radial-gradient(circle, rgba(58,97,134,0.18) 0%, transparent 70%);
  top: -100px; right: -100px;
}
.hero-bg-orb--2 {
  width: 300px; height: 300px;
  background: radial-gradient(circle, rgba(196,163,90,0.12) 0%, transparent 70%);
  bottom: 50px; left: 80px;
}

.hero-left {
  padding: 80px 60px 80px 100px;
  position: relative;
  z-index: 2;
}

.hero-eyebrow {
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--gold);
  margin-bottom: 24px;
  animation: fadeUp 0.7s 0.1s ease both;
}

.hero-name {
  font-family: 'Cormorant Garamond', serif;
  font-size: 64px;
  font-weight: 300;
  line-height: 1.05;
  color: var(--white);
  margin-bottom: 16px;
  animation: fadeUp 0.7s 0.2s ease both;
}
.hero-name em {
  font-style: italic;
  color: var(--crystal-light);
}

.hero-title {
  font-size: 16px;
  font-weight: 300;
  color: var(--crystal-light);
  margin-bottom: 36px;
  line-height: 1.6;
  animation: fadeUp 0.7s 0.3s ease both;
}

.hero-contact {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 28px;
  animation: fadeUp 0.7s 0.4s ease both;
}
.contact-item {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 13px;
  color: rgba(255,255,255,0.6);
}
.contact-dot {
  width: 5px; height: 5px;
  border-radius: 50%;
  background: var(--gold);
  flex-shrink: 0;
}

.hero-badges {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
  margin-bottom: 36px;
  animation: fadeUp 0.7s 0.5s ease both;
}
.hero-badge {
  padding: 6px 16px;
  border: 1px solid rgba(196,163,90,0.4);
  border-radius: 20px;
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--gold-light);
}

.hero-ctas {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
  animation: fadeUp 0.7s 0.6s ease both;
}

.hero-right {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 80px;
  position: relative;
  z-index: 2;
  animation: fadeUp 0.9s 0.3s ease both;
}

.photo-frame { position: relative; }
.photo-frame::before {
  content: '';
  position: absolute;
  inset: -12px;
  border: 1px solid rgba(196,163,90,0.3);
  border-radius: 50%;
}
.photo-frame::after {
  content: '';
  position: absolute;
  inset: -24px;
  border: 1px solid rgba(58,97,134,0.2);
  border-radius: 50%;
}
.photo-circle {
  width: 280px; height: 280px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid rgba(196,163,90,0.5);
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(30px); }
  to   { opacity: 1; transform: translateY(0); }
}

@media (max-width: 900px) {
  .hero { grid-template-columns: 1fr; padding-top: 64px; }
  .hero-left { padding: 60px 24px 32px; }
  .hero-right { padding: 0 24px 60px; }
  .hero-name { font-size: 44px; }
  .photo-circle { width: 200px; height: 200px; }
}
```

- [ ] **Step 3: Verify — hero section fills the viewport with photo, name, and CTAs**

Refresh `index.html`. You should see the dark navy hero with your name in large serif font, the circular photo on the right, gold badges, and two CTA buttons.

- [ ] **Step 4: Commit**

```bash
cd C:/Users/najee/portfolio
git add index.html
git commit -m "feat: add hero section with photo, badges, and CTA buttons"
```

---

### Task 5: About Section

**Files:**
- Modify: `index.html` — add about HTML and CSS

- [ ] **Step 1: Replace `<!-- ABOUT -->` comment with about HTML**

```html
<!-- ── ABOUT ──────────────────────────────────────────── -->
<section id="about" style="background: var(--cream);">
  <div class="section-inner fade-in">
    <p class="section-label">About</p>
    <h2 class="section-title">Data meets<br>operational insight</h2>
    <div class="about-grid">
      <p class="about-text">
        BSc. Business Informatics graduate with hands-on experience translating raw operational
        and IT data into structured insights, automated reporting, and process improvements.
        Scrum-certified practitioner who thrives at the intersection of analytics and
        cross-functional teamwork. Passionate about leveraging SQL, Python, and data
        visualisation to help organisations make smarter, faster, customer-centric decisions.
      </p>
      <div class="about-stats">
        <div class="stat-card">
          <div class="stat-number">4+</div>
          <div class="stat-label">Years professional IT &amp; data experience</div>
        </div>
        <div class="stat-card">
          <div class="stat-number">BSc.</div>
          <div class="stat-label">Business Informatics — FHNW Basel</div>
        </div>
        <div class="stat-card">
          <div class="stat-number">Zürich</div>
          <div class="stat-label">Based in Switzerland · Available immediately</div>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add about CSS in the `<style>` block**

```css
/* ── ABOUT ───────────────────────────────────────────── */
.about-grid {
  display: grid;
  grid-template-columns: 1.6fr 1fr;
  gap: 60px;
  align-items: start;
}
.about-text {
  font-size: 17px;
  line-height: 1.85;
  color: #3C3C50;
  font-weight: 300;
}
.about-stats {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.stat-card {
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 24px;
  position: relative;
  overflow: hidden;
}
.stat-card::before {
  content: '';
  position: absolute;
  left: 0; top: 0; bottom: 0;
  width: 3px;
  background: var(--crystal);
}
.stat-number {
  font-family: 'Cormorant Garamond', serif;
  font-size: 36px;
  font-weight: 300;
  color: var(--navy);
  line-height: 1;
  margin-bottom: 4px;
}
.stat-label {
  font-size: 12px;
  color: var(--muted);
}

@media (max-width: 768px) {
  .about-grid { grid-template-columns: 1fr; gap: 32px; }
}
```

- [ ] **Step 3: Verify — cream About section appears below the hero with stats cards on the right**

Scroll down past the hero. You should see the section label "ABOUT", large serif heading, summary paragraph, and three stat cards.

- [ ] **Step 4: Commit**

```bash
cd C:/Users/najee/portfolio
git add index.html
git commit -m "feat: add About section with summary and stat cards"
```

---

### Task 6: Skills Section

**Files:**
- Modify: `index.html` — add skills HTML and CSS

- [ ] **Step 1: Replace `<!-- SKILLS -->` comment with skills HTML**

```html
<!-- ── SKILLS ─────────────────────────────────────────── -->
<section id="skills" style="background: var(--navy);">
  <div class="section-inner fade-in">
    <p class="section-label section-label--gold">Skills</p>
    <h2 class="section-title section-title--white">Technical toolkit</h2>
    <div class="skills-grid">

      <div class="skill-card">
        <div class="skill-icon">📊</div>
        <div class="skill-name">Data Analytics</div>
        <div class="skill-tags">
          <span class="skill-tag">SQL</span>
          <span class="skill-tag">Python</span>
          <span class="skill-tag">KPI Design</span>
          <span class="skill-tag">Root Cause Analysis</span>
          <span class="skill-tag">Data Quality</span>
        </div>
      </div>

      <div class="skill-card">
        <div class="skill-icon">📈</div>
        <div class="skill-name">Reporting &amp; Visualisation</div>
        <div class="skill-tags">
          <span class="skill-tag">Power BI</span>
          <span class="skill-tag">Dashboards</span>
          <span class="skill-tag">Automated Reporting</span>
          <span class="skill-tag">Stakeholder Presentations</span>
        </div>
      </div>

      <div class="skill-card">
        <div class="skill-icon">⚙️</div>
        <div class="skill-name">Automation &amp; Systems</div>
        <div class="skill-tags">
          <span class="skill-tag">Python Scripts</span>
          <span class="skill-tag">ServiceNow</span>
          <span class="skill-tag">Microsoft 365</span>
          <span class="skill-tag">SharePoint</span>
          <span class="skill-tag">Confluence</span>
        </div>
      </div>

      <div class="skill-card">
        <div class="skill-icon">🔄</div>
        <div class="skill-name">Agile &amp; Delivery</div>
        <div class="skill-tags">
          <span class="skill-tag">Scrum (Certified)</span>
          <span class="skill-tag">Sprint Planning</span>
          <span class="skill-tag">Retrospectives</span>
          <span class="skill-tag">Iterative Delivery</span>
        </div>
      </div>

      <div class="skill-card">
        <div class="skill-icon">🗄️</div>
        <div class="skill-name">Data Management</div>
        <div class="skill-tags">
          <span class="skill-tag">Data Cleansing</span>
          <span class="skill-tag">Reconciliation</span>
          <span class="skill-tag">Multi-source Integration</span>
          <span class="skill-tag">Audit Trails</span>
        </div>
      </div>

      <div class="skill-card">
        <div class="skill-icon">🤝</div>
        <div class="skill-name">Collaboration</div>
        <div class="skill-tags">
          <span class="skill-tag">Cross-functional Teams</span>
          <span class="skill-tag">Documentation</span>
          <span class="skill-tag">Knowledge Transfer</span>
          <span class="skill-tag">SLA Compliance</span>
        </div>
      </div>

    </div>
  </div>
</section>
```

- [ ] **Step 2: Add skills CSS in the `<style>` block**

```css
/* ── SKILLS ──────────────────────────────────────────── */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}
.skill-card {
  background: rgba(255,255,255,0.04);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 12px;
  padding: 28px;
  transition: background 0.2s;
}
.skill-card:hover { background: rgba(58,97,134,0.15); }
.skill-icon {
  width: 36px; height: 36px;
  background: rgba(196,163,90,0.15);
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
  margin-bottom: 16px;
}
.skill-name {
  font-size: 15px;
  font-weight: 500;
  color: var(--white);
  margin-bottom: 10px;
}
.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}
.skill-tag {
  font-size: 11px;
  padding: 3px 10px;
  background: rgba(58,97,134,0.25);
  border-radius: 10px;
  color: var(--crystal-light);
}

@media (max-width: 900px) {
  .skills-grid { grid-template-columns: repeat(2, 1fr); }
}
@media (max-width: 600px) {
  .skills-grid { grid-template-columns: 1fr; }
}
```

- [ ] **Step 3: Verify — dark Skills section with 3×2 grid of cards**

Scroll to Skills. Dark background, gold section label, 6 skill cards in a 3-column grid each with emoji icon and tag pills.

- [ ] **Step 4: Commit**

```bash
cd C:/Users/najee/portfolio
git add index.html
git commit -m "feat: add Skills section with 6 skill cards"
```

---

### Task 7: Projects Section

**Files:**
- Modify: `index.html` — add projects HTML and CSS

- [ ] **Step 1: Replace `<!-- PROJECTS -->` comment with projects HTML**

```html
<!-- ── PROJECTS ───────────────────────────────────────── -->
<section id="projects" style="background: var(--cream);">
  <div class="section-inner fade-in">
    <p class="section-label">Projects</p>
    <h2 class="section-title">Selected work</h2>
    <div class="projects-grid">

      <div class="project-card">
        <div class="project-card-header">
          <span class="project-flag">🇬🇭</span>
          <div class="project-header-bg"></div>
        </div>
        <div class="project-card-body">
          <div class="project-tags">
            <span class="project-tag">React</span>
            <span class="project-tag">Vite</span>
            <span class="project-tag">JavaScript</span>
          </div>
          <h3 class="project-title">GhanaSource</h3>
          <p class="project-desc">
            Product sourcing platform for Ghana entrepreneurs. Browse suppliers from
            China, India &amp; UAE, calculate landed costs with Ghana import duties
            (VAT, NHIL, GETFUND), and track your sourcing pipeline from research to arrival.
          </p>
          <div class="project-links">
            <a href="https://najeem-codes.github.io/ghana-sourcing-app/" target="_blank" rel="noreferrer" class="btn btn-gold btn-sm">Live Site ↗</a>
            <a href="https://github.com/najeem-codes/ghana-sourcing-app" target="_blank" rel="noreferrer" class="btn btn-outline-crystal btn-sm">GitHub</a>
          </div>
        </div>
      </div>

      <div class="project-card project-card--placeholder">
        <div class="project-placeholder-inner">
          <div class="project-placeholder-icon">+</div>
          <p>More projects coming soon</p>
        </div>
      </div>

    </div>
  </div>
</section>
```

- [ ] **Step 2: Add projects CSS in the `<style>` block**

```css
/* ── PROJECTS ────────────────────────────────────────── */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 24px;
}
.project-card {
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: 16px;
  overflow: hidden;
  transition: transform 0.2s, box-shadow 0.2s;
}
.project-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 32px rgba(27,27,47,0.12);
}
.project-card-header {
  height: 140px;
  background: linear-gradient(135deg, var(--navy) 0%, var(--crystal) 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}
.project-flag {
  font-size: 48px;
  position: relative;
  z-index: 2;
}
.project-header-bg {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 70% 50%, rgba(196,163,90,0.15) 0%, transparent 60%);
}
.project-card-body { padding: 24px; }
.project-tags {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
  margin-bottom: 12px;
}
.project-tag {
  font-size: 10px;
  padding: 3px 10px;
  background: rgba(58,97,134,0.1);
  border-radius: 10px;
  color: var(--crystal);
  font-weight: 500;
}
.project-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 24px;
  font-weight: 600;
  color: var(--navy);
  margin-bottom: 10px;
}
.project-desc {
  font-size: 14px;
  line-height: 1.65;
  color: var(--muted);
  margin-bottom: 20px;
}
.project-links {
  display: flex;
  gap: 10px;
}
.btn-sm {
  padding: 8px 18px;
  font-size: 12px;
}
.project-card--placeholder {
  border: 2px dashed var(--border);
  background: transparent;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 280px;
}
.project-card--placeholder:hover {
  transform: none;
  box-shadow: none;
  border-color: var(--crystal);
}
.project-placeholder-inner {
  text-align: center;
  color: var(--muted);
}
.project-placeholder-icon {
  font-size: 32px;
  margin-bottom: 8px;
  color: var(--border);
}
.project-placeholder-inner p {
  font-size: 14px;
}

@media (max-width: 600px) {
  .projects-grid { grid-template-columns: 1fr; }
}
```

- [ ] **Step 3: Verify — GhanaSource card with live/GitHub buttons + placeholder card**

Scroll to Projects. Cream background, GhanaSource card with flag graphic header, description, and two buttons. Placeholder card with dashed border on the right.

- [ ] **Step 4: Commit**

```bash
cd C:/Users/najee/portfolio
git add index.html
git commit -m "feat: add Projects section with GhanaSource card and placeholder"
```

---

### Task 8: Experience Section

**Files:**
- Modify: `index.html` — add experience HTML and CSS

- [ ] **Step 1: Replace `<!-- EXPERIENCE -->` comment with experience HTML**

```html
<!-- ── EXPERIENCE ─────────────────────────────────────── -->
<section id="experience" style="background: var(--cream);">
  <div class="section-inner fade-in">
    <p class="section-label">Experience</p>
    <h2 class="section-title">Professional journey</h2>
    <div class="timeline">

      <div class="timeline-item">
        <div class="timeline-dot"></div>
        <div class="timeline-date">Dec 2024 – Present</div>
        <div class="timeline-role">Data Center Operations &amp; Security Officer</div>
        <div class="timeline-company">Protectas SA at AWS Data Center · Zürich</div>
        <ul class="timeline-bullets">
          <li>Maintain structured operational databases tracking access events and incidents, developing data accuracy skills directly applicable to CRM data management</li>
          <li>Design and maintain daily performance reporting formats and escalation workflows — analogous to CRM performance cockpit and KPI monitoring</li>
          <li>Analyse recurring incident patterns to identify root causes and recommend iterative process improvements</li>
          <li>Collaborate cross-functionally with AWS site teams, demonstrating stakeholder communication across technical and non-technical audiences</li>
        </ul>
      </div>

      <div class="timeline-item">
        <div class="timeline-dot"></div>
        <div class="timeline-date">Jun 2024 – Jan 2025</div>
        <div class="timeline-role">IT Service Desk Technician</div>
        <div class="timeline-company">Altor Equity · Switzerland (Freelance)</div>
        <ul class="timeline-bullets">
          <li>Tracked and structured incident data in ServiceNow, performing trend analysis and root cause identification to improve data quality</li>
          <li>Built and maintained SharePoint and ShareDrive frameworks — equivalent to CRM team sites and data collaboration structures</li>
          <li>Produced structured management reports and knowledge base documentation for consistent, high-quality findings delivery</li>
        </ul>
      </div>

      <div class="timeline-item">
        <div class="timeline-dot"></div>
        <div class="timeline-date">Dec 2020 – Nov 2024</div>
        <div class="timeline-role">IT Consultant &amp; Automation Specialist</div>
        <div class="timeline-company">STECHAD · Switzerland (Freelance)</div>
        <ul class="timeline-bullets">
          <li>Developed Python automation scripts and Slack bots to replace manual reporting tasks — directly comparable to automated no-touch reporting pipelines</li>
          <li>Managed multi-source data collection, cleansing, and integration ensuring consistency and eliminating data gaps</li>
          <li>Translated complex technical findings into clear presentations for senior stakeholders across diverse client environments</li>
          <li>Applied Agile/Scrum methodology delivering iterative improvements within sprint frameworks</li>
        </ul>
      </div>

      <div class="timeline-item">
        <div class="timeline-dot"></div>
        <div class="timeline-date">Jul 2020 – Jan 2021</div>
        <div class="timeline-role">Logistician</div>
        <div class="timeline-company">Swiss Post · Zürich</div>
        <ul class="timeline-bullets">
          <li>Managed technical inventory data ensuring accurate reconciliation and cross-referencing against third-party sources</li>
          <li>Identified and resolved data discrepancies, developing strong attention to detail and data quality discipline</li>
        </ul>
      </div>

    </div>
  </div>
</section>
```

- [ ] **Step 2: Add experience CSS in the `<style>` block**

```css
/* ── EXPERIENCE ──────────────────────────────────────── */
.timeline {
  position: relative;
  padding-left: 32px;
}
.timeline::before {
  content: '';
  position: absolute;
  left: 6px; top: 8px; bottom: 0;
  width: 1px;
  background: var(--border);
}
.timeline-item {
  position: relative;
  margin-bottom: 48px;
}
.timeline-item:last-child { margin-bottom: 0; }
.timeline-dot {
  position: absolute;
  left: -32px; top: 6px;
  width: 13px; height: 13px;
  border-radius: 50%;
  background: var(--crystal);
  border: 2px solid var(--cream);
  box-shadow: 0 0 0 3px rgba(58,97,134,0.2);
}
.timeline-date {
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: var(--crystal);
  margin-bottom: 6px;
}
.timeline-role {
  font-family: 'Cormorant Garamond', serif;
  font-size: 22px;
  font-weight: 600;
  color: var(--navy);
  margin-bottom: 2px;
}
.timeline-company {
  font-size: 13px;
  color: var(--muted);
  margin-bottom: 16px;
  font-style: italic;
}
.timeline-bullets {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
.timeline-bullets li {
  font-size: 14px;
  line-height: 1.6;
  color: #4A4A5A;
  padding-left: 16px;
  position: relative;
}
.timeline-bullets li::before {
  content: '';
  position: absolute;
  left: 0; top: 9px;
  width: 5px; height: 1px;
  background: var(--crystal);
}
```

- [ ] **Step 3: Verify — cream Experience section with vertical timeline and 4 entries**

Scroll to Experience. Crystal-blue timeline dots with vertical line, serif role titles, italic company names, bullet-pointed achievements.

- [ ] **Step 4: Commit**

```bash
cd C:/Users/najee/portfolio
git add index.html
git commit -m "feat: add Experience section with 4-entry timeline"
```

---

### Task 9: Credentials Section

**Files:**
- Modify: `index.html` — add credentials HTML and CSS

- [ ] **Step 1: Replace `<!-- CREDENTIALS -->` comment with credentials HTML**

```html
<!-- ── CREDENTIALS ────────────────────────────────────── -->
<section id="credentials" style="background: var(--white);">
  <div class="section-inner fade-in">
    <p class="section-label">Credentials</p>
    <h2 class="section-title">Education &amp; Certifications</h2>
    <div class="cred-grid">

      <div class="cred-card cred-card--crystal">
        <div class="cred-year">2020 – 2024</div>
        <div class="cred-title">BSc. Business Informatics</div>
        <div class="cred-org">FHNW Basel — University of Applied Sciences &amp; Arts Northwestern Switzerland</div>
      </div>

      <div class="cred-card cred-card--gold">
        <div class="cred-year">2025</div>
        <div class="cred-title">Scrum Certification</div>
        <div class="cred-org">Certified Scrum practitioner — Agile sprint delivery, iterative improvement, cross-team collaboration</div>
      </div>

      <div class="cred-card cred-card--light">
        <div class="cred-year">In Progress</div>
        <div class="cred-title">Power BI &amp; SQL Advanced</div>
        <div class="cred-org">Actively developing data visualisation and advanced query skills for analytics environments</div>
      </div>

    </div>
    <div class="attach-note">
      University certificate, professional job references, and all other certificates are available on request.
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add credentials CSS in the `<style>` block**

```css
/* ── CREDENTIALS ─────────────────────────────────────── */
.cred-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin-bottom: 32px;
}
.cred-card {
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 28px;
  position: relative;
  overflow: hidden;
}
.cred-card::after {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 3px;
}
.cred-card--crystal::after { background: var(--crystal); }
.cred-card--gold::after    { background: linear-gradient(90deg, var(--crystal), var(--gold)); }
.cred-card--light::after   { background: var(--crystal-light); }

.cred-year {
  font-size: 11px;
  color: var(--gold);
  font-weight: 500;
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 8px;
}
.cred-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 20px;
  font-weight: 600;
  color: var(--navy);
  margin-bottom: 6px;
}
.cred-org {
  font-size: 13px;
  color: var(--muted);
  font-style: italic;
  line-height: 1.5;
}
.attach-note {
  background: rgba(58,97,134,0.06);
  border: 1px solid rgba(58,97,134,0.15);
  border-radius: 10px;
  padding: 20px 24px;
  font-size: 14px;
  color: var(--crystal);
  display: flex;
  align-items: center;
  gap: 12px;
}
.attach-note::before { content: '📎'; font-size: 18px; }

@media (max-width: 768px) {
  .cred-grid { grid-template-columns: 1fr; }
}
```

- [ ] **Step 3: Verify — white Credentials section with 3 cards and the attachment note**

Scroll to Credentials. White background, 3 cards with coloured top border accents, attachment note in blue below.

- [ ] **Step 4: Commit**

```bash
cd C:/Users/najee/portfolio
git add index.html
git commit -m "feat: add Credentials section with education and certification cards"
```

---

### Task 10: Contact Section and Footer

**Files:**
- Modify: `index.html` — add contact HTML, footer HTML, and CSS

- [ ] **Step 1: Replace `<!-- CONTACT -->` comment with contact HTML**

```html
<!-- ── CONTACT ────────────────────────────────────────── -->
<section id="contact" style="background: var(--navy);">
  <div class="section-inner fade-in">
    <p class="section-label section-label--gold">Contact</p>
    <h2 class="section-title section-title--white">Let's connect</h2>
    <div class="contact-grid">

      <div class="contact-info">
        <div class="contact-detail">
          <span class="contact-detail-icon">✉</span>
          <a href="mailto:njmtdeen@gmail.com" class="contact-detail-text">njmtdeen@gmail.com</a>
        </div>
        <div class="contact-detail">
          <span class="contact-detail-icon">📍</span>
          <span class="contact-detail-text">Zürich, Switzerland</span>
        </div>
        <div class="contact-detail">
          <span class="contact-detail-icon">📞</span>
          <a href="tel:+41787447675" class="contact-detail-text">+41 78 744 76 75</a>
        </div>
        <div class="contact-socials">
          <a href="https://github.com/najeem-codes" target="_blank" rel="noreferrer" class="btn btn-gold btn-sm">GitHub</a>
          <a href="#" class="btn btn-outline-gold btn-sm">LinkedIn</a>
        </div>
      </div>

      <form class="contact-form" action="mailto:njmtdeen@gmail.com" method="GET" enctype="text/plain">
        <div class="form-group">
          <input type="text" name="subject" placeholder="Your name" class="form-input" required>
        </div>
        <div class="form-group">
          <input type="email" name="email" placeholder="Your email" class="form-input">
        </div>
        <div class="form-group">
          <textarea name="body" placeholder="Your message..." class="form-input form-textarea" rows="4" required></textarea>
        </div>
        <button type="submit" class="btn btn-gold" style="width:100%; justify-content:center;">Send Message</button>
      </form>

    </div>
  </div>
</section>
```

- [ ] **Step 2: Replace `<!-- FOOTER -->` comment with footer HTML**

```html
<!-- ── FOOTER ─────────────────────────────────────────── -->
<footer class="site-footer">
  <p>© 2026 Najeem Takiyu-Deen · njmtdeen@gmail.com · Zürich, Switzerland</p>
</footer>
```

- [ ] **Step 3: Add contact and footer CSS in the `<style>` block**

```css
/* ── CONTACT ─────────────────────────────────────────── */
.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: start;
}
.contact-info {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.contact-detail {
  display: flex;
  align-items: center;
  gap: 14px;
}
.contact-detail-icon {
  width: 36px; height: 36px;
  background: rgba(196,163,90,0.1);
  border: 1px solid rgba(196,163,90,0.2);
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 16px;
  flex-shrink: 0;
}
.contact-detail-text {
  font-size: 15px;
  color: rgba(255,255,255,0.7);
  transition: color 0.2s;
}
a.contact-detail-text:hover { color: var(--gold); }
.contact-socials {
  display: flex;
  gap: 12px;
  margin-top: 8px;
}

/* Form */
.contact-form { display: flex; flex-direction: column; gap: 14px; }
.form-group { width: 100%; }
.form-input {
  width: 100%;
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 8px;
  padding: 14px 16px;
  font-family: 'DM Sans', sans-serif;
  font-size: 14px;
  color: rgba(255,255,255,0.8);
  transition: border-color 0.2s;
  outline: none;
}
.form-input::placeholder { color: rgba(255,255,255,0.3); }
.form-input:focus { border-color: rgba(196,163,90,0.5); }
.form-textarea { resize: vertical; min-height: 100px; }

@media (max-width: 768px) {
  .contact-grid { grid-template-columns: 1fr; gap: 40px; }
}

/* ── FOOTER ──────────────────────────────────────────── */
.site-footer {
  background: var(--navy-deep);
  text-align: center;
  padding: 32px;
}
.site-footer p {
  font-size: 12px;
  color: rgba(255,255,255,0.3);
  letter-spacing: 1px;
}
```

- [ ] **Step 4: Verify — dark Contact section with details + form, and footer below**

Scroll to Contact. Gold section label, email/phone/location on the left, contact form on the right. Deep navy footer at the very bottom.

- [ ] **Step 5: Commit**

```bash
cd C:/Users/najee/portfolio
git add index.html
git commit -m "feat: add Contact section with form and footer"
```

---

### Task 11: JavaScript — scroll nav, animations, hamburger

**Files:**
- Modify: `index.html` — fill in the `<script>` block

- [ ] **Step 1: Replace `/* ── JS GOES HERE ── */` in the `<script>` block with the full JS**

```js
// ── NAV: scroll transparency + active section highlight ──
const header = document.getElementById('site-header');
const navLinks = document.querySelectorAll('.nav-link');
const sections = document.querySelectorAll('section[id], div[id]');

window.addEventListener('scroll', () => {
  // Toggle scrolled class for nav background
  if (window.scrollY > 80) {
    header.classList.add('scrolled');
  } else {
    header.classList.remove('scrolled');
  }

  // Highlight active nav link
  let current = '';
  sections.forEach(section => {
    const sectionTop = section.offsetTop - 100;
    if (window.scrollY >= sectionTop) {
      current = section.getAttribute('id');
    }
  });
  navLinks.forEach(link => {
    link.classList.remove('active');
    if (link.getAttribute('href') === '#' + current) {
      link.classList.add('active');
    }
  });
});

// ── HAMBURGER MENU ──────────────────────────────────────
const hamburger = document.getElementById('nav-hamburger');
const navList = document.getElementById('nav-links');

hamburger.addEventListener('click', () => {
  hamburger.classList.toggle('open');
  navList.classList.toggle('open');
});

// Close menu when a link is clicked
navList.querySelectorAll('.nav-link').forEach(link => {
  link.addEventListener('click', () => {
    hamburger.classList.remove('open');
    navList.classList.remove('open');
  });
});

// ── SCROLL ANIMATIONS (IntersectionObserver) ────────────
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
      observer.unobserve(entry.target); // animate once only
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));
```

- [ ] **Step 2: Verify scroll behaviour**

Open `index.html` and scroll down. The nav should:
- Start transparent over the hero
- Turn dark/opaque after scrolling ~80px
- Highlight the correct nav link as you scroll through sections

- [ ] **Step 3: Verify hamburger on mobile**

Resize the browser to < 768px width. The nav links should disappear and a hamburger icon should appear. Clicking it should show/hide the mobile menu.

- [ ] **Step 4: Verify fade-in animations**

Scroll through the page. Each section (About, Skills, Projects, etc.) should fade up into view the first time it enters the viewport.

- [ ] **Step 5: Commit**

```bash
cd C:/Users/najee/portfolio
git add index.html
git commit -m "feat: add scroll nav, IntersectionObserver animations, and hamburger menu"
```

---

### Task 12: Cleanup and Deploy

**Files:**
- Delete: `index.html.html`
- Modify: `index.html` — verify final state
- Modify: `.gitignore` — add `.superpowers/`

- [ ] **Step 1: Add `.superpowers/` to `.gitignore`**

Create or edit `C:/Users/najee/portfolio/.gitignore`:

```
.superpowers/
```

- [ ] **Step 2: Do a full visual check of the deployed file**

Open `index.html` in the browser. Walk through every section and verify:
- [ ] Nav is sticky and transparent on hero, dark on scroll
- [ ] Hero photo loads correctly from `assets/photo.webp`
- [ ] All 6 skill cards render correctly
- [ ] GhanaSource project card links work (`target="_blank"`)
- [ ] Timeline has 4 entries
- [ ] Credentials has 3 cards
- [ ] Contact form opens mail client on Submit
- [ ] Hamburger works on narrow viewport

- [ ] **Step 3: Delete the old file**

```bash
cd C:/Users/najee/portfolio
rm "index.html.html"
```

- [ ] **Step 4: Commit everything**

```bash
cd C:/Users/najee/portfolio
git add .gitignore
git rm "index.html.html"
git commit -m "chore: remove old index.html.html, add .gitignore for .superpowers"
```

- [ ] **Step 5: Push to GitHub**

```bash
cd C:/Users/najee/portfolio
git push
```

- [ ] **Step 6: Enable GitHub Pages**

Go to `https://github.com/najeem-codes/portfolio/settings/pages`, set Source to **main branch / root**, click Save.

The site will be live at `https://najeem-codes.github.io/portfolio/` within ~1 minute.
