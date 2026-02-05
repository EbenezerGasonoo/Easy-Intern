# Deployment Guide for EasyIntern

## Quick Deploy Options

### Option 1: Vercel (Recommended - Easiest)

#### Frontend Deployment:
1. Install Vercel CLI: `npm i -g vercel`
2. Navigate to frontend: `cd frontend`
3. Run: `vercel`
4. Follow prompts to deploy

#### Backend Deployment:
1. Navigate to backend: `cd backend`
2. Run: `vercel`
3. Add environment variables in Vercel dashboard:
   - `DATABASE_URL` - Your PostgreSQL connection string
   - `JWT_SECRET` - Your JWT secret key
   - `PORT` - (optional, defaults to 5000)

### Option 2: Railway (Great for Full-Stack)

1. Go to [railway.app](https://railway.app)
2. Create new project
3. Add PostgreSQL service
4. Add Node.js service for backend
5. Add Node.js service for frontend
6. Set environment variables
7. Deploy!

### Option 3: Render

#### Backend:
1. Go to [render.com](https://render.com)
2. Create new Web Service
3. Connect your GitHub repo
4. Set build command: `cd backend && npm install && npm run prisma:generate`
5. Set start command: `cd backend && npm start`
6. Add environment variables

#### Frontend:
1. Create new Static Site
2. Connect GitHub repo
3. Set build command: `cd frontend && npm install && npm run build`
4. Set publish directory: `frontend/dist`

### Option 4: Heroku

#### Backend:
```bash
cd backend
heroku create easyintern-backend
heroku addons:create heroku-postgresql:hobby-dev
heroku config:set JWT_SECRET=your-secret-key
git push heroku main
```

#### Frontend:
```bash
cd frontend
npm run build
# Use static hosting like Netlify or Vercel for frontend
```

## Environment Variables Needed

### Backend:
- `DATABASE_URL` - PostgreSQL connection string
- `JWT_SECRET` - Secret key for JWT tokens
- `PORT` - Server port (default: 5000)
- `NODE_ENV` - Environment (production/development)

### Frontend:
- Update API URL in `vite.config.js` or use environment variables

## Database Setup

1. Create PostgreSQL database (Railway, Supabase, or Neon.tech)
2. Get connection string
3. Run migrations:
```bash
cd backend
npm run prisma:migrate deploy
npm run prisma:seed
```

## Post-Deployment Checklist

- [ ] Database migrations run successfully
- [ ] Environment variables set correctly
- [ ] Frontend API URL points to backend
- [ ] CORS configured correctly
- [ ] Test registration/login
- [ ] Test job posting
- [ ] Test application flow

## Recommended Free Hosting:

- **Frontend**: Vercel, Netlify (Free tier)
- **Backend**: Railway, Render (Free tier)
- **Database**: Supabase, Neon.tech (Free tier)

## Quick Deploy Script

For Vercel:
```bash
# Backend
cd backend && vercel --prod

# Frontend  
cd frontend && vercel --prod
```

For Railway:
```bash
# Install Railway CLI
npm i -g @railway/cli

# Login
railway login

# Deploy
railway up
```
