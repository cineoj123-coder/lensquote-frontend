# 📷 LensQuote — GitHub Pages + Koyeb Deployment Guide
## 100% Free · No Credit Card Required

---

## 📁 Project Structure

You have **2 separate repositories** to create:

```
lensquote-backend/        ← Deploy to Koyeb (free backend)
├── server.js
├── package.json
├── Procfile
└── .gitignore

lensquote-frontend/       ← Deploy to GitHub Pages (free frontend)
├── index.html
└── .gitignore
```

---

## STEP 1 — Deploy the Backend to Koyeb (FREE)

### 1.1 Create GitHub repo for backend

1. Go to **github.com** → click **"New repository"**
2. Name it: `lensquote-backend`
3. Set to **Public** → click **"Create repository"**
4. Upload all files from the `lensquote-backend/` folder

   **Using GitHub web upload:**
   - Click "uploading an existing file"
   - Drag & drop: `server.js`, `package.json`, `Procfile`, `.gitignore`
   - Click "Commit changes"

### 1.2 Deploy to Koyeb

1. Go to **app.koyeb.com** → Sign up with GitHub (free, no card)
2. Click **"Create App"**
3. Choose **"GitHub"** as source
4. Select your `lensquote-backend` repo
5. Koyeb auto-detects Node.js ✅
6. Set **Environment Variables** (click "Add Variable"):
   ```
   ADMIN_USER   =   admin
   ADMIN_PASS   =   YourStrongPassword123!
   ```
7. Click **"Deploy"**
8. Wait ~2 minutes — you'll get a URL like:
   ```
   https://lensquote-backend-xxxx.koyeb.app
   ```
   **Copy this URL — you need it in Step 2!**

---

## STEP 2 — Deploy Frontend to GitHub Pages (FREE)

### 2.1 Edit the frontend file

Open `lensquote-frontend/index.html` and find these two lines near the top of the `<script>` section:

```javascript
// Line 1 — Paste your Koyeb URL here:
let API_BASE_URL = localStorage.getItem('apiUrl') || "YOUR_KOYEB_URL_HERE";

// Line 2 — Change to your WhatsApp number (country code + number):
const ADMIN_PHONE = "919876543210";
```

Replace:
- `YOUR_KOYEB_URL_HERE` → your actual Koyeb URL (e.g., `https://lensquote-xxxx.koyeb.app`)
- `919876543210` → your WhatsApp number (91 = India country code + 10 digit number)

### 2.2 Create GitHub repo for frontend

1. Go to **github.com** → click **"New repository"**
2. Name it: `lensquote` (or anything you like)
3. Set to **Public** → click **"Create repository"**
4. Upload `index.html` and `.gitignore`

### 2.3 Enable GitHub Pages

1. In your frontend repo → go to **Settings**
2. Click **"Pages"** in the left sidebar
3. Under "Source" → select **"Deploy from a branch"**
4. Branch: **main** | Folder: **/ (root)**
5. Click **Save**
6. Wait ~1 minute — your site will be live at:
   ```
   https://YOUR-GITHUB-USERNAME.github.io/lensquote/
   ```

---

## STEP 3 — Connect Frontend to Backend (CORS)

In your **Koyeb dashboard**:
1. Go to your app → **Settings → Environment Variables**
2. Add one more variable:
   ```
   FRONTEND_URL = https://YOUR-GITHUB-USERNAME.github.io
   ```
3. Koyeb will auto-redeploy

This allows your GitHub Pages site to call your Koyeb API securely. ✅

---

## ✅ Final Checklist

- [ ] Backend live on Koyeb (`/` returns `{"status":"ok"}`)
- [ ] `API_BASE_URL` updated in `index.html` with Koyeb URL
- [ ] `ADMIN_PHONE` updated with your WhatsApp number
- [ ] `ADMIN_PASS` changed from default
- [ ] Frontend live on GitHub Pages
- [ ] `FRONTEND_URL` set in Koyeb env vars

---

## 🔑 Admin Panel Access

Go to your GitHub Pages URL → click **"Admin"** in header

Default credentials:
```
Username: admin
Password: photo@admin123   ← Change this in Koyeb env vars!
```

---

## 💡 Tips

**Testing locally:**
```bash
# Terminal 1 — backend
cd lensquote-backend
npm install
mkdir data
node server.js
# → http://localhost:3000

# Open lensquote-frontend/index.html in browser
# Enter http://localhost:3000 in the API URL banner
```

**If Koyeb app goes to sleep:**
- Free tier apps may sleep after inactivity
- First request after sleep takes ~10 seconds
- Upgrade to hobby plan ($0/month with free credits) to prevent this

**Updating prices:**
- Log into admin panel → Pricing tab → change values → Save

**WhatsApp not working:**
- Ensure `ADMIN_PHONE` format: no `+`, no spaces, country code first
- India: `91` + 10 digit number = 12 digits total

---

## 📞 Support
If you face issues, check:
1. Koyeb logs (App → Deployments → Logs)
2. Browser console (F12 → Console tab) for frontend errors
3. Make sure `FRONTEND_URL` in Koyeb matches your GitHub Pages URL exactly
