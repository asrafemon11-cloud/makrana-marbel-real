# 🪨 Makrana Marble — Website

Professional business website for **Makrana Marble**, Sahi Sherpur, Murshidabad, West Bengal.

**Live features:** AI marble assistant · Search & filters · Price comparison · 35 real photos · Admin panel · WhatsApp enquiry

---

## 📁 File Structure

```
makrana-marble/
├── index.html                  ← Main website
├── admin.html                  ← Admin panel (password protected)
├── wrangler.toml               ← Cloudflare Pages config
├── .env.example                ← Netlify/Node env template
├── .dev.vars.example           ← Cloudflare local secrets template
├── .gitignore                  ← Keeps secrets out of GitHub
├── README.md                   ← This file
│
├── images/                     ← 35 real product & shop photos
│   ├── owner.jpg
│   ├── marble-000.jpg → marble-021.jpg
│   └── shop-000.jpg  → shop-011.jpg
│
├── functions/
│   └── api/
│       └── ai.js               ← Cloudflare Pages AI proxy function
│
└── netlify/
    └── functions/
        └── ai.js               ← Netlify AI proxy function
```

---

## 🐛 Bugs Fixed (v2)

All 12 bugs have been fixed in this release:

| # | Bug | Fix Applied |
|---|-----|-------------|
| 1 | `data-market` missing → "Best Savings" sort broken | Added to all 6 product cards |
| 2 | `#about` background didn't fill full width | Wrapped in full-width section |
| 3 | Price table overflowed screen on mobile | Added `overflow-x: auto` wrapper |
| 4 | `nav.scrolled` padding wrong on mobile | Added `nav.scrolled` to 900px breakpoint |
| 5 | `div#about` skipped by `section` responsive rule | Added `#about` to both 900px & 600px rules |
| 6 | Contact form sent `alert()` instead of WhatsApp | Replaced with `submitEnquiry()` → WhatsApp |
| 7 | Footer missing Pricing & Gallery links | Added all nav links to footer |
| 8 | Stale `⚠️ REPLACE THIS KEY` comment in code | Removed |
| 9 | `applyText()` only synced 4 of 10 admin fields | Extended to sync all fields incl. contact, stats |
| 10 | No `<meta>` description or Open Graph tags | Added full SEO + OG meta tags |
| 11 | AI fetch didn't check `res.ok` | Added `res.ok` check with friendly error message |
| 12 | No `wrangler.toml` for local Cloudflare dev | Created `wrangler.toml` + `.dev.vars.example` |

---

## 🖥️ Running Locally

### Option A — Simple (No AI, no server needed)

1. Unzip `makrana-marble-website.zip`
2. Double-click `index.html`

Opens in your browser instantly. All features work **except** the AI chat (which needs a server).

---

### Option B — Full Local Dev with AI (Cloudflare Wrangler)

This runs the full site including the AI assistant on your computer.

**Step 1 — Install Node.js**

Download from https://nodejs.org (choose LTS version) and install.

Verify it worked — open Command Prompt or Terminal and type:
```
node -v
```
You should see something like `v20.10.0`

**Step 2 — Open the project folder in terminal**

Windows: Open the unzipped folder → right-click empty space → "Open in Terminal"
Mac: Drag the folder to Terminal, or right-click → "New Terminal at Folder"

