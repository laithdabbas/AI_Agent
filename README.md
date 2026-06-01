# 🎮 LIBERO Gaming Center — AI Agent Chatbot

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python" />
  <img src="https://img.shields.io/badge/FastAPI-Backend-009688?style=for-the-badge&logo=fastapi" />
  <img src="https://img.shields.io/badge/LLM-Powered-blueviolet?style=for-the-badge&logo=openai" />
  <img src="https://img.shields.io/badge/RAG-ChromaDB-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge" />
</p>

> An intelligent AI-powered chatbot agent built for **LIBERO Gaming Center** — the premium gaming and entertainment destination in Jordan. This assistant helps visitors get instant answers about services, pricing, availability, events, and more.

---

## 🏢 About LIBERO Gaming Center

**LIBERO Gaming Center** is a premium entertainment destination offering a wide variety of gaming and leisure experiences for all ages. Located in a modern, welcoming space, LIBERO is the go-to spot for competitive players, casual gamers, and social groups looking for fun.

### 🎯 Available Activities

| Activity | Description |
|---|---|
| 🎱 Billiard Tables | Professional-grade tables for casual and competitive play |
| 🎮 PlayStation 4 & 5 | Latest titles, multiplayer sessions, and tournaments |
| 🏎️ Racing Wheel Simulators | Immersive driving experience with high-end sim rigs |
| 🎯 Snooker Tables | Full-size tables in a calm, focused environment |
| 🃏 Card Games Area | Dedicated space for card game enthusiasts |

LIBERO hosts **weekly tournaments**, group events, and offers **hourly or package-based pricing** to suit every visitor.

---

## 🤖 Project Overview

The **LIBERO AI Agent Chatbot** is a conversational AI assistant designed to enhance the customer experience at LIBERO Gaming Center. It can answer visitor questions in real-time, assist with bookings, explain pricing, and provide information about upcoming events — all through a natural chat interface.

The agent is built on a **RAG (Retrieval-Augmented Generation)** pipeline combined with an **AI Agent Orchestrator**, enabling it to understand complex queries and provide accurate, context-aware responses.

---

## ✨ Features

- 💬 **Natural Language Conversations** — Understands and responds in a friendly, human-like tone
- 📚 **RAG Pipeline** — Retrieves relevant information from a knowledge base about LIBERO's services and policies
- 🧠 **AI Agent Orchestrator** — Routes queries intelligently between tools and knowledge sources
- 💰 **Pricing & Availability Info** — Answers questions about hourly rates and package deals
- 📅 **Events & Tournaments** — Provides details about upcoming events and how to register
- 🔌 **FastAPI Backend** — High-performance REST API layer for seamless integration
- 🌐 **Multi-interface Ready** — Can be embedded in a website, WhatsApp, or Telegram

---

## 🏗️ Architecture

```
User Query
    │
    ▼
┌─────────────────────┐
│   FastAPI Backend   │  ◄──── REST API Layer
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│  Agent Orchestrator │  ◄──── Decides routing logic
└──────┬──────────────┘
       │
  ┌────┴────┐
  │         │
  ▼         ▼
RAG Tool   Direct LLM
  │
  ▼
ChromaDB (Vector Store)
  │
  ▼
SentenceTransformers (Embeddings)
  │
  ▼
LLM Response Generation
  │
  ▼
Final Answer to User
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Language** | Python 3.10+ |
| **LLM** | OpenAI GPT / Groq / Ollama (configurable) |
| **RAG Framework** | LangChain + ChromaDB |
| **Embeddings** | SentenceTransformers |
| **API Backend** | FastAPI |
| **Frontend (Optional)** | Gradio / React |
| **Deployment** | Docker / Hugging Face Spaces |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- pip / uv package manager
- API key for your chosen LLM provider

### Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/libero-chatbot.git
cd libero-chatbot

# Install dependencies
pip install -r requirements.txt
# or using uv
uv pip install -r requirements.txt
```

### Configuration

Create a `.env` file in the root directory:

```env
OPENAI_API_KEY=your_api_key_here
# or
GROQ_API_KEY=your_groq_key_here

CHROMA_DB_PATH=./chroma_db
MODEL_NAME=gpt-4o-mini
```

### Run the Application

```bash
# Start the FastAPI server
uvicorn app.main:app --reload --port 8000
```

The API will be available at `http://localhost:8000`  
Interactive docs: `http://localhost:8000/docs`

### Docker (Optional)

```bash
docker build -t libero-chatbot .
docker run -p 8000:8000 --env-file .env libero-chatbot
```

---

## 📁 Project Structure

```
libero-chatbot/
│
├── app/
│   ├── main.py               # FastAPI entry point
│   ├── agent/
│   │   ├── orchestrator.py   # Agent logic & routing
│   │   └── tools.py          # Agent tools definitions
│   ├── rag/
│   │   ├── retriever.py      # ChromaDB retrieval
│   │   └── embeddings.py     # SentenceTransformer embeddings
│   └── api/
│       └── routes.py         # API endpoints
│
├── data/
│   └── libero_knowledge.txt  # LIBERO's knowledge base
│
├── chroma_db/                # Vector store (auto-generated)
├── .env                      # Environment variables (not committed)
├── requirements.txt
├── Dockerfile
└── README.md
```

---

## 💬 Example Interactions

```
User: What games do you have at LIBERO?
Bot:  At LIBERO, we offer PlayStation 4 & 5, Racing Wheel Simulators,
      Billiard Tables, Snooker Tables, and a Card Games Area! 🎮

User: How much does it cost to play PS5 for an hour?
Bot:  We offer hourly rates and flexible packages for PlayStation 5.
      You can check our latest pricing at the front desk or I can
      give you a summary — just ask!

User: Are there any tournaments this week?
Bot:  Yes! LIBERO hosts weekly tournaments. Stay tuned to our
      social media or ask our staff for the current schedule. 🏆
```

---

## 🤝 Contributing

Contributions are welcome! If you'd like to improve the chatbot or add new features:

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/my-feature`)
3. Commit your changes (`git commit -m 'Add new feature'`)
4. Push to the branch (`git push origin feature/my-feature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Laith Dabbas**  
AI & Robotics Graduate | AI Engineer  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/laith-dabbas-b9a38a289/)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=flat&logo=github)](https://github.com/laithdabbas)

---

<p align="center">Built with ❤️ for LIBERO Gaming Center — Where Gamers Unite 🎮</p>
