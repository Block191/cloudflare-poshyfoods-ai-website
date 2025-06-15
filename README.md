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
- **Premium DTC theme** baseline (Astro E-commerce by Creative Tim) for a designer-grade user experience  

---

## 🛠️ Tech Stack  
| Layer             | Technology               | Purpose                                                  |
|-------------------|--------------------------|----------------------------------------------------------|
| **Framework**     | Astro (v5+)              | Static SSG, MDX, components                              |
| **Styling**       | Tailwind CSS             | Utility-first design, custom theme tokens                |
| **Content**       | MDX Collections          | Products, Recipes, Pages via frontmatter + Markdown body |
| **International** | `astro-i18n`             | en-CA / fr-CA routes & hreflang                          |
| **SEO & Schema**  | JSON-LD + `@astrojs/sitemap` | Rich structured data + `sitemap.xml`                 |
| **Hosting**       | Cloudflare Pages         | Free global CDN                                          |
| **Edge Logic**    | Cloudflare Workers + KV  | Geo-redirect `/api/buyurl` to correct marketplace link   |
| **Forms & Email** | Workers + MailChannels / Klaviyo | Contact form routing, optional list sign-up        |
| **AI-Dev**        | ChatGPT Codex & Cursor AI + GitHub | Prompt-driven code & content gen               |
| **CI / QA**       | GitHub Actions           | Build / link-check / Lighthouse / axe-playwright tests   |

---

## 📋 Roadmap & Tasks

### 1. Prerequisites  
- [ ] Install Node.js ≥ v20  
- [ ] Install & authenticate Wrangler CLI v3+ (`wrangler login`)  
- [ ] Clone this repo `cloudflare-poshyfoods-ai-website`  
- [ ] Configure ChatGPT Codex API & Cursor AI in IDE  

### 2. Scaffold & Integrations  
1. **Scaffold using the Astro E-commerce theme**  
   ```bash
   npm create astro@latest . \
     --template https://github.com/creativetimofficial/astro-ecommerce
````

* This pulls in Creative Tim’s polished e-commerce starter with landing, product & shopping pages.

2. **Install dependencies & run dev**

   ```bash
   npm install
   npm run dev
   ```

   ▶️ **Local preview**: [http://localhost:4321](http://localhost:4321)
3. **Add core integrations**

   ```bash
   npx astro add tailwind
   npx astro add sitemap
   npm install astro-i18n
   ```

   Update `astro.config.mjs`:

   ```js
   import tailwind from '@astrojs/tailwind';
   import sitemap from '@astrojs/sitemap';
   import i18n from 'astro-i18n';

   export default defineConfig({
     integrations: [
       tailwind(),
       sitemap(),
       i18n({ locales: ['en-ca','fr-ca'], defaultLocale: 'en-ca' })
     ],
   });
   ```

### 3. Design System

* [ ] Create `tailwind.config.ts` with brand colors & fonts:

  ```ts
  theme: {
    extend: {
      colors: {
        pfSand:  '#F7F3EF',
        pfCacao: '#3D3028',
        pfYellow:'#FFC93C',
        pfCoral: '#FF835E',
        pfMint:  '#37C99E',
      },
      fontFamily: {
        serif: ['"Fraunces Variable"','serif'],
        sans:  ['Inter','sans-serif'],
      },
    }
  }
  ```
* [ ] Install fonts:

  ```bash
  npm install @fontsource-variable/fraunces @fontsource/inter
  ```
* [ ] Create `src/styles/app.css` importing Tailwind & fonts; apply global body styles

### 4. Content & Schema

* [ ] Enable MDX:

  ```bash
  npx astro add mdx
  ```
* [ ] Add **product** MDX under `src/content/products/` (e.g. `white-ogi.mdx`) with frontmatter fields
* [ ] Add **recipe** MDX under `src/content/recipes/`
* [ ] Create `src/components/ProductSchema.astro` & `RecipeSchema.astro` for JSON-LD
* [ ] Create dynamic pages:

  * `src/pages/products/[slug].astro`
  * `src/pages/recipes/[slug].astro`
    with `getStaticPaths()` & `Astro.props` binding

### 5. Geo-Aware Marketplace Worker

* [ ] Create `workers/buyLink.js` reading `req.cf.country` + KV lookup
* [ ] Configure `wrangler.toml` with KV namespace `LINKS` & route `/api/buyurl*`
* [ ] Seed KV with marketplace URLs (CA, US, ROW)
* [ ] Update all “Buy” buttons to hit `/api/buyurl?sku=…`

### 6. Internationalization

* [ ] Duplicate content under `src/content/en-ca/` & `fr-ca/`
* [ ] Translate MDX via AI or manually
* [ ] Ensure `<link rel="alternate" hreflang="…">` in layouts

### 7. SEO & AI-GEO Files

* [ ] Insert JSON-LD schemas in each page `<head>`
* [ ] Add `public/robots.txt` (allow GPTBot, Gemini, Claude)
* [ ] Add `public/llms.txt` (AI crawl policy CC-BY-4.0)
* [ ] Ensure `sitemap.xml` & `rss.xml` generation

### 8. Visual Assets & Theme

* [ ] Replace placeholder assets with Poshy Foods imagery in `public/images/`
* [ ] Use `<picture>` (AVIF/WebP + lazy-load) for hero & product images

### 9. UI & Fill-in Forms

* [ ] Create MDX templates under `src/templates/` for products & recipes
* [ ] Document “how to add a product” in `CONTRIBUTING.md`
* [ ] (Optional) Integrate a Git-based CMS or Worker form to auto-generate MDX

### 10. Accessibility & Performance

* [ ] Add `axe-playwright` tests → `npm run test:a11y`
* [ ] Integrate Lighthouse CI → performance ≥ 90 Mobile
* [ ] Add `scripts/linkCheck.js` → fail on broken links

### 11. CI / Deployment

* [ ] Create GitHub Actions workflow (`.github/workflows/ci.yml`): build → tests → deploy to Pages
* [ ] Connect Cloudflare Pages: build `npm run build`, publish `dist/`
* [ ] Configure custom domain `www.poshyfoods.com` → SSL

### 12. Monitoring & Handoff

* [ ] Add `scripts/serpSnapshot.js` for weekly AI-SERP checks → Google Sheet
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

Use this README as your single source of truth. AI agents (Codex, Cursor) and human contributors can follow these steps, run the CLI commands, and commit changes to deliver a fully-functional, AI-GEO-optimized Poshy Foods website.

```
```
