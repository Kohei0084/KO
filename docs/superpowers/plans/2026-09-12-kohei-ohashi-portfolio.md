# Kohei Ohashi Portfolio Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a bilingual, understated, searchable personal and research portfolio on GitHub Pages in `Kohei0084/KO`.

**Architecture:** A dependency-free static multi-page site shares one stylesheet and one progressive-enhancement script. Japanese and English copy is present in every document, while JavaScript persists the selected language and controls mobile navigation. Node built-in tests validate structure, metadata, links, and privacy constraints.

**Tech Stack:** Semantic HTML5, CSS3, vanilla JavaScript, JSON-LD, Node.js built-in test runner, GitHub Pages

**Spec:** `docs/superpowers/specs/2026-09-12-kohei-ohashi-portfolio-design.md`

## Global Constraints

- Base URL: `https://kohei0084.github.io/KO/`
- No runtime dependencies or build step
- Complete Japanese and English copy
- Calm, precise, evidence-led tone without boastful claims
- No profile photograph or public email address in the initial release
- No unverified rankings, novelty claims, metrics, or Scholar profile URL
- Published and ongoing work must be visibly distinguished
- Essential content and links remain usable without JavaScript
- No raw data, animal identifiers, unpublished results, credentials, secrets, or local paths
- Responsive, keyboard accessible, sufficient contrast, and reduced-motion aware

## File map

- `index.html`: general introduction and four main routes
- `research.html`: questions, methods, published findings, ongoing work
- `publications.html`: verified papers and presentation categories
- `projects.html`: pose estimation, napari tools, analysis workflow
- `career.html`: education, capabilities, recruiter-oriented context
- `activities.html`: SEA.ing and marine conservation
- `assets/css/styles.css`: design tokens, layout, components, accessibility
- `assets/js/main.js`: language persistence and mobile navigation
- `tests/site.test.mjs`: structure, metadata, link, and privacy tests
- `robots.txt`, `sitemap.xml`, `404.html`: discovery and recovery
- `README.md`: site and maintenance guide

---

### Task 1: Create the tested Home shell and design system

**Files:**
- Create: `tests/site.test.mjs`
- Create: `index.html`
- Create: `assets/css/styles.css`

**Interfaces:**
- Consumes: routes and editorial rules from the approved spec
- Produces: `.site-header`, `.language-switch`, `[data-lang]`, `.card-grid`, `.site-footer`, and canonical navigation used by every page

- [ ] **Step 1: Write failing contract tests**

Create a Node `node:test` suite that uses `readFile` and `access` from `node:fs/promises`. Define the page list as `index.html`, `research.html`, `publications.html`, `projects.html`, `career.html`, `activities.html`, and `404.html`. Assert that Home contains `Kohei Ohashi`, `大橋 康平`, both `data-lang="ja"` and `data-lang="en"`, links to the four main routes, Researchmap, and GitHub. For each primary page assert a nonempty title, description, canonical URL under `/KO/`, skip link, and `main#main-content`. For every page reject `mailto:`, `@seaing.jp`, `@gmail.com`, and Google Scholar citation-profile URLs.

- [ ] **Step 2: Run the test and observe failure**

Run: `node --test tests/site.test.mjs`

Expected: FAIL because the planned pages are absent.

- [ ] **Step 3: Implement `index.html`**

Use semantic HTML with a skip link, shared header/navigation, Japanese/English language controls, and a hero containing:

```text
魚の集団行動を研究しながら、画像解析ツールの開発と海洋保全活動に取り組んでいます。
I study collective fish behavior while developing image-analysis tools and working on marine conservation.
```

Add four restrained cards for Research, Projects, Career, and Activities; a short About section; Researchmap and GitHub links; and a minimal footer. Add canonical/Open Graph metadata and verified `Person` JSON-LD with name, alternate name, site URL, GitHub, and Researchmap only.

- [ ] **Step 4: Implement `assets/css/styles.css`**

Start with these tokens:

```css
:root {
  --ink: #152638;
  --muted: #5b6b78;
  --paper: #f8fbfb;
  --surface: #ffffff;
  --navy: #123047;
  --sea: #147d7e;
  --line: #dbe5e7;
  --focus: #f1a43c;
  --max: 72rem;
  --radius: 1rem;
}
```

Add a centered max-width layout, readable typography, visible focus outlines, responsive card grid, 48rem mobile breakpoint, language visibility selectors, and a `prefers-reduced-motion` rule. Do not use animated statistics or decorative effects that compete with the content.

- [ ] **Step 5: Run focused tests and commit**

Run: `node --test --test-name-pattern="home" tests/site.test.mjs`

Expected: Home assertions PASS.

