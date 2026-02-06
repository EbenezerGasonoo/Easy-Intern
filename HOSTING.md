# Host EasyIntern – Step-by-step

Follow these steps to get EasyIntern live on the internet.

---

## What you’ll use

| Part       | Where it runs | Service (free tier) |
|-----------|----------------|----------------------|
| Frontend  | Static files   | Vercel or GitHub Pages |
| Backend   | Node.js server | Vercel or Railway     |
| Database  | PostgreSQL     | Supabase or Neon      |

---

## Step 1: Push your code to GitHub

1. Create a new repo: [github.com/new](https://github.com/new)  
   - Name: `Easy-Intern` (or any name)  
   - Do **not** add a README (you already have one).

2. In your project folder, run (replace `YOUR_USERNAME` with your GitHub username):

```bash
cd "/Users/macbook/Documents/Easy Intern"
git remote add origin https://github.com/YOUR_USERNAME/Easy-Intern.git
git branch -M main
git push -u origin main
```

---

## Step 2: Create a database (PostgreSQL)

1. Go to [supabase.com](https://supabase.com) and sign up.
2. **New project** → choose a name and password → Create.
3. Open **Settings** → **Database**.
4. Under **Connection string** choose **URI** and copy it.  
   It looks like:  
   `postgresql://postgres.xxxx:YOUR_PASSWORD@aws-0-region.pooler.supabase.com:6543/postgres`
5. Replace `YOUR_PASSWORD` with your database password and keep this URI for the next step.

---

## Step 3: Deploy the backend (Vercel)

1. Go to [vercel.com](https://vercel.com) and sign in with GitHub.
2. **Add New** → **Project** → import the **Easy-Intern** repo.
3. **Configure:**
   - **Root Directory:** click **Edit** → set to `backend` → **Continue**.
   - **Build Command:** `npm run build` (or leave default if it runs `npm run build`).
   - **Output Directory:** leave default.
   - **Install Command:** `npm install`.
4. **Environment variables** – add these (Replace values with your own):

   | Name           | Value                                      |
   |----------------|--------------------------------------------|
   | `DATABASE_URL` | Your Supabase connection string from Step 2 |
   | `JWT_SECRET`   | Long random string (e.g. 32+ characters)   |
   | `NODE_ENV`     | `production`                               |

5. Click **Deploy**.
6. When it’s done, open your backend URL, e.g. `https://easy-intern-xxxx.vercel.app`.  
   Copy this **full URL** (e.g. `https://easy-intern-xxxx.vercel.app`) for the frontend.

---

## Step 4: Run database migrations

You need to apply Prisma migrations and (optionally) seed data.

**Option A – From your Mac (easiest):**

1. In `backend` folder create/update `.env` with the same `DATABASE_URL` you used on Vercel.
2. Run:

```bash
cd backend
npm install
npx prisma migrate deploy
npx prisma db seed
```

**Option B – From Vercel (build hook):**  
You can later add a custom build command that runs `prisma migrate deploy` if you want migrations to run on every deploy. For the first time, Option A is simpler.

---

## Step 5: Deploy the frontend

### Option A: Vercel (recommended – one place for frontend + backend)

1. In Vercel, **Add New** → **Project** again.
2. Import the **same** Easy-Intern repo.
3. **Configure:**
   - **Root Directory:** set to `frontend` (not `backend`).
   - **Build Command:** `npm run build`.
   - **Output Directory:** `dist`.
4. **Environment variable:**
   - Name: `VITE_API_URL`  
   - Value: `https://your-backend-url.vercel.app/api`  
   (Use the backend URL from Step 3 and add `/api` at the end.)
5. **Deploy**.

Your app will be at the URL Vercel gives you (e.g. `https://easy-intern-frontend.vercel.app`).

### Option B: GitHub Pages

1. In your GitHub repo go to **Settings** → **Pages**.
2. Under **Source** choose **GitHub Actions**.
3. Add a repository secret:  
   **Settings** → **Secrets and variables** → **Actions** → **New repository secret**  
   - Name: `VITE_API_URL`  
   - Value: `https://your-backend-url.vercel.app/api`
4. Push a commit (or re-run the workflow). The workflow in `.github/workflows/deploy-pages.yml` will build and deploy the frontend.

Your site will be at: `https://YOUR_USERNAME.github.io/Easy-Intern/`  
(Replace `YOUR_USERNAME` and repo name if different.)

---

## Step 6: CORS

The backend is already set to accept requests from any origin (`cors()` with no options). If your API calls work from the deployed frontend, you don’t need to change anything. If you later want to restrict which sites can call your API, you can configure CORS in `backend/src/server.js`.

---

## Checklist

- [ ] Code pushed to GitHub
- [ ] Supabase project created and `DATABASE_URL` copied
- [ ] Backend deployed on Vercel with `DATABASE_URL`, `JWT_SECRET`, `NODE_ENV`
- [ ] Migrations (and seed) run against the hosted database
- [ ] Frontend deployed (Vercel or GitHub Pages) with `VITE_API_URL` set to `https://your-backend.vercel.app/api`
- [ ] CORS on backend updated with your frontend URL(s)

---

## If something doesn’t work

- **“Network error” or API not loading**  
  Check `VITE_API_URL`: it must be exactly your backend URL + `/api`, and the backend must be deployed and healthy.

- **“Invalid credentials” or auth errors**  
  Make sure `JWT_SECRET` is the same whenever you restart/redeploy the backend and that the database has been migrated.

- **Blank page on GitHub Pages**  
  Confirm in repo **Settings** → **Pages** that the source is **GitHub Actions** and that the last workflow run succeeded. Check that `VITE_API_URL` is set in repo secrets.

- **Database connection errors**  
  Use the **Connection string** from Supabase (URI). Ensure the password in the URI is correct and that you’re using the **pooler** port (e.g. 6543) if Supabase shows one.

Once these steps are done, your app is hosted and reachable at your frontend URL.
