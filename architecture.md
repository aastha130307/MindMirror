1. 🧩 High-Level Architecture

MindMirror follows a lightweight client-server architecture where Streamlit acts as both frontend and backend controller, while models and database handle processing and persistence.

User Browser
     ↓
Streamlit UI (Frontend + Backend Logic)
     ↓
---------------------------------------
|  NLP Layer (Sentiment + Emotion)    |
|  - TextBlob                         |
|  - HuggingFace Transformer Model    |
---------------------------------------
     ↓
SQLite Database (journal.db)
     ↓
Visualization Layer (Matplotlib / Pandas / WordCloud)
2. ⚙️ Core Components
🖥️ 1. Frontend (Streamlit UI)
Built using Streamlit for rapid web deployment
Provides:
Journal input interface
Mood trend dashboard
Entry history viewer
Weekly/monthly analytics
Supports dynamic theme switching (dark/light mode via session state)
🧠 2. NLP Processing Layer

Handles text analysis in real time:

a) Sentiment Analysis
Library: TextBlob
Output: Positive / Negative / Neutral
Based on polarity scoring
b) Emotion Detection
Model: j-hartmann/emotion-english-distilroberta-base
Framework: Hugging Face Transformers + PyTorch
Output classes:
anger, joy, sadness, fear, disgust, neutral, surprise
💾 3. Data Storage Layer
Database: SQLite (journal.db)
Stores:
id (primary key)
date
journal entry
sentiment
emotion
Lightweight embedded DB suitable for local + small cloud deployment
📊 4. Analytics & Visualization Layer
Libraries:
Matplotlib → mood trend line chart
Pandas → data aggregation
WordCloud → frequent word visualization
Features:
Mood trend over time (Positive/Neutral/Negative mapped to -1/0/1)
Weekly/monthly summaries
Emotion distribution
Keyword extraction using regex + Counter
3. 🔄 Application Workflow
Step-by-step flow:
User writes journal entry in Streamlit UI
Entry is passed to NLP layer:
Sentiment computed via TextBlob
Emotion predicted using Transformer model
Results + entry are stored in SQLite
Data is retrieved for:
trend analysis
summaries
visualization dashboards
Streamlit renders updated insights instantly
4. ☁️ Deployment Architecture (Streamlit Cloud)
GitHub Repo
    ↓
Streamlit Cloud Deployment
    ↓
Streamlit App Server
    ↓
SQLite DB (persistent in deployment or attached storage)
Deployment Features:
Auto-deploy from GitHub
Stateless frontend execution per session
Model loaded at runtime (HuggingFace transformers)
Lightweight inference suitable for CPU hosting
5. 🧱 Key Design Decisions (Important for Evaluation)
Streamlit chosen → fast full-stack prototyping without separate frontend/backend
Hybrid NLP approach:
Rule-based sentiment (TextBlob)
Deep learning emotion model (Transformer)
SQLite used → minimal overhead, portable storage
Local inference → no external API dependency → privacy-friendly journaling
Modular functions → easy upgrade to cloud DB or FastAPI backend later
