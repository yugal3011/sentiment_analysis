# ✅ Pre-Deployment Checklist

Use this checklist to ensure everything is ready before deploying.

## 📝 Code Preparation

- [ ] All code committed to Git
- [ ] `.env` file is NOT committed (check `.gitignore`)
- [ ] No hardcoded secrets or API keys in code
- [ ] Backend debug mode is OFF (`debug=False` in app.py)
- [ ] All tests passing locally
- [ ] Frontend builds successfully (`npm run build`)

## 🔑 API Keys & Credentials

- [ ] Gemini API key obtained from Google AI Studio
- [ ] Gemini API key tested locally
- [ ] Ready to create Render account
- [ ] Ready to create Vercel account

## 📦 Dependencies

- [ ] `requirements.txt` includes all backend dependencies
- [ ] `requirements.txt` includes `gunicorn`
- [ ] `package.json` has all frontend dependencies
- [ ] No missing dependencies

## 🗂️ Files Required for Deployment

Backend:
- [ ] `Procfile` exists
- [ ] `runtime.txt` exists
- [ ] `requirements.txt` updated
- [ ] `.env.example` exists

Frontend:
- [ ] `.env.example` exists
- [ ] Build command works locally

Root:
- [ ] `vercel.json` exists
- [ ] `.gitignore` properly configured
- [ ] `DEPLOYMENT.md` read and understood
- [ ] `ENV_VARIABLES.md` reviewed

## 🚀 GitHub Repository

- [ ] GitHub repository created
- [ ] Code pushed to GitHub
- [ ] Repository is Public or accessible to Vercel/Render

## 📖 Documentation

- [ ] README.md updated with deployment info
- [ ] Deployment guide reviewed
- [ ] Environment variables documented

## 🎯 Ready to Deploy?

If all boxes are checked, you're ready! Follow the [DEPLOYMENT.md](DEPLOYMENT.md) guide.

### Deployment Order:

1. **Push to GitHub** ✅
2. **Deploy Backend to Render** (10-15 minutes)
3. **Deploy Frontend to Vercel** (3-5 minutes)
4. **Update environment variables** (connect frontend ↔ backend)
5. **Test the live application** 🎉

---

## 📞 Need Help?

- Review [DEPLOYMENT.md](DEPLOYMENT.md) for detailed instructions
- Check [ENV_VARIABLES.md](ENV_VARIABLES.md) for configuration help
- Verify all environment variables are set correctly
