# Jyothicherukuri.com Site Build Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the complete static Jyothicherukuri.com site (6 pages, 3 blog posts, shared CSS/JS) locally, ready for review before deployment.

**Architecture:** Plain static HTML5/CSS3/vanilla JS, no framework, no build step. One shared stylesheet and one shared script included by every page via relative paths. Six top-level pages plus an `insights/` subfolder holding the blog index and three posts.

**Tech Stack:** HTML5, CSS3 (custom properties, flexbox/grid), vanilla JavaScript (no libraries), Google Fonts (Inter) via CDN link, Formspree (free tier) for contact form submission.

## Global Constraints

- No build tools — static HTML5/CSS3/vanilla JS only, matches the local machine having no Node/Python.
- Every page includes exactly one stylesheet (`css/styles.css`) and one script (`js/main.js`), via relative paths (`../` prefix for pages inside `insights/`).
- Design tokens are defined once as CSS custom properties in Task 1 and never redefined per page: accent `#0f5c57` (deep teal), text `#1f2933`, muted text `#52606d`, background `#ffffff`, surface `#f4f6f5`, border `#e3e8e6`.
- Public-facing contact info is limited to email (`jcherukuri03@gmail.com`) and LinkedIn (`https://www.linkedin.com/in/jyothi-cherukuri-42a14824/`) — no phone number appears in any committed file, per prior privacy decision.
- Every page shares identical header nav (Home / About / Experience / Skills / Insights / Contact) and footer (copyright + LinkedIn + email) markup, adjusting only relative link paths for pages inside `insights/`.
- Blog content is original reflective writing grounded in the resume's real roles/responsibilities — no fabricated project specifics beyond what the resume documents.
- The Formspree form action is a placeholder (`https://formspree.io/f/YOUR_FORM_ID`) until the user creates their free account in Task 11 — that task includes the exact replacement step.
- Commit after every task with a descriptive message.

---

### Task 1: CSS Design System

**Files:**
- Create: `css/styles.css`

**Interfaces:**
- Consumes: nothing (first task)
- Produces: CSS custom properties (`--color-bg`, `--color-surface`, `--color-text`, `--color-text-muted`, `--color-accent`, `--color-accent-dark`, `--color-border`, `--font-sans`, `--max-width`, `--radius`) and classes (`.container`, `.site-header`, `.nav-inner`, `.logo`, `.site-nav`, `.nav-toggle`, `.hero`, `.hero-monogram`, `.tagline`, `.hero-sub`, `.hero-cta`, `.btn`, `.btn-primary`, `.btn-outline`, `.stat-strip`, `.stat`, `.section`, `.section-surface`, `.cards`, `.card`, `.timeline`, `.timeline-item`, `.timeline-role`, `.timeline-meta`, `.skills-grid`, `.tag-list`, `.tag`, `.post-list`, `.post-card`, `.post-meta`, `.article`, `.back-link`, `.contact-grid`, `.form-group`, `.contact-side`, `.site-footer`, `.footer-inner`, `.footer-links`, `.fade-in`/`.visible`) that every later task's HTML relies on by exact name.

- [ ] **Step 1: Create the stylesheet with full content**

