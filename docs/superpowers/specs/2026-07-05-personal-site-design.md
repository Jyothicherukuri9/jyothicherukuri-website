# Jyothicherukuri.com — Personal Brand Website Design

## Purpose

A personal brand + thought-leadership website for Jyothi Cherukuri, a Project
Manager / Scrum Master with 10+ years across banking, pharma, and GenAI
delivery. The site serves two audiences equally: recruiters/hiring managers
evaluating her for roles, and industry peers (PMs, Scrum Masters, GenAI/
delivery professionals) building her professional reputation.

## Content Sources

- **Primary:** resume (`Midlevel PM Scrum Master Resume.docx`), already
  extracted — covers AIFA Labs/Johnson & Johnson (GenAI delivery, current),
  Bank7 (Assistant Branch Manager, Executive Personal Banker), Telecom
  Gateway/AT&T (RF Engineer), Visual IT Services (HR Manager), Axis Bank
  (Operations Executive), plus certifications (CSM, Kore.AI Automation AI,
  Prompt Engineering).
- **Secondary:** LinkedIn official data export. The user requests this
  themselves via LinkedIn Settings & Privacy → Data Privacy → "Get a copy of
  your data" (read-only, official channel — no scraping, no automation, no
  unofficial LinkedIn MCP/API is used anywhere in this project). The user
  shares the relevant exported text/files for content drafting.
- All copy is drafted by Claude and reviewed/edited by the user before
  publishing — nothing goes live unreviewed.

## Site Structure (launching complete, all sections at once)

1. **Home** — hero with name, tagline ("Project Manager | Scrum Master |
   Banking, Pharma & GenAI Delivery Specialist"), short intro, nav links to
   other sections.
2. **About** — professional summary plus career narrative. Notably her path
   (banking operations in India → RF engineer → HR manager → Assistant
   Branch Manager → PM/Scrum Master leading GenAI platform delivery at J&J)
   is an adaptability story worth telling directly, not just summarized as a
   list of titles.
3. **Experience** — reverse-chronological timeline covering all roles from
   the resume.
4. **Skills** — Core Competencies, Technical Skills/Tools, Methodologies
   (Agile/Scrum/Hybrid/Waterfall), Certifications.
5. **Insights/Blog** — launches with 2-3 starter posts drafted from her
   experience:
   - "Agile in a Regulated World: Balancing Scrum with BSA/AML and GxP
     Compliance"
   - "Bringing GenAI Governance to Pharma: Lessons from the Field"
   - "From Bank Teller to GenAI Platform PM: A Career Built on Adapting"
6. **Contact** — Formspree-powered contact form (name/email/message →
   emailed to user), plus LinkedIn URL and email listed as text.

## Visual Style

Modern minimalist: generous whitespace, sans-serif type, single accent color
(deep teal, against a charcoal/white base — professional enough for banking
credibility, modern enough for the GenAI angle), subtle hover/scroll motion.
No dark mode in v1. Fully responsive for mobile/tablet/desktop. The exact
shade is finalized visually during implementation, not re-litigated here.

## Technical Approach

- **Stack:** static HTML/CSS/vanilla JS. No framework, no build step —
  matches the local machine's lack of Node/Python, and is the simplest thing
  to deploy for free.
- **Contact form:** Formspree free tier (up to 50 submissions/month) handles
  form submission without any backend code.
- **Repo:** a git repository is initialized in this project directory (none
  existed previously) since GitHub Pages hosting requires one.

## Hosting & Domain

- Deploy via GitHub Pages (free), from a GitHub repository.
- Point `Jyothicherukuri.com` (currently registered at GoDaddy) at GitHub
  Pages using DNS records configured in the GoDaddy dashboard (A records for
  the apex domain + CNAME for `www`, exact values provided during
  implementation).
- HTTPS via GitHub Pages' automatic free certificate.

## Testing / QA Approach

- Manual visual check across desktop/tablet/mobile viewport widths.
- Navigation and internal link verification across all pages.
- Formspree submission test (end-to-end) before going live.
- DNS propagation and HTTPS certificate check after domain connection.

## Out of Scope (this phase)

- No automated LinkedIn scraping/API integration of any kind (explicitly
  rejected due to ToS risk).
- No CMS or dynamic backend — blog posts are static HTML pages added
  manually/by Claude on request.
- No analytics/SEO tooling beyond basic meta tags (can be a future
  enhancement).
