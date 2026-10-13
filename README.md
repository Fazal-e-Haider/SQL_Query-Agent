# 🤖 SQL Query Agent

An autonomous AI database assistant powered by **LangChain** and **LLM Tool Calling**. Connects to SQLite databases and answers complex natural language queries by inspecting schemas, synthesizing SQL, executing read-safe queries, and returning structured markdown reports.

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![LangChain](https://img.shields.io/badge/LangChain-1.x%20%2F%200.3%2B-green.svg)](https://www.langchain.com/)
[![SQLite](https://img.shields.io/badge/Database-SQLite3-lightgrey.svg)](https://www.sqlite.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## ✨ Features

- 🧠 **Natural Language to SQL**: Converts analytical business questions into accurate SQL queries.
- 🛡️ **Read-Only Safety by Default**: Mounts SQLite databases using read-only URIs (`?mode=ro`) to prevent accidental data modifications or destructive queries.
- 🔌 **Universal LLM Compatibility**: Works seamlessly with OpenAI (`gpt-4o-mini`, `gpt-4o`) as well as OpenAI-compatible endpoints (Groq, OpenRouter, Ollama, vLLM).
- 📦 **Zero-Config Demo Database**: Automatically provisions an e-commerce database with customers, products, and order tables for instant testing.
- 💬 **Interactive & One-Shot CLI Modes**: Query in a continuous conversational loop or execute single questions via command-line arguments.

---

## 🏗️ Architecture

```
User Query (Natural Language)
       │
       ▼
┌─────────────────────────┐
│   LangChain SQL Agent   │ ◄─── Schema Introspection (Tables, Columns)
└────────────┬────────────┘
             │
             ├─────► Generates SQL Query
             │
             ▼
┌─────────────────────────┐
│ SQLite Database Engine  │ (Read-Only Mode)
└────────────┬────────────┘
             │
             ├─────► Executes Query & Returns Rows
             │
             ▼
┌─────────────────────────┐
│   LLM Response Engine   │ ───► Formats Markdown Tables & Insights
└─────────────────────────┘
```

---

## 🚀 Quick Start

### 1. Clone & Set Up Environment

```bash
git clone https://github.com/Fazal-e-Haider/SQL_Query-Agent.git
cd SQL_Query-Agent

# Create and activate virtual environment
python -m venv .venv

# Windows:
.\.venv\Scripts\activate

# Linux / macOS:
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Configure API Keys

Copy the sample environment file and add your credentials:

```bash
cp .env.example .env
```

Edit `.env`:

```env
OPENAI_API_KEY=your_api_key_here

# Optional: To use Groq or another OpenAI-compatible provider:
# OPENAI_BASE_URL=https://api.groq.com/openai/v1
# MODEL=llama-3.3-70b-versatile
```

---

## 💻 Usage

### Demo Mode (Interactive)
Automatically provisions a sample e-commerce store (`demo.sqlite`) and launches an interactive chat session:

```bash
python agent.py
```

### Single Question
Directly execute queries from scripts or the terminal:

```bash
python agent.py --question "What are the top 3 best-selling products by quantity?"
```

**Example Output:**
```text
📊 Connected to: demo.sqlite
🔒 Mode: read-only
📋 Tables: customers, orders, products

❓ Question: What are the top 3 best-selling products by quantity?

✅ Answer:
| Rank | Product        | Total Quantity Sold |
|------|----------------|---------------------|
| 1    | Wireless Mouse | 5                   |
| 2    | Laptop Pro     | 2                   |
| 3    | Python Book    | 1                   |
```

### Connect to Custom Database
Point the agent to any existing SQLite file:

```bash
python agent.py --db /path/to/your/database.sqlite
```

### Write Mode (Optional)
If you intentionally need to perform insert, update, or table mutation operations on disposable databases:

```bash
python agent.py --db mydb.sqlite --allow-write
```

---

## 📂 Project Structure

```
sql-query-agent/
├── agent.py            # Main agent implementation & CLI runner
├── requirements.txt    # Python dependencies
├── metadata.yaml       # Project specifications
├── .env.example        # Environment variable template
├── .gitignore          # Git exclusion rules
└── README.md           # Documentation
```

---

## 👤 Author

* **Fazal-e-Haider**
  * GitHub: [@fazal-e-haider](https://github.com/fazal-e-haider)

---

## 📄 License

This project is licensed under the MIT License.