```css
:root {
  --color-bg: #ffffff;
  --color-surface: #f4f6f5;
  --color-text: #1f2933;
  --color-text-muted: #52606d;
  --color-accent: #0f5c57;
  --color-accent-dark: #0b4541;
  --color-border: #e3e8e6;
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --max-width: 1080px;
  --radius: 10px;
  --shadow-sm: 0 1px 2px rgba(31, 41, 51, 0.06);
  --shadow-md: 0 8px 24px rgba(31, 41, 51, 0.08);
}

* { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; }

body {
  font-family: var(--font-sans);
  color: var(--color-text);
  background: var(--color-bg);
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}

img { max-width: 100%; display: block; }

a { color: var(--color-accent); text-decoration: none; }
a:hover { color: var(--color-accent-dark); }

.container {
  max-width: var(--max-width);
  margin: 0 auto;
  padding: 0 24px;
}

h1, h2, h3 { line-height: 1.25; font-weight: 700; }
h1 { font-size: 2.5rem; }
h2 { font-size: 1.9rem; margin-bottom: 16px; }
h3 { font-size: 1.3rem; margin-bottom: 8px; }
p { margin-bottom: 16px; color: var(--color-text-muted); }

/* Header / Nav */
.site-header {
  border-bottom: 1px solid var(--color-border);
  position: sticky;
  top: 0;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(6px);
  z-index: 100;
}

.nav-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 72px;
}

.logo { font-weight: 700; font-size: 1.1rem; color: var(--color-text); }

.site-nav { display: flex; gap: 28px; }

.site-nav a { color: var(--color-text-muted); font-weight: 500; font-size: 0.95rem; }

.site-nav a.active,
.site-nav a:hover { color: var(--color-accent); }

.nav-toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
}

.nav-toggle span {
  width: 22px;
  height: 2px;
  background: var(--color-text);
  transition: transform 0.2s ease, opacity 0.2s ease;
}

/* Hero */
.hero { padding: 96px 0 64px; text-align: center; }

.hero-monogram {
  width: 96px;
  height: 96px;
  border-radius: 50%;
  background: var(--color-accent);
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  font-weight: 700;
  margin: 0 auto 32px;
}

.hero h1 { margin-bottom: 12px; }

.tagline { color: var(--color-accent); font-weight: 600; font-size: 1.1rem; margin-bottom: 20px; }

.hero-sub { max-width: 640px; margin: 0 auto 32px; font-size: 1.05rem; }

.hero-cta { display: flex; gap: 16px; justify-content: center; flex-wrap: wrap; }

/* Buttons */
.btn {
  display: inline-block;
  padding: 12px 28px;
  border-radius: var(--radius);
  font-weight: 600;
  font-size: 0.95rem;
  border: 2px solid transparent;
  cursor: pointer;
}

.btn-primary { background: var(--color-accent); color: #fff; }
.btn-primary:hover { background: var(--color-accent-dark); color: #fff; }

.btn-outline { border-color: var(--color-accent); color: var(--color-accent); }
.btn-outline:hover { background: var(--color-accent); color: #fff; }

/* Stat strip */
.stat-strip {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  padding: 48px 0;
  border-top: 1px solid var(--color-border);
  border-bottom: 1px solid var(--color-border);
}

.stat { text-align: center; }
.stat .stat-number { font-size: 1.8rem; font-weight: 700; color: var(--color-accent); display: block; margin-bottom: 6px; }
.stat p { margin-bottom: 0; font-size: 0.95rem; }

/* Section spacing */
.section { padding: 72px 0; }
.section-surface { background: var(--color-surface); }

/* Cards */
.cards { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 24px; }

.card {
  background: #fff;
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  padding: 28px;
  box-shadow: var(--shadow-sm);
}

/* Timeline (Experience page) */
.timeline { display: flex; flex-direction: column; gap: 40px; }

.timeline-item { border-left: 3px solid var(--color-accent); padding-left: 24px; position: relative; }

.timeline-item::before {
  content: '';
  position: absolute;
  left: -8px;
  top: 4px;
  width: 13px;
  height: 13px;
  border-radius: 50%;
  background: var(--color-accent);
}

.timeline-role { font-size: 1.2rem; font-weight: 700; margin-bottom: 2px; }
.timeline-meta { color: var(--color-text-muted); font-size: 0.9rem; margin-bottom: 12px; }
.timeline-item ul { padding-left: 20px; }
.timeline-item li { margin-bottom: 8px; color: var(--color-text-muted); }

/* Skills */
.skills-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 12px 32px; }

.skills-grid li {
  list-style: none;
  padding: 10px 0;
  border-bottom: 1px solid var(--color-border);
  color: var(--color-text-muted);
}

.tag-list { display: flex; flex-wrap: wrap; gap: 10px; }
.tag {
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: 999px;
  padding: 6px 16px;
  font-size: 0.88rem;
  color: var(--color-text);
}

/* Blog list */
.post-list { display: flex; flex-direction: column; gap: 24px; }
.post-card { border: 1px solid var(--color-border); border-radius: var(--radius); padding: 28px; }
.post-meta { color: var(--color-text-muted); font-size: 0.85rem; margin-bottom: 8px; }

/* Blog post article */
.article { max-width: 720px; margin: 0 auto; }
.article h1 { margin-bottom: 8px; }
.article .post-meta { margin-bottom: 32px; }
.article p { color: var(--color-text); font-size: 1.05rem; }
.back-link { display: inline-block; margin-bottom: 32px; font-weight: 600; }

/* Contact form */
.contact-grid { display: grid; grid-template-columns: 1.2fr 0.8fr; gap: 48px; }

.form-group { margin-bottom: 20px; }
.form-group label { display: block; font-weight: 600; margin-bottom: 6px; font-size: 0.9rem; }

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 12px 14px;
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  font-family: var(--font-sans);
  font-size: 0.95rem;
}

.form-group textarea { min-height: 140px; resize: vertical; }

.contact-side .card { margin-bottom: 16px; }

/* Footer */
.site-footer { border-top: 1px solid var(--color-border); padding: 32px 0; margin-top: 48px; }

.footer-inner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 16px;
  color: var(--color-text-muted);
  font-size: 0.9rem;
}

.footer-links { display: flex; gap: 20px; }

/* Fade-in animation */
.fade-in { opacity: 0; transform: translateY(16px); transition: opacity 0.6s ease, transform 0.6s ease; }
.fade-in.visible { opacity: 1; transform: translateY(0); }

/* Responsive */
@media (max-width: 768px) {
  .nav-toggle { display: flex; }
  .site-nav {
    position: absolute;
    top: 72px;
    left: 0;
    right: 0;
    background: #fff;
    flex-direction: column;
    padding: 16px 24px;
    border-bottom: 1px solid var(--color-border);
    display: none;
  }
  .site-nav.open { display: flex; }
  .contact-grid { grid-template-columns: 1fr; }
  .stat-strip { grid-template-columns: 1fr; gap: 32px; }
  h1 { font-size: 2rem; }
}

@media (max-width: 480px) {
  .hero { padding: 64px 0 40px; }
  .section { padding: 48px 0; }
}
```

- [ ] **Step 2: Verify the file was written correctly**

Run: `grep -c "^\.\|^:root" css/styles.css`
Expected: a non-zero count (confirms the file has selector/rule blocks, not empty or truncated).

Run: `grep -c "color-accent: #0f5c57" css/styles.css`
Expected: `1`

- [ ] **Step 3: Commit**

```bash
git add css/styles.css
git commit -m "Add shared CSS design system for the site"
```

---

### Task 2: Shared JS Behavior

**Files:**
- Create: `js/main.js`

**Interfaces:**
- Consumes: `#navToggle`, `#siteNav`, `.site-nav a`, `.fade-in` (all defined in Task 1's CSS and referenced by every page's HTML in later tasks)
- Produces: mobile nav toggle behavior, active-nav-link highlighting, and scroll fade-in behavior that every page depends on by including this script.

- [ ] **Step 1: Create the script with full content**

```javascript
document.addEventListener('DOMContentLoaded', function () {
  var toggle = document.getElementById('navToggle');
  var nav = document.getElementById('siteNav');

  if (toggle && nav) {
    toggle.addEventListener('click', function () {
      var isOpen = nav.classList.toggle('open');
      toggle.setAttribute('aria-expanded', isOpen ? 'true' : 'false');
    });

    nav.querySelectorAll('a').forEach(function (link) {
      link.addEventListener('click', function () {
        nav.classList.remove('open');
        toggle.setAttribute('aria-expanded', 'false');
      });
    });
  }

  var currentPage = window.location.pathname.split('/').pop() || 'index.html';
  document.querySelectorAll('.site-nav a').forEach(function (link) {
    var linkPage = link.getAttribute('href').split('/').pop();
    if (linkPage === currentPage) {
      link.classList.add('active');
    }
  });

  var fadeEls = document.querySelectorAll('.fade-in');
  if ('IntersectionObserver' in window && fadeEls.length) {
    var observer = new IntersectionObserver(function (entries) {
      entries.forEach(function (entry) {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible');
          observer.unobserve(entry.target);
        }
      });
    }, { threshold: 0.15 });

    fadeEls.forEach(function (el) { observer.observe(el); });
  } else {
    fadeEls.forEach(function (el) { el.classList.add('visible'); });
  }
});
```

- [ ] **Step 2: Verify the file was written correctly**

Run: `grep -c "getElementById" js/main.js`
Expected: `2`

- [ ] **Step 3: Commit**

```bash
git add js/main.js
git commit -m "Add shared nav toggle and scroll-reveal JS behavior"
```

---

### Task 3: Home Page

**Files:**
- Create: `index.html`

**Interfaces:**
- Consumes: `css/styles.css` (Task 1), `js/main.js` (Task 2)
- Produces: `index.html` — the root link target every other page's nav/footer/logo points to.

