---
title: "Appendix — MBA Portfolio Website (BUSI 654)"
author: "Rupinder Kaur"
format: gfm
---

> **Purpose of this appendix**  
> This document records the site map, LLM-assisted drafts, my revisions, Quarto/Git commands used to build and publish the website, design decisions, assets and attributions, accessibility checks, and a concise change log. LLM output is **clearly labeled** and my edits are **annotated**.

---

## A. Final Site Map

**Pages (navigation order):**

1. **Home**  → `index.qmd`  
2. **Resume**  → `resume.qmd`  
3. **Projects**  → `projects.qmd`  
4. **Leadership**  → `leadership.qmd`  
5. **Skills**  → `skills.qmd`  
6. **Contact**  → `contact.qmd`  

**Global elements:**  
- **Header:** left-aligned “RK” badge + site title; right-aligned circular navigation (single bar on all pages).  
- **Footer:** `©2025 Rupinder Kaur` (no LLM/Quarto text on public site).  
- **Page layout:** full width with generous whitespace; same rhythm and scale across pages.

---

## B. LLM Brainstorming & Drafts (with my revisions)

**Model used:** GPT-5 Thinking (via ChatGPT).  
**Use allowed in course:** brainstorming, outlining, polishing. Final content reviewed and personalized.

Below are the **key prompts**, the **LLM’s concise response (excerpt)**, and **my edits (✔)**.

### B1. Site Map Prompt
**Prompt** (LLM):  
“Design an MBA portfolio website with at least four pages (Home/About, Resume, Projects/Case Studies, Skills & Certifications; plus Contact). Keep it simple, professional, and accessible. Suggest file names for Quarto.”

**LLM (excerpt):**  
- Pages: Home, Resume/CV, Projects, Skills, **Contact**, optional Leadership.  
- Filenames: `index.qmd`, `resume.qmd`, `projects.qmd`, `skills.qmd`, `contact.qmd`, `leadership.qmd` (optional).  
- Navigation on the right; logo/name on the left.

**My revisions (✔):**  
- Kept all six pages (added **Leadership** as a separate page).  
- Replaced default navbar with **circular navigation** (consistent across the site).  
- Footer simplified to **©2025 Rupinder Kaur**.

---

### B2. Home (Hero + Highlights) Prompt
**Prompt** (LLM):  
“Draft a concise hero for an MBA student working as an opening shift lead at Firehouse Subs (Tsawwassen). Add 3 bullet highlights and a quick-stats panel (location, program, current role). Tone: professional, first person.”

**LLM (excerpt):**  
> “I am an MBA student at UCW (Vancouver) and an opening shift lead at Firehouse Subs, Tsawwassen. I enjoy fast-paced teamwork, hospitality, and process‑driven operations that deliver a great guest experience.”  
> Highlights: checklist-driven opens; customer-first service; reliability.  
> Quick stats: Vancouver, MBA at UCW, Opening Shift Lead.

**My revisions (✔):**  
- Adjusted wording for voice and brevity.  
- Rewrote bullet phrasing for clarity and authenticity.  
- Sized the hero grid so **photo and intro are on the same row** at desktop widths.

---

### B3. Resume Prompt
**Prompt** (LLM):  
“Create a one-page resume section suitable for an MBA student with food service leadership experience; include role bullets (handling prep, sanitation, POS, time management), and a clean email/contact line.”

**LLM (excerpt):**  
- Role: Opening Shift Lead — bullets for prep, sanitation/organization, POS, teamwork/time management.  
- Contact: email link; optional PDF download.

**My revisions (✔):**  
- Converted bullets to **action-first phrasing**.  
- Ensured **no confidential employer data**; kept descriptions generic and verifiable.  
- Added a clear **Download Resume (PDF)** button.

---

### B4. Projects & Leadership Prompts
**Prompt** (LLM):  
“Draft a single case card about process and leadership in quick service; neutral, non‑confidential; include measurable habits (checklists, delegation, labeling, readiness).”

**LLM (excerpt):**  
- Title suggestion referencing Firehouse Subs site.  
- Emphasis on checklists, labeling, readiness, supporting teammates.

**My revisions (✔):**  
- Kept content **non-proprietary**; replaced any brand‑specific internal details with **role‑level skills**.  
- Tuned headings and captions; added **alt text** to the image.

---

### B5. Skills Prompt
**Prompt** (LLM):  
“List skills buckets: interpersonal, operations/tools, reliability/punctuality; keep to short, scannable bullets.”

**LLM (excerpt):**  
- Buckets: Interpersonal, Operations & Tools, Reliability & Punctuality.

**My revisions (✔):**  
- Consolidated into **cards** with succinct descriptions.  
- Verified phrasing matches resume + leadership sections.

---

### B6. Contact Prompt
**Prompt** (LLM):  
“Produce a contact section with a mailto button and a resume download button.”

**LLM (excerpt):**  
- Email link + primary CTA; secondary PDF download button with `target="_blank"` and `download`.

**My revisions (✔):**  
- Implemented as **buttons**; tested the `mailto:` action.  
- Ensured link text has **accessible names** and sufficient contrast.

