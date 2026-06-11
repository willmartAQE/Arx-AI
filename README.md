<div align="center">
  <img src="arx.png" alt="ArX-AI Logo" width="150" height="150" style="border-radius: 32px; box-shadow: 0 4px 24px rgba(0, 0, 0, .45);">
  
  # ArX-AI — Your Private AI Workspace
  
  **A powerful, self-hosted AI workspace that runs 100% locally on your machine.**<br>
  *No subscriptions. No data mining. Complete privacy.*

  [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
  [![Platform: Cross-platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-success)](#installation-guide)

</div>

---

## 🌟 Why ArX-AI?

Have you ever wanted the power of ChatGPT, Perplexity, and Notion all in one place, but without sharing your sensitive data with big tech companies? 

**ArX-AI** is the answer. It is a stunning, lightweight, local-first interface that turns your computer into a private AI powerhouse. Whether you are coding, doing deep research, managing documents, or just exploring the latest open-source AI models, ArX-AI gives you a beautiful, unified workspace where **your data never leaves localhost**.

---

## 🔥 Features that will blow your mind

ArX-AI isn't just another chat wrapper. It's an entire ecosystem built around local AI:

### 💬 Intelligent Chat & Agents
- **Seamless Conversations:** Chat with any local Ollama model effortlessly.
- **Rich Markdown & Code:** Full support for syntax highlighting, making it perfect for developers.
- **Agent Mode:** Equip your AI with real tools! Let it browse the web (privately), read/write files on your computer, or even run sandboxed shell commands.

### 📚 Model Cookbook & One-Click Downloads
- **Hardware Auto-Detect:** ArX-AI analyzes your system's RAM and GPU to recommend the perfect models for your specific hardware.
- **One-Click Pull:** Download and manage models directly from the UI. No more typing commands in the terminal!

### 🥊 Model Arena (Blind A/B Testing)
- **Compare Models:** Send the exact same prompt to two different models side-by-side.
- **Blind Voting:** Vote for the best response without knowing which model generated it, then reveal the winner! Keep track of your battle history to find the ultimate model for your needs.

### 🔍 Deep Research
- Ask complex questions and let ArX-AI do the heavy lifting. It connects to a private SearXNG instance to search the web and arXiv simultaneously, reads multiple sources, extracts key information, and generates a fully cited, structured research report.

### 📝 Integrated Productivity Suite
- **Document Editor:** A rich text editor with AI superpower. Ask the AI to grammar-check, rewrite, or summarize your documents instantly.
- **Notes & Tasks:** Keep track of your ideas with freeform notes and task lists. The AI can even automatically extract action items from your chats!
- **Email & Calendar:** Connect IMAP/CalDAV accounts to let the AI triage your inbox, draft replies, and act as your personal scheduling assistant.

---

## 🚀 Installation Guide

ArX-AI is cross-platform and incredibly lightweight. Follow these simple steps to get your private AI running in minutes.

### Step 1 — Install the Engine (Ollama)

Ollama is the open-source engine that powers the AI models locally.
- **Windows:** Download from [ollama.com/download/windows](https://ollama.com/download/windows)
- **macOS:** Download from [ollama.com/download/mac](https://ollama.com/download/mac)
- **Linux:** Run `curl -fsSL https://ollama.com/install.sh | sh`

*Verify the installation by opening your terminal and typing `ollama --version`.*

### Step 2 — Launch ArX-AI

You can launch ArX-AI in several ways depending on your needs:

#### Option A: Simple file opening (Fastest)
The interface is entirely self-contained! Just clone the repo and open the `index.html` file using your OS's default opener:
```bash
# macOS
open index.html

# Linux
xdg-open index.html

# Windows
start index.html
```

#### Option B: Python Local Server
If you prefer to serve the file over localhost (recommended for some API features):
```bash
python3 -m http.server 3000
# Then open http://localhost:3000 in your browser
```

#### Option C: Node.js / npx Server
If you have Node.js installed:
```bash
npx serve .
# Then open the URL provided in the terminal
```

#### Option D: Full Docker Setup (Recommended for Deep Research & Memory)
To unlock **Deep Research (SearXNG)** and **Long-term Memory (ChromaDB)**, run the full stack using Docker. Requires [Docker Desktop](https://www.docker.com/products/docker-desktop/).

```bash
# 1. Clone the repository
git clone https://github.com/willmartAQE/Arx-AI.git
cd Arx-AI

# 2. Start all services
docker compose up -d

# 3. Open your browser at http://localhost:3000
```

---

## 💻 Recommended Models

Not sure which model to use? ArX-AI's Cookbook will guide you, but here are some safe bets:

| Your Hardware | Recommended Model | Use Case |
|----------|-------------------|----------|
| **Standard PC / 8GB RAM** | `llama3.2:3b` or `phi3.5` | Fast, lightweight general assistance |
| **Good PC / Mac 16GB RAM** | `llama3.1:8b` or `mistral:7b` | Excellent balance of speed and quality |
| **High-End PC / Mac 32GB+** | `llama3.1:70b` | Near-GPT-4 quality directly on your desk |

---

## 🔒 Your Privacy is Guaranteed

ArX-AI binds to `127.0.0.1` by default. **Zero data is sent to the cloud.** Your chats, your documents, and your API keys never leave your hard drive. 

*(Note: You can optionally connect external API models like OpenAI or Anthropic in the settings. If you do, standard API privacy policies apply).*

---

## 📜 License

ArX-AI is open-source and released under the **MIT License**. You are completely free to use, modify, and self-host it!

---
<div align="center">
  <b>Ready to take control of your AI? Scroll up and follow the Installation Guide!</b>
</div>
