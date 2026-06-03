# rachitsharma.space

Personal brand portfolio — AI Systems Builder, Melbourne AU.

## Tech Stack

- **Framework:** Astro 4
- **Styling:** Pure CSS with CSS variables (no Tailwind)
- **Fonts:** Syne (display) + JetBrains Mono + Crimson Pro
- **Deploy:** Vercel
- **Domain:** rachitsharma.space

## Local Dev

```bash
npm install
npm run dev
# http://localhost:4321
```

## Deploy (Vercel — recommended)

```bash
npm install -g vercel
vercel login
vercel --prod
```

Then in Vercel dashboard:
1. Add custom domain: `rachitsharma.space`
2. Point DNS at Ventra IP:
   - A record: `76.76.21.21`
   - CNAME `www`: `cname.vercel-dns.com`

## Before Launch Checklist

- [ ] Replace `YOUR_FORM_ID` in `Contact.astro` with real Formspree ID
- [ ] Update email in `Contact.astro` and `Footer.astro`
- [ ] Add real photo/avatar if desired (optional)
- [ ] Update GitHub secrets for Vercel auto-deploy
- [ ] Add `og:image` (1200x630 PNG) to `/public/`

## Structure

```
src/
  components/
    Nav.astro        -- sticky navbar + mobile menu
    Hero.astro       -- animated terminal + stats
    About.astro      -- bio + current status cards
    Stack.astro      -- tech stack grid
    Projects.astro   -- shipped projects
    Consulting.astro -- services + CTA
    Contact.astro    -- form + contact methods
    Footer.astro
  layouts/
    Base.astro       -- HTML shell, meta tags
  styles/
    global.css       -- design tokens, fonts, animations
  pages/
    index.astro      -- assembles all sections
```

## Design System

- **Theme:** Dark industrial, saffron/orange accent
- **Fonts:** Syne 800 for headings, JetBrains Mono for labels/code, Crimson Pro for body
- **Colors:** `#0a0a08` bg, `#f5a623` accent, `#e8390e` accent2, `#4ade80` green
- **Motion:** CSS keyframes, staggered fade-up on load, terminal typewriter loop

## Customization

All personal data is in the component files — no CMS needed.
Edit each `.astro` file directly. Data is at the top in the `---` frontmatter.
