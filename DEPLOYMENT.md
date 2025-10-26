# 🚀 Deployment Guide - Vercel (Frontend) + Render (Backend)

This guide will help you deploy your Employer Feedback Sentiment Analysis application to the internet for free!

## 📋 Prerequisites

Before you start, make sure you have:
- ✅ A GitHub account (create one at https://github.com)
- ✅ Your Gemini API key (from https://aistudio.google.com/app/apikey)
- ✅ Git installed on your computer

---

## 🔄 Step 1: Push Your Code to GitHub

### 1.1 Initialize Git Repository (if not already done)

```bash
cd "d:\final project api"
git init
git add .
git commit -m "Initial commit - ready for deployment"
```

### 1.2 Create a New Repository on GitHub

1. Go to https://github.com/new
2. Name your repository (e.g., `feedback-sentiment-analysis`)
3. Make it **Public** or **Private** (both work)
4. **DO NOT** initialize with README (you already have one)
5. Click "Create repository"

### 1.3 Push Your Code

```bash
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git branch -M main
git push -u origin main
```

---

## 🖥️ Step 2: Deploy Backend to Render

### 2.1 Create Render Account

1. Go to https://render.com
2. Click "Get Started for Free"
3. Sign up with GitHub (recommended)

### 2.2 Create PostgreSQL Database

1. Click "New +" → "PostgreSQL"
2. Configure:
   - **Name**: `feedback-db` (or any name you like)
   - **Database**: `feedback_db`
   - **User**: `feedback_user` (auto-generated)
   - **Region**: Choose closest to you
   - **Plan**: **Free** ✅
3. Click "Create Database"
4. **IMPORTANT**: Copy the **Internal Database URL** (you'll need this soon)

### 2.3 Deploy Backend Web Service

1. Click "New +" → "Web Service"
2. Connect your GitHub repository
3. Configure the web service:
   - **Name**: `feedback-backend` (or any name)
   - **Region**: Same as your database
   - **Branch**: `main`
   - **Root Directory**: `backend`
   - **Runtime**: `Python 3`
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `gunicorn app:app`
   - **Plan**: **Free** ✅

4. **Add Environment Variables** (click "Advanced" → "Add Environment Variable"):

   ```
   DATABASE_URL = [Paste the Internal Database URL from step 2.4]
   GEMINI_API_KEY = your_gemini_api_key_here
   LLM_PROVIDER = gemini
   GEMINI_MODEL = gemini-2.0-flash
   FLASK_ENV = production
   FRONTEND_URL = https://your-app-name.vercel.app
   ```
   
   **Note**: You'll update `FRONTEND_URL` after deploying the frontend in Step 3

5. Click "Create Web Service"
6. Wait 5-10 minutes for deployment to complete
7. **Copy your backend URL** (e.g., `https://feedback-backend.onrender.com`)

### 2.4 Download TextBlob Corpora (One-time Setup)

After your backend deploys successfully:

1. Go to your Render dashboard → Select your backend service
2. Click "Shell" tab (bottom of page)
3. Run this command in the shell:
   ```bash
   python -m textblob.download_corpora
   ```
4. Wait for it to complete (about 1 minute)
5. This only needs to be done once!

---

## 🌐 Step 3: Deploy Frontend to Vercel

### 3.1 Create Vercel Account

1. Go to https://vercel.com
2. Click "Sign Up"
3. Sign up with GitHub (recommended)

### 3.2 Import Your Project

1. Click "Add New..." → "Project"
2. Import your GitHub repository
3. Vercel will auto-detect it's a React app

### 3.3 Configure Build Settings

1. **Framework Preset**: Create React App (should auto-detect)
2. **Root Directory**: `frontend`
3. **Build Command**: `npm run build`
4. **Output Directory**: `build`

### 3.4 Add Environment Variables

Click "Environment Variables" and add:

```
REACT_APP_API_URL = https://your-backend-url.onrender.com
```

Replace `your-backend-url.onrender.com` with the URL from Step 2.3 (step 7)

### 3.5 Deploy

1. Click "Deploy"
2. Wait 2-5 minutes for deployment
3. You'll get a URL like: `https://your-app.vercel.app`

---

## 🔧 Step 4: Update Backend with Frontend URL

1. Go back to Render dashboard
2. Click on your backend service
3. Go to "Environment" tab
4. Find `FRONTEND_URL` and update it to your Vercel URL:
   ```
   FRONTEND_URL = https://your-app.vercel.app
   ```
5. Click "Save Changes"
6. Your backend will automatically redeploy

---

## ✅ Step 5: Test Your Deployment

1. Open your Vercel URL: `https://your-app.vercel.app`
2. Try submitting feedback
3. Check if sentiment analysis works
4. Verify AI suggestions are generated
5. Test the dashboard and charts

---

## 🎉 You're Live!

Your application is now accessible worldwide! Share your Vercel URL with anyone.

**Your URLs:**
- Frontend: `https://your-app.vercel.app`
- Backend API: `https://your-backend.onrender.com`

---

## 🔄 Making Updates

Whenever you make changes to your code:

```bash
git add .
git commit -m "Description of changes"
git push
```

- Vercel will **automatically redeploy** your frontend
- Render will **automatically redeploy** your backend

---

## 💡 Important Notes

### Free Tier Limitations

**Render Free Tier:**
- ✅ 750 hours/month (enough for 24/7)
- ⚠️ Spins down after 15 minutes of inactivity
- ⚠️ First request after inactivity takes ~30 seconds (cold start)
- ✅ Automatic HTTPS
- ✅ PostgreSQL database included

**Vercel Free Tier:**
- ✅ Unlimited deployments
- ✅ 100GB bandwidth/month
- ✅ Automatic HTTPS
- ✅ Global CDN
- ✅ No cold starts

### Keeping Your Backend Awake

To avoid cold starts, you can use a free service like [UptimeRobot](https://uptimerobot.com) to ping your backend every 14 minutes.

---

## 🆘 Troubleshooting

### Backend won't start
- Check environment variables are set correctly
- Check logs in Render dashboard
- Verify DATABASE_URL format is correct

### Frontend can't connect to backend
- Verify REACT_APP_API_URL is set correctly
- Check CORS settings allow your Vercel domain
- Check backend is running (visit backend URL directly)

### Database connection error
- Make sure you're using the **Internal Database URL**
- Verify DATABASE_URL environment variable is set
- Check if database is in the same region as backend

### Gemini API not working
- Verify GEMINI_API_KEY is correct
- Check you haven't exceeded free tier quota
- Check API key is enabled in Google AI Studio

---

## 📧 Support

If you encounter issues:
1. Check Render logs (Dashboard → Your Service → Logs)
2. Check Vercel deployment logs
3. Check browser console for errors (F12)

---

## 🎓 Next Steps

- ✅ Add a custom domain (Vercel supports this for free!)
- ✅ Set up UptimeRobot to prevent cold starts
- ✅ Monitor your Gemini API usage
- ✅ Share your project with the world! 🌍
