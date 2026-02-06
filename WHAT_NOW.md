# What to do now – get EasyIntern live

Your database (Supabase) is set up and your repo is connected to **GitHub** (`EbenezerGasonoo/Easy-Intern`). Do these in order:

---

## 1. Run migrations and seed (on your Mac)

In Terminal:

```bash
cd "/Users/macbook/Documents/Easy Intern/backend"
npx prisma migrate deploy
npx prisma db seed
```

If that works, your Supabase database has the tables and sample data.

---

## 2. Push your latest code to GitHub

```bash
cd "/Users/macbook/Documents/Easy Intern"
git add -A
git status
git commit -m "Ready for deploy"   # only if there are changes
git push origin master
```

If GitHub expects branch `main`:

```bash
git branch -M main
git push -u origin main
```

---

## 3. Deploy the backend on Vercel

1. Go to **https://vercel.com** and sign in with GitHub.
2. **Add New** → **Project** → import **Easy-Intern**.
3. Set **Root Directory** to **`backend`** (Edit → `backend` → Continue).
4. **Environment Variables** – add these:

   | Name           | Value                                                                 |
   |----------------|-----------------------------------------------------------------------|
   | `DATABASE_URL` | Copy from your `backend/.env` (the full postgresql://... pooler URL)  |
   | `JWT_SECRET`   | Any long random string (e.g. `my-super-secret-jwt-key-12345`)         |
   | `NODE_ENV`     | `production`                                                          |

5. **Deploy**.
6. When it’s done, copy your backend URL (e.g. `https://easy-intern-xxx.vercel.app`).  
   Your **API URL** is that + `/api`, e.g. `https://easy-intern-xxx.vercel.app/api`.

---

## 4. Deploy the frontend on Vercel

1. On Vercel: **Add New** → **Project** again → same repo **Easy-Intern**.
2. Set **Root Directory** to **`frontend`** (not backend).
3. **Environment Variables** – add one:

   | Name            | Value                              |
   |-----------------|------------------------------------|
   | `VITE_API_URL`  | `https://YOUR-BACKEND-URL.vercel.app/api` |

   Use the real backend URL from step 3 (e.g. `https://easy-intern-xxx.vercel.app/api`).

4. **Deploy**.
5. Open the URL Vercel gives you – that’s your live app.

---

## 5. Optional: use GitHub Pages for the frontend

- In the repo: **Settings** → **Pages** → **Source**: **GitHub Actions**.
- **Settings** → **Secrets and variables** → **Actions** → **New repository secret**:  
  Name: `VITE_API_URL`  
  Value: `https://YOUR-BACKEND-URL.vercel.app/api`
- Push a commit; the workflow will build and deploy.  
  Site: `https://ebenezergasonoo.github.io/Easy-Intern/`

---

## Quick checklist

- [ ] Run `npx prisma migrate deploy` and `npx prisma db seed` in `backend`
- [ ] Push to GitHub (`git push origin master` or `main`)
- [ ] Deploy **backend** on Vercel (root: `backend`, add `DATABASE_URL`, `JWT_SECRET`, `NODE_ENV`)
- [ ] Deploy **frontend** on Vercel (root: `frontend`, add `VITE_API_URL` = backend URL + `/api`)
- [ ] Open the frontend URL and test the app

After that, EasyIntern is live.
