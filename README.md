# Che Peru — Website

Single-file restaurant website for **Che Peru**, Peruvian-Argentinian fusion, Toronto.  
Built with HTML + CSS + vanilla JS. No build step, no dependencies (beyond Google Fonts).

---

## 1. How to Deploy

### Option A — Netlify (recommended, free)
1. Go to [netlify.com](https://netlify.com) and sign up / log in.
2. Drag the entire project folder onto the Netlify dashboard.
3. Done — you get a live URL in seconds. Connect a custom domain like `cheperu.ca` in Settings → Domains.

### Option B — Vercel
1. Install the Vercel CLI: `npm i -g vercel`
2. Run `vercel` inside the project folder and follow the prompts.
3. Vercel will detect it as a static site automatically.

### Option C — GitHub Pages
1. Push this folder to a GitHub repository.
2. Go to Settings → Pages → Source: select `main` branch, `/root`.
3. Your site will be live at `https://<username>.github.io/<repo>`.

---

## 2. How to Update Content

All content lives in `index.html`. Each section is clearly marked with a comment like `<!-- MENU -->`.

### Update menu prices or descriptions
Search for the dish name (e.g. `Ceviche Clásico`). Each item looks like:
```html
<div class="menu-item">
  <div class="menu-item-header">
    <span class="menu-item-name">Ceviche Clásico</span>
    <span class="menu-item-price">$18</span>   <!-- ← change price here -->
  </div>
  <p class="menu-item-desc">Fresh white fish…</p>   <!-- ← change description here -->
  <span class="menu-tag">Chef's Pick</span>          <!-- ← change or remove tag -->
</div>
```

To **add a dish**, copy an entire `<div class="menu-item">…</div>` block and paste it inside the correct `<div id="tab-starters">` (or mains/desserts/drinks) section.

### Update opening hours
Find the `<div class="hours-list">` block (inside the `#reserve` section) and edit the time text directly.

The same hours appear in the **footer** — search for `Tues–Thurs:` and update those lines too.

### Update contact info
Search for `416` to find all phone number instances, and `hello@cheperu.ca` for email.  
The address appears in three places: the Visit section, the footer, and the JSON-LD schema block at the top of `<head>`.

### Add a real hero photo
In the `<style>` block, find the comment `/* Photo placeholder */` inside `.hero-bg`. Uncomment and adjust:
```css
.hero-bg {
  background-image: url('assets/hero.jpg');
  background-size: cover;
  background-position: center;
}
```
Place your photo at `assets/hero.jpg`. Recommended size: 1920×1080px, under 400KB (use [Squoosh](https://squoosh.app) to compress).

---

## 3. Connecting the Reservation Form to a Real Email Service

The form currently shows a success message without sending any data. To make it functional:

### Easiest path — Formspree (free tier: 50 submissions/month)
1. Go to [formspree.io](https://formspree.io) and create a free account.
2. Create a new form — Formspree gives you an endpoint like `https://formspree.io/f/xabcdefg`.
3. In `index.html`, find the `<form>` tag and add the action attribute:
   ```html
   <form id="reservationForm" action="https://formspree.io/f/xabcdefg" method="POST">
   ```
4. Remove or comment out the JavaScript `form.addEventListener('submit', …)` block at the bottom, since Formspree handles the submission natively. Or keep it and replace the `setTimeout` simulation with a real `fetch` call to the Formspree endpoint.

Formspree sends all submissions directly to the restaurant's email inbox. No server needed.

---

## Photo Placeholders

The hero background is a solid dark colour waiting for a real photo. When the owner provides images:

| Where | CSS selector | Recommended size |
|---|---|---|
| Hero background | `.hero-bg` | 1920 × 1080 px |
| Open Graph image | `<meta property="og:image">` in `<head>` | 1200 × 630 px |

---

*Built with Claude Code — [https://claude.ai/code](https://claude.ai/code)*