- [ ] **Step 1: Create the page with full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Jyothi Cherukuri | Project Manager &amp; Scrum Master</title>
  <meta name="description" content="Jyothi Cherukuri is a Project Manager and Certified Scrum Master specializing in banking, pharma, and GenAI delivery.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>
  <header class="site-header">
    <div class="container nav-inner">
      <a href="index.html" class="logo">Jyothi Cherukuri</a>
      <button class="nav-toggle" id="navToggle" aria-label="Toggle navigation" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <nav class="site-nav" id="siteNav">
        <a href="index.html">Home</a>
        <a href="about.html">About</a>
        <a href="experience.html">Experience</a>
        <a href="skills.html">Skills</a>
        <a href="insights/index.html">Insights</a>
        <a href="contact.html">Contact</a>
      </nav>
    </div>
  </header>

  <main>
    <section class="hero container">
      <div class="hero-monogram">JC</div>
      <h1>Jyothi Cherukuri</h1>
      <p class="tagline">Project Manager | Scrum Master | Banking, Pharma &amp; GenAI Delivery Specialist</p>
      <p class="hero-sub">10+ years turning complex, regulated environments into shipped products &mdash; from banking compliance to GenAI platform delivery at Johnson &amp; Johnson.</p>
      <div class="hero-cta">
        <a href="experience.html" class="btn btn-primary">View Experience</a>
        <a href="contact.html" class="btn btn-outline">Get in Touch</a>
      </div>
    </section>

    <section class="container stat-strip">
      <div class="stat">
        <span class="stat-number">10+ Years</span>
        <p>Delivery leadership across banking, pharma &amp; telecom</p>
      </div>
      <div class="stat">
        <span class="stat-number">GenAI Platforms</span>
        <p>Led GenAI platform &amp; governance implementations at J&amp;J</p>
      </div>
      <div class="stat">
        <span class="stat-number">CSM Certified</span>
        <p>Hybrid Agile/Waterfall practitioner &amp; facilitator</p>
      </div>
    </section>

    <section class="section container">
      <h2>Latest Insight</h2>
      <div class="post-card fade-in">
        <p class="post-meta">Insights &middot; June 29, 2026</p>
        <h3><a href="insights/bank-teller-to-genai-pm.html">From Bank Teller to GenAI Platform PM: A Career Built on Adapting</a></h3>
        <p>A look back at a non-linear career path &mdash; and why every stop along the way turned out to matter.</p>
        <a href="insights/index.html" class="btn btn-outline">Read More Insights</a>
      </div>
    </section>
  </main>

  <footer class="site-footer">
    <div class="container footer-inner">
      <p>&copy; 2026 Jyothi Cherukuri. All rights reserved.</p>
      <div class="footer-links">
        <a href="https://www.linkedin.com/in/jyothi-cherukuri-42a14824/" target="_blank" rel="noopener noreferrer">LinkedIn</a>
        <a href="mailto:jcherukuri03@gmail.com">jcherukuri03@gmail.com</a>
      </div>
    </div>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Verify the file was written correctly**

Run: `grep -c "site-nav" index.html`
Expected: `1`

