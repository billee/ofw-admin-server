# OFW Admin Dashboard & Chat API Server

A Flask web server that provides:
- **Admin Dashboard** for tracking user journeys in real-time
- **Chat API** for mobile app AI functionality
- **Firebase Integration** for user data and analytics

## 🚀 Features

### Admin Dashboard (`/`)
- Real-time user journey tracking
- Statistics: users, trials, subscriptions, conversion rates
- User table with registration → trial → subscription → cancellation flow
- Days remaining counter for active trials
- Manual refresh control (no auto-refresh)

### Chat API (`/chat`)
- OpenAI GPT integration for mobile app
- Chat summarization endpoint (`/summarize_chat`)
- Health check endpoint (`/health`)

## 📦 Deployment to Render.com

### Prerequisites
1. **Firebase Project**: Your serviceAccountKey.json file
2. **OpenAI API Key**: For chat functionality
3. **Render.com Account**: For deployment

### Files Structure
```
flask-admin-server/
├── app.py                    # Main Flask application
├── templates/
│   └── admin_dashboard.html  # Admin dashboard UI
├── requirements.txt          # Python dependencies
├── render.yaml              # Render deployment config
├── serviceAccountKey.json   # Firebase credentials (add this)
├── .env                     # Environment variables (add this)
└── README.md               # This file
```

### Setup Steps

1. **Deploy to Render.com**
   - Connect your repository to Render.com
   - Render will automatically use `render.yaml` for configuration
   - Set environment variables in Render dashboard (see below)

2. **Set Environment Variables in Render Dashboard**
   - `OPENAI_API_KEY`: Your OpenAI API key
   - `FIREBASE_SERVICE_ACCOUNT_KEY`: Your Firebase credentials (base64 encoded)

### Environment Variables (Render.com)
- `OPENAI_API_KEY`: Your OpenAI API key for chat functionality
- `FIREBASE_SERVICE_ACCOUNT_KEY`: Base64 encoded Firebase service account JSON

### How to Encode Firebase Credentials
```bash
# Convert your serviceAccountKey.json to base64
base64 -i serviceAccountKey.json
# Copy the output and paste it as FIREBASE_SERVICE_ACCOUNT_KEY in Render
```

## 🔗 API Endpoints

### Admin Dashboard
- `GET /` - Admin dashboard interface
- `GET /api/users` - Get all users with journey data
- `GET /api/stats` - Get dashboard statistics

### Chat API (for mobile app)
- `POST /chat` - Send chat messages to AI
- `POST /summarize_chat` - Summarize conversation
- `GET /health` - Health check

### Debug
- `GET /debug/trials` - View all trial history data

## 🎯 User Journey Tracking

The dashboard tracks users through these stages:
1. **Registration** - User signs up
2. **Email Verification** - User verifies email
3. **Trial Start** - 7-day trial begins
4. **Trial → Subscription** - User converts to paid
5. **Cancellation** - User cancels subscription

## 🔧 Local Development

```bash
# Install dependencies
pip install -r requirements.txt

# Option 1: Use serviceAccountKey.json file (easier for local dev)
# Copy your Firebase service account key to project root
cp /path/to/your/serviceAccountKey.json ./serviceAccountKey.json

# Option 2: Use environment variables (matches production)
cp .env.example .env
# Edit .env with your API keys and base64 encoded Firebase credentials

# Run locally
python app.py
# Visit http://localhost:5000
```

## 📊 Firebase Collections Used

- `users` - User accounts and verification status
- `trial_history` - Trial start/end dates and status
- `subscriptions` - Subscription data and cancellations

## 🎨 Dashboard Features

- **Responsive Design** - Works on desktop and mobile
- **Color-coded Status** - Easy visual scanning
- **Compact Layout** - No horizontal scrolling
- **Real-time Data** - Manual refresh for latest info
- **Trial Countdown** - Days remaining in trials

## 🔒 Security Notes

- Firebase service account key should be kept secure
- OpenAI API key should be set as environment variable
- Consider adding authentication for production admin dashboard