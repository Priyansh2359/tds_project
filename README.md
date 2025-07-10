## 📘 About the Project

This is a **Retrieval-Augmented Generation (RAG) API** built using **FastAPI**. It allows users to ask questions (with optional images), and intelligently answers them using content retrieved from:

- 🧵 **Discourse Forum Posts** (from IIT Madras' Online Degree program)
- 📄 **Markdown-based Documentation** (like course notes)

The system uses **OpenAI's GPT-4o-mini** (via the [aipipe.org](https://aipipe.org) proxy) to generate embeddings and answers. It combines **vector similarity search** and **language modeling** to provide accurate, context-aware responses with source citations.

---

## 🔧 Features

- ✅ **Multimodal Support** – Accepts both text and Base64-encoded images
- 🔍 **Vector Search** – Uses cosine similarity on stored embeddings to find relevant content
- 📚 **Context Expansion** – Enriches responses with adjacent chunks for deeper understanding
- 🤖 **LLM Answering** – Uses GPT-4o-mini to generate answers grounded in retrieved context
- 🔗 **Source Citations** – Each answer includes clickable URLs with matching content snippets
- ⚙️ **Health Endpoint** – Checks DB, API key, and table status for monitoring

---

## 🧱 Tech Stack

- **Backend**: FastAPI + SQLite
- **LLM + Embedding**: GPT-4o-mini (`text-embedding-3-small`) via [aipipe.org](https://aipipe.org)
- **Libraries**: `aiohttp`, `numpy`, `uvicorn`, `dotenv`, `logging`, `re`, `pydantic`

---

## 🚀 API Endpoints

### POST `/query`

> Ask a question with optional image and receive a structured answer.

**Request Body**:
```json
{
  "question": "What is PCA in Data Science?",
  "image": "<optional_base64_encoded_image>"
}
```

**Response**:
```json
{
  "answer": "PCA (Principal Component Analysis)...",
  "links": [
    {
      "url": "https://discourse.onlinedegree.iitm.ac.in/t/123",
      "text": "PCA is used for dimensionality reduction..."
    }
  ]
}
```

---

### GET `/health`

> Returns DB and API status for monitoring.

**Example Response**:
```json
{
  "status": "healthy",
  "database": "connected",
  "api_key_set": true,
  "discourse_chunks": 5420,
  "markdown_chunks": 310,
  "discourse_embeddings": 5420,
  "markdown_embeddings": 310
}
```
