# Nexus — Private Local AI Workspace

A self-hosted AI workspace that runs entirely on your machine.
Chat, research, notes, email, calendar, and a model cookbook — all in one beautiful UI.

---

## Quick Start — macOS Monterey (Recommended)

### Prerequisites
- macOS 12 Monterey or later
- [Homebrew](https://brew.sh)
- [Docker Desktop for Mac](https://www.docker.com/products/docker-desktop/) (optional, for SearXNG + ChromaDB)

### Step 1 — Install Ollama (local LLM inference)
```bash
brew install ollama
```

Or download the macOS app from https://ollama.com/download/mac

### Step 2 — Start Ollama and pull a model
```bash
# Start Ollama (runs in background, uses Metal GPU on Apple Silicon)
ollama serve &

# Pull a fast 3B model to start (~2 GB download)
ollama pull llama3.2:3b

# Optional: pull a more capable 8B model (~5 GB)
ollama pull llama3.1:8b

# Optional: pull Mistral for coding
ollama pull mistral:7b
```

### Step 3 — Open Nexus
```bash
# Option A: Open directly in browser (no server needed)
open index.html

# Option B: Serve via Python (better for IMAP/CalDAV features)
python3 -m http.server 3000
open http://localhost:3000

# Option C: Full Docker stack (adds SearXNG search + ChromaDB memory)
docker compose up -d
open http://localhost:3000
```

---

## Full Docker Setup

```bash
# Clone / unzip Nexus
cd nexus-ai

# (Optional) Configure environment
cp .env.example .env
nano .env   # set passwords, ports, bind address

# Start all services
docker compose up -d

# Check everything is running
docker compose ps

# View logs
docker compose logs -f nexus
```

---

## Model Recommendations by Hardware

| Hardware             | Recommended model       | Why                                   |
|----------------------|-------------------------|---------------------------------------|
| Apple M1/M2 8 GB     | llama3.2:3b, phi3.5     | Fits in RAM with headroom             |
| Apple M1/M2 16 GB    | llama3.1:8b, mistral:7b | Best quality/speed balance            |
| Apple M2/M3 Pro 18 GB| llama3.1:8b, gemma2:9b  | Can run 13B models too                |
| Apple M3 Max 36 GB+  | llama3.1:70b (Q4)       | Near-GPT-4 quality locally            |
| PC with 16 GB RAM    | mistral:7b (Q4)         | CPU-only, slower but capable          |
| PC with RTX 3090+    | llama3.1:70b            | Full GPU acceleration                 |

---

## Features

### Chat
- Multi-turn conversations with any Ollama or API model
- Streaming responses
- Code highlighting, Markdown rendering
- File attachment (PDF, TXT, images)
- Conversation history with search

### Agent Mode
Tools the agent can use (toggle per session):
- 🌐 **Web search** — via local SearXNG (private, no tracking)
- 📎 **Files** — read/write files in your workspace directory
- 💻 **Shell** — run bash commands (sandboxed in Docker)
- 🧠 **Memory** — long-term memory via ChromaDB embeddings
- ⚡ **Skills** — saved prompt templates and tool chains

### Deep Research
1. Enter a query
2. Nexus searches web + arXiv simultaneously
3. Evaluates source credibility
4. Extracts key passages
5. Generates a structured report with citations
6. Export to PDF, Markdown, or save to Documents

### Model Arena (Blind A/B Testing)
- Send the same prompt to two models side-by-side
- Both models are hidden — vote for the better response
- Reveal identities after voting
- Battle history saved locally

### Model Cookbook
- Auto-detects your hardware (RAM, GPU, Apple Neural Engine)
- Recommends models you can actually run
- One-click download via Ollama
- Benchmarks and performance ratings

### Document Editor
- Rich text editor with AI suggestions
- Grammar and tone checking
- Summarise, expand, rewrite sections
- Export to Markdown or PDF
- Documents stored locally in `~/nexus-workspace/docs/`

### Notes & Tasks
- Freeform notes with full-text search
- Task lists with due dates and reminders
- AI can create notes/tasks from chat
- Everything stored in local SQLite

### Email (IMAP/SMTP)
- Connect any email account (Gmail, Outlook, Fastmail, self-hosted)
- AI triage: auto-categorise, summarise, detect urgency
- Draft reply suggestions
- Extract action items → tasks
- All email stored and processed locally

### Calendar (CalDAV)
- Sync with Nextcloud, Radicale, iCloud, Google Calendar
- Local-first: works offline, syncs when connected
- AI scheduling assistant
- Reminders and recurring events

---

## Connecting API Models (Optional)

Nexus works 100% locally with Ollama. For cloud models, add keys in Settings:

| Provider   | Where to get key                    | Models available           |
|------------|-------------------------------------|----------------------------|
| OpenAI     | platform.openai.com/api-keys        | gpt-4o, o3, o4-mini        |
| Anthropic  | console.anthropic.com               | claude-sonnet, claude-opus |
| OpenRouter | openrouter.ai/keys                  | 100+ models, one key       |

**Privacy note:** When using API models, your messages are sent to those providers' servers. Anthropic, OpenAI, and others have their own privacy policies. For fully private usage, use only Ollama/llama.cpp models.

---

## Security

### Default (safe)
Nexus binds to `127.0.0.1:3000` — only accessible from your own machine.
No authentication is required in this mode since only you can access it.

### Exposing to your local network (LAN)
⚠️ **Warning:** If you change the bind address to `0.0.0.0`, anyone on your network can access Nexus, including your chats, documents, email, and API keys.

If you need LAN access:
1. Set a strong password in Settings → Security
2. Keep Nexus on `0.0.0.0` only on trusted networks (home, not café WiFi)
3. Consider HTTPS via Caddy or nginx reverse proxy with a self-signed cert

### Exposing to the internet
🚨 **Not recommended** without:
- HTTPS with a valid certificate (Let's Encrypt via Caddy)
- Strong authentication (password + optional 2FA)
- Firewall rules limiting access by IP
- Regular security updates

---

## Directory Structure

```
nexus-ai/
├── index.html          # Main app (single-file, works standalone)
├── docker-compose.yml  # Full stack with SearXNG + ChromaDB
├── nginx.conf          # Reverse proxy config
├── .env.example        # Environment variable template
├── README.md           # This file
└── searxng/            # SearXNG configuration (auto-created)
    └── settings.yml
```

---

## Environment Variables (.env)

```bash
# Network
NEXUS_HOST=127.0.0.1     # Change to 0.0.0.0 for LAN access
NEXUS_PORT=3000

# Security
NEXUS_PASSWORD=          # Set a strong password for LAN/internet access
SEARXNG_SECRET=          # Auto-generated on first run

# API Keys (stored encrypted in local keychain on macOS)
OPENAI_API_KEY=
ANTHROPIC_API_KEY=
OPENROUTER_API_KEY=
```

---

## Updating

```bash
# Pull latest and restart
git pull
docker compose pull
docker compose up -d
```

---

## Troubleshooting

**Ollama not connecting?**
```bash
# Check it's running
curl http://localhost:11434/api/tags

# Restart
pkill ollama && ollama serve &
```

**"No models available"?**
```bash
# List downloaded models
ollama list

# Pull the recommended starter model
ollama pull llama3.2:3b
```

**Docker services not starting?**
```bash
docker compose logs searxng
docker compose logs chromadb
```

**macOS Monterey specific notes:**
- Metal acceleration requires macOS 12.0+ ✓ (Monterey is 12.x)
- Ollama native app works best — avoids Docker networking complexity
- If using Docker Desktop, ensure "Use Virtualization framework" is enabled in settings

---

## License

MIT — use, modify, self-host freely.
