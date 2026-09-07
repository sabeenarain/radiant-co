# radiant — Watch & Bracelet Store

This is a real, deployable React website (not just a preview) — everything
you saw in Claude now lives in a normal project folder you fully own.

---

## 1. What you own vs. what's here

- **The code is 100% yours.** There's no Claude/Anthropic branding, license,
  or lock-in. You can move it, sell it, or hand it to a developer.
- **You will own the hosting account** (e.g. Vercel/Netlify — free tier is
  fine) and the **domain name** (bought separately, ~$10–15/year).
- Nothing here calls Claude or any Anthropic service. It's a plain
  React + Tailwind site.

---

## 2. Run it on your computer first

You need **Node.js** installed (version 18 or newer).
Check: https://nodejs.org — download the "LTS" version and install it.

Then, in a terminal, inside this folder:

```bash
npm install
npm run dev
```

This prints a local address like `http://localhost:5173`. Open it in your
browser — that's your live store, running on your machine. Leave this
terminal running while you work; every time you save a file, the page
updates automatically.

---

## 3. How to make changes

### A. Edit store info, products, prices (no coding knowledge needed)
Open `src/App.jsx` in any text editor (VS Code is a good free one:
https://code.visualstudio.com). Near the top you'll find:

- `DEFAULT_SETTINGS` — brand name, phone, WhatsApp, email, socials,
  address, delivery charge, return policy, payment methods.
- `SAMPLE_WATCHES` and `SAMPLE_BRACELETS` — one line per product, with
  name, price, description, images, colors, sizes, stock, etc.

Change the text/numbers directly, save the file, and your local preview
(step 2) updates instantly.

You can also make these same changes **live in the browser**, without
touching code, using the **Admin** link in the site footer — it has tabs
for Products, Orders, Customers, and Settings.

### B. Add a picture
You have two options:

**Option 1 — use an image already on the internet (easiest)**
Find or upload your photo somewhere (e.g. Google Drive → "Get shareable
link", or a free image host like https://imgur.com), copy the **direct
image URL** (it should end in `.jpg`/`.png`/`.webp`), and paste it into
the product's `images: [...]` array in `App.jsx`, or into the image field
in the Admin → Products editor. Example:

```js
images: ["https://i.imgur.com/yourphoto.jpg"]
```

**Option 2 — use your own photo file**
1. Put the image file in the `public/images/` folder in this project
   (e.g. `public/images/meridian-1.jpg`).
2. Reference it with a leading slash and no `public`:
   ```js
   images: ["/images/meridian-1.jpg"]
   ```
This works both locally and once deployed.

### C. Edit colors, layout, or add a page
Everything else lives in `src/App.jsx` as plain React components
(`Home`, `ShopPage`, `ProductDetails`, `AdminPage`, etc.). If you're not
comfortable editing React/Tailwind directly, just tell Claude what you
want changed and paste the updated file back here when you're ready to
redeploy — or ask Claude to walk you through the specific edit.

---

## 4. Put it on GitHub (recommended before deploying)

GitHub is free and gives you version history + easy deploys.

1. Create a free account at https://github.com
2. Create a new repository (e.g. `radiant-store`), keep it **private** if you
   don't want the code public.
3. In this project folder, run:
   ```bash
   git init
   git add .
   git commit -m "Initial store"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/radiant-store.git
   git push -u origin main
   ```
   (GitHub shows you these exact commands when you create the repo — you
   can copy them from there instead of retyping.)

---

## 5. Deploy it live (Vercel — free, ~5 minutes)

1. Go to https://vercel.com and sign up (you can sign up with your GitHub
   account — this also makes redeploying automatic later).
2. Click **Add New → Project**, and import the `radiant-store` GitHub repo
   you just pushed.
3. Vercel auto-detects it's a Vite project. Leave the defaults and click
   **Deploy**.
4. In under a minute you'll get a live URL like
   `https://radiant-store.vercel.app` — that's a real, working, public link
   you can send to anyone right now.

**No GitHub yet?** Vercel also has a CLI you can run straight from this
folder without GitHub:
```bash
npm install -g vercel
vercel
```
Follow the prompts — it deploys directly from your computer.

*(Netlify — https://netlify.com — works almost identically if you prefer
it: "Add new site → Import from Git", same auto-detected Vite settings.)*

---

## 6. Connect your own domain name (full ownership)

1. Buy a domain from a registrar — Namecheap, GoDaddy, or Google Domains
   are common (roughly $10–15/year for a `.com`).
2. In your Vercel project, go to **Settings → Domains**, and add your
   domain (e.g. `radiantwatches.com`).
3. Vercel shows you 1–2 DNS records to add (usually an `A` record and a
   `CNAME`). Go to your domain registrar's DNS settings and add exactly
   what Vercel shows.
4. Wait 10 minutes–a few hours for DNS to propagate. Vercel will show a
   green checkmark once it's live — your store is now at your own domain,
   with free HTTPS included automatically.

You now own: the code, the GitHub repo, the hosting account, and the
domain. Nothing here depends on Claude or Anthropic to keep running.

---

## 7. Important limitation to know about (read before taking real orders)

This build saves your cart, product catalog, orders, and settings using
your **browser's local storage**. That means:

- It works great for demos, testing, and even a single-admin store where
  you always manage things from the same browser/device.
- It does **not** sync between devices — if a customer orders from their
  phone, that order will *not* appear in your admin dashboard unless
  you're using the exact same browser they used.
- Clearing browser data/cache will wipe the store's data.

**For a real store taking real customer orders**, you'll want to connect
a proper backend so all data lives in one shared place. Good, beginner-
friendly options:
- **Supabase** (https://supabase.com) — free tier, Postgres database,
  easiest to wire into this kind of app.
- **Firebase** (https://firebase.google.com) — free tier, also popular.

When you're ready for that step, tell Claude — it can help you replace
the storage layer in `App.jsx` with real Supabase/Firebase calls without
changing how the site looks or works.

---

## Quick reference

| I want to...                        | Do this |
|--------------------------------------|---------|
| Preview changes on my computer       | `npm run dev` |
| Change brand name/contact/prices     | Edit `DEFAULT_SETTINGS` / product arrays in `src/App.jsx`, or use Admin in-browser |
| Add a product photo                  | Put it in `public/images/` and reference `/images/filename.jpg` |
| Publish changes to my live site      | `git add . && git commit -m "update" && git push` (Vercel redeploys automatically) |
| Get a real shared database           | Ask Claude to help connect Supabase or Firebase |
