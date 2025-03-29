# Concisio - Chat Summarization and Insights Platform

A powerful platform that combines a FastAPI backend with a Streamlit frontend to process chat data, generate summaries, and provide real-time insights using Google's Gemini API.

## Features

- Real-time chat processing with WebSocket support
- MongoDB-based chat storage and retrieval
- Advanced chat summarization using Gemini API
- Sentiment analysis and keyword extraction
- Streamlit-based interactive UI
- RESTful API endpoints for chat operations
- Efficient pagination and filtering capabilities

## Prerequisites

- Python 3.11 or higher
- MongoDB instance (local or cloud)
- Google Cloud account for Gemini API access

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/concisio.git
   cd concisio
   ```

2. Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   # On Windows
   .venv\Scripts\activate
   # On Unix or MacOS
   source .venv/bin/activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Set up environment variables:
   Create a `.env` file in the backend directory with the following variables:
   ```env
   MONGODB_URL=your_mongodb_connection_string
   GEMINI_API_KEY=your_gemini_api_key
   ```

## Usage

### Running the Backend

1. Navigate to the backend directory:

   ```bash
   cd backend
   ```

2. Start the FastAPI server:
   ```bash
   uvicorn app.main:app --reload --port 8000
   ```
   The API will be available at `http://localhost:8000`

### Running the Frontend

1. Navigate to the frontend directory:

   ```bash
   cd frontend
   ```

2. Launch the Streamlit app:
   ```bash
   streamlit run app.py
   ```
   The UI will be available at `http://localhost:8501`

### API Documentation

Once the backend is running, access the interactive API documentation at:

- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

### Available Endpoints

- `POST /chats` - Create a new chat message
- `GET /chats/{conversation_id}` - Retrieve conversation history
- `GET /chats/users/{user_id}/messages` - Get user's chat history (paginated)
- `POST /chats/summarize` - Generate conversation summary
- `DELETE /chats/{conversation_id}` - Delete a conversation
- `WebSocket /chats/ws/{client_id}` - Real-time chat connection

## Docker Deployment

1. Create a `.env` file in the project root with your environment variables:
   ```env
   MONGODB_URL=your_mongodb_connection_string
   GOOGLE_API_KEY=your_google_api_key
   JWT_SECRET=your_jwt_secret
   ```

2. Build the Docker image:
   ```bash
   docker build -t concisio .
   ```

3. Run the container:
   ```bash
   docker run -d \
     --name concisio \
     -p 8000:8000 \
     -p 8501:8501 \
     --env-file .env \
     -v $(pwd)/data:/app/data \
     concisio
   ```

   This command:
   - Maps ports 8000 (FastAPI backend) and 8501 (Streamlit frontend)
   - Loads environment variables from .env file
   - Mounts a data volume for persistence

4. Access the applications:
   - Frontend: http://localhost:8501
   - Backend API: http://localhost:8000
