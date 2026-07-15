# oasaka.xyz Product Showcase Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Ship a single-page, light-theme product showcase at `oasaka.xyz` using plain HTML/CSS on GitHub Pages, with no revenue metrics and no frontend framework.

**Architecture:** Static files only. One `index.html` for structure and copy, one `styles.css` for light-theme layout, one avatar under `assets/`, and a `CNAME` for the custom domain. No build step; GitHub Pages serves the repository root.

**Tech Stack:** HTML5, CSS3 (custom properties), GitHub Pages, custom domain `oasaka.xyz`

## Global Constraints

- English-first copy only; tagline exactly: `Goal: Free and Flexible Work`
- Display name exactly: `Yiqiang Chen (Ethan)`
- Path line exactly: `China → Japan → Thailand → Vietnam` (no flag emojis)
- No revenue / MRR numbers anywhere
- No Live / Building badges on product cards
- No footer link to desktop site
- Section title exactly: `What I'm building`
- Vault URL must be `https://vault.oasaka.xyz` (https)
- No Astro/React/Vue; no `package.json` or build pipeline for v1
- Light theme only
- Spec: `docs/superpowers/specs/2026-07-15-product-showcase-design.md`

## File map

| File | Responsibility |
|------|----------------|
| `index.html` | Full page markup: head meta, hero, products, footer |
| `styles.css` | Light theme, layout, cards, responsive, a11y focus/motion |
| `assets/avatar.png` | Profile photo for hero and OG image |
| `CNAME` | GitHub Pages custom domain (`oasaka.xyz`) |
| `README.md` | Repo purpose + local preview + Pages notes |
| `.gitignore` | Ignore OS junk only |

---

### Task 1: Scaffold static assets and repo docs

**Files:**
- Create: `assets/avatar.png`
- Create: `CNAME`
- Create: `README.md`
- Create: `.gitignore`

**Interfaces:**
- Consumes: avatar source at `/Users/ethan/workspace/ethan0xbuilds/public/avatar.png`
- Produces: `assets/avatar.png` (same image), `CNAME` content `oasaka.xyz`, README describing static Pages deploy

- [ ] **Step 1: Create assets directory and copy avatar**

```bash
cd /Users/ethan/workspace/oasaka-xyz
mkdir -p assets
cp /Users/ethan/workspace/ethan0xbuilds/public/avatar.png assets/avatar.png
file assets/avatar.png
```

Expected: PNG image data reported (size may be ~800KB; acceptable for v1).

- [ ] **Step 2: Write `CNAME`**

```bash
printf 'oasaka.xyz\n' > CNAME
```

- [ ] **Step 3: Write `.gitignore`**

```gitignore
.DS_Store
.idea/
.vscode/
*.log
```

- [ ] **Step 4: Write `README.md`**

```markdown
# oasaka.xyz

Personal product showcase for [Yiqiang Chen (Ethan)](https://x.com/ethan0xbuilds).

Static HTML/CSS site — no build step. Spec: `docs/superpowers/specs/2026-07-15-product-showcase-design.md`.

## Local preview

```bash
# from repo root
python3 -m http.server 8080
# open http://127.0.0.1:8080
```

## Deploy

GitHub Pages serves the repository root on branch `main`. Custom domain: `oasaka.xyz` (see `CNAME`).

Product hosts (`jlpt`, `x402`, `vault`, `desktop` subdomains) are separate and unchanged.
```

- [ ] **Step 5: Commit scaffold**

```bash
git add assets/avatar.png CNAME README.md .gitignore
git commit -m "chore: scaffold assets, CNAME, and README for static site"
```

---

### Task 2: Implement `index.html` (structure, copy, meta)

**Files:**
- Create: `index.html`

**Interfaces:**
- Consumes: `assets/avatar.png`, product URLs from spec
- Produces: complete document linked to `styles.css` (file may be empty until Task 3)

- [ ] **Step 1: Create `index.html` with full markup**

