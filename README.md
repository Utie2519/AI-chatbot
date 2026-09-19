# 🤖 AI Chatbot

An AI-powered document-aware chatbot built with Flask and Python. The application provides a conversational interface that can work with uploaded documents and maintain session-based conversations.

The system supports document ingestion for formats such as PDF, DOCX, XLSX, and TXT, extracts their textual content, stores uploaded files using MongoDB GridFS, and uses an AI model to generate responses.

## 🚀 Features

* 🤖 AI-powered conversational interface
* 💬 Session-based chat
* 📄 Document upload and processing
* 📕 PDF text extraction
* 📝 DOCX text extraction
* 📊 Excel/XLSX text extraction
* 📃 TXT file processing
* 🗄️ MongoDB-based persistence
* 📦 MongoDB GridFS for file storage
* 🔄 Local and Global chat modes
* 📚 Session-specific document management
* 🗑️ Document deletion
* 🧹 Session deletion
* 🌐 Flask REST API
* 🔐 Environment-based API configuration
* 🧪 Demo/fallback responses when AI services are unavailable

## 🏗️ Architecture

```text
┌───────────────────────────────┐
│          Web Frontend         │
│        HTML / CSS / JS        │
└──────────────┬────────────────┘
               │
               │ HTTP / REST API
               ▼
┌───────────────────────────────┐
│          Flask Backend        │
│                               │
│ Session Management            │
│ Chat Processing               │
│ Document Upload               │
│ Document Extraction           │
│ Mode Switching                │
│ Document Management           │
└──────────────┬────────────────┘
               │
       ┌───────┴────────────┐
       ▼                    ▼
┌───────────────┐    ┌────────────────┐
│    MongoDB    │    │   AI21 Jamba   │
│               │    │      LLM       │
│ Sessions      │    └────────────────┘
│ Chat History  │
│ Documents     │
│ GridFS Files  │
└───────────────┘
```

## 🛠️ Technology Stack

### Backend

* Python
* Flask
* Gunicorn
* Requests
* python-dotenv

### Database

* MongoDB
* PyMongo
* GridFS

### AI

* AI21 Jamba Large
* AI-powered conversational responses

### Document Processing

* PyMuPDF
* python-docx
* pandas
* openpyxl

### Frontend

* HTML
* CSS
* JavaScript

## 📂 Project Structure

```text
AI-chatbot/
│
├── static/
│   ├── script.js
│   └── style.css
│
├── templates/
│   └── index.html
│
├── app.py
├── task.py
├── requirements.txt
├── runtime.txt
├── doc.txt
├── sample.xlsx
├── Full.pdf
├── Title.docx
├── .gitignore
└── README.md
```

## 🔄 Application Workflow

```text
User
 │
 ▼
Web Interface
 │
 ├── Start Session
 │
 ├── Ask Question
 │
 └── Upload Documents
 │
 ▼
Flask Backend
 │
 ├── Process Request
 │
 ├── Extract Document Content
 │
 ├── Store Files in GridFS
 │
 ├── Store Text in MongoDB
 │
 └── Send Context to AI Model
 │
 ▼
AI21 Jamba
 │
 ▼
Generated Response
 │
 ▼
Web Interface
```

## 📄 Supported Documents

The application can process several common document formats:

| Format | Processing                            |
| ------ | ------------------------------------- |
| PDF    | Text extraction using PyMuPDF         |
| DOCX   | Text extraction using python-docx     |
| XLSX   | Data extraction using pandas/openpyxl |
| TXT    | Direct text decoding                  |

Extracted content is associated with the user's session and stored for subsequent application operations.

## 💬 Chat Sessions

Each conversation is associated with a session ID.

The backend stores information such as:

* Session ID
* Chat mode
* User question
* AI response
* Timestamp

This allows conversations and uploaded documents to remain associated with a particular session.

## 🔀 Chat Modes

The application supports two modes:

### Local Mode

Designed around the documents and information associated with the current session.

### Global Mode

Designed for broader AI-powered conversational interaction.

Users can switch between the available modes through the `/switch_mode` API endpoint.

## 📤 Document Upload

The `/upload` endpoint accepts uploaded files and:

1. Validates the session.
2. Checks uploaded filenames.
3. Stores files in MongoDB GridFS.
4. Detects the document type.
5. Extracts textual content.
6. Stores extracted content in the documents collection.
7. Associates the document with the current session.

## 🗑️ Document & Session Management

The backend provides endpoints for:

* Listing session documents
* Deleting individual documents
* Deleting complete sessions

When a document is deleted, its GridFS entry and corresponding extracted document record are removed.

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/Utie2519/AI-chatbot.git
cd AI-chatbot
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it on macOS/Linux:

```bash
source venv/bin/activate
```

On Windows:

```bash
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

Create a `.env` file:

```env
AI21_API_KEY=your_ai21_api_key
MONGO_URI=your_mongodb_connection_string
```

Add any additional environment variables required by your deployment configuration.

**Never commit `.env` or API keys to GitHub.**

### 5. Start the application

```bash
python app.py
```

The application can then be accessed through the local Flask server.

For production deployment, Gunicorn is included in the project dependencies.

## 🔐 Security

Sensitive configuration should be stored through environment variables rather than directly inside the source code.

Recommended practices:

* Keep `.env` out of Git
* Never publish API keys
* Use separate development and production credentials
* Restrict database permissions
* Validate uploaded files
* Limit upload sizes in production
* Use HTTPS for deployed applications

## 🧠 AI Response Handling

The application sends user input to the configured AI service and extracts the generated response from the model output.

The current implementation uses the AI21 Jamba model and includes fallback responses when the AI service is unavailable or cannot provide a response.

## 🎯 Future Improvements

* Retrieval-Augmented Generation (RAG)
* Vector database integration
* Semantic document search
* Conversation memory
* Streaming AI responses
* Authentication and user accounts
* Document previews
* Improved file validation
* Background document processing
* Chat export
* Voice input/output
* Better error handling and observability

## ⚠️ Disclaimer

This project is intended for educational and experimental purposes. AI-generated responses may contain inaccuracies and should be independently verified before being relied upon for important decisions.

## 👨‍💻 Author

**Utkarsh Sharma**

GitHub: [@Utie2519](https://github.com/Utie2519)

---

⭐ If you find this project useful, consider giving it a star.
