# 🛡️ AI Cyberbullying & Harassment Detection System

An advanced, AI-powered cyberbullying and online harassment detection platform built with **Django** and powered by **Google Gemini LLM** and **Multimodal Computer Vision**.

---

## 🌟 Key Features

### 1. 🤖 LLM-Powered Cyberbullying Detection
- Uses **Google Gemini 1.5 Flash** for deep contextual text moderation.
- Classifies abusive text into fine-grained categories:
  - Bullying & Humiliation
  - Hate Speech & Racism
  - Threats & Violence
  - Offensive Language / Swearing
  - Sexual Harassment
  - Discrimination
- Detects severity levels (**LOW**, **MEDIUM**, **HIGH**, **CRITICAL**) with an exact confidence score and detailed AI reasoning.
- **Multilingual Support**: Detects insults, hate speech, and slang across English, Hindi, Tamil, Malayalam, Arabic, etc.
- **Graceful Fallback**: Automatically falls back to a built-in keyword engine if an API key is not supplied or network is unavailable.

### 2. 👁️ Image Recognition & Multimodal Vision
- Utilizes Gemini's vision capabilities to detect abusive visual content:
  - Hurtful memes, humiliating edits, body-shaming imagery
  - Hate symbols and extremist insignia
  - Violent or threatening graphics
- **OCR Text Extraction**: Powered by Tesseract OCR to read text embedded inside images and screenshots.

### 3. 📸 Instagram Reel & ▶️ YouTube Comment Section Scanner
- **Direct Link Scanning**: Paste any public Instagram Reel URL (`instagram.com/reel/...`) or YouTube Video URL (`youtube.com/watch?v=...` or `youtu.be/...`).
- Automatically extracts comments using API integrations (or headless fallback extractors like `yt-dlp` and `instaloader`).
- **Batch AI Analysis**: Evaluates every fetched comment, computes an **Overall Toxicity Score**, and classifies comments into Clean vs Abusive.
- **Visual Analytics**: Interactive toxicity meter, detailed breakdown by comment author, likes, severity rating, and AI explanations.

### 4. ⚖️ Indian Cyber Law & Rules AI Assistant ("CyberNyaya AI")
- Dedicated AI Legal Chatbot explaining all **Indian Cyberbullying Laws, Sections & Regulations**:
  - **Information Technology Act, 2000 (IT Act)**: Sections 66C (Identity Theft / Fake profiles), 66D (Cheating by Personation), 66E (Privacy violation / non-consensual images), 67 & 67A (Obscenity & Sexually explicit acts), 67B (Child cyber abuse), 72/72A (Doxxing).
  - **Bharatiya Nyaya Sanhita, 2023 (BNS / IPC)**: BNS Section 78 (Cyber Stalking of women), BNS Section 79 (Insulting Modesty of Women), BNS Section 356 (Cyber Defamation), BNS Section 351 (Criminal Intimidation / Threats).
  - **IT Intermediary Rules (2021)**: 24-hour non-consensual content takedown mandate.
  - **Emergency Helplines & Procedures**: National Helpline **1930**, Police **112**, Women Helpline **1091**, and official filing guide for **cybercrime.gov.in**.
  - One-click legal prompt chips, quick sections reference sidebar, and full citation tags.

### 5. 💬 Live Community Feed & Moderated Chat Room
- Real-time moderation for community posts and group chat.
- Abusive content is automatically blocked or flagged for admin intervention.
- User-reported posts appear on the moderation dashboard.

### 6. 🚩 Abuse Reporting & Administrative Control
- Users can file external abuse reports containing links, text, or screenshot proof.
- Full tracking of filed reports and scan history under **My Reports**.
- Comprehensive Django Admin moderation dashboard to review, approve, dismiss, or delete reported content.

---

## 🚀 Quick Start Guide

### 1. Prerequisites
- Python 3.10+
- (Optional) Tesseract OCR installed on your system for local OCR

### 2. Installation
Clone the repository and install the dependencies:
```bash
pip install -r requirements.txt
```

### 3. Configuration (`.env`)
Create a `.env` file in the project root (you can copy `.env.example`):
```env
# Google Gemini API Key (Get free key from https://aistudio.google.com/app/apikey)
GEMINI_API_KEY=your_gemini_api_key_here

# YouTube Data API Key (Optional; yt-dlp is used as fallback)
YOUTUBE_API_KEY=your_youtube_api_key_here

# Instagram Access Token (Optional; instaloader is used as fallback)
INSTAGRAM_ACCESS_TOKEN=your_instagram_token_here
```

### 4. Database Setup & Migrations
```bash
python manage.py migrate
```

Create a superuser for accessing the moderation admin portal:
```bash
python manage.py createsuperuser
```

### 5. Run the Development Server
```bash
python manage.py runserver
```
Visit `http://127.0.0.1:8000/` in your browser.

---

## 🧪 Running Tests

The test suite covers chat moderation, fallback keyword checks, AI parsing, URL format extractors, batch comments scanning, and views:
```bash
python manage.py test
```

---

## 📁 Project Architecture
```
cyberbullying_system/
│── cyberbullying_system/      # Django settings and URL routing
│── moderation/                # Core moderation application
│   ├── ai_engine.py           # Gemini LLM, Vision, YouTube & Instagram scrapers
│   ├── engine.py              # Rule-based fallback and OCR extractor
│   ├── models.py              # Post, ChatMessage, Report, AbuseReport, SocialMediaScan
│   ├── views.py               # Feed, chat, scanning, reporting views
│   ├── forms.py               # URL & Report validation forms
│   ├── admin.py               # Admin moderation interface
│   └── tests.py               # Automated test suite
│── templates/                 # Glassmorphic UI templates
│   ├── base.html              # Navigation and base layout
│   ├── scan_comments.html     # Social media scanning page
│   ├── scan_detail.html       # Comment scan breakdown & analytics
│   ├── report_abuse.html      # External report submission
│   ├── report_detail.html     # Abuse analysis report view
│   └── ...
│── static/css/style.css       # Design system & responsive styles
│── .env.example               # Environment variables template
└── requirements.txt           # Python dependencies
```