Write exactly this file (Task 3 will style it):

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Yiqiang Chen (Ethan)</title>
    <meta
      name="description"
      content="Indie builder · Digital nomad. Goal: Free and Flexible Work."
    />
    <link rel="canonical" href="https://oasaka.xyz/" />
    <meta property="og:type" content="website" />
    <meta property="og:url" content="https://oasaka.xyz/" />
    <meta property="og:title" content="Yiqiang Chen (Ethan)" />
    <meta
      property="og:description"
      content="Indie builder · Digital nomad. Goal: Free and Flexible Work."
    />
    <meta property="og:image" content="https://oasaka.xyz/assets/avatar.png" />
    <meta name="twitter:card" content="summary" />
    <meta name="twitter:site" content="@ethan0xbuilds" />
    <meta name="twitter:title" content="Yiqiang Chen (Ethan)" />
    <meta
      name="twitter:description"
      content="Indie builder · Digital nomad. Goal: Free and Flexible Work."
    />
    <meta name="twitter:image" content="https://oasaka.xyz/assets/avatar.png" />
    <link rel="icon" href="assets/avatar.png" type="image/png" />
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <div class="page">
      <header class="hero">
        <img
          class="avatar"
          src="assets/avatar.png"
          alt="Portrait of Yiqiang Chen (Ethan)"
          width="112"
          height="112"
        />
        <h1 class="name">Yiqiang Chen (Ethan)</h1>
        <p class="handle">
          <a href="https://x.com/ethan0xbuilds" rel="noopener noreferrer"
            >@ethan0xbuilds</a
          >
        </p>
        <p class="role">Indie builder · Digital nomad</p>
        <p class="path">China → Japan → Thailand → Vietnam</p>
        <p class="tagline">Goal: Free and Flexible Work</p>
        <nav class="social" aria-label="Social links">
          <a href="https://x.com/ethan0xbuilds" rel="noopener noreferrer">X</a>
          <a href="https://github.com/ethan0xbuilds" rel="noopener noreferrer"
            >GitHub</a
          >
          <a href="https://t.me/ethan0xbuilds" rel="noopener noreferrer"
            >Telegram</a
          >
          <a href="mailto:ethan0xbuilds@proton.me">Email</a>
        </nav>
      </header>

      <main>
        <section class="projects" aria-labelledby="projects-heading">
          <h2 id="projects-heading">What I'm building</h2>
          <ul class="project-grid">
            <li>
              <a
                class="project-card"
                href="https://jlpt.oasaka.xyz"
                target="_blank"
                rel="noopener noreferrer"
              >
                <span class="project-name">JLPT Materials</span>
                <span class="project-desc"
                  >Free JLPT study materials — read online or download</span
                >
              </a>
            </li>
            <li>
              <a
                class="project-card"
                href="https://x402.oasaka.xyz"
                target="_blank"
                rel="noopener noreferrer"
              >
                <span class="project-name">x402 Pay Demo</span>
                <span class="project-desc">A live demo of x402 payments</span>
              </a>
            </li>
            <li>
              <a
                class="project-card"
                href="https://vault.oasaka.xyz"
                target="_blank"
                rel="noopener noreferrer"
              >
                <span class="project-name">AI Context Vault</span>
                <span class="project-desc"
                  >Give AI the context to actually understand you</span
                >
              </a>
            </li>
            <li>
              <a
                class="project-card"
                href="https://desktop.oasaka.xyz"
                target="_blank"
                rel="noopener noreferrer"
              >
                <span class="project-name">Desktop</span>
                <span class="project-desc"
                  >A Linux-desktop-style personal site</span
                >
              </a>
            </li>
          </ul>
        </section>
      </main>

      <footer class="footer">
        <p>oasaka.xyz</p>
      </footer>
    </div>
  </body>
</html>
```

- [ ] **Step 2: Verify required copy and URLs with grep**

```bash
cd /Users/ethan/workspace/oasaka-xyz
grep -n "Yiqiang Chen (Ethan)" index.html
grep -n "Goal: Free and Flexible Work" index.html
grep -n "China → Japan → Thailand → Vietnam" index.html
grep -n "What I'm building" index.html
grep -n "https://vault.oasaka.xyz" index.html
grep -ni "mrr\|/month\|live badge\|Live</" index.html || true
# footer must not link to desktop
grep -A2 'class="footer"' index.html
```

Expected: name/tagline/path/section present; vault https present; no MRR; footer is only `oasaka.xyz` text.

- [ ] **Step 3: Commit HTML**

```bash
git add index.html
git commit -m "feat: add product showcase page markup and meta tags"
```

---

### Task 3: Implement light-theme `styles.css`

**Files:**
- Create: `styles.css`

**Interfaces:**
- Consumes: class names from `index.html` (`.page`, `.hero`, `.avatar`, `.project-grid`, `.project-card`, etc.)
- Produces: light theme, max-width ~680px, 2-col grid desktop / 1-col mobile, focus styles, reduced-motion

- [ ] **Step 1: Write `styles.css`**

```css
:root {
  --bg: #f7f7f5;
  --surface: #ffffff;
  --text: #1a1a1a;
  --muted: #5c5c5c;
  --border: #e6e6e2;
  --border-hover: #c8c8c2;
  --link: #1a1a1a;
  --link-hover: #000000;
  --focus: #2563eb;
  --radius: 12px;
  --shadow-hover: 0 4px 14px rgba(0, 0, 0, 0.06);
  --max: 680px;
  --space: 1rem;
  font-family: system-ui, -apple-system, "Segoe UI", Roboto, Helvetica, Arial,
    sans-serif;
  color: var(--text);
  background: var(--bg);
  line-height: 1.5;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  margin: 0;
  min-height: 100vh;
  background: var(--bg);
  color: var(--text);
  -webkit-font-smoothing: antialiased;
}

