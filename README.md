
# AROGYA WELLNESS ASSISTANT

Arogya Wellness Assistant is a full-stack health and wellness application that provides AI-powered health guidance, personalized recommendations, and user profile management.  
The project is built with a Flask backend and a React (Vite) frontend, designed with a clear separation of concerns and a modular, extensible architecture.

This repository is suitable for academic projects, demos, and further enhancement into a production-ready system.

---

## Overview

The application allows users to:
- Interact with an AI-based health assistant
- Maintain and update personal health profiles
- View past health conversations
- Receive relevant YouTube-based health recommendations

The system emphasizes clarity, simplicity, and structured AI-driven workflows.

---

## Project Structure

```

Wellness_project/
├── healthbackend/              # Flask-based backend
│   ├── app.py                  # Main application entry point
│   ├── wsgi.py                 # WSGI configuration
│   ├── config/                 # Application and environment settings
│   ├── services/               # Core business logic (agents, orchestration, APIs)
│   ├── storage/                # JSON-based persistent storage
│   ├── utils/                  # Helper utilities
│   └── requirements.txt        # Python dependencies
│
└── wellness-frontend/          # React + Vite frontend
├── src/                    # Frontend source code
├── components/             # Reusable React components
├── package.json            # Node.js dependencies
└── vite.config.js          # Vite configuration

````

---

## Prerequisites

Before running the project, ensure the following are installed:

- Python 3.8 or higher
- Node.js 16 or higher
- pip (Python package manager)
- npm (Node.js package manager)
- Git

---

## Quick Start (Run Locally)

This section is for anyone cloning the repository for the first time.

### Step 1: Clone the Repository

```bash
git clone <your-repository-url>
cd Wellness_project
````

Ensure you are inside the project root directory.

---

### Step 2: Backend Setup (Flask)

1. Create a Python virtual environment:

```bash
python -m venv venv
```

2. Activate the virtual environment:

```bash
venv\Scripts\activate        # Windows
source venv/bin/activate     # macOS / Linux
```

3. Install backend dependencies:

```bash
pip install -r healthbackend/requirements.txt
```

4. Create a `.env` file inside the `healthbackend/` directory and add:

```
GROQ_API_KEY=your_groq_api_key
GROQ_MODEL_NAME=llama-3.3-70b-versatile
YOUTUBE_API_KEY=your_youtube_api_key
```

5. Start the backend server:

```bash
python -m healthbackend.app
```

If successful, the backend will run at:

```
http://127.0.0.1:5000
```

Keep this terminal running.

---

### Step 3: Frontend Setup (React + Vite)

1. Open a new terminal.
2. Navigate to the frontend directory:

```bash
cd wellness-frontend
```

3. Install frontend dependencies:

```bash
npm install
```

4. Start the frontend development server:

```bash
npm run dev
```

The frontend will be available at:

```
http://localhost:5173
```

---

### Step 4: Use the Application

* Open `http://localhost:5173` in your browser
* Register or log in
* Enter health-related queries
* View AI-generated guidance and recommendations

---

## Key Features

* User authentication and profile management
* AI-powered health assistance using Groq models
* Persistent health profiles
* Conversation history tracking
* Context-aware YouTube video recommendations
* Lightweight JSON-based data storage
* Modular, service-oriented backend design

---

## API Endpoints

### Authentication

* `POST /login`
  Authenticates a user.

* `POST /register`
  Registers a new user.

### User Profile

* `GET /profile/<username>`
  Retrieves a user profile.

* `POST /profile/<username>`
  Updates a user profile.

### Health Assistance and Chat

* `POST /chat_stream`
  Streams AI-generated responses.

* `POST /health-assist`
  Returns structured health guidance.

* `GET /history/<username>`
  Retrieves user chat history.

### Recommendations

* `POST /youtube-recommendations`
  Returns health-related YouTube video suggestions.

---

## Environment and API Keys

The application depends on external APIs:

* Groq API for AI model responses
* YouTube Data API for video recommendations

Ensure API keys are:

* Added only to the `.env` file
* Never committed to version control

---

## Troubleshooting

### Backend Issues

**ModuleNotFoundError: No module named `healthbackend`**

* Run commands from the project root
* Confirm dependencies are installed

**HTTP 429 (Rate Limit Exceeded)**

* Groq API quota has been exceeded
* Retry after some time or add additional API keys

**Backend Not Starting**

* Ensure port 5000 is free
* Verify virtual environment is activated

---

### Frontend Issues

**Missing Dependencies**

* Delete `node_modules/` and `package-lock.json`
* Run `npm install` again

**Port Already in Use**

* Vite will automatically select another port
* Or stop the conflicting process

---

## Development Notes

* Backend is built using Flask with async support
* LangChain is used for LLM orchestration and agent interaction
* Frontend uses React with Vite for fast builds and hot reload
* Data storage is intentionally simple for clarity and ease of debugging

---

## Git and Version Control

Ensure the following are listed in `.gitignore`:

* `venv/`
* `node_modules/`
* `.env`
* `__pycache__/`

This prevents sensitive data and unnecessary files from being committed.

---

## Support and Debugging

For issues:

* Check backend terminal logs
* Review stack traces carefully
* Validate environment variables and API keys

---
