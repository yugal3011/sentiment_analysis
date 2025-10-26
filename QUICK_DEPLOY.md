# 🚀 Quick Deployment Commands

Copy and paste these commands to deploy your project quickly!

## 1️⃣ Push to GitHub

```bash
# Navigate to your project
cd "d:\final project api"

# Initialize Git (if not done)
git init

# Add all files
git add .

# Commit
git commit -m "Ready for deployment - Vercel + Render"

# Add remote (replace with YOUR repository URL)
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git

# Push to GitHub
git branch -M main
git push -u origin main
```

## 2️⃣ Render Backend Deployment

### Create PostgreSQL Database:
1. Go to https://render.com/dashboard
2. Click "New +" → "PostgreSQL"
3. Name: `feedback-db`
4. Plan: **Free**
5. Click "Create Database"
6. **Copy Internal Database URL**

### Deploy Backend:
1. Click "New +" → "Web Service"
2. Connect GitHub repo
3. Configure:
   - Name: `feedback-backend`
   - Root Directory: `backend`
   - Build Command: `pip install -r requirements.txt`
   - Start Command: `gunicorn app:app`
   - Plan: **Free**

4. Add Environment Variables:
```
DATABASE_URL = [paste internal database URL]
GEMINI_API_KEY = your_gemini_api_key
LLM_PROVIDER = gemini
GEMINI_MODEL = gemini-2.0-flash
FLASK_ENV = production
FRONTEND_URL = https://your-app.vercel.app
```

5. Click "Create Web Service"
6. **Copy your backend URL** (e.g., https://feedback-backend.onrender.com)

### Download TextBlob Corpora (after deployment):
1. Go to Render Dashboard → Your Service → Shell
2. Run: `python -m textblob.download_corpora`

## 3️⃣ Vercel Frontend Deployment

1. Go to https://vercel.com/new
2. Import your GitHub repository
3. Configure:
   - Framework: Create React App
   - Root Directory: `frontend`
   - Build Command: `npm run build`
   - Output Directory: `build`

4. Add Environment Variable:
```
REACT_APP_API_URL = https://your-backend-url.onrender.com
```
(Use the URL from step 2.6)

5. Click "Deploy"
6. **Copy your Vercel URL**

## 4️⃣ Update Backend FRONTEND_URL

1. Go back to Render
2. Your backend service → Environment tab
3. Update `FRONTEND_URL` to your Vercel URL
4. Save (will auto-redeploy)

## 5️⃣ Test Your App! 🎉

Open your Vercel URL and test:
- ✅ Submit feedback
- ✅ Check sentiment analysis
- ✅ Verify AI suggestions
- ✅ Test dashboard charts
- ✅ Generate PDF report

---

## 🔄 Future Updates

When you make changes:

```bash
git add .
git commit -m "Description of changes"
git push
```

Both Vercel and Render will automatically redeploy! 🚀

---

## 📚 Detailed Instructions

For step-by-step guidance with screenshots and troubleshooting:
- See [DEPLOYMENT.md](DEPLOYMENT.md)
- See [ENV_VARIABLES.md](ENV_VARIABLES.md)
- See [DEPLOYMENT_CHECKLIST.md](DEPLOYMENT_CHECKLIST.md)
