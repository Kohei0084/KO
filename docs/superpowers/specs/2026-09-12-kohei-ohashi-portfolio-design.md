# Kohei Ohashi Portfolio — Design Specification

Date: 2026-09-12  
Status: Approved for implementation planning  
Repository: `Kohei0084/KO`

## 1. Purpose

Create a bilingual GitHub Pages site that serves as the primary public introduction to Kohei Ohashi (大橋康平). The site should present the whole person first, then guide researchers and employers to deeper, audience-specific information.

The site must communicate credibility through clear descriptions, verifiable records, and links to primary sources. It must not use boastful language or unsupported claims.

## 2. Primary audiences

1. People searching for “大橋康平” or “Kohei Ohashi”
2. Researchers and prospective collaborators
3. Corporate recruiters and technical hiring managers
4. People interested in marine conservation, SEA.ing, or diving activities

## 3. Information architecture

- **Home** — concise, general introduction
- **Research** — collective fish behavior, tail-beat synchronization, light environment, experimental systems, and analysis workflow
- **Publications** — peer-reviewed papers and presentations with DOI or official links
- **Projects** — YOLOv11 pose estimation, napari-based review tools, and related repositories
- **Career** — education, technical capabilities, project leadership, and recruiter-oriented context
- **Activities** — SEA.ing and marine-conservation activities

The Home page provides four principal entry points: Research, Engineering/Projects, Marine Activities, and Career.

## 4. Editorial direction

### Tone

- Calm, precise, and approachable
- Evidence-led rather than promotional
- Explain significance without inflated superlatives
- Use first-person language sparingly
- Distinguish published results, ongoing research, and future plans

### Opening message

Japanese:

> 魚の集団行動を研究しながら、画像解析ツールの開発と海洋保全活動に取り組んでいます。

English:

> I study collective fish behavior while developing image-analysis tools and working on marine conservation.

This wording may be refined during implementation without changing its meaning or tone.

## 5. Content rules

- Display Japanese and English through a language switcher.
- Both languages remain available in the document structure for accessibility and indexing.
- Every publication should link to a DOI or authoritative publication page when available.
- Include routes to Google Scholar, Researchmap, and GitHub.
- Do not guess a Google Scholar profile URL. Use a verified profile URL or omit it until verified.
- Do not publish an email address in the initial version.
- Do not include unverified metrics, rankings, or claims of novelty.
- Describe the six related student projects as the development of a broader research program, not as a claim of personal superiority.
- Separate peer-reviewed publications from conference presentations and ongoing work.
- Do not expose raw research data, animal identifiers, unpublished results, credentials, secrets, or local file paths.

## 6. Visual design

- Palette: white, deep navy, and restrained blue-green accents
- Character: youthful, maritime, technically credible, and understated
- Generous whitespace and readable typography
- No oversized achievement counters, animated statistics, or self-congratulatory labels
- Responsive layout for desktop and mobile
- No profile photograph in the initial release
- Respect `prefers-reduced-motion`

## 7. Technical architecture

Use dependency-free static files suitable for GitHub Pages:

- `index.html`
- `research.html`
- `publications.html`
- `projects.html`
- `career.html`
- `activities.html`
- `assets/css/styles.css`
- `assets/js/main.js`
- `robots.txt`
- `sitemap.xml`
- `404.html`
- updated `README.md`

JavaScript should only enhance language switching and navigation. All essential content and links must remain usable without JavaScript.

The canonical base URL is initially `https://kohei0084.github.io/KO/`.

## 8. Search and sharing

Each page must include:

- A unique bilingual-aware title and description
- Canonical URL
- Open Graph metadata
- Meaningful heading hierarchy
- Descriptive link text
- JSON-LD structured data where relevant

The Home page will use `Person` structured data with only verified fields. The sitemap will include all public pages. `robots.txt` will allow normal indexing and reference the sitemap.

SEO will support discoverability but cannot guarantee a search-engine ranking or indexing date.

## 9. Accessibility

- Semantic HTML landmarks
- Keyboard-accessible navigation and language control
- Visible focus states
- Sufficient color contrast
- Language attributes for Japanese and English content
- No information conveyed by color alone
- Responsive menu with accessible state labels

## 10. External links

Initial external link set:

- GitHub: `https://github.com/Kohei0084`
- Researchmap: `https://researchmap.jp/kohei_ohashi`
- Google Scholar: verified profile URL only
- DOI links for confirmed publications

External links must be clearly identified and must not depend on tracking parameters.

## 11. Deployment

The site will live in the existing public `Kohei0084/KO` repository. GitHub Pages should publish from the default branch after the site files are implemented. If repository administration is unavailable through the connected integration, the owner must enable Pages once in repository settings.

A future profile README repository (`Kohei0084/Kohei0084`) may link to this site, but creating it is outside the initial implementation scope.

## 12. Validation

Before completion:

- Confirm every navigation route and external link
- Confirm both languages across all pages
- Check responsive layouts at common mobile and desktop widths
- Run an HTML validation/lint pass where tooling permits
- Check for missing metadata, images, and inaccessible controls
- Verify no private or unconfirmed information is exposed
- Confirm that GitHub Pages resolves relative asset paths correctly

## 13. Success criteria

The initial release is successful when:

1. A visitor can understand who Kohei Ohashi is within one screen.
2. Researchers can reach research details, publications, Researchmap, and Scholar within two interactions.
3. Recruiters can find education, technical capabilities, and projects without reading the entire site.
4. Japanese and English content are both complete and usable.
5. The site is fast, mobile-friendly, accessible, and maintainable without a build system.
6. All factual claims are verified or clearly labeled as ongoing work.