**Step 3 — Install Wrangler (Cloudflare's dev tool)**

```bash
npm install -g wrangler
```

**Step 4 — Create your local secrets file**

Copy `.dev.vars.example` to `.dev.vars`:

```bash
# Windows
copy .dev.vars.example .dev.vars

# Mac / Linux
cp .dev.vars.example .dev.vars
```

Then open `.dev.vars` in Notepad/TextEdit and replace `your_gemini_api_key_here` with your real key from https://aistudio.google.com/app/apikey

**Step 5 — Start the local server**

```bash
npx wrangler pages dev .
```

It will print something like:
```
✨ Success! Your site is available at http://localhost:8788
```

Open http://localhost:8788 in your browser. The AI assistant will work! 🎉

**Step 6 — Stop the server**

Press `Ctrl + C` in the terminal window.

---

## 🚀 Publishing to Cloudflare Pages (Free)

Cloudflare Pages is **free**, fast, and perfect for India users.  
Your site URL will be: `https://makrana-marble.pages.dev`

---

### Step 1 — Create Accounts

- GitHub: https://github.com (free sign-up)
- Cloudflare: https://dash.cloudflare.com (free sign-up)

---

### Step 2 — Push Project to GitHub

**If you have Git installed:**

```bash
cd makrana-marble
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/makrana-marble.git
git push -u origin main
```

**If you don't have Git (easier method):**

1. Go to https://github.com → New repository → name it `makrana-marble` → Private → Create
2. Click **uploading an existing file** on the empty repo page
3. Drag ALL files and folders from the unzipped folder into the browser window
4. Click **Commit changes**

> ⚠️ Do NOT upload `.env` or `.dev.vars` — those contain your secret keys

---

### Step 3 — Connect to Cloudflare Pages

1. Log into https://dash.cloudflare.com
2. Left sidebar → **Workers & Pages** → **Create application**
3. Click **Pages** tab → **Connect to Git**
4. Click **GitHub** → Authorize Cloudflare → Select your `makrana-marble` repo
5. **Build settings:**
   - Build command: *(leave blank)*
   - Build output directory: `/` *(root)*
6. Click **Save and Deploy**

Your site deploys in about 60 seconds!

---

### Step 4 — Add Your Gemini API Key

This activates the AI marble assistant on your live site.

1. In Cloudflare → Workers & Pages → `makrana-marble`
2. Click **Settings** → **Environment variables**
3. Under **Production**, click **Add variable**
   - Variable name: `GEMINI_API_KEY`
   - Value: your Gemini key from aistudio.google.com
   - Click **Encrypt** (hides it in the UI)
4. Click **Save**
5. Go to **Deployments** tab → **Retry deployment** (or push a new commit)

---

### Step 5 — (Optional) Use a Custom Domain

Example: `www.makranamarblesherpur.com`

1. Buy a domain at GoDaddy.com or Namecheap.com (~₹600–800/year)
2. In Cloudflare → your Pages project → **Custom domains** → **Set up a custom domain**
3. Enter your domain name and follow the steps
4. Cloudflare gives you **free HTTPS** automatically

---

### Step 6 — Future Updates

Every time you push a change to GitHub, Cloudflare redeploys automatically.

To update the website (e.g., after editing `index.html`):

```bash
git add .
git commit -m "Updated pricing"
git push
```

Cloudflare picks it up in ~30 seconds. ✅

---

## ⚙️ Admin Panel

Access at: `https://your-site.pages.dev/admin.html`

**Default password: `marble2025`** ← Change this immediately!

| Tab | What you can edit |
|---|---|
| 💰 Pricing | Add/remove marble types, set market price → our price auto-calculates 10% lower |
| 🖼️ Gallery | Upload photos from phone or computer |
| 🏠 Hero | Main title and tagline |
| 📖 About | Shop description, stats |
| 📞 Contact | Phone, address, WhatsApp, hours |
| 🔒 Password | Change admin password |

**Tip:** Press `Ctrl+S` (Windows) or `Cmd+S` (Mac) to save from any tab.

All changes are stored in the browser's local storage and show on the site immediately.

---

## 🔐 Security Checklist

| Item | Status |
|---|---|
| Gemini API key never in source code | ✅ |
| `.env` / `.dev.vars` blocked from GitHub | ✅ via `.gitignore` |
| Admin panel password protected | ✅ |
| HTTPS on live site | ✅ auto-enabled by Cloudflare |
| WhatsApp enquiry (no backend needed) | ✅ |

**After going live — rotate any previously shared keys:**

| Key | Rotate at |
|---|---|
| Gemini | https://aistudio.google.com/app/apikey |
| OpenAI | https://platform.openai.com/api-keys |
| OpenRouter | https://openrouter.ai/settings/keys |

---

## 🛟 Troubleshooting

| Problem | Solution |
|---|---|
| Images not showing | Make sure `images/` folder is in the same directory as `index.html` |
| AI chat says "unavailable" | Add `GEMINI_API_KEY` in Cloudflare env vars and redeploy |
| AI chat works locally but not live | Check the env var is set for **Production** (not just Preview) |
| Admin password not working | Default is `marble2025` — check for typos |
| Wrangler command not found | Run `npm install -g wrangler` first |
| `git` command not found | Download from https://git-scm.com and install |
| Site not updating after push | Go to Cloudflare → Deployments — check if build failed |
| Custom domain not working | DNS changes take up to 24 hours to propagate |

---

## 📞 Shop

**Makrana Marble**
Sherpur to Rampurhat Road, Vill & P.O. – Sahi Sherpur
P.S. – Khargram, Murshidabad, West Bengal – 742159
📞 +91 76993 83308 · Mon–Sat: 9:00 AM – 7:00 PM

---

Built with Claude AI (claude.ai) | Photos © Makrana Marble
