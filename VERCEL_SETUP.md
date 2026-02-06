# Set up Vercel – step by step

Do this after your Supabase database has tables and seed data.

---

## 1. Open Vercel

Go to **https://vercel.com** and sign in with **GitHub**.

---

## 2. Deploy the **backend** first

1. Click **Add New** → **Project**.
2. Import the **Easy-Intern** repo (from GitHub).
3. **Root Directory:** click **Edit** → type `backend` → **Continue**.
4. **Environment Variables** – add these (click "Add" for each):

   | Name           | Value |
   |----------------|--------|
   | `DATABASE_URL` | Paste from your `backend/.env` (must end with `?pgbouncer=true`) |
   | `JWT_SECRET`   | Any long random string, e.g. `easyintern-jwt-secret-2024-xyz` |
   | `NODE_ENV`     | `production` |

5. Click **Deploy**.
6. Wait for the build to finish. Then copy your **backend URL** (e.g. `https://easy-intern-abc123.vercel.app`).  
   You’ll need: **API URL** = backend URL + `/api`  
   Example: `https://easy-intern-abc123.vercel.app/api`

---

## 3. Deploy the **frontend**

1. On Vercel, click **Add New** → **Project** again.
2. Select the **same** repo **Easy-Intern**.
3. **Root Directory:** click **Edit** → type `frontend` → **Continue**.
4. **Environment Variables** – add one:

   | Name            | Value |
   |-----------------|--------|
   | `VITE_API_URL`  | `https://YOUR-BACKEND-URL.vercel.app/api` |

   Replace `YOUR-BACKEND-URL` with the real backend URL from step 2 (e.g. `https://easy-intern-abc123.vercel.app/api`).

5. Click **Deploy**.
6. When it’s done, open the URL Vercel shows for this project. That’s your live EasyIntern app.

---

## Checklist

- [ ] Backend project on Vercel (root: `backend`), with `DATABASE_URL`, `JWT_SECRET`, `NODE_ENV`.
- [ ] Frontend project on Vercel (root: `frontend`), with `VITE_API_URL` = backend URL + `/api`.
- [ ] Open frontend URL and test: browse interns/jobs, then log in (e.g. `kwame.mensah@knust.edu.gh` / `password123`).

If anything fails to build, check the build logs on Vercel and that all env vars are set correctly.