a {
  color: var(--link);
  text-decoration-thickness: 1px;
  text-underline-offset: 0.15em;
}

a:hover {
  color: var(--link-hover);
}

a:focus-visible {
  outline: 2px solid var(--focus);
  outline-offset: 3px;
  border-radius: 4px;
}

.page {
  width: min(var(--max), 100% - 2.5rem);
  margin: 0 auto;
  padding: 3.5rem 0 2.5rem;
}

/* Hero */
.hero {
  text-align: center;
  margin-bottom: 3rem;
}

.avatar {
  width: 112px;
  height: 112px;
  border-radius: 50%;
  object-fit: cover;
  border: 1px solid var(--border);
  display: block;
  margin: 0 auto 1.25rem;
  background: var(--surface);
}

.name {
  margin: 0 0 0.35rem;
  font-size: 1.75rem;
  font-weight: 650;
  letter-spacing: -0.02em;
  line-height: 1.2;
}

.handle {
  margin: 0 0 1rem;
  font-size: 1rem;
  color: var(--muted);
}

.handle a {
  color: var(--muted);
  text-decoration: none;
}

.handle a:hover {
  color: var(--text);
  text-decoration: underline;
}

.role,
.path,
.tagline {
  margin: 0.25rem 0;
  color: var(--muted);
  font-size: 0.98rem;
}

.tagline {
  margin-top: 0.85rem;
  color: var(--text);
  font-weight: 500;
}

.social {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 0.75rem 1.25rem;
  margin-top: 1.5rem;
}

.social a {
  font-size: 0.95rem;
  color: var(--muted);
  text-decoration: none;
}

.social a:hover {
  color: var(--text);
  text-decoration: underline;
}

/* Projects */
.projects h2 {
  margin: 0 0 1.25rem;
  font-size: 1.05rem;
  font-weight: 600;
  letter-spacing: -0.01em;
}

.project-grid {
  list-style: none;
  margin: 0;
  padding: 0;
  display: grid;
  grid-template-columns: 1fr;
  gap: 0.85rem;
}

@media (min-width: 560px) {
  .project-grid {
    grid-template-columns: 1fr 1fr;
  }
}

.project-card {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
  height: 100%;
  padding: 1.1rem 1.15rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  text-decoration: none;
  color: inherit;
  transition: border-color 0.15s ease, box-shadow 0.15s ease,
    transform 0.15s ease;
}

.project-card:hover {
  border-color: var(--border-hover);
  box-shadow: var(--shadow-hover);
  transform: translateY(-1px);
  color: inherit;
}

.project-card:focus-visible {
  outline: 2px solid var(--focus);
  outline-offset: 2px;
}

.project-name {
  font-weight: 600;
  font-size: 1rem;
  letter-spacing: -0.01em;
}

.project-desc {
  font-size: 0.9rem;
  color: var(--muted);
  line-height: 1.45;
}

/* Footer */
.footer {
  margin-top: 3.5rem;
  text-align: center;
  color: var(--muted);
  font-size: 0.85rem;
}

.footer p {
  margin: 0;
}

@media (prefers-reduced-motion: reduce) {
  .project-card {
    transition: none;
  }

  .project-card:hover {
    transform: none;
  }
}
```

- [ ] **Step 2: Local preview check**

```bash
cd /Users/ethan/workspace/oasaka-xyz
python3 -m http.server 8080
```

Open `http://127.0.0.1:8080` in a browser (or use `open http://127.0.0.1:8080` on macOS).

