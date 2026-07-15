# oasaka.xyz Product Showcase — Design Spec

**Date:** 2026-07-15  
**Status:** Draft for user review  
**Scope:** Single-page personal product wall at `oasaka.xyz`

---

## 1. Goals and non-goals

### Goals

- Make `oasaka.xyz` a simple, modern, English-first **product showcase** (indie “business card”).
- Visitor should understand within seconds: who I am, what I care about, and which products exist.
- **No revenue / MRR** numbers or income-focused framing.
- Host on **GitHub Pages** (no personal VPS for this site).
- Zero frontend framework; easy to edit by hand.

### Non-goals

- No Linux-desktop UI (that remains at `desktop.oasaka.xyz`).
- No blog, i18n toggle, CMS, analytics dashboard, or server APIs in v1.
- No Astro/React/Vue or build step in v1.
- No “Live” status badges on product cards.
- No footer link back to the desktop site.

---

## 2. Positioning vs Marc Lou–style pages

| Marc Lou–style | This site |
|----------------|-----------|
| Large monthly revenue | **Omitted** |
| Dense product list with $/mo | Small set of products, one-liners only |
| Often dark / loud | **Light theme**, calm, lots of whitespace |
| Growth experiments in bio | Evergreen copy only |

---

## 3. Information architecture

Single scroll page, top to bottom:

1. **Hero** — identity + tagline + social links  
2. **What I'm building** — product cards  
3. **Footer** — minimal credit only  

No secondary routes in v1.

---

## 4. Hero content (final)

| Field | Value |
|-------|--------|
| Display name | Yiqiang Chen (Ethan) |
| Handle | @ethan0xbuilds → `https://x.com/ethan0xbuilds` |
| Role line | Indie builder · Digital nomad |
| Path | China → Japan → Thailand → Vietnam (**no flag emojis**) |
| Tagline | Goal: Free and Flexible Work |
| Avatar | Same personal avatar as X / existing assets |

### Social links

| Label | Target |
|-------|--------|
| X | https://x.com/ethan0xbuilds |
| GitHub | https://github.com/ethan0xbuilds |
| Telegram | https://t.me/ethan0xbuilds |
| Email | mailto:ethan0xbuilds@proton.me |

---

## 5. Products section

**Section title:** `What I'm building`  
**Badge:** none (no Live / Building labels)

| Display name | One-liner | URL |
|--------------|-----------|-----|
| JLPT Materials | Free JLPT study materials — read online or download | https://jlpt.oasaka.xyz |
| x402 Pay Demo | A live demo of x402 payments | https://x402.oasaka.xyz |
| AI Context Vault | Give AI the context to actually understand you | https://vault.oasaka.xyz |
| Desktop | A Linux-desktop-style personal site | https://desktop.oasaka.xyz |

### Card behavior

- Entire card is a link; open in new tab (`target="_blank"`, `rel="noopener noreferrer"`).
- Hover: subtle border/elevation change only.
- No price, MRR, or status chip.
- Layout: **2 columns** on desktop, **1 column** on mobile.

---

## 6. Visual design

### Theme

- **Light theme** (default and only theme in v1).
- Background: near-white / soft off-white.
- Text: near-black primary; muted gray secondary.
- Cards: white surface, light border, medium radius.
- Accent: restrained (links / focus ring); avoid loud brand gradients.

### Layout

- Centered column, `max-width` ≈ 640–720px.
- Generous vertical spacing; uncluttered.
- System font stack (e.g. `system-ui, -apple-system, Segoe UI, sans-serif`). Optional single webfont later; **not required** for v1.

### Motion and a11y

- Minimal transitions; respect `prefers-reduced-motion`.
- Visible focus styles for keyboard users.
- Sufficient color contrast for body text and links.
- Semantic HTML: one `h1` (name), section heading for products, lists/links as appropriate.

### Footer

- Minimal only, e.g. site name or short credit.
- **Do not** link to `desktop.oasaka.xyz` in the footer (Desktop is already a product card).

---

## 7. Technical approach

### Stack

| Choice | Decision |
|--------|----------|
| Markup | Hand-written HTML |
| Styles | Single `styles.css` (CSS variables for colors/spacing) |
| JS | None required for v1 |
| Framework | **None** (Astro not used; desktop site needed it for interaction, this page does not) |
| Hosting | **GitHub Pages** |
| Build | **None** — publish static files as-is |

### Repository layout

```text
/
  index.html
  styles.css
  assets/
    avatar.*          # profile image
  CNAME               # oasaka.xyz
  README.md
  docs/superpowers/specs/
    2026-07-15-product-showcase-design.md
```

Suggested repo name: `oasaka-xyz` or `oasaka.xyz` (new dedicated repo).

### SEO / social meta

- `<title>` e.g. `Yiqiang Chen (Ethan)`
- Meta description from role + tagline
- Open Graph / Twitter card basics (`og:title`, `og:description`, `og:image` using avatar or simple asset)
- Canonical URL `https://oasaka.xyz/`

---

## 8. Deployment and DNS

| Host | Points to |
|------|-----------|
| `oasaka.xyz` (and optionally `www`) | This GitHub Pages site |
| `desktop.oasaka.xyz` | Existing desktop site (**unchanged**) |
| `jlpt` / `x402` / `vault` subdomains | Existing product hosts (**unchanged**) |

### Pages setup

1. Enable GitHub Pages from repo root (or `/docs` if preferred; **prefer root** for simplicity).
2. Add custom domain `oasaka.xyz` via `CNAME` + DNS at registrar.
3. Enforce HTTPS in Pages settings.

No VPS, no Vercel for v1. (Vercel remains a future option if preview deploys or server features are needed.)

---

## 9. Success criteria

- [ ] On mobile and desktop, identity + products are clear without scrolling past the fold on a typical laptop (products may need a short scroll on small phones — acceptable).
- [ ] All four product URLs work; Vault uses **https://vault.oasaka.xyz**.
- [ ] No revenue figures; no time-bound campaign copy (e.g. “21-day experiment”).
- [ ] Light theme, no Live badges, no footer desktop link, section titled **What I'm building**.
- [ ] Deployed on GitHub Pages with custom domain and HTTPS.

---

## 10. Out of scope / later

- Dark mode toggle  
- Status badges (Live / Building)  
- Blog, newsletter form, analytics  
- i18n (Chinese UI)  
- Migrating product list to JSON + tiny build  
- Framework upgrade if the page grows substantially  

---

## 11. Implementation notes (for planning)

1. Scaffold repo files listed above.  
2. Implement light-theme layout and hero copy exactly as specified.  
3. Implement four product cards with final one-liners.  
4. Add meta tags and `CNAME`.  
5. Configure GitHub Pages + DNS; verify HTTPS and all outbound links.  
6. Quick visual check on mobile width.

No automated test suite required for pure static v1; manual link and responsive checks are enough.
