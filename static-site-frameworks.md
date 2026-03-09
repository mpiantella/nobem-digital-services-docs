# Static Site Frameworks for South American SMBs

## Context & Constraints

Building sites for South American small businesses introduces specific constraints that shape framework choice: variable internet connectivity (especially outside major metros), cost sensitivity for hosting, need for fast page loads on mid-range mobile devices, multilingual support (Spanish/Portuguese), and the ability to produce polished sites quickly with a small team.

This guide evaluates frameworks beyond Hugo and Astro (assumed known), focusing on practical fit for this market.

---

## Framework Landscape

### 1. Eleventy (11ty)

**What it is:** A zero-config, JavaScript-based static site generator that's deliberately simple. No client-side JS by default — it outputs pure HTML/CSS.

**Architecture:** Template-driven. Supports Nunjucks, Liquid, Markdown, Handlebars, and more. Data cascade system lets you layer global, directory, and file-level data. No framework lock-in — your output is just HTML.

**UXD patterns:** Content-first design. Because there's zero JS bundle by default, you're pushed toward progressive enhancement — add interactivity only where needed. This naturally produces accessible, fast-loading sites that work on low-bandwidth connections.

**Pros:**
- Near-zero learning curve if you know HTML/CSS — no framework abstractions to learn
- Fastest build times of any SSG (seconds, not minutes)
- Zero client JS = perfect Lighthouse scores out of the box
- Extremely lightweight output — ideal for Venezuelan mobile networks
- Template language flexibility (use what you already know)
- Easy i18n through data files and directory structure

**Cons:**
- No built-in component model — you manage partials manually
- Styling is BYO (no design system included)
- Ecosystem is smaller than Next.js or Gatsby — fewer plugins
- Image optimization requires manual setup or plugins
- Less "wow factor" in developer experience compared to newer tools

**Data points:**

| Metric | Rating |
|--------|--------|
| Ease to learn | ★★★★★ (if you know HTML) |
| Dev time for a 5-page site | 1–2 days |
| Deployment complexity | Minimal — static files anywhere |
| Bundle size | 0 KB JS (unless you add it) |

---

### 2. Next.js (Static Export Mode)

**What it is:** React's dominant meta-framework. While known for SSR, its `output: 'export'` mode generates fully static sites. You get React's component model with static output.

**Architecture:** React-based with file-system routing. App Router (recommended) or Pages Router. Static export pre-renders all pages at build time. API routes are NOT available in static mode — external services (Supabase, etc.) handle dynamic needs.

**UXD patterns:** Component-driven UI. React's ecosystem gives access to design systems like shadcn/ui, Radix, and Chakra UI, which follow modern UXD standards including WAI-ARIA accessibility, responsive design tokens, and consistent spacing/typography systems. Supports layout patterns (shared navs, footers) natively.

**Pros:**
- Massive ecosystem — component libraries, UI kits, templates
- If the team grows, the same codebase can evolve into SSR/ISR without rewrite
- shadcn/ui + Tailwind = professional-looking sites fast
- Image optimization with next/image (though limited in static export)
- Strong TypeScript support
- Easy path from static to dynamic if a client outgrows a static site

**Cons:**
- React overhead — even static pages ship a JS runtime (~80-120KB gzipped)
- Learning curve is steeper than template-based SSGs
- Build times are slower than Hugo or 11ty
- Static export mode has limitations (no middleware, no API routes, no ISR)
- Overkill for a simple brochure site

**Data points:**

| Metric | Rating |
|--------|--------|
| Ease to learn | ★★★☆☆ (React knowledge required) |
| Dev time for a 5-page site | 2–3 days |
| Deployment complexity | Low — Vercel, Netlify, or any CDN |
| Bundle size | 80–150 KB JS baseline |

---

### 3. SvelteKit

**What it is:** Svelte's official application framework. Can generate fully static sites via `@sveltejs/adapter-static`. Svelte compiles components to vanilla JS at build time — no virtual DOM, no runtime framework.

**Architecture:** Component-based with file-system routing. Svelte's compiler approach means components are compiled away, leaving only the minimal JS needed for actual interactivity. Layouts, error pages, and loading states are first-class concepts.

**UXD patterns:** Svelte's reactivity model makes animations, transitions, and micro-interactions trivial — `transition:fade`, `animate:flip` are built-in. This enables polished UX without heavy animation libraries. Skeleton UI and DaisyUI provide Svelte-native design systems. Built-in accessibility warnings in the compiler.

**Pros:**
- Smallest JS bundles of any component framework — great for bandwidth-constrained users
- Compiler catches accessibility issues at build time
- Built-in transitions and animations = polished feel with less effort
- Intuitive syntax — closest to writing plain HTML/CSS/JS
- Faster to learn than React or Vue for someone coming from vanilla web dev
- Strong SEO defaults in static mode