Manual checklist:
- Light background, readable dark text
- Avatar round and centered
- Four product cards; 2 columns when window ≥560px, 1 column when narrow
- Hover elevates card slightly
- No Live badges; no MRR
- Footer only shows `oasaka.xyz` with no link
- Tab through links: focus ring visible

Stop the server with Ctrl+C when done.

- [ ] **Step 3: Commit CSS**

```bash
git add styles.css
git commit -m "feat: add light theme styles for product showcase"
```

---

### Task 4: Enable GitHub Pages and custom domain

**Files:**
- Modify: GitHub repo settings (Pages) — not a local file except existing `CNAME`
- Optional verify: DNS at domain registrar (user may already point `oasaka.xyz`)

**Interfaces:**
- Consumes: public repo `ethan0xbuilds/oasaka-xyz`, `CNAME` = `oasaka.xyz`
- Produces: site reachable at `https://ethan0xbuilds.github.io/oasaka-xyz/` and (after DNS) `https://oasaka.xyz/`

- [ ] **Step 1: Push all commits to `origin/main`**

```bash
cd /Users/ethan/workspace/oasaka-xyz
git status
git push -u origin main
```

Expected: push succeeds.

- [ ] **Step 2: Enable GitHub Pages from root of `main`**

```bash
gh api repos/ethan0xbuilds/oasaka-xyz/pages -X POST \
  -f build_type=legacy \
  -f source[branch]=main \
  -f source[path]=/
```

If the API returns that Pages already exists, update instead:

```bash
gh api repos/ethan0xbuilds/oasaka-xyz/pages -X PUT \
  -f build_type=legacy \
  -f source[branch]=main \
  -f source[path]=/
```

Then set custom domain:

```bash
gh api repos/ethan0xbuilds/oasaka-xyz/pages -X PUT \
  -f cname=oasaka.xyz \
  -F source[branch]=main \
  -F source[path]=/
```

Note: GitHub’s Pages API shape can vary; if `gh api` fails, enable via UI: **Settings → Pages → Deploy from branch `main` / root (/**) → Custom domain `oasaka.xyz` → Enforce HTTPS**.

- [ ] **Step 3: Document DNS records for the user (do not change DNS without confirmation)**

Tell the user to ensure apex (and optionally www) point at GitHub Pages. Typical setup:

| Type | Name | Value |
|------|------|--------|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `ethan0xbuilds.github.io` |

Do **not** change `desktop`, `jlpt`, `x402`, or `vault` subdomain records.

- [ ] **Step 4: Verify Pages deployment**

```bash
# GitHub Pages project URL (works before custom domain)
curl -sI "https://ethan0xbuilds.github.io/oasaka-xyz/" | head -n 15

# After DNS + HTTPS are ready:
curl -sI "https://oasaka.xyz/" | head -n 15
```

Expected eventually: HTTP 200 (or 301/302 to https) and HTML content-type.

- [ ] **Step 5: Final link smoke check on live HTML**

```bash
# Once https://oasaka.xyz is up; else use the github.io URL
curl -sL "https://ethan0xbuilds.github.io/oasaka-xyz/" | grep -oE 'https://[^"]+oasaka\.xyz[^"]*' | sort -u
```

Expected unique product hosts include:
- `https://jlpt.oasaka.xyz`
- `https://x402.oasaka.xyz`
- `https://vault.oasaka.xyz`
- `https://desktop.oasaka.xyz`

- [ ] **Step 6: Commit only if any deploy docs changed**

If README was updated with live URLs or DNS notes during this task:

```bash
git add README.md
git commit -m "docs: note GitHub Pages deploy and custom domain"
git push origin main
```

If nothing changed, skip commit.

---

## Plan self-review

| Spec requirement | Task |
|------------------|------|
| Single-page product wall | Task 2–3 |
| Light theme | Task 3 |
| Hero copy + no flags | Task 2 |
| What I'm building + 4 products, no badges | Task 2 |
| No footer desktop link | Task 2 |
| HTML/CSS only, no framework | Tasks 1–3 |
| GitHub Pages + CNAME | Tasks 1, 4 |
| Meta / OG | Task 2 |
| Success criteria checks | Task 3 manual + Task 4 curl |

No intentional placeholders left; CSS/HTML are complete in-plan for agent execution.
