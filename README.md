# 🤖 CrewAI QA Test Case Generator

An AI-powered QA automation project using [CrewAI](https://www.crewai.com/) and [Ollama](https://ollama.com/) to automatically generate test cases for software features using local LLMs.

## 📋 Overview

This project demonstrates how to build a multi-agent AI crew that acts as a Senior QA Engineer to analyze features and generate structured test cases — including titles, steps, and expected results — without any manual effort.

## 🚀 Features

- 🧠 **Local LLM via Ollama** — runs on your machine, no cloud API required (uses `llama3.2:1b`)
- 🤝 **CrewAI Agents** — define role-based agents with goals and backstories
- 📝 **Automated Test Case Generation** — generates structured test cases with title, steps, and expected results
- 🔧 **Easy Configuration** — environment-based setup via `.env`

## 🗂️ Project Structure

```
Crew_AI/
├── testcase_crew.py   # Main crew: QA agent + task + crew runner
├── test_llm.py        # Quick LLM connectivity test
├── .env               # Environment variables (API keys, Ollama URL)
├── .env.example       # Example env file (safe to commit)
└── README.md          # This file
```

## ⚙️ Prerequisites

- Python 3.10+
- [Ollama](https://ollama.com/) installed and running locally
- `llama3.2:1b` model pulled in Ollama

```bash
# Pull the model
ollama pull llama3.2:1b
```

## 📦 Installation

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd Crew_AI
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv .venv
   .venv\Scripts\activate       # Windows
   # source .venv/bin/activate  # macOS/Linux
   ```

3. **Install CrewAI**
   ```bash
   pip install crewai
   ```

   Install additional dependencies:
   ```bash
   pip install python-dotenv
   ```

   Or install everything at once:
   ```bash
   pip install crewai python-dotenv
   ```

4. **Verify CrewAI installation**

   Check that CrewAI is installed correctly:
   ```bash
   pip show crewai
   ```

   Expected output:
   ```
   Name: crewai
   Version: x.x.x
   Summary: Cutting-edge framework for orchestrating role-playing, autonomous AI agents
   ...
   ```

   You can also verify by importing it in Python:
   ```bash
   python -c "import crewai; print('CrewAI version:', crewai.__version__)"
   ```

5. **Configure environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your values
   ```

## 🔑 Environment Variables

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here   # Optional: for Groq cloud LLM
Ollama_URL=http://localhost:11434      # Local Ollama server URL
```

> ⚠️ **Never commit your `.env` file** — it contains sensitive API keys.

## ▶️ Usage

### Test LLM Connectivity

Verify that Ollama is running and the model responds:

```bash
python test_llm.py
```

Expected output:
```
Hello! It's great to meet you. How can I assist you today?
```

### Run the QA Crew

Generate test cases for the login page feature:

```bash
python testcase_crew.py
```

> 💡 Make sure Ollama is running (`ollama serve`) and your `.env` file is configured before executing.

The crew will output **5 structured test cases** for a login page (email + password), each containing:
- **Title** — a short descriptive name for the test
- **Steps** — numbered steps to execute the test
- **Expected Result** — what should happen if the feature works correctly
- **Actual Result** — placeholder for manual QA execution

**Sample output snippet:**
```
# Test Case 1: Valid Login with Correct Credentials
Steps:
  1. Navigate to the login page
  2. Enter a valid email address
  3. Enter the correct password
  4. Click the "Login" button
Expected Result: User is redirected to the dashboard
```

## 🛠️ How It Works

```
┌─────────────────────────────────────────┐
│              CrewAI Crew                │
│                                         │
│  ┌─────────────────┐                   │
│  │    QA Agent     │  Role: QA Engineer │
│  │  (llama3.2:1b)  │  15 yrs experience│
│  └────────┬────────┘                   │
│           │                             │
│  ┌────────▼────────┐                   │
│  │  Test Plan Task │  5 test cases for  │
│  │                 │  login page        │
│  └────────┬────────┘                   │
│           │                             │
│  ┌────────▼────────┐                   │
│  │     Output      │  Structured test   │
│  │                 │  cases printed     │
│  └─────────────────┘                   │
└─────────────────────────────────────────┘
```

## 🧩 Extending the Project

You can easily extend this project by:

- **Adding more agents** — e.g., a Test Automation Engineer to convert test cases into Selenium scripts
- **Adding more tasks** — e.g., generate test data, prioritize test cases, or write bug reports
- **Switching LLMs** — swap `ollama/llama3.2:1b` with any Groq, OpenAI, or other supported model
- **Parameterizing the feature** — accept the feature description as a CLI argument

## 📚 Tech Stack

| Tool | Purpose |
|------|---------|
| [CrewAI](https://www.crewai.com/) | Multi-agent AI framework |
| [Ollama](https://ollama.com/) | Local LLM runner |
| [llama3.2:1b](https://ollama.com/library/llama3.2) | Language model |
| [python-dotenv](https://pypi.org/project/python-dotenv/) | Env variable management |

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

*Built with ❤️ using CrewAI + Ollama*