```bash
git add index.html assets/css/styles.css tests/site.test.mjs
git commit -m "feat: add bilingual portfolio home shell"
```

### Task 2: Add research-facing content

**Files:**
- Create: `research.html`
- Create: `publications.html`
- Create: `projects.html`
- Modify: `tests/site.test.mjs`

**Interfaces:**
- Consumes: shared navigation and CSS from Task 1
- Produces: stable research, publication, and project routes

- [ ] **Step 1: Add failing content tests**

Assert that Research contains `Plecoglossus altivelis`, `査読済み研究`, `Published work`, `進行中の研究`, and `Ongoing research`. Assert that Publications contains both DOI strings `10.1007/s10015-025-01080-8` and `10.1007/s10015-026-01132-7`, plus Japanese and English peer-reviewed headings. Assert that Projects links to `Kohei0084/napari-pose` and `Kohei0084/yolov11`.

- [ ] **Step 2: Run and observe failure**

Run: `node --test --test-name-pattern="research|publications|projects" tests/site.test.mjs`

Expected: FAIL because the pages are absent.

- [ ] **Step 3: Create `research.html`**

Explain the question of how environmental information shapes fish coordination; juvenile ayu as the study animal; wavelength-dependent cohesion/alignment and dynamic visual stimuli as published work; and tail-beat synchronization as ongoing work without unpublished numerical conclusions. Describe controlled shallow-water arenas, imaging, pose estimation, and trajectory/kinematic analysis. Link Publications and Researchmap.

- [ ] **Step 4: Create `publications.html`**

Link the two confirmed DOI URLs. Separate peer-reviewed publications, conference presentations, and ongoing manuscripts. Do not invent titles, author order, volume, issue, or pages if not independently verified. State neutrally that full records are maintained on Researchmap. Render Scholar as “profile link pending verification,” not a guessed URL.

- [ ] **Step 5: Create `projects.html`**

Describe six-keypoint YOLOv11 pose estimation, the napari review/correction interface, and the evolving reproducible analysis workflow. Link the two existing repositories and describe access status neutrally.

- [ ] **Step 6: Run tests and commit**

Run: `node --test tests/site.test.mjs`

Expected: All research-facing assertions PASS; later-page existence assertions may still fail.

```bash
git add research.html publications.html projects.html tests/site.test.mjs
git commit -m "feat: add research publications and projects"
```

### Task 3: Add Career and Activities

**Files:**
- Create: `career.html`
- Create: `activities.html`
- Modify: `tests/site.test.mjs`

**Interfaces:**
- Consumes: shared shell and research-facing routes
- Produces: recruiter and marine-activity destinations

- [ ] **Step 1: Add failing audience tests**

Assert that Career contains `University of Tsukuba`, `筑波大学`, `Computer vision`, `画像解析`, and Researchmap. Assert that Activities contains `SEA.ing`, `marine conservation`, `海洋保全`, `beach clean`, and `ビーチクリーン`.

- [ ] **Step 2: Run and observe failure**

Run: `node --test --test-name-pattern="career|activities" tests/site.test.mjs`

Expected: FAIL because both pages are absent.

- [ ] **Step 3: Create `career.html`**

List University of Tsukuba bachelor’s (2020–2024), master’s (2024–2026), and doctoral program (2026–present). Group capabilities into collective behavior/behavioral ecology; Python/computer vision/pose and time-series analysis; experimental systems/scientific visualization; and collaborative project development. Explain related student projects as growth of the research program. Include Research, Projects, Publications, GitHub, and Researchmap routes. Exclude rankings and salary claims.

- [ ] **Step 4: Create `activities.html`**

Describe founding SEA.ing during undergraduate study, serving as representative director, beach-clean work in Ibaraki, cooperation with local institutions, and educational outreach. Connect ocean observation, research, diving, and practical conservation without solicitation or unverified awards.

- [ ] **Step 5: Run tests and commit**

Run: `node --test tests/site.test.mjs`

Expected: Career and Activities assertions PASS.

```bash
git add career.html activities.html tests/site.test.mjs
git commit -m "feat: add career and marine activity pages"
```

### Task 4: Add progressive language and navigation controls

**Files:**
- Create: `assets/js/main.js`
- Modify: all six primary HTML pages
- Modify: `assets/css/styles.css`
- Modify: `tests/site.test.mjs`

**Interfaces:**
- Consumes: `[data-lang]`, `[data-language-button]`, `[data-menu-button]`, `[data-site-menu]`
- Produces: `html[data-language]`, current document `lang`, `aria-pressed`, and mobile-menu `aria-expanded`

- [ ] **Step 1: Add failing script tests**

Assert every primary page loads `assets/js/main.js` with `defer`, includes Japanese and English language buttons, and contains accessible menu state attributes. Assert the script refers to `portfolio-language`, updates `document.documentElement.lang`, and updates `aria-pressed`.