**Cons:**
- Smaller ecosystem than React — fewer pre-built components and templates
- Fewer developers in the LATAM market know Svelte (hiring consideration)
- Some enterprise clients may question "non-standard" tech choice
- Less mature than Next.js for complex use cases
- Fewer ready-made templates/themes available

**Data points:**

| Metric | Rating |
|--------|--------|
| Ease to learn | ★★★★☆ (intuitive if you know HTML/JS) |
| Dev time for a 5-page site | 1.5–2.5 days |
| Deployment complexity | Low — static adapter outputs files for any CDN |
| Bundle size | 5–30 KB JS (only what's needed) |

---

### 4. Nuxt (Static Mode)

**What it is:** Vue's meta-framework, analogous to Next.js for React. `nuxt generate` produces a fully static site. Since you know Vue, this is the natural static site path.

**Architecture:** Vue 3 + Composition API with file-system routing. Nuxt Content module turns Markdown/YAML into a queryable content layer — ideal for client sites where non-devs need to update content. Auto-imports components and composables.

**UXD patterns:** Vue's ecosystem includes Vuetify, PrimeVue, and Nuxt UI — mature design systems following Material Design or custom design tokens. Nuxt UI in particular provides a modern, accessible component library tailored for Nuxt. NuxtImage handles responsive images and lazy loading automatically.

**Pros:**
- You already know Vue — zero framework learning curve
- Nuxt Content makes content management almost CMS-like without a CMS
- Auto-imports reduce boilerplate significantly
- Strong i18n module (@nuxtjs/i18n) with SEO-friendly locale routing
- Nuxt UI provides beautiful, accessible components out of the box
- Great developer experience with Nuxt DevTools

**Cons:**
- Vue runtime adds JS weight (~30-50KB gzipped)
- Build times are moderate (faster than Gatsby, slower than Hugo)
- Some Nuxt 3 modules are still maturing
- Hydration can cause layout shifts if not careful
- Smaller talent pool than React in general market

**Data points:**

| Metric | Rating |
|--------|--------|
| Ease to learn | ★★★★★ (you know Vue already) |
| Dev time for a 5-page site | 1–2 days |
| Deployment complexity | Low — Netlify/Vercel/static hosting |
| Bundle size | 30–60 KB JS baseline |

---

### 5. Webflow

**What it is:** A visual web design tool that generates production-ready static sites. No code required for standard sites, but supports custom code embeds. Exports clean HTML/CSS/JS.

**Architecture:** Visual canvas → hosted site or exported code. CMS is built-in (visual content management). Hosting is on Webflow's CDN or you export and self-host. Interactions and animations are visual, GSAP-based under the hood.

**UXD patterns:** Webflow's design model is based on the CSS box model — it teaches proper web design thinking. Built-in interactions follow modern motion design principles. Responsive design is visual breakpoint-based. Client Billing lets you manage client sites under your agency account.

**Pros:**
- Fastest path from design to production — no code needed
- Client can update content themselves via CMS (huge for SMBs)
- Professional-quality animations and interactions without code
- Built-in form handling, SEO controls, and responsive design
- Agency/freelancer features (client billing, white-label, transferable sites)
- Extensive template marketplace for quick starts

**Cons:**
- Monthly cost per site ($14-39/month per site, or $23-49 with CMS)
- Vendor lock-in — exporting produces code that's hard to maintain manually
- Custom functionality requires workarounds or third-party integrations
- Limited to what the visual builder supports
- Pricing in USD can be significant for Venezuelan SMB budgets
- Internet required for development (no offline mode)

**Data points:**

| Metric | Rating |
|--------|--------|
| Ease to learn | ★★★★☆ (visual, but CSS model knowledge helps) |
| Dev time for a 5-page site | 0.5–1 day |
| Deployment complexity | None (hosted) or export static files |
| Bundle size | 50–150 KB (depends on interactions) |

---

### 6. Framer

**What it is:** Design-to-production tool evolved from a prototyping tool. Generates static sites with React under the hood. More opinionated and modern-feeling than Webflow.

**Architecture:** Visual editor with component system. Sites are hosted on Framer's infrastructure (Vercel-backed). No code export — you're committed to Framer hosting. CMS is built-in and simpler than Webflow's.

**UXD patterns:** Framer's design model emphasizes modern layout patterns — auto-layout (Flexbox), responsive variants, and scroll-based animations. Pre-built sections follow contemporary landing page patterns. Strong typography and spacing controls.

**Pros:**
- Extremely fast for landing pages and marketing sites
- Beautiful default aesthetics — hard to make an ugly site
- Built-in SEO optimization and analytics
- Simpler learning curve than Webflow
- AI-powered features for content and layout suggestions
- Great for rapid prototyping and client presentations

**Cons:**
- No code export — full vendor lock-in
- Pricing per site ($5-30/month per site)
- Less flexible than Webflow for complex layouts
- Limited CMS compared to Webflow
- Not suitable for sites requiring custom backend logic
- Relatively new — less established agency ecosystem

**Data points:**

| Metric | Rating |
|--------|--------|
| Ease to learn | ★★★★★ (most intuitive visual builder) |
| Dev time for a 5-page site | 3–6 hours |
| Deployment complexity | None (hosted only) |
| Bundle size | 60–120 KB (React-based) |

---

### 7. Bridgetown

**What it is:** A progressive Ruby-based site generator, spiritual successor to Jekyll. Modern architecture with component support via Ruby or web components.

**Architecture:** Ruby + ERB/Liquid templates with optional Roda server for SSR. Component model supports both Ruby components and web components. Built-in Markdown processing with front matter. Integrates with esbuild for JS bundling.

**UXD patterns:** Convention-over-configuration approach. Encourages progressive enhancement — start static, add interactivity via islands. Supports Tailwind CSS out of the box. Layout and partial system for consistent page structures.

**Pros:**
- Clean, modern API with good documentation
- Component model bridges static and interactive needs
- Built-in Tailwind integration
- Good for content-heavy sites (blogs, documentation)
- Active community with modern Ruby practices

**Cons:**
- Ruby dependency — outside your current stack (Go/JS)
- Smaller ecosystem than JS-based alternatives
- Fewer templates and themes available
- Community is passionate but small
- Not the best choice if you're standardizing on JS/Go

**Data points:**

| Metric | Rating |
|--------|--------|
| Ease to learn | ★★★☆☆ (requires Ruby knowledge) |
| Dev time for a 5-page site | 2–3 days |
| Deployment complexity | Low — static output to any CDN |
| Bundle size | 0–20 KB (progressive enhancement) |

---

## Comparative Matrix

| Framework | Learning Curve | Dev Speed | JS Bundle | Client Self-Service | Monthly Cost | Offline Dev | LATAM Fit |
|-----------|---------------|-----------|-----------|-------------------|-------------|------------|-----------|
| 11ty | Very Low | Fast | 0 KB | No (needs CMS) | $0 + hosting | Yes | ★★★★★ |
| Next.js Static | Medium | Medium | 80–150 KB | Via headless CMS | $0 + hosting | Yes | ★★★☆☆ |
| SvelteKit | Low-Med | Fast | 5–30 KB | No (needs CMS) | $0 + hosting | Yes | ★★★★☆ |
| Nuxt Static | Low (for you) | Fast | 30–60 KB | Via Nuxt Content | $0 + hosting | Yes | ★★★★☆ |
| Webflow | Low-Med | Very Fast | 50–150 KB | Yes (built-in) | $14–49/site | No | ★★★☆☆ |
| Framer | Very Low | Fastest | 60–120 KB | Yes (built-in) | $5–30/site | No | ★★☆☆☆ |
| Bridgetown | Medium | Medium | 0–20 KB | No (needs CMS) | $0 + hosting | Yes | ★★☆☆☆ |

---

## Recommendations for Your Context

### For maximum speed with minimum cost:
**Nuxt Static + Nuxt UI + Nuxt Content.** You already know Vue, Nuxt UI gives you polished components instantly, and Nuxt Content lets you structure client content in Markdown files. Pair with Cloudflare Pages (free tier, good LATAM edge nodes) for deployment.

### For the lightest possible output:
**11ty + Tailwind CSS.** Zero JS shipped to the client. Sites load instantly even on 3G connections. The tradeoff is more manual work on interactive elements and no built-in design system — but for simple business sites (restaurant, store, professional services), this produces the fastest possible result.

### For scalability as clients grow:
**Astro** (which you know) is actually the sweet spot here. It supports multiple UI frameworks, ships zero JS by default with opt-in islands, and has a growing content layer. If a client later needs dynamic features, you add them without changing frameworks.

### For non-technical client handoff:
**Webflow**, if the client's budget supports it. The ability for the client to update their own content without calling you is a huge value proposition for SMBs. Build it once, hand it over, charge for maintenance.

### Stack recommendation for the agency:
Standardize on **Astro** as the primary SSG (you know it, it's flexible, minimal JS) with **Nuxt** for sites that need more interactivity. Use **Tailwind CSS** across both for design consistency. Deploy to **Cloudflare Pages** for free hosting with excellent Latin American edge coverage. Add a headless CMS like **Decap CMS** (free, Git-based) when clients need self-service content editing.
