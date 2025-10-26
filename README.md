## Employer Feedback Sentiment Analysis — Full Stack App

A full-stack web application to collect employer feedback, analyze sentiment using AI (Transformer + LLM), and visualize insights. Features hybrid sentiment analysis with DistilBERT and Gemini API for intelligent suggestions.

## 📚 Documentation

Comprehensive documentation is available in the [`docs/`](docs/) folder:

- **[Gemini API Setup](docs/GEMINI_API_SETUP.md)** - Setting up Google Gemini API
- **[Hybrid Sentiment Analysis](docs/HYBRID_SENTIMENT_ANALYSIS.md)** - Understanding the AI sentiment system
- **[Gemini Integration](docs/GEMINI_INTEGRATION_SUMMARY.md)** - LLM setup and configuration
- **[Performance Guide](docs/PERFORMANCE_OPTIMIZATIONS.md)** - Optimization strategies
- **[More Documentation](docs/)** - See all available documentation

## 🚀 Quick Start

### Prerequisites
- Python 3.11+
- Node.js 18+
- Google Gemini API Key (free from Google AI Studio)
- GPU (optional, for faster sentiment analysis)

### Backend Setup (Flask)
1. Create and activate a virtual environment (optional)
```bash
cd backend
python -m venv .venv
.venv\Scripts\activate  # Windows PowerShell
```
2. Install dependencies
```bash
pip install -r requirements.txt
```
3. Configure Gemini API
- Get your free API key from https://aistudio.google.com/app/apikey
- Create `.env` file:
```bash
cp .env.example .env
```
- Edit `.env` and add your API key:
```
GEMINI_API_KEY=your_api_key_here
LLM_PROVIDER=gemini
GEMINI_MODEL=gemini-2.0-flash
```

4. (Optional) Configure PostgreSQL
- Create a database (example): `feedback_db`
- Set env var in `.env`:
```
DATABASE_URL=postgresql+psycopg2://postgres:yourpassword@localhost:5432/feedback_db
```
If not set, the app will use a local SQLite file `app.db`.

5. Initialize TextBlob corpora (first run only)
```bash
python -m textblob.download_corpora
```
6. Run the server
```bash
python app.py
# Server at http://localhost:5000
```

### Frontend Setup (React + Tailwind)
1. Install dependencies
```bash
cd ../frontend
npm install
```
2. Run the dev server
```bash
npm start
# App at http://localhost:3000 (talks to backend at http://localhost:5000)
```

### API Endpoints
- POST `/api/feedback` — body: `{ "feedback_text": string }` → returns saved feedback with sentiment
- GET `/api/feedback` — returns all feedback entries
- GET `/api/dashboard_stats` — returns totals, avg sentiment score, counts per label, and daily timeseries

### Project Structure
```
final project api/
├── backend/
│   ├── app.py                    # Flask API server
│   ├── sentiment_analyzer.py    # Hybrid sentiment analysis (DistilBERT + TextBlob)
│   ├── gemini_suggestions.py    # Gemini API integration
│   ├── test_gemini.py           # Gemini API testing script
│   ├── requirements.txt         # Python dependencies
│   ├── .env                     # Environment configuration (not in git)
│   └── .env.example             # Environment template
├── frontend/
│   ├── package.json             # Node.js dependencies
│   ├── public/
│   │   └── index.html
│   ├── src/
│   │   ├── index.js
│   │   ├── index.css
│   │   ├── App.js
│   │   └── components/
│   │       ├── FeedbackForm.js
│   │       ├── FeedbackList.js
│   │       ├── Dashboard.js
│   │       ├── DistributionChart.js
│   │       └── TrendChart.js
│   ├── tailwind.config.js
│   └── postcss.config.js
├── docs/                        # Comprehensive documentation
├── .gitignore                   # Git ignore rules
└── README.md                    # Project documentation
```

### Notes
- CORS is enabled on the backend to allow the React dev server.
- For production, set `DATABASE_URL` to a managed PostgreSQL instance and use `npm run build` to produce a static build.
- The application uses Google Gemini API for intelligent, personalized feedback suggestions.

## Features

### AI-Powered Sentiment Analysis
- **Hybrid Model**: Combines DistilBERT transformer with TextBlob for accurate sentiment detection
- **Real-time Analysis**: Instant sentiment scoring (Positive/Neutral/Negative)
- **Confidence Scores**: Provides reliability metrics for each analysis

### Intelligent Suggestions (Gemini API)
- **Personalized Development Plans**: AI-generated action plans based on feedback
- **Domain-Specific Insights**: Tailored suggestions for different fields:
  - ✅ Engineering: Technical skills, debugging, system design
  - ✅ Commerce: Excel, financial modeling, business analysis
  - ✅ Science: Research methodology, lab techniques, statistical analysis
  - ✅ Arts: Portfolio development, creative skills
  - ✅ Medical: Clinical skills, patient communication
  - ✅ Law: Legal research, case analysis
  - ✅ Management: Leadership, team delegation, strategic planning

### Analytics Dashboard
- **Sentiment Distribution**: Visual breakdown of feedback types
- **Trend Analysis**: Track sentiment over time
- **PDF Reports**: Export detailed analysis reports

---

## 🌐 Deployment

Ready to deploy your application online? Follow our comprehensive deployment guide:

**📖 [Complete Deployment Guide](DEPLOYMENT.md)**

Deploy for **FREE** using:
- **Frontend**: Vercel (React hosting with global CDN)
- **Backend**: Render (Flask API with PostgreSQL database)

**Quick Links:**
- [Environment Variables Reference](ENV_VARIABLES.md)
- [Vercel Deployment](https://vercel.com)
- [Render Deployment](https://render.com)

---

## 🛠️ Tech Stack

**Frontend:**
- React 18
- TailwindCSS
- Chart.js
- Axios

**Backend:**
- Flask (Python)
- SQLAlchemy
- PostgreSQL/SQLite
- DistilBERT (Transformers)
- TextBlob
- Google Gemini API

**Deployment:**
- Vercel (Frontend)
- Render (Backend + Database)
