# Gallavance Comfort Tracker - Deployment Guide

## Overview

This guide covers deploying the Comfort Tracker to:
1. **Vercel** (free hosting)
2. **Shopify** (iframe embed)
3. **gallavance.com** (iframe or direct integration)

---

## PART 1: Deploy to Vercel (Free Hosting)

### Option A: Quick Deploy (No GitHub needed)

1. Go to [vercel.com](https://vercel.com) and sign up (free)
2. Install Vercel CLI: `npm i -g vercel`
3. In terminal, navigate to the folder containing `index.html`
4. Run: `vercel`
5. Follow prompts → You'll get a URL like `gallavance-tracker.vercel.app`

### Option B: GitHub Deploy (Recommended for updates)

1. Create a GitHub repo called `gallavance-tracker`
2. Upload the `index.html` file to the repo
3. Go to [vercel.com](https://vercel.com) → "Add New Project"
4. Import your GitHub repo
5. Deploy → Get your URL

### Set Up Custom Domain (Optional but Recommended)

1. In Vercel dashboard → Your project → Settings → Domains
2. Add: `tracker.gallavance.com`
3. In Namecheap (your domain registrar):
   - Add CNAME record: `tracker` → `cname.vercel-dns.com`
4. Wait 5-10 minutes for DNS propagation

**Your tracker will now live at:** `https://tracker.gallavance.com`

---

## PART 2: Embed in Shopify

### Step 1: Create a New Page

1. Shopify Admin → Online Store → Pages
2. Click "Add page"
3. Title: "My Comfort Tracker" or "14-Day Challenge Tracker"
4. Click `<>` (Show HTML) in the content editor

### Step 2: Paste This Embed Code

```html
<div style="max-width: 450px; margin: 0 auto;">
  <iframe 
    src="https://tracker.gallavance.com" 
    width="100%" 
    height="700" 
    frameborder="0" 
    style="border: none; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.1);"
    title="Gallavance Comfort Tracker"
    allow="clipboard-write"
  ></iframe>
</div>

<style>
  @media (max-width: 480px) {
    iframe {
      height: 650px !important;
    }
  }
</style>
```

### Step 3: Configure Page Settings

1. **Template:** Use "page.full-width" if available, or default
2. **SEO:** 
   - Title: "Comfort Tracker | Gallavance"
   - Description: "Track your digestive comfort with our 14-Day Challenge tracker."
   - URL handle: `my-tracker`
3. **Visibility:** Visible (or Hidden if you want customers-only access)

### Step 4: Add to Navigation (Optional)

1. Online Store → Navigation → Main menu (or Footer)
2. Add menu item:
   - Name: "My Tracker"
   - Link: `/pages/my-tracker`

---

## PART 3: Add to Customer Account Area (Advanced)

If you want the tracker to appear in the customer account dashboard:

### Using Shopify Theme Customizer

1. Online Store → Themes → Customize
2. Go to: Templates → Customers → Account
3. Add a "Custom Liquid" section
4. Paste:

```liquid
{% if customer %}
<div class="tracker-section" style="margin: 40px 0;">
  <h2 style="font-size: 24px; margin-bottom: 20px;">Your Comfort Tracker</h2>
  <div style="max-width: 450px;">
    <iframe 
      src="https://tracker.gallavance.com" 
      width="100%" 
      height="700" 
      frameborder="0" 
      style="border: none; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.1);"
      title="Gallavance Comfort Tracker"
    ></iframe>
  </div>
</div>
{% endif %}
```

---

## PART 4: Embed on gallavance.com

### If Using WordPress

Add this to any page/post using Custom HTML block:

```html
<div style="max-width: 450px; margin: 40px auto;">
  <iframe 
    src="https://tracker.gallavance.com" 
    width="100%" 
    height="700" 
    frameborder="0" 
    style="border: none; border-radius: 12px; box-shadow: 0 4px 20px rgba(0,0,0,0.1);"
    title="Gallavance Comfort Tracker"
  ></iframe>
</div>
```

### If Using Squarespace/Wix/Webflow

1. Add an "Embed" or "Code" block
2. Paste the same iframe code above

### If Building Custom (React/Next.js)

You can import the component directly instead of using iframe:

```jsx
// Copy the GallavanceComfortTracker component into your project
import GallavanceComfortTracker from './components/ComfortTracker';

export default function TrackerPage() {
  return (
    <div className="container mx-auto py-8">
      <GallavanceComfortTracker />
    </div>
  );
}
```

---

## PART 5: Important Placement Guidelines

### ✅ DO place the tracker:
- On a dedicated `/my-tracker` or `/14-day-challenge` page
- In the customer account area
- In post-purchase email flows (link to tracker page)

### ❌ DON'T place the tracker:
- On product pages (next to Buy buttons = implied claims)
- In the cart or checkout flow
- Anywhere that directly correlates usage with purchase

### Recommended User Flow:
1. Customer purchases Gallavance
2. Order confirmation email includes: "Start your 14-Day Comfort Challenge → [Link to tracker]"
3. Customer accesses tracker from their account or bookmarked page
4. Tracker data stays on their device (localStorage)

---

## PART 6: Testing Checklist

Before going live, verify:

- [ ] Tracker loads correctly on desktop
- [ ] Tracker loads correctly on mobile
- [ ] Consent screen appears on first visit
- [ ] Check-in flow works (all 4 steps)
- [ ] Data persists after page refresh
- [ ] Export CSV works
- [ ] Delete All Data works
- [ ] Disclaimer text is visible in footer
- [ ] No product purchase CTAs near the tracker

---

## PART 7: Future Enhancements (V2)

When ready to add features:

1. **Magic Link Login** - Cross-device sync via email
2. **Shopify Customer SSO** - Tie to Shopify accounts
3. **Auto-reminder emails** - "Don't forget to log today!"
4. **Share functionality** - With proper FTC disclosure flow
5. **PDF Summary export** - Branded 14-day report

---

## Support Files Included

- `index.html` - Self-contained tracker app (deploy this)
- `README.md` - This file

---

## Questions?

This tracker was built with compliance in mind (FDA structure/function language, FTC disclosure requirements, CCPA data rights). For legal sign-off, have your attorney review before launch.
