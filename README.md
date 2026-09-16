# MALIWAD DEVOPS — Website

**Cloud. DevOps. Automation. Real-World Engineering.**

A single-file, production-ready website for the MALIWAD DEVOPS brand. Everything — HTML, CSS and JavaScript — lives inside `index.html`. No build step, no package manager, no framework.

---

## Run it

Open the file:

```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

Or serve it locally if you want clean URLs and correct caching:

```bash
python3 -m http.server 8080
# then visit http://localhost:8080
```

---

## What's inside

| Section | Anchor | Notes |
|---|---|---|
| Hero | `#home` | Headline, terminal panel, animated node network on canvas |
| Technology strip | — | Ten inline-SVG tech badges |
| About | `#about` | Two columns + "What You'll Learn" glass card |
| The DevOps Stack | `#skills` | Eight skill cards |
| Real-World Projects | `#projects` | MahiOpsAI 2.0, MahiOpsAI, MahiCV-AI |
| Your DevOps Journey | — | Ten-step learning roadmap |
| Latest DevOps Content | `#content` | Six article cards |
| Follow the DevOps Journey | `#social` | Instagram, YouTube, Medium |
| Command of the Day | — | Interactive terminal, three tools |
| Statistics | — | Counters that animate on scroll |
| Free DevOps Resources | `#resources` | Six downloadable resources |
| Call to action | — | Animated grid background |
| Footer | — | Links, social icons, copyright |

---

## Interactive parts

- **Mobile navigation** — hamburger menu below 980px, closes on link tap.
- **Command of the Day** — the Docker / Kubernetes / Terraform buttons swap the command, the output, the window title and the tip line. Arrow keys move between tabs.
- **Animated counters** — fire once when the statistics block enters the viewport.
- **Scroll reveal** — sections fade up via `IntersectionObserver`.
- **Active nav highlighting** — the current section is underlined in the navbar.
- **Node network** — a lightweight `<canvas>` drawing drifting nodes and connecting lines behind the hero. Pauses when the tab is hidden.
- **Back to top** — appears after 700px of scroll.

`prefers-reduced-motion: reduce` is respected throughout: the canvas renders a single static frame, counters jump to their final values, reveals start visible, and smooth scrolling is disabled.

---

## Before you publish

1. **Replace the placeholder links.** Every `href="#"` in the file is a stub. The ones that matter most:
   - Social buttons in `#social` and the footer (Instagram, YouTube, Medium, GitHub, LinkedIn)
   - `View Project →` buttons in `#projects`
   - `Read Article →` links in `#content`
   - `Access Resource →` links in `#resources`
2. **Update the URLs in `<head>`.** Swap `https://maliwaddevops.example.com/` in the canonical tag, the Open Graph tags and the JSON-LD block for your real domain.
3. **Add a social preview image.** Create a 1200×630 PNG and add:
   ```html
   <meta property="og:image" content="https://yourdomain.com/og.png" />
   <meta name="twitter:image" content="https://yourdomain.com/og.png" />
   ```
4. **Fill in `sameAs` in the JSON-LD.** Replace the `"#"` entries with your real profile URLs so search engines link the brand to its accounts.
5. **Update the statistics.** The four numbers are placeholders and are labelled as such on the page. Edit the `data-count` and `data-suffix` attributes in the `#stats` block, and remove the note below it once the figures are yours.
6. **Check the year** in the footer copyright line.

---

## Customising the look

All colours, spacing and typefaces are CSS custom properties declared in `:root` near the top of the file. Changing the accent across the whole site is two lines:

```css
:root{
  --blue:#3b82f6;   /* primary accent, buttons, links */
  --cyan:#22d3ee;   /* secondary accent, highlights, terminal */
  --green:#34d399;  /* success and status indicators */
}
```

Other useful tokens: `--bg`, `--text`, `--muted`, `--line` (border colour), `--maxw` (content width), `--r` (card radius), and the three font variables `--f-display`, `--f-body`, `--f-mono`.

### Adding a skill card

Copy one `<article class="card skill reveal">` block inside `.grid-3` and change the icon, heading and description. The grid reflows automatically.

### Adding a command to the terminal

Add an entry to the `COMMANDS` object in the script, then add a matching button:

```js
ansible: {
  title: "maliwad@devops: ~/labs/ansible",
  note: "Tip: -C runs the playbook in check mode.",
  cmd: "ansible-playbook site.yml",
  out: [
    ['key', 'PLAY [webservers]'],
    ['br',  ''],
    ['ok',  'ok=6  changed=2  failed=0']
  ]
}
```

```html
<button class="tab" role="tab" id="tab-ansible" aria-selected="false"
        aria-controls="cmdPanel" data-key="ansible">Ansible</button>
```

Row types: `key` (dim), `ok` (green), `val` (cyan), `txt` (default), `br` (line break).

---

## Responsive behaviour

- **Desktop (>980px)** — two-column hero and about, multi-column card grids.
- **Tablet (≤980px)** — hamburger nav, hero terminal moves below the text, single-column projects.
- **Mobile (≤560px)** — tighter padding, full-width buttons, single-column grids, smaller terminal type. Verified against a 390px viewport with no horizontal scroll.

---

## SEO and accessibility

Included: title and meta description, Open Graph and Twitter card tags, a canonical placeholder, JSON-LD (`WebSite` + `EducationalOrganization`), semantic landmarks (`header`, `main`, `section`, `footer`, `article`), and a single `H1` with an ordered `H2`/`H3` hierarchy.

Accessibility: visible keyboard focus rings, ARIA on the nav toggle and terminal tabs, `aria-live` on the terminal output, labelled icon-only links, and decorative SVGs marked `aria-hidden`.

---

## Deploying

The site is one static file, so any static host works.

**GitHub Pages**

```bash
git init
git add index.html README.md
git commit -m "MALIWAD DEVOPS website"
git branch -M main
git remote add origin https://github.com/<you>/<repo>.git
git push -u origin main
```

Then enable Pages in repository settings, serving from `main` / root.

**Netlify or Vercel** — drag the folder onto the dashboard, or connect the repo. No build command, publish directory `.`.

**S3 + CloudFront** — upload `index.html`, set it as the index document, enable static site hosting, and put CloudFront in front for HTTPS and caching.

---

## Dependencies

One external request: Google Fonts (Space Grotesk, Inter, JetBrains Mono). Everything else — icons, layout, animation — is inline. If you want the page fully offline, remove the two `<link rel="preconnect">` tags and the stylesheet link; the fallback font stack takes over.

---

© 2026 MALIWAD DEVOPS. Built with ❤️ for Cloud & DevOps Engineers.