- [ ] **Step 2: Run and observe failure**

Run: `node --test --test-name-pattern="script|language" tests/site.test.mjs`

Expected: FAIL because the script is absent.

- [ ] **Step 3: Implement `assets/js/main.js`**

Implement `setLanguage(language)` that normalizes to `ja` or `en`, sets `root.dataset.language`, sets `root.lang`, safely stores `portfolio-language`, and updates each button’s `aria-pressed`. Initialize from safe local storage or `navigator.language`. Toggle the mobile menu’s `hidden` and the button’s `aria-expanded`. Wrap storage access in `try/catch` so privacy settings cannot break navigation.

- [ ] **Step 4: Wire all pages**

Add two language buttons and one mobile-menu button to each shared header, load the deferred script, and add a tiny guarded head script to apply a saved language before first paint. Ensure all essential content remains in the HTML source.

- [ ] **Step 5: Run tests and commit**

Run: `node --test tests/site.test.mjs`

Expected: Script and language assertions PASS.

```bash
git add assets/js/main.js assets/css/styles.css *.html tests/site.test.mjs
git commit -m "feat: add accessible language and navigation controls"
```

### Task 5: Complete discovery, recovery, and maintenance docs

**Files:**
- Create: `robots.txt`
- Create: `sitemap.xml`
- Create: `404.html`
- Modify: `README.md`
- Modify: `tests/site.test.mjs`

**Interfaces:**
- Consumes: final canonical routes
- Produces: crawler inventory, broken-route recovery, and maintainer instructions

- [ ] **Step 1: Add failing discovery tests**

Assert `robots.txt` includes `User-agent: *`, `Allow: /`, and the canonical sitemap URL. Assert the sitemap contains Home and all five subpage canonical URLs. Assert README includes the live URL, `python -m http.server 8000`, and `node --test tests/site.test.mjs`.

- [ ] **Step 2: Run and observe failure**

Run: `node --test --test-name-pattern="crawler|README" tests/site.test.mjs`

Expected: FAIL because discovery files and documentation are absent.

- [ ] **Step 3: Create crawler and recovery files**

Use this crawler policy:

```text
User-agent: *
Allow: /

Sitemap: https://kohei0084.github.io/KO/sitemap.xml
```

Create standards-compliant XML containing the six canonical URLs. Create a bilingual 404 page with one clear route to `/KO/`.

- [ ] **Step 4: Replace README**

Document the site purpose, live URL, page map, zero-build local preview, Node test command, bilingual editing convention, default-branch deployment, and primary-source factual-correction policy.

- [ ] **Step 5: Run tests and commit**

Run: `node --test tests/site.test.mjs`

Expected: PASS with zero failed tests.

```bash
git add robots.txt sitemap.xml 404.html README.md tests/site.test.mjs
git commit -m "docs: add discovery files and maintenance guide"
```

### Task 6: Verify and publish

**Files:**
- Modify only files that fail verification

**Interfaces:**
- Consumes: complete site
- Produces: verified GitHub Pages release

- [ ] **Step 1: Scan for accidental disclosure**

Run:

```bash
rg -n -i 'mailto:|@seaing\.jp|@gmail\.com|password|secret|api[_-]?key|C:\\|/Users/|/home/' --glob '*.html' --glob '*.js' --glob '*.md'
```

Expected: no private contact, credential, or local-path exposure in public site files. Inspect documentation-only matches manually.

- [ ] **Step 2: Run complete automated verification**

Run: `node --test tests/site.test.mjs`

Expected: PASS.

- [ ] **Step 3: Preview responsively**

Run: `python -m http.server 8000` and inspect `http://localhost:8000/` at 375px and 1440px widths. Verify all routes, both complete languages, persistent language choice, visible keyboard focus, mobile navigation, and reduced-motion behavior.

- [ ] **Step 4: Verify authoritative links**

Open GitHub, Researchmap, repository, and DOI links. Scholar remains unlinked until its exact profile is verified.

- [ ] **Step 5: Commit corrections if verification changed files**

```bash
git add .
git commit -m "fix: address portfolio release verification"
```

Do not create this commit if no correction was required.

- [ ] **Step 6: Enable GitHub Pages**

In repository Settings → Pages, choose **Deploy from a branch**, select `main` and `/ (root)`, and save. Use an authorized API equivalent if one is available.

Expected route: `https://kohei0084.github.io/KO/`.

- [ ] **Step 7: Verify deployment**

Open Home, one subpage, `sitemap.xml`, and a deliberately missing URL. Confirm all assets resolve beneath `/KO/` and the 404 page returns visitors to Home.
