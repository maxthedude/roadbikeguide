# Implementation Plan: Phase 1 — Landing Page MVP

## Purpose
Create a lightweight, high-conversion landing page for RoadBikeGuide to capture early interest, collect emails, and provide a clear value proposition while the full SPA is developed.

## Scope (MVP)
- Single static HTML landing page (mobile-first, responsive)
- Hero section with background image and headline
- Short features / value propositions (3 cards)
- Email signup form (Mailchimp, Formspree or Netlify Forms)
- Basic footer with links to GitHub, privacy, and social
- Quick deploy to GitHub Pages / Vercel / Netlify

## Deliverables
- IMPLEMENTATION_PLAN.md (this file)
- index.html
- assets/
  - images/hero.jpg (placeholder)
  - logo.svg
- css/styles.css
- js/main.js (for small interactions and form handling)
- _redirects or netlify.toml (if using Netlify)

## Tech Stack
- HTML5, CSS3 (prefer Tailwind or simple custom CSS)
- Minimal vanilla JS
- Hosting: Vercel (recommended) or Netlify or GitHub Pages
- Email: Mailchimp embed, Formspree, or Netlify Forms (no server required)
- Optional: Google Analytics / Plausible for lightweight analytics

## File Structure
roadbikeguide/
├─ index.html
├─ css/
│  └─ styles.css
├─ js/
│  └─ main.js
├─ assets/
│  ├─ images/
│  │  └─ hero.jpg
│  └─ logo.svg
└─ README.md

## Detailed Implementation Tasks
1. Repo & Branch
   - Create a branch `phase-1-landing-page` (already created).
   - Ensure .gitignore is up-to-date.

2. HTML Skeleton (index.html)
   - Mobile-first meta tags
   - Hero section with H1 headline and CTA
   - 3 feature cards section
   - Email signup form (inline with action to chosen email service)
   - Footer with links to repo and privacy
   - Include minimal structured data (JSON-LD) for SEO

3. Styling (css/styles.css)
   - Reset / base styles
   - Responsive layout using CSS Grid/Flexbox
   - Accessible color contrast
   - Small utility classes for spacing

4. Interactivity (js/main.js)
   - Form submission handling and user feedback (success / error)
   - Small animations (fade-in) for hero and cards
   - Lazy-load hero image for performance

5. Assets
   - Add placeholder hero image (optimize to <200 KB webp or jpeg)
   - Add a small SVG logo

6. Email Signup Options (choose one)
   a) Mailchimp: embed form and GDPR checkbox
   b) Formspree: fetch POST to Formspree endpoint
   c) Netlify Forms: add form attributes and let Netlify capture submissions

7. Deploy
   - Prefer Vercel for simplicity: connect repo → select branch → deploy
   - Alternatively: Netlify or GitHub Pages (if static build only)

8. Analytics & Tracking (optional)
   - Add lightweight analytics (Plausible recommended) or GA4 if needed
   - Add UTM campaign tracking to CTA links

9. Accessibility & SEO
   - Alt text for images, semantic headings
   - Meta description, open graph tags, twitter card
   - Ensure keyboard navigability

10. Testing
    - Cross-device test (mobile, tablet, desktop)
    - Performance: Lighthouse score target >80 mobile
    - Form submit tests (success path & failure path)

## Timeline (Suggested)
- Day 0: Branch creation and planning (done)
- Day 1: Create index.html, styles.css, main.js with placeholder content
- Day 2: Integrate email provider and add assets
- Day 3: Deploy to Vercel / Netlify, smoke test, fix issues
- Day 4: Final tweaks, add analytics, and merge PR

## Acceptance Criteria
- Landing page is live at a public URL
- Email signup successfully records submissions
- Mobile-first design with accessible markup
- Basic SEO/meta tags present

## PR Checklist
- [ ] Branch name `phase-1-landing-page`
- [ ] Files: index.html, css/styles.css, js/main.js, assets/*
- [ ] Descriptive commit messages
- [ ] Deployed preview available for review
- [ ] Lighthouse score & manual QA logged

## Next Steps After Merge
- Start Angular SPA scaffolding in `main` or `dev` branch
- Build climb data API and basic demo list of climbs
- Integrate map library (Leaflet) and sample climb

## Notes
- Keep the landing page minimal and conversion-optimized; the goal is to collect interest, not ship full features.
- Use privacy-aware analytics and be explicit about data capture in the privacy link.

---

# Implementation-specific Templates

Below are skeleton templates you can copy into files.

## index.html (skeleton)

<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <title>RoadBikeGuide — Find your next climb</title>
    <meta name="description" content="Discover road bike climbs, KOM/QOM data, and plan your next ride." />
    <link rel="stylesheet" href="/css/styles.css" />
  </head>
  <body>
    <header class="site-header">
      <div class="container">
        <img src="/assets/logo.svg" alt="RoadBikeGuide logo" class="logo" />
      </div>
    </header>

    <main>
      <section class="hero">
        <div class="container">
          <h1>Find the climbs that challenge you</h1>
          <p>Discover elevation, difficulty, and KOM/QOM stats for road climbs near you.</p>

          <form id="signup-form" action="#" method="POST">
            <input type="email" name="email" placeholder="Enter your email" required />
            <button type="submit">Get early access</button>
          </form>
        </div>
      </section>

      <section class="features container">
        <div class="feature">Search climbs</div>
        <div class="feature">Elevation profiles</div>
        <div class="feature">KOM / QOM data</div>
      </section>
    </main>

    <footer>
      <div class="container">
        <small>© RoadBikeGuide</small>
      </div>
    </footer>

    <script src="/js/main.js"></script>
  </body>
</html>

## css/styles.css (skeleton)

/* Simple reset */
*{box-sizing:border-box}body{font-family:system-ui,-apple-system,Segoe UI,Roboto,Inter,Arial;line-height:1.35;margin:0;color:#111}.container{max-width:1100px;margin:0 auto;padding:1rem}.hero{padding:4rem 1rem;text-align:center;background:#0b1220;color:#fff}.hero h1{font-size:1.8rem;margin:.5rem 0}.features{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:1rem;padding:2rem 0}.feature{background:#fff;padding:1rem;border-radius:8px;text-align:center}

## js/main.js (skeleton)

document.getElementById('signup-form')?.addEventListener('submit', async function(e){
  e.preventDefault();
  const form = e.target;
  const email = form.querySelector('input[name="email"]').value;
  // TODO: replace with actual endpoint
  try{
    // Example using fetch to Formspree or Netlify function
    const res = await fetch(form.action || '/', {method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({email})});
    alert('Thanks — you are signed up!');
  }catch(err){
    alert('There was a problem signing up.');
  }
});