Run: `grep -o '<title>.*</title>' index.html`
Expected: `<title>Jyothi Cherukuri | Project Manager &amp; Scrum Master</title>`

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "Add home page"
```

---

### Task 4: About Page

**Files:**
- Create: `about.html`

**Interfaces:**
- Consumes: `css/styles.css`, `js/main.js`
- Produces: `about.html`, linked from every page's nav.

- [ ] **Step 1: Create the page with full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>About | Jyothi Cherukuri</title>
  <meta name="description" content="From banking operations in Hyderabad to leading GenAI platform delivery at Johnson & Johnson — Jyothi Cherukuri's career story.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>
  <header class="site-header">
    <div class="container nav-inner">
      <a href="index.html" class="logo">Jyothi Cherukuri</a>
      <button class="nav-toggle" id="navToggle" aria-label="Toggle navigation" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <nav class="site-nav" id="siteNav">
        <a href="index.html">Home</a>
        <a href="about.html">About</a>
        <a href="experience.html">Experience</a>
        <a href="skills.html">Skills</a>
        <a href="insights/index.html">Insights</a>
        <a href="contact.html">Contact</a>
      </nav>
    </div>
  </header>

  <main>
    <section class="section container">
      <h1>About Me</h1>
      <p>Jyothi Cherukuri is a Project Manager and Certified Scrum Master with 10+ years of experience across banking, pharmaceutical, and GenAI delivery. She currently leads technology, compliance, and AI-driven initiatives for AIFA Labs on the Johnson &amp; Johnson account, working across GenAI platform implementation, model governance, and enterprise innovation programs.</p>
      <p>Her path here wasn&rsquo;t a straight line. It started on the floor of a bank branch in Hyderabad, India, processing savings accounts, FD/RD services, and ATM reconciliations at Axis Bank. From there, it wound through HR management, a stint as an RF engineer migrating AT&amp;T&rsquo;s LTE network sites, and back into banking as an Executive Personal Banker and Assistant Branch Manager at Bank7 &mdash; each role adding hands-on fluency in a different discipline: operational rigor, people management, technical systems, and regulatory compliance.</p>
      <p>That range is exactly what she draws on today. Leading Agile ceremonies across IT, QA, Compliance, Risk, SMEs, and AI/ML teams means speaking each group&rsquo;s language fluently &mdash; something a decade of varied, hands-on experience makes possible in a way a single-track career rarely does.</p>
    </section>

    <section class="section section-surface container">
      <h2>Certifications &amp; Education</h2>
      <div class="tag-list">
        <span class="tag">Certified Scrum Master (CSM)</span>
        <span class="tag">Certified Automation AI &ndash; Basic Training (Kore.AI)</span>
        <span class="tag">Certified Introduction to Prompt Engineering</span>
        <span class="tag">Bachelor of Computer Applications (BCA)</span>
      </div>
    </section>
  </main>

  <footer class="site-footer">
    <div class="container footer-inner">
      <p>&copy; 2026 Jyothi Cherukuri. All rights reserved.</p>
      <div class="footer-links">
        <a href="https://www.linkedin.com/in/jyothi-cherukuri-42a14824/" target="_blank" rel="noopener noreferrer">LinkedIn</a>
        <a href="mailto:jcherukuri03@gmail.com">jcherukuri03@gmail.com</a>
      </div>
    </div>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Verify the file was written correctly**

Run: `grep -c "tag-list" about.html`
Expected: `1`

- [ ] **Step 3: Commit**

```bash
git add about.html
git commit -m "Add about page"
```

---

### Task 5: Experience Page

**Files:**
- Create: `experience.html`

**Interfaces:**
- Consumes: `css/styles.css` `.timeline`/`.timeline-item` classes, `js/main.js`
- Produces: `experience.html`, linked from nav.

- [ ] **Step 1: Create the page with full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Experience | Jyothi Cherukuri</title>
  <meta name="description" content="Jyothi Cherukuri's professional experience across GenAI delivery, banking, telecom, and HR.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>
  <header class="site-header">
    <div class="container nav-inner">
      <a href="index.html" class="logo">Jyothi Cherukuri</a>
      <button class="nav-toggle" id="navToggle" aria-label="Toggle navigation" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <nav class="site-nav" id="siteNav">
        <a href="index.html">Home</a>
        <a href="about.html">About</a>
        <a href="experience.html">Experience</a>
        <a href="skills.html">Skills</a>
        <a href="insights/index.html">Insights</a>
        <a href="contact.html">Contact</a>
      </nav>
    </div>
  </header>

  <main>
    <section class="section container">
      <h1>Experience</h1>
      <div class="timeline">
        <div class="timeline-item">
          <p class="timeline-role">Project Manager / Scrum Master &mdash; Pharmaceutical &amp; GenAI Projects</p>
          <p class="timeline-meta">AIFA Labs &middot; Client: Johnson &amp; Johnson &middot; Global &middot; Oct 2022 &ndash; Present</p>
          <ul>
            <li>Led delivery of technology, compliance, and AI-driven initiatives across pharma and enterprise innovation teams, ensuring alignment with GxP and validation requirements.</li>
            <li>Delivered a GenAI Platform Implementation, defining use cases, managing model lifecycle workflows, and establishing responsible-AI governance.</li>
            <li>Managed development of a GenAI eLearning Application with adaptive learning paths and automated content generation.</li>
            <li>Led GovernAI implementation, establishing governance workflows, model approval processes, and audit-ready documentation.</li>
            <li>Oversaw GenAI Line Performance Optimization, improving throughput and reducing cycle time.</li>
            <li>Facilitated Agile ceremonies and coordinated with IT, QA, Compliance, Risk, SMEs, and AI/ML teams.</li>
            <li>Managed budgets, timelines, risks, and KPIs with executive-level reporting.</li>
          </ul>
        </div>

        <div class="timeline-item">
          <p class="timeline-role">Assistant Branch Manager (2 Branches)</p>
          <p class="timeline-meta">Bank7 &middot; Irving &amp; Frisco, TX &middot; Sep 2020 &ndash; Mar 2022</p>
          <ul>
            <li>Managed daily branch operations and supervised a team of up to 15 employees.</li>
            <li>Ensured compliance with OFAC, AML, SAR, and regulatory requirements; supported audits.</li>
            <li>Oversaw reconciliations, cash management, and discrepancy resolution.</li>
            <li>Hands-on experience with BSA/AML, KYC, and risk-management processes.</li>
          </ul>
        </div>

        <div class="timeline-item">
          <p class="timeline-role">Executive Personal Banker</p>
          <p class="timeline-meta">Bank7 &middot; Irving &amp; Frisco, TX &middot; Jun 2017 &ndash; Sep 2020</p>
          <ul>
            <li>Assisted customers with account opening/closing and product selection.</li>
            <li>Supported Treasury and BSA teams with fraud review and CTR/SAR preparation.</li>
            <li>Collaborated with mortgage and lending teams on customer requests.</li>
          </ul>
        </div>

        <div class="timeline-item">
          <p class="timeline-role">RF Engineer</p>
          <p class="timeline-meta">Telecom Gateway &middot; Client: AT&amp;T &middot; Frisco, TX &middot; Dec 2016 &ndash; May 2017</p>
          <ul>
            <li>Performed SIAD migrations (Backhaul, LTE, UMTS, RET) from Cisco 2941 to ASR 901/903.</li>
            <li>Integrated LTE macro sites and validated RF node performance.</li>
            <li>Monitored KPIs and collaborated with field engineers to resolve LTE issues.</li>
          </ul>
        </div>

        <div class="timeline-item">
          <p class="timeline-role">HR Manager</p>
          <p class="timeline-meta">Visual IT Services &middot; Coppell, TX &middot; May 2014 &ndash; Sep 2016</p>
          <ul>
            <li>Managed communication, scheduling, and administrative support.</li>
            <li>Processed invoices, payroll, timesheets, and employee updates in QuickBooks.</li>
            <li>Performed full-cycle recruiting: job postings, screening, interviews, and resume preparation.</li>
          </ul>
        </div>

        <div class="timeline-item">
          <p class="timeline-role">Operations Executive</p>
          <p class="timeline-meta">Axis Bank &middot; Hyderabad, India &middot; Jul 2008 &ndash; Jan 2010</p>
          <ul>
            <li>Supported daily branch operations including Savings, Current, FD/RD services, debit card management, and internet banking.</li>
            <li>Processed account openings, NEFT transactions, Demat services, and customer inquiries.</li>
            <li>Managed ATM reconciliation and clearing operations.</li>
          </ul>
        </div>
      </div>
    </section>
  </main>

  <footer class="site-footer">
    <div class="container footer-inner">
      <p>&copy; 2026 Jyothi Cherukuri. All rights reserved.</p>
      <div class="footer-links">
        <a href="https://www.linkedin.com/in/jyothi-cherukuri-42a14824/" target="_blank" rel="noopener noreferrer">LinkedIn</a>
        <a href="mailto:jcherukuri03@gmail.com">jcherukuri03@gmail.com</a>
      </div>
    </div>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Verify the file was written correctly**

Run: `grep -c "timeline-item" experience.html`
Expected: `6` (one opening `<div class="timeline-item">` per role)

Run: `grep -c "timeline-role" experience.html`
Expected: `6`

- [ ] **Step 3: Commit**

```bash
git add experience.html
git commit -m "Add experience timeline page"
```

---

### Task 6: Skills Page

**Files:**
- Create: `skills.html`

**Interfaces:**
- Consumes: `css/styles.css` `.skills-grid`/`.tag-list`/`.tag` classes, `js/main.js`
- Produces: `skills.html`, linked from nav.

- [ ] **Step 1: Create the page with full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Skills | Jyothi Cherukuri</title>
  <meta name="description" content="Core competencies, tools, methodologies, and certifications for Jyothi Cherukuri.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>
  <header class="site-header">
    <div class="container nav-inner">
      <a href="index.html" class="logo">Jyothi Cherukuri</a>
      <button class="nav-toggle" id="navToggle" aria-label="Toggle navigation" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <nav class="site-nav" id="siteNav">
        <a href="index.html">Home</a>
        <a href="about.html">About</a>
        <a href="experience.html">Experience</a>
        <a href="skills.html">Skills</a>
        <a href="insights/index.html">Insights</a>
        <a href="contact.html">Contact</a>
      </nav>
    </div>
  </header>

  <main>
    <section class="section container">
      <h1>Skills</h1>
      <h2>Core Competencies</h2>
      <ul class="skills-grid">
        <li>Project Lifecycle Management</li>
        <li>Agile/Scrum Facilitation</li>
        <li>Sprint Planning &amp; Backlog Refinement</li>
        <li>Regulatory &amp; Compliance Alignment (BSA/AML, KYC, GxP)</li>
        <li>Cross-Functional Team Leadership</li>
        <li>Risk Identification &amp; Mitigation</li>
        <li>KPI Tracking &amp; Executive Reporting</li>
        <li>Vendor &amp; Stakeholder Management</li>
        <li>Process Improvement &amp; Change Management</li>
        <li>Hybrid Agile/Waterfall Delivery</li>
        <li>Resource &amp; Capacity Planning</li>
        <li>Quality Assurance &amp; Documentation Standards</li>
      </ul>
    </section>

    <section class="section section-surface container">
      <h2>Technical Skills</h2>
      <h3>Tools</h3>
      <div class="tag-list">
        <span class="tag">Jira</span>
        <span class="tag">Confluence</span>
        <span class="tag">Access Management</span>
        <span class="tag">MS Project</span>
        <span class="tag">Azure DevOps</span>
        <span class="tag">Trello</span>
        <span class="tag">SharePoint</span>
        <span class="tag">IRIS</span>
      </div>
      <h3 style="margin-top: 24px;">Methodologies</h3>
      <div class="tag-list">
        <span class="tag">Agile</span>
        <span class="tag">Scrum</span>
        <span class="tag">Waterfall</span>
        <span class="tag">Hybrid</span>
      </div>
      <h3 style="margin-top: 24px;">Additional</h3>
      <div class="tag-list">
        <span class="tag">Requirements Gathering</span>
        <span class="tag">Jira Setup &amp; Administration</span>
        <span class="tag">Access Management Setup &amp; Maintenance</span>
        <span class="tag">SIT &amp; UAT Coordination</span>
        <span class="tag">Process Mapping</span>
        <span class="tag">Dashboard Creation</span>
        <span class="tag">Post-Production Support Management</span>
      </div>
    </section>

    <section class="section container">
      <h2>Certifications &amp; Education</h2>
      <div class="tag-list">
        <span class="tag">Certified Scrum Master (CSM)</span>
        <span class="tag">Certified Automation AI &ndash; Basic Training (Kore.AI)</span>
        <span class="tag">Certified Introduction to Prompt Engineering</span>
        <span class="tag">Bachelor of Computer Applications (BCA)</span>
      </div>
    </section>
  </main>

  <footer class="site-footer">
    <div class="container footer-inner">
      <p>&copy; 2026 Jyothi Cherukuri. All rights reserved.</p>
      <div class="footer-links">
        <a href="https://www.linkedin.com/in/jyothi-cherukuri-42a14824/" target="_blank" rel="noopener noreferrer">LinkedIn</a>
        <a href="mailto:jcherukuri03@gmail.com">jcherukuri03@gmail.com</a>
      </div>
    </div>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Verify the file was written correctly**

Run: `grep -c "class=\"tag\"" skills.html`
Expected: `19` (8 tools + 4 methodologies + 7 additional)

- [ ] **Step 3: Commit**

```bash
git add skills.html
git commit -m "Add skills page"
```

---

### Task 7: Insights Listing Page

**Files:**
- Create: `insights/index.html`

**Interfaces:**
- Consumes: `../css/styles.css`, `../js/main.js`, `.post-list`/`.post-card`/`.post-meta` classes from Task 1
- Produces: `insights/index.html`, linked from every page's nav as "Insights", and links onward to the three post pages built in Tasks 8-10.

- [ ] **Step 1: Create the page with full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Insights | Jyothi Cherukuri</title>
  <meta name="description" content="Reflections on Agile delivery, regulatory compliance, and GenAI governance from Jyothi Cherukuri.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="../css/styles.css">
</head>
<body>
  <header class="site-header">
    <div class="container nav-inner">
      <a href="../index.html" class="logo">Jyothi Cherukuri</a>
      <button class="nav-toggle" id="navToggle" aria-label="Toggle navigation" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <nav class="site-nav" id="siteNav">
        <a href="../index.html">Home</a>
        <a href="../about.html">About</a>
        <a href="../experience.html">Experience</a>
        <a href="../skills.html">Skills</a>
        <a href="index.html">Insights</a>
        <a href="../contact.html">Contact</a>
      </nav>
    </div>
  </header>

  <main>
    <section class="section container">
      <h1>Insights</h1>
      <p>Reflections on Agile delivery, regulatory compliance, and GenAI governance, drawn from 10+ years across banking, pharma, and technology.</p>
      <div class="post-list">
        <div class="post-card">
          <p class="post-meta">June 15, 2026 &middot; 5 min read</p>
          <h3><a href="agile-in-regulated-world.html">Agile in a Regulated World: Balancing Scrum with BSA/AML and GxP Compliance</a></h3>
          <p>Agile promises speed. Regulated industries demand control. Here's how to design ceremonies so those aren't opposing forces.</p>
        </div>
        <div class="post-card">
          <p class="post-meta">June 22, 2026 &middot; 5 min read</p>
          <h3><a href="genai-governance-pharma.html">Bringing GenAI Governance to Pharma: Lessons from the Field</a></h3>
          <p>The hardest part of a GenAI initiative in a regulated industry isn't the model &mdash; it's proving who approved it and why.</p>
        </div>
        <div class="post-card">
          <p class="post-meta">June 29, 2026 &middot; 4 min read</p>
          <h3><a href="bank-teller-to-genai-pm.html">From Bank Teller to GenAI Platform PM: A Career Built on Adapting</a></h3>
          <p>A look back at a non-linear career path &mdash; and why every stop along the way turned out to matter.</p>
        </div>
      </div>
    </section>
  </main>

  <footer class="site-footer">
    <div class="container footer-inner">
      <p>&copy; 2026 Jyothi Cherukuri. All rights reserved.</p>
      <div class="footer-links">
        <a href="https://www.linkedin.com/in/jyothi-cherukuri-42a14824/" target="_blank" rel="noopener noreferrer">LinkedIn</a>
        <a href="mailto:jcherukuri03@gmail.com">jcherukuri03@gmail.com</a>
      </div>
    </div>
  </footer>

  <script src="../js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Verify the file was written correctly**

Run: `grep -c "post-card" insights/index.html`
Expected: `3`

- [ ] **Step 3: Commit**

```bash
git add insights/index.html
git commit -m "Add insights listing page"
```

---

### Task 8: Blog Post — Agile in a Regulated World

**Files:**
- Create: `insights/agile-in-regulated-world.html`

**Interfaces:**
- Consumes: `../css/styles.css` `.article`/`.back-link` classes, `../js/main.js`
- Produces: `insights/agile-in-regulated-world.html`, linked from Task 7's listing page.

- [ ] **Step 1: Create the page with full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Agile in a Regulated World | Jyothi Cherukuri</title>
  <meta name="description" content="How to design Agile ceremonies so Scrum and regulatory compliance (BSA/AML, GxP) stop being opposing forces.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="../css/styles.css">
</head>
<body>
  <header class="site-header">
    <div class="container nav-inner">
      <a href="../index.html" class="logo">Jyothi Cherukuri</a>
      <button class="nav-toggle" id="navToggle" aria-label="Toggle navigation" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <nav class="site-nav" id="siteNav">
        <a href="../index.html">Home</a>
        <a href="../about.html">About</a>
        <a href="../experience.html">Experience</a>
        <a href="../skills.html">Skills</a>
        <a href="index.html">Insights</a>
        <a href="../contact.html">Contact</a>
      </nav>
    </div>
  </header>

  <main>
    <section class="section container">
      <article class="article">
        <a href="index.html" class="back-link">&larr; Back to Insights</a>
        <h1>Agile in a Regulated World: Balancing Scrum with BSA/AML and GxP Compliance</h1>
        <p class="post-meta">June 15, 2026 &middot; 5 min read</p>

        <p>Agile promises speed. Regulated industries demand control. On paper, those sound like opposing forces &mdash; and for a long time, I treated them that way, running Scrum ceremonies in one track and compliance checkpoints in another, hoping the two would meet somewhere before go-live.</p>

        <p>They don&rsquo;t meet on their own. You have to design them to.</p>

        <p>In banking, that meant treating BSA/AML, KYC, and SAR requirements not as a final gate before release, but as acceptance criteria baked into the backlog itself. A user story wasn&rsquo;t &ldquo;done&rdquo; when the feature worked &mdash; it was done when the control tied to that feature could be evidenced, tested, and traced back to the requirement that created it. That single shift, moving compliance language into the definition of done, is what let sprints stay sprints instead of turning into two-week feature builds followed by a six-week audit scramble.</p>

        <p>In pharma, the same principle applies to GxP and validation standards, just with a different vocabulary. Model lifecycle workflows, data lineage, and validation evidence all need to exist somewhere durable and reviewable &mdash; and the teams that fight this hardest are usually the ones trying to bolt documentation on after the sprint closes. It&rsquo;s far cheaper, and far less painful, to generate that documentation as a byproduct of the same tools the team already uses to track delivery &mdash; Jira tickets that double as change records, Confluence pages that double as validation artifacts.</p>

        <p>The other lesson, harder to systematize but just as important: bring Compliance, Risk, and QA into the ceremonies themselves, not just the sign-off at the end. When a compliance SME sits in sprint planning and can flag a control gap while the story is still being scoped, that&rsquo;s a five-minute conversation. When the same gap surfaces during UAT, it&rsquo;s a re-opened sprint, a missed release date, and a much less five-minute conversation with stakeholders.</p>

        <p>None of this means slowing Agile down to match the pace of compliance. It means recognizing that in regulated environments, &ldquo;working software&rdquo; was never the whole definition of done &mdash; it just took some environments longer to admit it. Once a team designs its ceremonies, its Jira workflow, and its Definition of Done around that reality, Scrum and regulation stop being opposing forces and start being the same conversation, held once, instead of twice.</p>
      </article>
    </section>
  </main>

  <footer class="site-footer">
    <div class="container footer-inner">
      <p>&copy; 2026 Jyothi Cherukuri. All rights reserved.</p>
      <div class="footer-links">
        <a href="https://www.linkedin.com/in/jyothi-cherukuri-42a14824/" target="_blank" rel="noopener noreferrer">LinkedIn</a>
        <a href="mailto:jcherukuri03@gmail.com">jcherukuri03@gmail.com</a>
      </div>
    </div>
  </footer>

  <script src="../js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Verify the file was written correctly**

Run: `grep -c "class=\"article\"" insights/agile-in-regulated-world.html`
Expected: `1`

- [ ] **Step 3: Commit**

```bash
git add insights/agile-in-regulated-world.html
git commit -m "Add blog post: Agile in a Regulated World"
```

---

### Task 9: Blog Post — GenAI Governance in Pharma

**Files:**
- Create: `insights/genai-governance-pharma.html`

**Interfaces:**
- Consumes: `../css/styles.css` `.article`/`.back-link` classes, `../js/main.js`
- Produces: `insights/genai-governance-pharma.html`, linked from Task 7's listing page.

- [ ] **Step 1: Create the page with full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bringing GenAI Governance to Pharma | Jyothi Cherukuri</title>
  <meta name="description" content="Lessons from leading GenAI governance frameworks and model approval workflows in a regulated pharma environment.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="../css/styles.css">
</head>
<body>
  <header class="site-header">
    <div class="container nav-inner">
      <a href="../index.html" class="logo">Jyothi Cherukuri</a>
      <button class="nav-toggle" id="navToggle" aria-label="Toggle navigation" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <nav class="site-nav" id="siteNav">
        <a href="../index.html">Home</a>
        <a href="../about.html">About</a>
        <a href="../experience.html">Experience</a>
        <a href="../skills.html">Skills</a>
        <a href="index.html">Insights</a>
        <a href="../contact.html">Contact</a>
      </nav>
    </div>
  </header>

  <main>
    <section class="section container">
      <article class="article">
        <a href="index.html" class="back-link">&larr; Back to Insights</a>
        <h1>Bringing GenAI Governance to Pharma: Lessons from the Field</h1>
        <p class="post-meta">June 22, 2026 &middot; 5 min read</p>

        <p>The hardest part of a GenAI initiative in a regulated industry usually isn&rsquo;t the model. It&rsquo;s answering, clearly and durably, three questions: who approved this model for this use case, how do we know it&rsquo;s still behaving the way it was approved to behave, and what happens the moment it doesn&rsquo;t.</p>

        <p>Standing up a GenAI governance framework &mdash; model approval workflows, audit-ready documentation, responsible-AI review gates &mdash; sounds like a compliance exercise, and part of it is. But the more useful way to think about it is as a delivery discipline, because the teams that treat governance as a separate track from delivery are the ones who end up bolting it on after a model is already in production, which is exactly the wrong order.</p>

        <p>The practical version looks like this: every model use case gets scoped with its governance requirements alongside its functional ones, before a single sprint touches it. Model approval isn&rsquo;t a signature collected at the end &mdash; it&rsquo;s a checkpoint built into the same cadence as sprint reviews, so that by the time a model is ready to move toward production, the governance conversation has already happened in pieces, not all at once under deadline pressure.</p>

        <p>Cross-functional coordination matters more here than in almost any other kind of delivery I&rsquo;ve led. A GenAI initiative touches IT, QA, Compliance, Risk, subject-matter experts, and the AI/ML team itself, often simultaneously, and none of them speak quite the same language about what &ldquo;ready&rdquo; means. Part of the Scrum Master&rsquo;s job in this context is translation: turning a Risk team&rsquo;s concern about model drift into a concrete acceptance criterion an engineer can build against, and turning an engineer&rsquo;s technical caveat into language a compliance reviewer can actually sign off on.</p>

        <p>The payoff for getting this right isn&rsquo;t just passing an audit. It&rsquo;s speed, counterintuitively. Teams that build governance into their delivery cadence from day one move faster later, because they&rsquo;re not re-litigating foundational questions &mdash; what counts as evidence, who has approval authority, how changes get tracked &mdash; every time a new use case comes up. They already answered those questions once, and now they&rsquo;re reusing the answer.</p>

        <p>GenAI is still new enough in pharma that most of these frameworks are being built, not inherited. That&rsquo;s a real opportunity: the teams doing it now get to decide whether governance is a brake on innovation or the thing that lets innovation move responsibly. I&rsquo;ve found it can be both fast and careful &mdash; but only if governance is designed in from the start, not bolted on at the end.</p>
      </article>
    </section>
  </main>

  <footer class="site-footer">
    <div class="container footer-inner">
      <p>&copy; 2026 Jyothi Cherukuri. All rights reserved.</p>
      <div class="footer-links">
        <a href="https://www.linkedin.com/in/jyothi-cherukuri-42a14824/" target="_blank" rel="noopener noreferrer">LinkedIn</a>
        <a href="mailto:jcherukuri03@gmail.com">jcherukuri03@gmail.com</a>
      </div>
    </div>
  </footer>

  <script src="../js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Verify the file was written correctly**

Run: `grep -c "class=\"article\"" insights/genai-governance-pharma.html`
Expected: `1`

- [ ] **Step 3: Commit**

```bash
git add insights/genai-governance-pharma.html
git commit -m "Add blog post: Bringing GenAI Governance to Pharma"
```

---

### Task 10: Blog Post — From Bank Teller to GenAI Platform PM

**Files:**
- Create: `insights/bank-teller-to-genai-pm.html`

**Interfaces:**
- Consumes: `../css/styles.css` `.article`/`.back-link` classes, `../js/main.js`
- Produces: `insights/bank-teller-to-genai-pm.html`, linked from Task 7's listing page and from Task 3's home page "Latest Insight" card.

- [ ] **Step 1: Create the page with full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>From Bank Teller to GenAI Platform PM | Jyothi Cherukuri</title>
  <meta name="description" content="A reflection on a non-linear career path from banking operations in Hyderabad to leading GenAI platform delivery.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="../css/styles.css">
</head>
<body>
  <header class="site-header">
    <div class="container nav-inner">
      <a href="../index.html" class="logo">Jyothi Cherukuri</a>
      <button class="nav-toggle" id="navToggle" aria-label="Toggle navigation" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <nav class="site-nav" id="siteNav">
        <a href="../index.html">Home</a>
        <a href="../about.html">About</a>
        <a href="../experience.html">Experience</a>
        <a href="../skills.html">Skills</a>
        <a href="index.html">Insights</a>
        <a href="../contact.html">Contact</a>
      </nav>
    </div>
  </header>

  <main>
    <section class="section container">
      <article class="article">
        <a href="index.html" class="back-link">&larr; Back to Insights</a>
        <h1>From Bank Teller to GenAI Platform PM: A Career Built on Adapting</h1>
        <p class="post-meta">June 29, 2026 &middot; 4 min read</p>

        <p>If you&rsquo;d told me, standing behind a teller window at Axis Bank in Hyderabad processing savings account deposits, that I&rsquo;d eventually be leading GenAI platform governance for a Fortune 500 pharmaceutical program, I don&rsquo;t think I would have believed you. Not because it seemed impossible &mdash; but because at the time, I wasn&rsquo;t thinking about a &ldquo;career path&rdquo; at all. I was thinking about getting the reconciliation right before close of business.</p>

        <p>Looking back, that&rsquo;s probably the throughline: every role I&rsquo;ve held taught me something the next one needed, even when I couldn&rsquo;t see the connection at the time. Banking operations taught me that process rigor isn&rsquo;t bureaucracy for its own sake &mdash; it&rsquo;s what protects customers and the institution when something goes wrong. HR taught me that no initiative succeeds without genuinely understanding the people executing it, not just the plan on paper. A brief detour into RF engineering, migrating LTE network sites for AT&amp;T, taught me to read technical systems I hadn&rsquo;t been trained on and ask the right questions of people who had. Coming back to banking as a personal banker and then an assistant branch manager taught me BSA/AML and KYC compliance from the inside, not from a training slide.</p>

        <p>By the time I became a Scrum Master and then a Project Manager, I wasn&rsquo;t starting from zero &mdash; I was drawing on a decade of oddly specific, oddly relevant experience that most PMs on a straight-line career path simply don&rsquo;t have. When I sit in a room with Compliance, Risk, Engineering, and AI/ML teams all talking past each other, I&rsquo;m not guessing at what each of them needs. I&rsquo;ve sat in most of those chairs.</p>

        <p>I don&rsquo;t think this is a story about a &ldquo;non-traditional path&rdquo; being secretly better than a traditional one. It&rsquo;s simpler than that: the skills compound if you let them. Every role added a lens I still use today &mdash; operational rigor from banking, empathy and process from HR, technical curiosity from telecom, and now, facilitation and governance from Agile delivery and GenAI program leadership.</p>

        <p>If there&rsquo;s a lesson in it for anyone looking at their own resume and seeing a set of jobs that don&rsquo;t obviously connect: they connect more than you think. You just have to keep asking what each one taught you, and stay open to where that answer takes you next. Mine took me from a teller window to a GenAI governance table. I&rsquo;m curious where it goes from here.</p>
      </article>
    </section>
  </main>

  <footer class="site-footer">
    <div class="container footer-inner">
      <p>&copy; 2026 Jyothi Cherukuri. All rights reserved.</p>
      <div class="footer-links">
        <a href="https://www.linkedin.com/in/jyothi-cherukuri-42a14824/" target="_blank" rel="noopener noreferrer">LinkedIn</a>
        <a href="mailto:jcherukuri03@gmail.com">jcherukuri03@gmail.com</a>
      </div>
    </div>
  </footer>

  <script src="../js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Verify the file was written correctly**

Run: `grep -c "class=\"article\"" insights/bank-teller-to-genai-pm.html`
Expected: `1`

- [ ] **Step 3: Commit**

```bash
git add insights/bank-teller-to-genai-pm.html
git commit -m "Add blog post: From Bank Teller to GenAI Platform PM"
```

---

### Task 11: Contact Page with Formspree

**Files:**
- Create: `contact.html`

**Interfaces:**
- Consumes: `css/styles.css` `.contact-grid`/`.form-group`/`.contact-side` classes, `js/main.js`
- Produces: `contact.html`, linked from nav on every page.

- [ ] **Step 1: Create the page with full content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact | Jyothi Cherukuri</title>
  <meta name="description" content="Get in touch with Jyothi Cherukuri for opportunities, collaboration, or a conversation about Agile delivery.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>
  <header class="site-header">
    <div class="container nav-inner">
      <a href="index.html" class="logo">Jyothi Cherukuri</a>
      <button class="nav-toggle" id="navToggle" aria-label="Toggle navigation" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <nav class="site-nav" id="siteNav">
        <a href="index.html">Home</a>
        <a href="about.html">About</a>
        <a href="experience.html">Experience</a>
        <a href="skills.html">Skills</a>
        <a href="insights/index.html">Insights</a>
        <a href="contact.html">Contact</a>
      </nav>
    </div>
  </header>

  <main>
    <section class="section container">
      <h1>Let&rsquo;s Connect</h1>
      <p>Whether you&rsquo;re hiring, collaborating, or just want to talk shop about Agile delivery in regulated industries &mdash; I&rsquo;d love to hear from you.</p>

      <div class="contact-grid">
        <form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
          <div class="form-group">
            <label for="name">Name</label>
            <input type="text" id="name" name="name" required>
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" id="email" name="_replyto" required>
          </div>
          <div class="form-group">
            <label for="message">Message</label>
            <textarea id="message" name="message" required></textarea>
          </div>
          <button type="submit" class="btn btn-primary">Send Message</button>
        </form>

        <div class="contact-side">
          <div class="card">
            <h3>Email</h3>
            <p><a href="mailto:jcherukuri03@gmail.com">jcherukuri03@gmail.com</a></p>
          </div>
          <div class="card">
            <h3>LinkedIn</h3>
            <p><a href="https://www.linkedin.com/in/jyothi-cherukuri-42a14824/" target="_blank" rel="noopener noreferrer">View Profile</a></p>
          </div>
        </div>
      </div>
    </section>
  </main>

  <footer class="site-footer">
    <div class="container footer-inner">
      <p>&copy; 2026 Jyothi Cherukuri. All rights reserved.</p>
      <div class="footer-links">
        <a href="https://www.linkedin.com/in/jyothi-cherukuri-42a14824/" target="_blank" rel="noopener noreferrer">LinkedIn</a>
        <a href="mailto:jcherukuri03@gmail.com">jcherukuri03@gmail.com</a>
      </div>
    </div>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 2: Verify the file was written correctly**

Run: `grep -c "formspree.io" contact.html`
Expected: `1`

- [ ] **Step 3: Commit**

```bash
git add contact.html
git commit -m "Add contact page with Formspree form"
```

- [ ] **Step 4: Sign up for Formspree and wire the real endpoint**

1. Go to `https://formspree.io` and create a free account (email + password, or "Sign up with Google").
2. Click "+ New Form", name it something like "Jyothicherukuri.com Contact", and set the notification email to `jcherukuri03@gmail.com`.
3. Formspree gives you an endpoint URL like `https://formspree.io/f/abcdwxyz`. Copy it.
4. Replace `https://formspree.io/f/YOUR_FORM_ID` in `contact.html`'s `<form action="...">` with your real endpoint.
5. Commit: `git add contact.html && git commit -m "Wire real Formspree endpoint into contact form"`

