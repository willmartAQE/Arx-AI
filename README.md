# ArX-AI — Private Local AI Workspace

A self-hosted AI workspace that runs entirely on your machine.
Chat, research, manage models, and compare them — all in one beautiful UI.
Compatible with all major operating systems: **Windows, macOS, and Linux**.

---

## What does it do?

ArX-AI is a private, local-first interface for your AI workflows. Your data never leaves your computer.
- **Chat:** Multi-turn conversations with any Ollama model, supporting code highlighting and Markdown.
- **Model Cookbook:** Automatically detects your hardware and recommends models. Download and manage models with one click directly from the UI.
- **Model Arena:** Blind A/B testing to compare two models side-by-side.
- **Deep Research:** Web search and document extraction capabilities.
- **Tools & Agents:** Equip your models with tools like web search, shell execution, and file reading.

---

## Installation Guide

You can run ArX-AI on any operating system. Follow the steps below for a quick local setup.

### Step 1 — Install Ollama (Required)

Ollama is the engine that runs the AI models locally.
- **Windows:** Download from [ollama.com/download/windows](https://ollama.com/download/windows)
- **macOS:** Download from [ollama.com/download/mac](https://ollama.com/download/mac)
- **Linux:** Run `curl -fsSL https://ollama.com/install.sh | sh`

Once installed, verify it's running by opening your terminal/command prompt and typing:
```bash
ollama --version
```

### Step 2 — Open ArX-AI

ArX-AI is built to be extremely lightweight. You can run it via the terminal in several ways, depending on what tools you have installed:

**Option A: Simple file opening (No Server Needed)**
Since the interface is entirely self-contained, you can simply open the `index.html` file using your OS's default opener:
```bash
# macOS
open index.html

# Linux
xdg-open index.html

# Windows
start index.html
```

**Option B: Python Local Server**
If you have Python installed and prefer to serve the file over localhost (recommended for some API features):
```bash
python3 -m http.server 3000
# Then open http://localhost:3000 in your browser
```

**Option C: Node.js / npx Server**
If you have Node.js installed:
```bash
npx serve .
# Then open the URL provided in the terminal
```

**Option D: Full Docker Setup (Recommended for Advanced Features)**
If you want to use advanced features like SearXNG (private web search) and ChromaDB (vector memory), you can run the full stack using Docker.
Requires [Docker Desktop](https://www.docker.com/products/docker-desktop/).

```bash
# 1. Clone or download the repository
git clone https://github.com/willmartAQE/Arx-AI.git
cd Arx-AI

# 2. Start all services
docker compose up -d

# 3. Open your browser
# Go to http://localhost:3000
```

---

## Model Recommendations

Depending on your hardware, here are some recommended models to pull via the Cookbook or Terminal:

| Hardware | Recommended model |
|----------|-------------------|
| Standard PC / 8GB RAM | `llama3.2:3b` , `phi3.5` |
| Good PC / Mac 16GB RAM | `llama3.1:8b` , `mistral:7b` |
| High-End PC / Mac 32GB+ | `llama3.1:70b` (Requires 40GB+ RAM/VRAM) |

---

## Security & Privacy

**ArX-AI binds to `127.0.0.1` by default.** This means it is only accessible from your own machine.
When using local Ollama models, **zero data is sent to the internet**. Your prompts, documents, and chats remain 100% private.

*(Optional)* You can connect external API models (like OpenAI or Anthropic) in the Settings. If you do, standard API privacy policies apply for those specific models.

---

## License

MIT License — Use, modify, and self-host freely.
