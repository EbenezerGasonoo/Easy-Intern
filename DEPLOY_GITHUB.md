# Deploy EasyIntern on GitHub

## Step 1: Push Code to GitHub

1. **Create a new repository on GitHub:**
   - Go to [github.com](https://github.com)
   - Click "New repository"
   - Name it: `Easy-Intern` (or your preferred name)
   - **Don't** initialize with README (we already have one)
   - Click "Create repository"

2. **Push your code:**
   ```bash
   cd "/Users/macbook/Documents/Easy Intern"
   git remote add origin https://github.com/YOUR_USERNAME/Easy-Intern.git
   git branch -M main
   git push -u origin main
   ```

## Step 2: Deploy Frontend to GitHub Pages

### Option A: Using GitHub Actions (Automatic)

1. The workflow file is already created at `.github/workflows/deploy.yml`
2. Go to your GitHub repository
3. Go to **Settings** → **Pages**
4. Under "Source", select **GitHub Actions**
5. The frontend will auto-deploy on every push to main branch

### Option B: Manual Deploy

1. Build the frontend:
   ```bash
   cd frontend
   npm install
   npm run build
   ```

2. Go to repository **Settings** → **Pages**
3. Select **Deploy from a branch**
4. Choose `gh-pages` branch and `/root` folder
5. Push the dist folder:
   ```bash
   git subtree push --prefix frontend/dist origin gh-pages
   ```

## Step 3: Deploy Backend (Required!)

GitHub Pages **cannot** host Node.js backends. You need a separate service:

### Recommended: Vercel (Free & Easy)

1. Go to [vercel.com](https://vercel.com)
2. Sign up with GitHub
3. Click "New Project"
4. Import your `Easy-Intern` repository
5. Set **Root Directory** to `backend`
6. Add environment variables:
   - `DATABASE_URL` - Your PostgreSQL connection string
   - `JWT_SECRET` - A random secret key
   - `NODE_ENV` - `production`
7. Click "Deploy"

### Alternative: Railway (Also Free)

1. Go to [railway.app](https://railway.app)
2. Sign up with GitHub
3. Create new project
4. Add PostgreSQL service
5. Add Node.js service → Connect GitHub repo
6. Set root directory to `backend`
7. Add environment variables
8. Deploy!

## Step 4: Update Frontend API URL

After deploying backend, update the API URL:

1. In your GitHub repo, go to **Settings** → **Secrets and variables** → **Actions**
2. Add a new secret:
   - Name: `API_URL`
   - Value: `https://your-backend-url.vercel.app/api` (or your Railway URL)

Or manually update `frontend/vite.config.js`:
```javascript
baseURL: 'https://your-backend-url.vercel.app/api'
```

## Step 5: Set Up Database

You need a PostgreSQL database:

### Free Options:
1. **Supabase** (Recommended):
   - Go to [supabase.com](https://supabase.com)
   - Create free project
   - Get connection string from Settings → Database
   - Use it as `DATABASE_URL`

2. **Neon.tech**:
   - Go to [neon.tech](https://neon.tech)
   - Create free database
   - Copy connection string

3. **Railway PostgreSQL**:
   - If using Railway, add PostgreSQL service
   - Connection string is auto-provided

### Run Migrations:

After setting up database, run:
```bash
cd backend
npm run prisma:migrate deploy
npm run prisma:seed
```

## Final URLs

- **Frontend**: `https://YOUR_USERNAME.github.io/Easy-Intern/`
- **Backend**: `https://your-backend-url.vercel.app` (or Railway URL)

## Troubleshooting

### Frontend not loading?
- Check if base path in `vite.config.js` matches your repo name
- Ensure GitHub Pages is enabled in Settings

### API calls failing?
- Check CORS settings in backend
- Verify API URL is correct
- Check browser console for errors

### Database connection issues?
- Verify `DATABASE_URL` is correct
- Check if database allows connections from your hosting IP
- Run migrations: `npm run prisma:migrate deploy`

## Quick Deploy Commands

```bash
# 1. Push to GitHub
git add .
git commit -m "Ready for deployment"
git push origin main

# 2. Build frontend locally (optional)
cd frontend
npm run build

# 3. Deploy backend to Vercel
cd backend
vercel --prod
```

Your app will be live! 🚀
