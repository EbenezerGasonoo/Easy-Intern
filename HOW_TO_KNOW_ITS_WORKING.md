# How to know EasyIntern is working

Use these checks in order.

---

## 1. Database (Supabase)

**Migrations ran OK if you saw:**
```text
X migrations have been successfully applied.
```

**Seed ran OK if you saw:**
```text
✅ Created company: MTN Ghana
✅ Created intern: Kwame Mensah
…
🎉 Seeding completed successfully!
```

**Or check in Supabase:**  
Go to [supabase.com](https://supabase.com) → your project → **Table Editor**. You should see tables: `users`, `companies`, `interns`, `jobs`, `applications`, and rows inside them (after seed).

---

## 2. Backend (local)

In Terminal:

```bash
cd "/Users/macbook/Documents/Easy Intern/backend"
npm run dev
```

You should see: `Server running on port 5001` (or 5000).

Then in a browser open: **http://localhost:5001/api/health**

You should see:
```json
{"status":"ok","message":"EasyIntern API is running"}
```

If you see that → backend is working and talking to the app.

---

## 3. Frontend (local)

In a **new** Terminal:

```bash
cd "/Users/macbook/Documents/Easy Intern/frontend"
npm run dev
```

Open: **http://localhost:3000**

- Homepage loads with interns/jobs (or “No interns yet”).
- Click **Login** → use an intern email from the seed (e.g. `kwame.mensah@knust.edu.gh` / password `password123`) → you should land on the intern dashboard.

If that works → frontend + backend + database are all working together.

---

## 4. Backend (deployed on Vercel)

Open in the browser:

**https://YOUR-BACKEND-URL.vercel.app/api/health**

(Use your real Vercel backend URL.)

You should see the same JSON:
```json
{"status":"ok","message":"EasyIntern API is running"}
```

If you see that → deployed backend is working.

---

## 5. Frontend (deployed on Vercel or GitHub Pages)

Open your live frontend URL (e.g. `https://easy-intern-xxx.vercel.app` or `https://ebenezergasonoo.github.io/Easy-Intern/`).

- Homepage loads.
- You can open **Browse Interns** / **Browse Jobs**.
- **Login** with `kwame.mensah@knust.edu.gh` / `password123` works.

If that works → the full app is working in production.

---

## Quick checklist

| Check | How |
|-------|-----|
| DB | Supabase Table Editor has tables + data, or `prisma migrate deploy` + `prisma db seed` finished without errors |
| Backend local | `npm run dev` in backend → open http://localhost:5001/api/health → see `"status":"ok"` |
| Frontend local | `npm run dev` in frontend → open http://localhost:3000 → can browse and log in |
| Backend live | Open https://YOUR-API.vercel.app/api/health → see `"status":"ok"` |
| Frontend live | Open your app URL → can browse and log in |

If all of these pass, everything is working.