This step is done by the user (it requires creating an external account Claude has no access to).

---

### Task 12: Cross-Page Visual QA

**Files:** none created — verification only, plus any small fixes discovered.

**Interfaces:**
- Consumes: all files from Tasks 1-11.
- Produces: a verified, review-ready site with no broken links, console errors, or layout breaks at common viewport widths.

- [ ] **Step 1: Check whether the Chrome extension is connected**

Call `mcp__claude-in-chrome__list_connected_browsers`. If a browser is connected, proceed with Step 2. If not, skip to Step 3 (manual fallback) and ask the user to check visually instead.

- [ ] **Step 2: Automated check via claude-in-chrome (if connected)**

For each of the 9 pages (`index.html`, `about.html`, `experience.html`, `skills.html`, `contact.html`, `insights/index.html`, `insights/agile-in-regulated-world.html`, `insights/genai-governance-pharma.html`, `insights/bank-teller-to-genai-pm.html`):

1. Navigate to the local `file://` path of the page (e.g., `file:///C:/Users/jyoth/Claude/Projects/jyothicherukuri/index.html`).
2. Use `resize_window` to check widths 1280px (desktop), 768px (tablet), and 375px (mobile) — confirm the nav collapses to the hamburger toggle below 768px and no content overflows horizontally.
3. Use `read_console_messages` to confirm no JavaScript errors.
4. Click every nav link and every in-page link (e.g., "Read More Insights", each post's "Back to Insights") to confirm it resolves to the correct page, not a 404.
5. On `contact.html`, confirm the form renders correctly (full end-to-end Formspree submission can only be tested after Task 11 Step 4 wires the real endpoint — note this as a follow-up rather than blocking this task).

Expected: no console errors, no broken internal links, no horizontal overflow, nav toggle works on narrow widths.

- [ ] **Step 3: Manual fallback (if Chrome extension not connected)**

Ask the user to open `index.html` directly in their browser (double-click the file, or drag it into a browser window) and click through every nav link and blog post link, then resize the window narrow to confirm the mobile menu appears. Ask them to report back anything that looks broken.

- [ ] **Step 4: Fix any issues found**

If Step 2 or Step 3 surfaces a broken link, typo, or layout issue, fix it directly in the affected file(s) and commit:

```bash
git add <fixed-file>
git commit -m "Fix QA issue: <short description>"
```

- [ ] **Step 5: Final confirmation commit**

Once QA passes cleanly, make a final summary commit if any fixes were made in Step 4 (already committed individually), or simply confirm with the user that the site is ready for the deployment phase (a separate plan covering GitHub Pages + GoDaddy DNS setup).
