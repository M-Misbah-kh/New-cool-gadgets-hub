# Fix: Deploy Your Lovable Site to Cloudflare Pages

## Why Your Build Failed

Your site uses **TanStack Start** (a React framework). Cloudflare Pages needs:
1. A `cloudflare-pages` adapter in the config
2. A `wrangler.toml` file telling Cloudflare where your built files are
3. The correct build command (`vinxi build`)

---

## Step-by-Step Fix

### Step 1 — Add the Fix Files to Your GitHub Repo

Open your GitHub repo and add/replace these files (copy from the files I gave you):

| File | What it does |
|------|-------------|
| `app.config.ts` | Tells TanStack Start to build for Cloudflare |
| `wrangler.toml` | Tells Cloudflare where the built files go |
| `tsconfig.json` | TypeScript settings (replace if you have one) |
| `package.json` | Make sure your build script is `vinxi build` |

### Step 2 — Set Cloudflare Pages Build Settings

In Cloudflare Pages dashboard → your project → Settings → Build:

| Setting | Value |
|---------|-------|
| **Framework preset** | None |
| **Build command** | `npm run build` |
| **Build output directory** | `.output/public` |
| **Node version** | `20` |

### Step 3 — Set Node Version (Important!)

In Cloudflare Pages → Settings → Environment Variables, add:

| Variable | Value |
|----------|-------|
| `NODE_VERSION` | `20` |

### Step 4 — Trigger a New Deploy

Go to your Cloudflare Pages project → click **"Retry deployment"** or push any change to GitHub.

---

## Fix Your Wrong Images & Descriptions

While you wait for the site to build, fix your product data:

### In your GitHub repo, open `Src/lib/data.ts`

This file contains all your products. Each product looks like this:

```typescript
{
  id: "product-1",
  title: "Product Title",        // ✅ Already correct
  image: "fake-image-url",       // ❌ WRONG — change this
  description: "Fake text...",   // ❌ WRONG — change this
  affiliateUrl: "https://amazon.com/dp/XXXXX?tag=yourtag-20"  // ✅ Correct
}
```

**To fix each product:**
1. Go to the Amazon product page
2. Right-click the main product image → "Copy image address"
3. Paste it as the `image` value
4. Copy the product's bullet points and paste as `description`

### Using Amazon SiteStripe for Images (Better Method)
1. Log into Amazon Associates
2. Browse to each product
3. In the SiteStripe bar at top → click **"Image"**
4. Copy the image URL from the code shown

---

## Affiliate Disclosure Check

Make sure your site has this text somewhere visible (required by law):

> *"This site contains affiliate links. If you click and make a purchase, I may earn a commission at no extra cost to you."*

Your Lovable site already has an `affiliate-disclosure` page — just make sure it's linked in your footer.

---

## After Publishing — Your Checklist

- [ ] Site builds successfully on Cloudflare Pages
- [ ] All product images are real Amazon images
- [ ] All descriptions match the actual products
- [ ] Affiliate links open correct Amazon pages
- [ ] Affiliate disclosure is visible
- [ ] Test on mobile (Pinterest traffic is mostly mobile!)
