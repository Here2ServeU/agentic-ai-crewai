# Agentic AI Systems Engineer — Video 4
### Build Your First Multi-Agent System with CrewAI
**Transformed 2 Succeed (T2S) · Emmanuel Naweji**
🌐 [emmanuelnaweji.com](https://www.emmanuelnaweji.com) · [github.com/Here2ServeU](https://github.com/Here2ServeU)

---

## What You Build in This Video

A three-agent CrewAI system that autonomously:

1. **Researches** the FinTech market (Market Researcher Agent)
2. **Analyzes** the top risk factors (Financial Analyst Agent)
3. **Writes** an executive briefing and saves it to a file (Report Writer Agent)

Each agent has a role, a goal, a backstory, and tools. They work in sequence — the output of one becomes the input of the next. This is multi-agent collaboration in production.

```
[Market Researcher] → research brief
                              ↓
                   [Financial Analyst] → risk analysis
                                               ↓
                                    [Report Writer] → executive_briefing.md
```

---

## Repository Structure

```
agentic-ai-crewai/
├── crew.py              # Main script — agents, tasks, crew, and runner
├── requirements.txt     # Python dependencies
├── .env.example         # Template for your API keys
├── .gitignore           # Protects secrets from being pushed to GitHub
└── README.md            # This file
```

---

## Prerequisites

Before you begin, make sure you have:

| Requirement | Version | Check Command |
|-------------|---------|---------------|
| Python | 3.10 or higher | `python --version` |
| pip | Latest | `pip --version` |
| VS Code | Latest | — |
| Git | Any | `git --version` |
| OpenAI API Key | — | [platform.openai.com](https://platform.openai.com) |

---

## Setup — Windows

### Step 1 — Install Python

1. Go to [python.org/downloads](https://www.python.org/downloads/)
2. Download Python 3.11 or higher
3. Run the installer — **check "Add Python to PATH"** before clicking Install
4. Open Command Prompt and verify:

```cmd
python --version
pip --version
```

### Step 2 — Install VS Code

1. Go to [code.visualstudio.com](https://code.visualstudio.com)
2. Download and install for Windows
3. Open VS Code → Extensions (Ctrl+Shift+X) → search **Python** → install the Microsoft Python extension

### Step 3 — Clone the Repository

```cmd
git clone https://github.com/Here2ServeU/agentic-ai-crewai.git
cd agentic-ai-crewai
```

### Step 4 — Create a Virtual Environment

```cmd
python -m venv venv
venv\Scripts\activate
```

You should see `(venv)` at the start of your prompt.

### Step 5 — Install Libraries

```cmd
pip install -r requirements.txt
```

### Step 6 — Set Your API Key

**Option A — Environment variable (session only):**

```cmd
set OPENAI_API_KEY=sk-your-key-here
```

**Option B — .env file (recommended, persists across sessions):**

```cmd
copy .env.example .env
```

Open `.env` in VS Code and replace `sk-your-openai-key-here` with your actual key.

> **Never commit `.env` to GitHub.** It is already listed in `.gitignore`.

### Step 7 — Open in VS Code

```cmd
code .
```

---

## Setup — macOS

### Step 1 — Install Python

Check if Python 3.10+ is already installed:

```bash
python3 --version
```

If not, install it with Homebrew (recommended):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install python@3.11
```

### Step 2 — Install VS Code

1. Go to [code.visualstudio.com](https://code.visualstudio.com)
2. Download for macOS and drag to Applications
3. Open VS Code → Extensions (⌘+Shift+X) → search **Python** → install

### Step 3 — Clone the Repository

```bash
git clone https://github.com/Here2ServeU/agentic-ai-crewai.git
cd agentic-ai-crewai
```

### Step 4 — Create a Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

You should see `(venv)` at the start of your prompt.

### Step 5 — Install Libraries

```bash
pip install -r requirements.txt
```

### Step 6 — Set Your API Key

**Option A — Environment variable (current terminal session only):**

```bash
export OPENAI_API_KEY="sk-your-key-here"
```

**Option B — .env file (recommended, persists across sessions):**

```bash
cp .env.example .env
```

Open `.env` and replace `sk-your-openai-key-here` with your actual key.

To make the environment variable permanent across all terminal sessions:

```bash
echo 'export OPENAI_API_KEY="sk-your-key-here"' >> ~/.zshrc
source ~/.zshrc
```

### Step 7 — Verify the Key Is Set

```bash
echo $OPENAI_API_KEY
```

You should see your key printed. If it returns blank, re-run the export command.

### Step 8 — Open in VS Code

```bash
code .
```

---

## Setup — Linux (Ubuntu / Debian)

### Step 1 — Install Python

```bash
sudo apt update
sudo apt install python3.11 python3.11-venv python3-pip -y
python3 --version
```

### Step 2 — Install VS Code

```bash
sudo apt install wget gpg -y
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
echo "deb [arch=amd64] https://packages.microsoft.com/repos/code stable main" | sudo tee /etc/apt/sources.list.d/vscode.list
sudo apt update
sudo apt install code -y
```

Then install the Python extension:

```bash
code --install-extension ms-python.python
```

### Step 3 — Clone the Repository

```bash
git clone https://github.com/Here2ServeU/agentic-ai-crewai.git
cd agentic-ai-crewai
```

### Step 4 — Create a Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 5 — Install Libraries

```bash
pip install -r requirements.txt
```

### Step 6 — Set Your API Key

**Option A — Environment variable (session only):**

```bash
export OPENAI_API_KEY="sk-your-key-here"
```

**Option B — .env file (recommended):**

```bash
cp .env.example .env
nano .env   # or: code .env
```

Replace `sk-your-openai-key-here` with your actual key.

To make the environment variable permanent:

```bash
echo 'export OPENAI_API_KEY="sk-your-key-here"' >> ~/.bashrc
source ~/.bashrc
```

### Step 7 — Open in VS Code

```bash
code .
```

---

## Understanding the Code

### Agents

Each agent is defined with four properties:

```python
market_researcher = Agent(
    role="Senior FinTech Market Researcher",   # WHO the agent is
    goal="Identify top FinTech trends...",     # WHAT the agent is trying to do
    backstory="You are a seasoned analyst...", # HOW the agent reasons and behaves
    tools=[search_tool],                       # WHAT tools the agent can call
    verbose=True,
)
```

### Tasks

Each task is assigned to one agent and specifies exactly what to produce:

```python
task_research = Task(
    description="Research the FinTech industry...",   # the assignment
    expected_output="A structured brief with...",     # the deliverable
    agent=market_researcher,                          # who does it
)
```

### Crew

The Crew wires agents and tasks together:

```python
crew = Crew(
    agents=[market_researcher, financial_analyst, report_writer],
    tasks=[task_research, task_analysis, task_report],
    process=Process.sequential,   # tasks run in order, output flows forward
)
```

### The Three-Agent Flow

| # | Agent | Task | Output |
|---|-------|------|--------|
| 1 | Market Researcher | Research FinTech trends | Research brief |
| 2 | Financial Analyst | Analyze risks from the brief | Risk analysis table |
| 3 | Report Writer | Write executive briefing | `fintech_executive_briefing.md` |

---

## Running the Script

Make sure your virtual environment is active and your API key is set, then:

```bash
python crew.py
```

You will see each agent's reasoning printed to the terminal in real time.
When the crew finishes, you will find `fintech_executive_briefing.md` in the project folder.

### Expected Terminal Output

```
============================================================
  T2S Agentic AI — FinTech Research Crew
  Transformed 2 Succeed · Emmanuel Naweji
============================================================

[Senior FinTech Market Researcher]: Starting task...
[Senior FinTech Market Researcher]: I will research the current state...
...
[Lead Financial Risk Analyst]: Received research brief. Analyzing risks...
...
[Executive Report Writer]: Drafting executive briefing...
...

============================================================
  CREW COMPLETED — Final Report Below
============================================================

# FinTech Executive Briefing — Q3 2025
...

[INFO] Report saved to: fintech_executive_briefing.md
```

---

## 🔧 Troubleshooting

| Error | Cause | Fix |
|-------|-------|-----|
| `OPENAI_API_KEY is not set` | Key not exported | Run `export OPENAI_API_KEY="sk-..."` |
| `ModuleNotFoundError: crewai` | venv not active or install failed | Run `source venv/bin/activate` then `pip install -r requirements.txt` |
| `AuthenticationError` | Wrong or expired API key | Regenerate at [platform.openai.com](https://platform.openai.com/api-keys) |
| `RateLimitError` | Free tier quota | Add billing at [platform.openai.com/billing](https://platform.openai.com/billing) |
| `command not found: python` | macOS/Linux uses `python3` | Replace `python` with `python3` |

---

## 📚 Libraries Used

| Library | Purpose |
|---------|---------|
| `crewai` | Agent and crew orchestration framework |
| `crewai-tools` | Pre-built tools including web search |
| `openai` | OpenAI API client (used by CrewAI internally) |
| `python-dotenv` | Loads `.env` file into environment variables |

---

## 🔒 Security Rules (Non-Negotiable)

1. **Never hardcode API keys** in your Python files
2. **Never commit `.env`** to GitHub — it is in `.gitignore`
3. **Always load keys from the environment** using `os.environ.get()`
4. **Rotate keys immediately** if you accidentally push them

---

## 🚀 What Comes Next

| Video | Topic |
|-------|-------|
| Video 5 | Adding memory to agents (short-term + long-term) |
| Video 6 | RAG pipeline — connecting agents to a vector database |
| Video 7 | Deploying agents to AWS / Azure / GCP |
| Video 8 | Observability — LangSmith tracing, token cost dashboards |

---

## 👤 About the Instructor

**Emmanuel Naweji** is a PhD candidate in AI/ML, Cloud Architect (AWS · Azure · GCP), SRE, and founder of **Transformed 2 Succeed (T2S)** — a training program that takes people from no IT experience to production-grade AI engineers.

- 🌐 [emmanuelnaweji.com](https://www.emmanuelnaweji.com)
- 💻 [github.com/Here2ServeU](https://github.com/Here2ServeU)

> *"A chatbot answers. An agent acts. This course teaches you to build the second kind."*

---

## 📄 License

MIT License — free to use, modify, and share with attribution.