---

## C. Quarto & Git Commands (A → Z)

> These are the **actual commands** I used (or their corrected forms), plus fixes for issues I encountered.

### C1. Project creation & run
```bash
# inside an empty folder e.g., rupinder-portfolio-quarto
# ensure _quarto.yml declares a website project

# Local preview during editing
quarto preview

# Build static site into _site/
quarto render
```

**Minimal `_quarto.yml` used:**
```yaml
project:
  type: website
  output-dir: _site

website:
  title: "Rupinder Kaur — MBA Portfolio"
  navbar: false   # hide default; custom header is included per-page
format:
  html:
    theme: cosmo
    css: styles.css
```

### C2. GitHub repository setup
```bash
git init
git branch -M main
git remote add origin https://github.com/Rupinder-Kaur-git/Rupinder-Kaur-MBA-portfolio

# Always ignore build and caches
echo "_site/" >> .gitignore
echo ".quarto/" >> .gitignore
echo ".quarto/project-cache/" >> .gitignore

git add .
git commit -m "Initial site"
git push -u origin main
```

### C3. Publish to GitHub Pages (gh-pages)
```bash
# Publish (creates/updates gh-pages branch)
quarto publish gh-pages
```

**If you see:**
```
error: The following untracked working tree files would be overwritten by checkout:
  .quarto/project-cache/deno-kv-file
```
**Fix:** commit or remove the cache, and ensure it’s in `.gitignore`:
```bash
git rm -r --cached .quarto .quarto/project-cache || true
git commit -m "Remove project cache from repo"
echo ".quarto/" >> .gitignore
echo ".quarto/project-cache/" >> .gitignore
git add .gitignore
git commit -m "Ignore Quarto caches"
git push
quarto publish gh-pages
```

**If you see:**  
`ERROR: The specified path … is not a website…`  
**Fix:** ensure `_quarto.yml` exists and has `project: type: website` and re-run `quarto render` before publishing.

**Cleaning builds:** Quarto doesn’t have a `quarto clean` command. If needed, remove the build and cache folders manually:
```bash
rm -rf _site .quarto .quarto/project-cache
quarto render
```

---

## D. Design System (brief)

- **Navigation:** custom **circular buttons** (Home, Resume, Projects, Leadership, Skills, Contact); sticky at top; keyboard-focus ring visible.  
- **Layout:** full-width, large gutters; Home hero uses a **two‑column grid** (avatar + intro).  
- **Cards:** subtle shadows, rounded corners (`24px`), comfortable line‑height.  
- **Type scale:** Heading sizes normalized for readability; no oversize hero text.  
- **Footer:** `©2025 Rupinder Kaur`.  
- **No LinkedIn link** (per requirement).

---

## E. Accessibility & Usability Checks

- **Alt text** added to images (profile photo, project image).  
- **Color contrast** checked against WCAG AA for text on circles and buttons.  
- **Keyboard**: tab order reaches all nav links and CTAs; focus ring visible.  
- **Links**: descriptive text (e.g., “Email Me”, “Download Resume”).  
- **Responsive**: hero stacks on small screens; nav remains usable.

---

## F. Assets & Attributions

- **Profile photo:** provided by student (Rupinder Kaur). File: `assets/images/profile.jpg`. Alt: “Rupinder Kaur portrait”.  
- **Project image (Firehouse Subs storefront):** classroom/portfolio use only. Source referenced during drafting: `https://cdn.sanity.io/...` (publicly available brand image). If publishing beyond coursework, replace with a **royalty‑free** or **self‑taken** image. Alt: “Firehouse Subs storefront.”

---

## G. Authenticity & Accuracy

- All text was **reviewed and edited** by me for accuracy and tone.  
- LLM content served as **drafting aid**, not final authority.  
- No confidential or proprietary information was included.  
- Role descriptions match publicly observable duties in quick service leadership.

---

## H. Change Log (short)

- **v1–v3:** initial scaffolding; default navbar.  
- **v4–v6:** added pages; PDF link; Contact.  
- **v7–v9:** replaced navbar with **circular nav**; added real photo; removed LinkedIn.  
- **v10–v12:** normalized type sizes; improved Contact; added **Highlights** and **Quick Stats** on Home.  
- **v13–v15:** fixed raw-HTML rendering by enabling Markdown inside `<div>` using `markdown="1"`; removed duplicate nav strips.  
- **v16–v17:** unified header on all pages; cleaned buttons and footer; corrected publish and cache issues.

---

## I. Reproducible Build — Step‑by‑Step

1. Clone or download the repo.  
2. Install Quarto: <https://quarto.org>.  
3. Run `quarto render` → check `_site/`.  
4. Run `quarto preview` during edits.  
5. Commit changes and push `main`.  
6. Run `quarto publish gh-pages` to update the live site.  

---

## J. References

- Quarto Documentation — <https://quarto.org>  
- OpenAI — Model assistance used for brainstorming/drafts (this appendix transparently documents its role).  
- APA Style guidance — for general citation practice.
