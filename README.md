# Wellness Project

A comprehensive health and wellness application with AI-powered health assistance, personalized recommendations, and user profile management.

## Project Structure

```
Wellness_project/
├── healthbackend/          # Flask Python backend
│   ├── app.py             # Main Flask application
│   ├── config/            # Configuration settings
│   ├── services/          # Business logic (agents, RAG, etc.)
│   ├── storage/           # Data storage (JSON files)
│   ├── utils/             # Utility functions
│   ├── requirements.txt    # Python dependencies
│   └── wsgi.py           # WSGI configuration
└── wellness-frontend/      # React/Vite frontend
    ├── src/              # Source code
    ├── components/       # React components
    ├── package.json      # Node dependencies
    └── vite.config.js    # Vite configuration
```

## Prerequisites

- **Python 3.8+** (for backend)
- **Node.js 16+** (for frontend)
- **pip** (Python package manager)
- **npm** (Node package manager)

## Installation

### 1. Install Backend Dependencies

Navigate to the project root and run:

```bash
pip install -r healthbackend/requirements.txt
```

**Note:** A Python virtual environment is recommended:

```bash
python -m venv venv
venv\Scripts\activate  # On Windows
# or
source venv/bin/activate  # On macOS/Linux

pip install -r healthbackend/requirements.txt
```

### 2. Install Frontend Dependencies

```bash
cd wellness-frontend
npm install
```

## Configuration

### Backend Environment Variables

Create or update a `.env` file in the `healthbackend/` directory with:

```
GROQ_API_KEY=your_groq_api_key
GROQ_MODEL_NAME=llama-3.3-70b-versatile
YOUTUBE_API_KEY=your_youtube_api_key
```

## Running the Application

### Start the Backend (Flask Server)

From the project root:

```bash
python -m healthbackend.app
```

The backend will run on: **http://127.0.0.1:5000**

### Start the Frontend (Vite Dev Server)

In a new terminal, navigate to the frontend directory:

```bash
cd wellness-frontend
npm run dev
```

The frontend will run on: **http://localhost:5173**

## Features

- 🔐 **User Authentication** - Login and profile management
- 🤖 **AI Health Assistance** - Chat with an AI health assistant powered by Groq
- 📊 **Health Profile** - Store and manage user health information
- 📚 **Chat History** - View previous conversations
- 🎥 **YouTube Recommendations** - Get health-related video recommendations
- 💾 **Local Data Storage** - JSON-based persistent storage

## API Endpoints

### Authentication

- `POST /login` - User login
- `POST /register` - User registration

### Profile

- `GET /profile/<username>` - Get user profile
- `POST /profile/<username>` - Update user profile

### Chat & Health Assistance

- `POST /chat_stream` - Stream chat responses
- `POST /health-assist` - Get health assistance
- `GET /history/<username>` - Get chat history

### Recommendations

- `POST /youtube-recommendations` - Get YouTube video recommendations

## Troubleshooting

### Backend Issues

**ModuleNotFoundError: No module named 'healthbackend'**

- Ensure you're in the project root directory
- Make sure dependencies are installed: `pip install -r healthbackend/requirements.txt`

**Rate Limit Error (429)**

- This occurs when the Groq API quota is exceeded
- The application has built-in retry logic with exponential backoff
- Check your API usage at https://console.groq.com
- Consider adding multiple API keys to the pool

**Flask Not Running**

- Check that port 5000 is not in use
- Run with a different port: `python -m flask --port 8000 run`

### Frontend Issues

**Cannot find module dependencies**

- Delete `node_modules/` and `package-lock.json`
- Run `npm install` again

**Port 5173 Already in Use**

- Vite will automatically use the next available port
- Or kill the process using that port

## API Key Configuration

The application uses the Groq API for AI models. To use the full functionality:

1. Get your API key from [Groq Console](https://console.groq.com)
2. Add it to your `.env` file
3. Configure the API key pool in `healthbackend/services/api_key_pool.py` if using multiple keys

## Development Notes

- The backend uses Flask with async support
- LangChain is used for AI/LLM integration
- Frontend uses React with Vite for fast development
- Data is stored in JSON files in `healthbackend/storage/`

## Git Operations

Before pushing to a repository, ensure the `.gitignore` file is in place to exclude:

- Virtual environments (`venv/`)
- Node modules (`node_modules/`)
- Environment files (`.env`)
- Python cache (`__pycache__/`)

## Support

For issues or questions, please check the logs in the backend terminal for error messages and stack traces.

---

**Last Updated:** December 12, 2025
