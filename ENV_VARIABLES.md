# 🔐 Environment Variables Reference

This document lists all environment variables needed for deployment.

---

## Backend Environment Variables (Render)

Add these in Render Dashboard → Your Service → Environment:

### Required Variables

```bash
# Database (automatically provided by Render PostgreSQL)
DATABASE_URL=postgresql://user:password@host:5432/database_name

# Gemini API (Get from https://aistudio.google.com/app/apikey)
GEMINI_API_KEY=your_gemini_api_key_here

# LLM Configuration
LLM_PROVIDER=gemini
GEMINI_MODEL=gemini-2.0-flash

# Frontend URL (Update after deploying frontend)
FRONTEND_URL=https://your-app-name.vercel.app

# Flask Configuration
FLASK_ENV=production
```

### Optional Variables

```bash
# Server Port (Render sets this automatically)
PORT=5000

# Flask Debug (should always be off in production)
FLASK_DEBUG=0
```

---

## Frontend Environment Variables (Vercel)

Add these in Vercel Dashboard → Your Project → Settings → Environment Variables:

### Required Variables

```bash
# Backend API URL (from Render deployment)
REACT_APP_API_URL=https://your-backend-name.onrender.com
```

---

## Local Development Environment Variables

### Backend (.env file)

Create `backend/.env` (already exists, just verify):

```bash
# Gemini API Configuration
GEMINI_API_KEY=your_gemini_api_key_here

# LLM Provider
LLM_PROVIDER=gemini

# Gemini Model Selection
GEMINI_MODEL=gemini-2.0-flash

# Database (optional - uses SQLite if not set)
# DATABASE_URL=postgresql+psycopg2://user:pass@localhost:5432/dbname

# Flask Configuration
FLASK_ENV=development
FLASK_DEBUG=1

# Frontend URL (for CORS)
FRONTEND_URL=http://localhost:3000
```

### Frontend (.env file)

Create `frontend/.env`:

```bash
# Backend API URL
REACT_APP_API_URL=http://localhost:5000
```

---

## 📝 Variable Descriptions

| Variable | Description | Example |
|----------|-------------|---------|
| `DATABASE_URL` | PostgreSQL connection string | `postgresql://user:pass@host:5432/db` |
| `GEMINI_API_KEY` | Your Google Gemini API key | `AIzaSy...` |
| `LLM_PROVIDER` | Which LLM to use (only gemini supported) | `gemini` |
| `GEMINI_MODEL` | Which Gemini model variant | `gemini-2.0-flash` |
| `FRONTEND_URL` | URL of your frontend (for CORS) | `https://app.vercel.app` |
| `FLASK_ENV` | Flask environment mode | `production` or `development` |
| `REACT_APP_API_URL` | Backend API endpoint for frontend | `https://api.onrender.com` |

---

## 🔒 Security Best Practices

1. **Never commit** `.env` files to Git (already in `.gitignore`)
2. **Use different API keys** for development and production
3. **Rotate keys** if they are accidentally exposed
4. **Monitor usage** of your Gemini API key in Google AI Studio
5. **Set up billing alerts** in Google Cloud Console (optional)

---

## ✅ Checklist Before Deployment

- [ ] Gemini API key is valid and working
- [ ] DATABASE_URL points to production PostgreSQL database
- [ ] FRONTEND_URL matches your Vercel deployment URL
- [ ] REACT_APP_API_URL matches your Render backend URL
- [ ] All sensitive values are set as environment variables (not hardcoded)
- [ ] `.env` files are in `.gitignore`
- [ ] Test locally before deploying

---

## 🆘 Troubleshooting Environment Variables

### How to verify environment variables are loaded:

**Backend (Render Shell):**
```bash
python -c "import os; print('GEMINI_API_KEY:', os.getenv('GEMINI_API_KEY')[:10] + '...')"
```

**Frontend (Browser Console):**
```javascript
console.log('API URL:', process.env.REACT_APP_API_URL);
```

### Common Issues:

1. **Variables not loading**: Make sure they're set in the platform dashboard, not just in your local `.env`
2. **CORS errors**: Check `FRONTEND_URL` is set correctly in backend
3. **API not connecting**: Verify `REACT_APP_API_URL` has no trailing slash
4. **Database errors**: Make sure `DATABASE_URL` uses `postgresql://` not `postgres://`

---

For step-by-step deployment instructions, see [DEPLOYMENT.md](DEPLOYMENT.md)
