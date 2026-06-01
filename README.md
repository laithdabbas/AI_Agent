# 🎮 LIBERO Gaming Center — AI Agent Chatbot

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python" />
  <img src="https://img.shields.io/badge/Gradio-UI-orange?style=for-the-badge&logo=gradio" />
  <img src="https://img.shields.io/badge/DeepSeek-V4--Pro-blueviolet?style=for-the-badge" />
  <img src="https://img.shields.io/badge/HuggingFace-Inference-yellow?style=for-the-badge&logo=huggingface" />
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge" />
</p>

> An intelligent AI-powered chatbot agent built for **LIBERO Gaming Center** — the premium gaming and entertainment destination. This assistant answers visitor questions about services, pricing, events, and more — and captures leads automatically via Pushover notifications.

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

The **LIBERO AI Agent Chatbot** is a conversational AI assistant that acts as a virtual staff member on LIBERO's website. It answers visitor questions in real-time, captures interested leads, and logs unanswered questions — all through a clean Gradio chat interface.

The agent uses **DeepSeek-V4-Pro** (via Hugging Face Inference API) and an **agentic tool-calling loop** that enables it to take real actions beyond just answering questions.

---

## ✨ Features

- 💬 **Natural Language Conversations** — Friendly, enthusiastic responses in the voice of a LIBERO staff member
- 🛠️ **Tool-Calling Agent Loop** — Keeps calling tools until the task is fully complete before replying
- 📋 **Lead Capture** — Automatically records visitor name, email, and notes when interest is shown
- ❓ **Unknown Question Logging** — Any question it can't answer gets recorded for follow-up
- 🔔 **Real-time Pushover Notifications** — Instant push alerts to your phone for every lead or unknown question
- 📄 **Context from PDF + Text** — Reads a LinkedIn-style PDF profile and a summary text file to ground its answers
- 🚀 **Deployed on Hugging Face Spaces** — Runs via Gradio with zero infrastructure setup

---

## 🏗️ Architecture

```
User Message (Gradio UI)
        │
        ▼
┌───────────────────────┐
│  system_prompt built  │  ← summary.txt + Profile.pdf (PyPDF)
│  from LIBERO context  │
└──────────┬────────────┘
           │
           ▼
┌───────────────────────┐
│  HuggingFace          │
│  InferenceClient      │  ← DeepSeek-V4-Pro:novita (via Novita)
└──────────┬────────────┘
           │
     ┌─────┴──────┐
     │            │
finish_reason   tool_calls
     │            │
     ▼            ▼
 Return       handle_tool_calls()
 Response          │
              ┌────┴─────────────────┐
              │                      │
   record_user_details()   record_unknown_question()
              │                      │
              └────────┬─────────────┘
                       ▼
              Pushover Push Notification
              (instant alert to phone 📱)
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Language** | Python 3.10+ |
| **LLM** | DeepSeek-V4-Pro via Novita (`deepseek-ai/DeepSeek-V4-Pro:novita`) |
| **LLM Client** | Hugging Face `InferenceClient` |
| **Tool Calling** | OpenAI-compatible function calling format |
| **PDF Parsing** | `pypdf` (PdfReader) |
| **Notifications** | Pushover API |
| **UI** | Gradio `ChatInterface` |
| **Config** | `python-dotenv` |
| **Deployment** | Hugging Face Spaces |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- A [Hugging Face](https://huggingface.co) account with an API token
- A [Pushover](https://pushover.net) account (user key + app token)

### Installation

```bash
# Clone the repository
git clone https://github.com/laithdabbas/AI_Agent
cd AI_Agent

# Install dependencies
pip install -r requirements.txt
```

### Required Files

Place the following in a `me/` folder:

```
me/
├── Profile.pdf      # Your LinkedIn-style profile (used as context)
└── summary.txt      # A plain-text summary of LIBERO's services
```

### Configuration

Create a `.env` file in the root directory:

```env
HF_TOKEN=your_huggingface_token_here
PUSHOVER_USER=your_pushover_user_key
PUSHOVER_TOKEN=your_pushover_app_token
```

### Run the Application

```bash
python app.py
```

Gradio will launch the chat UI locally at `http://localhost:7860`

---

## 📁 Project Structure

```
libero-chatbot/
│
├── app.py               # Main application — agent loop, tools, Gradio UI
├── me/
│   ├── Profile.pdf      # PDF context (parsed with pypdf)
│   └── summary.txt      # LIBERO services summary
│
├── .env                 # Environment variables (never commit this)
├── requirements.txt
└── README.md
```

---

## 🔧 Agent Tools

The agent has access to two tools it calls autonomously:

### `record_user_details`
Triggered when a visitor expresses interest in visiting or booking. Captures:
- `email` *(required)* — visitor's email address
- `name` *(optional)* — visitor's name
- `notes` *(optional)* — context about the conversation

### `record_unknown_question`
Triggered whenever the agent cannot answer a question. Captures:
- `question` — the unanswered question, for staff follow-up

Both tools send an **instant Pushover notification** to the owner's phone.

---

## 💬 Example Interactions

```
User: What games do you have at LIBERO?
Bot:  We have PlayStation 4 & 5, Racing Wheel Simulators,
      Billiard & Snooker Tables, and a Card Games Area! 🎮
      Which one sounds most exciting to you?

User: I'd love to visit — my email is ahmed@example.com
Bot:  Awesome, Ahmed! I've noted your details and someone from
      the LIBERO team will be in touch. Can't wait to see you! 🏆
      [→ record_user_details tool fires, Pushover notification sent]

User: Do you have VR headsets?
Bot:  Great question! I don't have details on that right now,
      but I've flagged it for our team to follow up on.
      [→ record_unknown_question tool fires]
```

---

## 🤝 Contributing

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
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://linkedin.com/in/YOUR_PROFILE)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=flat&logo=github)](https://github.com/YOUR_USERNAME)

---

<p align="center">Built with ❤️ for LIBERO Gaming Center — Where Gamers Unite 🎮</p>
