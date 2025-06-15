# cloudflare-poshyfoods-ai-website
````markdown
# Poshy Foods AI-GEO Website  
_Built with ChatGPT Codex & Cursor AI — Astro + Cloudflare Pages + Workers_

---

## 🏆 Project Overview  
This repo (`cloudflare-poshyfoods-ai-website`) contains source code and content for a **stunning, high-grade**, **AI-GEO & SEO-ready** storefront and content hub for **Poshy Foods**. It replaces an existing Shopify store (eliminating monthly fees) and delivers:

- **Static-First HTML** (zero-JS fallback) for maximum LLM & SEO crawlability  
- **Rich JSON-LD schemas** (`Product`, `Offer`, `Recipe`, `FAQPage`, `LocalBusiness`, `WebSite`)  
- **Geo-aware “Buy” CTAs** via Cloudflare Worker (`/api/buyurl?sku=…`)  
- **Bilingual** support (en-CA / fr-CA) with correct `<link rel="alternate" hreflang="…">`  
- **AI-agent enabled** development (ChatGPT Codex & Cursor AI + GitHub)  
- **Fill-in Markdown forms** for non-dev product & recipe additions  
- **Premium DTC theme** baseline (e.g. Minimog) for a designer-grade user experience  

---

## 🛠️ Tech Stack  
| Layer             | Technology               | Purpose                                                  |
|-------------------|--------------------------|----------------------------------------------------------|
| Framework         | Astro (v5+)              | Static SSG, MDX, components                              |
| Styling           | Tailwind CSS             | Utility-first design, custom theme tokens                |
| Content           | MDX Collections          | Products, Recipes, Pages via frontmatter + Markdown body |
| International     | `astro-i18n`             | en-CA / fr-CA routes & hreflang                          |
| SEO & Schema      | JSON-LD + `@astrojs/sitemap` | Rich structured data + sitemap.xml                     |
| Hosting           | Cloudflare Pages         | Free global CDN                                          |
| Edge Logic        | Cloudflare Workers + KV  | Geo-redirect `/api/buyurl` to correct marketplace link    |
| Forms & Email     | Workers + MailChannels / Klaviyo | Contact form routing, optional list sign-up         |
| AI-Dev            | ChatGPT Codex & Cursor AI + GitHub | Prompt-driven code & content gen                  |
| CI / QA           | GitHub Actions           | Build / link-check / Lighthouse / axe-playwright tests   |

---

## 📋 Roadmap & Tasks

### 1. Prerequisites  
- [ ] Install Node.js ≥ v20  
- [ ] Install & authenticate Wrangler CLI v3+ (`wrangler login`)  
- [ ] Clone this repo `cloudflare-poshyfoods-ai-website`  
- [ ] Configure ChatGPT Codex API & Cursor AI in IDE  

