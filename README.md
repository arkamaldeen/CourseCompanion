# 📚 CourseCompanion

> AI-Powered Learning Platform with RAG Chatbot and Course Discovery

CourseCompanion is an intelligent learning platform that helps users discover, learn, and master courses through AI-powered assistance. Built for the hackathon with a focus on demonstrating the power of LangChain, LangGraph, and modern AI capabilities.

## 🎯 Features

### 🔍 Course Discovery Agent
- Conversational AI agent built with LangGraph
- Understands user roles, skills, and learning goals
- Provides personalized course recommendations

### 💬 RAG-Powered Chatbot
- Course-specific knowledge bases
- Retrieval-Augmented Generation for accurate answers
- Source citations with module and timestamp references

### 📝 Smart Notepad
- Course-specific note-taking
- Add content from chat conversations
- Markdown support with live preview

### 🎨 Artifact Playground
- Pre-made learning artifacts (mindmaps, summaries, slides)
- Visual learning resources
- Downloadable materials

### 📊 Quiz & Assessment
- Course-specific quizzes
- Topic-based scoring
- Personalized recommendations based on results

## 🏗️ Architecture

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│    Streamlit    │────▶│     FastAPI     │────▶│    MongoDB      │
│    Frontend     │◀────│     Backend     │◀────│    Atlas        │
└─────────────────┘     └─────────────────┘     └─────────────────┘
                               │
                               ▼
                        ┌─────────────────┐
                        │   AI Services   │
                        │  • LangGraph    │
                        │  • LangChain    │
                        │  • OpenAI       │
                        └─────────────────┘
```

## 📁 Project Structure

```
CourseCompanion/
├── frontend/                    # Streamlit application
│   ├── app.py                   # Main entry point
│   ├── pages/                   # Application pages
│   │   ├── 1_landing.py         # Landing & course selection
│   │   ├── 2_discovery.py       # AI course discovery
│   │   ├── 3_learning.py        # Learning environment
│   │   ├── 4_quiz.py            # Quiz interface
│   │   └── 5_results.py         # Results & recommendations
│   ├── components/              # Reusable UI components
│   └── utils/                   # Utilities & API client
│
├── backend/                     # FastAPI server
│   ├── main.py                  # FastAPI entry point
│   ├── routers/                 # API route handlers
│   ├── services/                # Business logic
│   │   ├── discovery_agent.py   # LangGraph discovery agent
│   │   ├── rag_chatbot.py       # LangChain RAG chatbot
│   │   ├── quiz_service.py      # Quiz management
│   │   └── recommendation.py    # Recommendation engine
│   └── models/                  # Pydantic schemas & DB models
│
├── data/                        # Mock data & assets
│   ├── courses/                 # Course catalog & knowledge base
│   ├── quizzes/                 # Quiz questions
│   └── artifacts/               # Learning artifacts
│
├── scripts/                     # Utility scripts
│   ├── seed_database.py         # Database seeding
│   └── generate_embeddings.py   # Embedding generation
│
├── requirements.txt             # Python dependencies
├── env.example                  # Environment variables template
└── README.md                    # This file
```

## 🚀 Quick Start

### Prerequisites

- Python 3.10+
- MongoDB (local or Atlas)
- OpenAI API key

### 1. Clone & Setup

```bash
# Clone the repository
cd CourseCompanion

# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Configure Environment

```bash
# Copy environment template
cp env.example .env

# Edit .env with your values:
# - MONGODB_URI (your MongoDB connection string)
# - OPENAI_API_KEY (your OpenAI API key)
```

### 3. Seed Database

```bash
# Populate MongoDB with initial data
python scripts/seed_database.py

# Generate embeddings (optional, requires OpenAI API key)
python scripts/generate_embeddings.py
```

### 4. Start the Backend

```bash
cd backend
uvicorn main:app --reload --port 8000
```

### 5. Start the Frontend

```bash
# In a new terminal
cd frontend
streamlit run app.py --server.port 8501
```

### 6. Open the Application

Navigate to [http://localhost:8501](http://localhost:8501) in your browser.

## 🔧 Development

### Running Tests

```bash
pytest tests/
```

### Code Formatting

```bash
black .
isort .
flake8
```

## 📊 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/discover` | POST | Run discovery agent conversation |
| `/api/courses` | GET | List all courses |
| `/api/chat` | POST | RAG chatbot query |
| `/api/notes/{user}/{course}` | GET/POST/PUT | Notes CRUD |
| `/api/artifacts/{course}/{type}` | GET | Get artifact |
| `/api/quiz/{course}` | GET | Get quiz questions |
| `/api/quiz/submit` | POST | Submit quiz answers |
| `/api/results/{user}/{course}` | GET | Get results |

## 🛠️ Tech Stack

- **Frontend**: Streamlit
- **Backend**: FastAPI
- **Database**: MongoDB Atlas
- **AI/ML**: 
  - LangChain for RAG
  - LangGraph for agent workflows
  - OpenAI GPT-4 & Embeddings
- **Vector Search**: MongoDB Atlas Vector Search

## 📋 MongoDB Atlas Setup

1. Create a free cluster at [MongoDB Atlas](https://www.mongodb.com/atlas)
2. Create a database user
3. Whitelist your IP address
4. Get your connection string
5. Create a Vector Search index:
   ```json
   {
     "fields": [
       {
         "type": "vector",
         "path": "embedding",
         "numDimensions": 1536,
         "similarity": "cosine"
       },
       {
         "type": "filter",
         "path": "course_id"
       }
     ]
   }
   ```

## 🎯 Hackathon Demo Flow

1. **Landing Page**: Choose to browse courses or get AI recommendations
2. **Discovery**: Chat with the AI agent to find the right courses
3. **Learning**: Access course content, chat with the AI, take notes
4. **Artifacts**: Explore mindmaps, summaries, and slides
5. **Quiz**: Test your knowledge
6. **Results**: Get personalized recommendations for improvement

## 🤝 Team

Built with ❤️ for the hackathon!

## 📄 License

MIT License - feel free to use and modify!

