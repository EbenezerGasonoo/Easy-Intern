# 🚀 Quick Start: Deploy to GitHub

## Yes, you can deploy on GitHub! Here's how:

### Frontend → GitHub Pages ✅
### Backend → Vercel/Railway (Free) ✅

---

## Step-by-Step Guide

### 1️⃣ Create GitHub Repository

1. Go to [github.com](https://github.com) and sign in
2. Click the **+** icon → **New repository**
3. Name it: `Easy-Intern`
4. **Don't** check "Initialize with README"
5. Click **Create repository**

### 2️⃣ Push Your Code

Run these commands:

```bash
cd "/Users/macbook/Documents/Easy Intern"
git remote add origin https://github.com/YOUR_USERNAME/Easy-Intern.git
git branch -M main
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username!

### 3️⃣ Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages**
3. Under "Source", select **GitHub Actions**
4. Save!

The frontend will auto-deploy on every push! 🎉

### 4️⃣ Deploy Backend (Required!)

GitHub Pages can't run Node.js, so deploy backend separately:

#### Option A: Vercel (Easiest - 2 minutes)

1. Go to [vercel.com](https://vercel.com)
2. Sign up with GitHub
3. Click **Add New** → **Project**
4. Import your `Easy-Intern` repository
5. **Important**: Set **Root Directory** to `backend`
6. Add Environment Variables:
   ```
   DATABASE_URL=your_postgres_connection_string
   JWT_SECRET=any_random_string_here
   NODE_ENV=production
   ```
7. Click **Deploy**

#### Option B: Railway (Also Free)

1. Go to [railway.app](https://railway.app)
2. Sign up with GitHub
3. **New Project** → **Deploy from GitHub repo**
4. Select your repo
5. Add PostgreSQL service
6. Set root directory to `backend`
7. Add environment variables
8. Deploy!

### 5️⃣ Get a Free Database

You need PostgreSQL. Free options:

**Supabase** (Recommended):
1. Go to [supabase.com](https://supabase.com)
2. Create account → New project
3. Go to **Settings** → **Database**
4. Copy the connection string
5. Use it as `DATABASE_URL` in Vercel/Railway

**Neon.tech**:
1. Go to [neon.tech](https://neon.tech)
2. Create free database
3. Copy connection string

### 6️⃣ Run Database Migrations

After setting up database, connect and run:

```bash
cd backend
npm run prisma:migrate deploy
npm run prisma:seed
```

Or use Railway's CLI or Vercel's build command.

### 7️⃣ Update Frontend API URL

After backend is deployed:

1. Get your backend URL (e.g., `https://easyintern-backend.vercel.app`)
2. In GitHub repo: **Settings** → **Secrets and variables** → **Actions**
3. Add secret: `API_URL` = `https://your-backend-url.vercel.app/api`
4. Push a new commit to trigger rebuild

Or update `frontend/vite.config.js` manually.

---

## Your URLs Will Be:

- **Frontend**: `https://YOUR_USERNAME.github.io/Easy-Intern/`
- **Backend**: `https://your-backend.vercel.app` (or Railway URL)

---

## Quick Commands Summary

```bash
# Push to GitHub
git remote add origin https://github.com/YOUR_USERNAME/Easy-Intern.git
git push -u origin main

# Deploy backend to Vercel (after installing Vercel CLI)
cd backend
vercel --prod
```

---

## Need Help?

- Check `DEPLOY_GITHUB.md` for detailed instructions
- Check `DEPLOYMENT.md` for other hosting options
- GitHub Pages docs: https://docs.github.com/en/pages

---

**That's it! Your app will be live on GitHub Pages! 🎉**