### 2. Scaffold & Integrations  
- [ ] Initialize Astro:  
  ```bash
  npm create astro@latest .
````

Choose: Minimal + TypeScript + MDX + “Git init: No.”

* [ ] Add integrations:

  ```bash
  npx astro add tailwind
  npx astro add sitemap
  npm install astro-i18n
  ```

  Configure `astro.config.mjs` with `tailwind()`, `sitemap()`, `i18n({ locales: ['en-ca','fr-ca'] })`
* [ ] Run `npm install` & `npm run dev` → confirm Astro welcome

### 3. Design System

* [ ] Create `tailwind.config.ts` with brand colors & fonts:

  ```ts
  theme: {
    extend: {
      colors: { pfSand:'#F7F3EF', pfCacao:'#3D3028', pfYellow:'#FFC93C', pfCoral:'#FF835E', pfMint:'#37C99E' },
      fontFamily: { serif:['"Fraunces Variable"','serif'], sans:['Inter','sans-serif'] },
    }
  }
  ```
* [ ] Install fonts:

  ```bash
  npm install @fontsource-variable/fraunces @fontsource/inter
  ```
* [ ] Create `src/styles/app.css` importing Tailwind & fonts, apply global body styles

### 4. Content & Schema

* [ ] Enable MDX:

  ```bash
  npx astro add mdx
  ```
* [ ] Add product MDX (e.g. `src/content/products/white-ogi.mdx`) with frontmatter (`title`, `slug`, `description`, `image`, `price`, `currency`, `inStock`, `amazonUrlCA`, etc.)
* [ ] Add recipe MDX under `src/content/recipes/`
* [ ] Create `src/components/ProductSchema.astro` & `RecipeSchema.astro` to render JSON-LD
* [ ] Create dynamic pages:

  * `src/pages/products/[slug].astro`
  * `src/pages/recipes/[slug].astro`
    with `getStaticPaths()` & frontmatter binding

### 5. Geo-Aware Marketplace Worker

* [ ] Create `workers/buyLink.js` using `req.cf.country` + KV lookup
* [ ] Configure `wrangler.toml` with KV namespace `LINKS` binding & route `/api/buyurl*`
* [ ] Seed KV with marketplace URLs for CA, US, ROW
* [ ] Update all “Buy” links to `/api/buyurl?sku=…`

### 6. Internationalization

* [ ] Duplicate content into `src/content/en-ca/…` & `fr-ca/…`
* [ ] Translate MDX content via AI or manually
* [ ] Ensure `<link rel="alternate" hreflang>` in layouts

### 7. SEO & AI-GEO Files

* [ ] Insert JSON-LD schemas in each page `<head>`
* [ ] Add `public/robots.txt` (allow GPTBot, Gemini, Claude)
* [ ] Add `public/llms.txt` (AI crawl policy CC-BY-4.0)
* [ ] Ensure `sitemap.xml` & `rss.xml` are generated

### 8. Visual Assets & Theme

* [ ] Integrate Minimog-inspired Tailwind template (components, layout, typography)
* [ ] Add DALL·E hero images in `public/images/`
* [ ] Use `<picture>` with AVIF/WebP + lazy-load for large images

### 9. UI & Fill-in Forms

* [ ] Create markdown templates under `src/templates/` for products & recipes
* [ ] Document “how to add a product” in `CONTRIBUTING.md`
* [ ] Optionally integrate a Git-based CMS or Worker-based form to auto-generate MDX

### 10. Accessibility & Performance

* [ ] Add `axe-playwright` tests → `npm run test:a11y`
* [ ] Integrate Lighthouse CI → performance ≥ 90 Mobile
* [ ] Add `scripts/linkCheck.js` → fail on 404s

### 11. CI / Deployment

* [ ] Create GitHub Actions workflow (`.github/workflows/ci.yml`): build → tests → deploy to Cloudflare Pages
* [ ] Connect Pages to this repo; set build command `npm run build`, publish directory `dist/`
* [ ] Configure custom domain `www.poshyfoods.com` in Cloudflare → SSL

### 12. Monitoring & Handoff

* [ ] Add `scripts/serpSnapshot.js` for weekly AI-SERP checks (push to Google Sheet)
* [ ] Finalize `CONTRIBUTING.md` with fill-in form instructions
* [ ] Tag release `v1.0.0`

---

## 🚀 Local Preview & Testing

1. **Clone** the repo

   ```bash
   git clone https://github.com/your-org/cloudflare-poshyfoods-ai-website.git
   cd cloudflare-poshyfoods-ai-website
   ```
2. **Install**

   ```bash
   npm install
   ```
3. **Run**

   ```bash
   npm run dev
   ```
4. **View**
   Open 👉 [http://localhost:4321](http://localhost:4321)

Use this README as the single source of truth. AI agents (Codex, Cursor) and human contributors can follow these steps, run associated CLI commands, and commit changes to deliver a fully-functional, AI-GEO-optimized Poshy Foods website.

```
```
