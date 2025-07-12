# CodeGenAI - AI-Powered Coding Challenge Generator

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/Python-3.13+-blue.svg)](https://www.python.org/downloads/)
[![React](https://img.shields.io/badge/React-19.1+-61DAFB.svg)](https://reactjs.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115+-009688.svg)](https://fastapi.tiangolo.com/)

A full-stack web application that generates AI-powered coding challenges with multiple choice questions, featuring user authentication, difficulty levels, and comprehensive challenge history tracking.

## 🚀 Features

### 🧠 AI-Powered Challenge Generation
- **OpenAI Integration**: Leverages GPT-3.5 Turbo to generate contextually relevant coding challenges
- **Multiple Difficulty Levels**: Easy, Medium, and Hard challenges tailored to different skill levels
- **Dynamic Content**: Each challenge includes a title, multiple choice options, correct answer, and detailed explanation

### 🔐 User Authentication & Authorization
- **Clerk Authentication**: Secure user management with sign-in/sign-up functionality
- **JWT-based Authorization**: Protected API endpoints with bearer token authentication
- **User-specific Data**: Personal challenge history and quota tracking

### 📊 Quota Management System
- **Daily Limits**: 10 challenges per user per day (configurable)
- **Automatic Reset**: Quota automatically resets every 24 hours
- **Real-time Tracking**: Live quota display in the UI

### 📈 Challenge History
- **Personal Dashboard**: View all previously generated challenges
- **Persistent Storage**: SQLite database for reliable data persistence
- **Detailed Records**: Complete challenge data including timestamps and difficulty levels

## 🖼️ Dashboard Screenshots

### Main Challenge Generator
![Challenge Generator Dashboard](./images/dashboard-main.png)
*Generate new coding challenges with difficulty selection and quota tracking*

### Challenge History View
![Challenge History](./images/dashboard-history.png)
*Browse through your complete challenge history with detailed explanations*

### Interactive Challenge Interface
![Challenge Interface](./images/dashboard-challenge.png)
*Interactive multiple choice interface with instant feedback and explanations*

## 🛠️ Tech Stack

### Frontend
- **React 19.1** - Modern React with hooks and functional components
- **Vite** - Fast build tool and development server
- **React Router DOM** - Client-side routing
- **Clerk React** - Authentication components and hooks
- **CSS3** - Custom styling and responsive design

### Backend
- **FastAPI** - Modern Python web framework
- **SQLAlchemy** - Database ORM with SQLite
- **OpenAI API** - AI-powered challenge generation
- **Clerk Backend SDK** - Server-side authentication
- **Uvicorn** - ASGI server for production deployment

### Database
- **SQLite** - Lightweight database for development
- **SQLAlchemy Models** - Challenge and user quota management

### Authentication
- **Clerk** - Complete authentication solution
- **JWT Tokens** - Secure API authentication
- **Webhooks** - Automatic user provisioning

## 📋 Prerequisites

- **Python 3.13+**
- **Node.js 18+**
- **npm or yarn**
- **OpenAI API Key**
- **Clerk Account** (for authentication)

## 🚀 Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/codegenai.git
cd codegenai
```

### 2. Backend Setup

```bash
# Navigate to backend directory
cd backend

# Install dependencies using uv (recommended)
uv sync

# Or using pip
pip install -r requirements.txt

# Create environment file
cp .env.example .env
```

### 3. Configure Environment Variables

Create a `.env` file in the backend directory:

```env
# OpenAI Configuration
OPENAI_API_KEY=your_openai_api_key_here

# Clerk Configuration
CLERK_SECRET_KEY=your_clerk_secret_key
CLERK_WEBHOOK_SECRET=your_clerk_webhook_secret
JWT_KEY=your_jwt_key

# Database (SQLite - no configuration needed)
DATABASE_URL=sqlite:///./database.db
```

### 4. Frontend Setup

```bash
# Navigate to frontend directory
cd ../frontend

# Install dependencies
npm install

# Create environment file
cp .env.example .env.local
```

Add your Clerk publishable key to `.env.local`:

```env
VITE_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
```

### 5. Database Setup

The SQLite database will be created automatically when you first run the backend server.

## 🏃‍♂️ Running the Application

### Development Mode

**Terminal 1 - Backend:**
```bash
cd backend
python server.py
```
The backend will run on `http://localhost:8000`

**Terminal 2 - Frontend:**
```bash
cd frontend
npm run dev
```
The frontend will run on `http://localhost:5173`

### Production Mode

**Backend:**
```bash
cd backend
uvicorn src.app:app --host 0.0.0.0 --port 8000
```

**Frontend:**
```bash
cd frontend
npm run build
npm run preview
```

## 📚 API Documentation

### Authentication Endpoints

#### POST `/webhooks/clerk`
- **Purpose**: Handle user creation webhooks from Clerk
- **Authentication**: Webhook signature verification
- **Response**: Creates user quota entry

### Challenge Endpoints

#### POST `/api/generate-challenge`
- **Purpose**: Generate new AI-powered coding challenge
- **Authentication**: Required (Bearer token)
- **Request Body**:
  ```json
  {
    "difficulty": "easy" | "medium" | "hard"
  }
  ```
- **Response**:
  ```json
  {
    "id": 123,
    "difficulty": "easy",
    "title": "Challenge Title",
    "options": ["Option 1", "Option 2", "Option 3", "Option 4"],
    "correct_answer_id": 0,
    "explanation": "Detailed explanation",
    "timestamp": "2024-01-01T00:00:00"
  }
  ```

#### GET `/api/my-history`
- **Purpose**: Retrieve user's challenge history
- **Authentication**: Required (Bearer token)
- **Response**: Array of challenge objects

#### GET `/api/quota`
- **Purpose**: Get user's remaining daily quota
- **Authentication**: Required (Bearer token)
- **Response**:
  ```json
  {
    "user_id": "user_123",
    "quota_remaining": 7,
    "last_reset_date": "2024-01-01T00:00:00"
  }
  ```

## 🏗️ Architecture

### Frontend Architecture
```
src/
├── auth/              # Authentication components
├── challenge/         # Challenge generation and display
├── history/           # Challenge history management
├── layout/            # App layout and navigation
├── utils/             # API utilities and helpers
├── App.jsx            # Main app component
└── main.jsx           # App entry point
```

### Backend Architecture
```
src/
├── database/          # Database models and operations
├── routes/            # API route handlers
├── ai_generator.py    # OpenAI integration
├── utils.py           # Authentication utilities
└── app.py             # FastAPI application setup
```

## 🔧 Configuration

### Quota Settings
- **Default Daily Limit**: 10 challenges per user
- **Reset Interval**: 24 hours
- **Configurable**: Modify in `backend/src/database/db.py`

### AI Model Settings
- **Model**: GPT-3.5 Turbo
- **Temperature**: 0.7 (balanced creativity)
- **Response Format**: JSON structured output

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **OpenAI** for providing the GPT-3.5 Turbo API
- **Clerk** for authentication infrastructure
- **FastAPI** for the excellent Python web framework
- **React** team for the amazing frontend library

## 📞 Support

For support, please open an issue on GitHub or contact the maintainers.

---

**Made with ❤️ by [Your Name]** 