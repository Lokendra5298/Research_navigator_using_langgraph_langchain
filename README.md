# Scholarly Research Navigator

**AI-powered academic paper discovery, filtering, semantic search and literature review generator**  
using ArXiv metadata (~2M papers), LangChain/LangGraph agents, Google Gemini, and local embeddings.
## ✨ Features

- Natural language queries about research papers
- **SQL filtering** by category, author, year, etc.
- **Semantic vector search** over abstracts (using sentence-transformers)
- Automatic fetching & text extraction from arXiv PDFs
- Long-context literature review / comparison generation powered by **Gemini 1.5 Pro**
- Simple Streamlit web interface
- LangGraph-based agent workflow with clear tool routing

Example query:
> Find recent papers on Low-Rank Adaptation (LoRA) and explain how they differ from standard fine-tuning.

## 🛠 Tech Stack

| Layer                | Technology                                 |
|----------------------|--------------------------------------------|
| LLM / Chat           | Google Gemini 1.5 Pro                      |
| Embeddings           | sentence-transformers/all-MiniLM-L6-v2     |
| Agent framework      | LangGraph + LangChain                      |
| Vector store         | FAISS (local)                              |
| Structured filtering | SQLite + LangChain SQL toolkit             |
| PDF extraction       | PyPDF                                      |
| UI                   | Streamlit                                  |
| Data                 | arXiv metadata snapshot (Kaggle)           |

## 🚀 Quick Start

### 1. Prerequisites

- Python 3.10+
- Google Gemini API key → [Get one here](https://aistudio.google.com/app/apikey)
- ~20 GB free disk space (for full dataset + index)
- 16–32 GB RAM recommended for first indexing run

### 2. Installation

```bash
# Clone or download the repository
# cd into project folder

# Create and activate virtual environment
python -m venv venv
.\venv\Scripts\activate          # Windows
# source venv/bin/activate       # Linux/macOS

# Install dependencies
pip install -r requirements.txt

# Set your Gemini API key (choose ONE method)
$env:GOOGLE_API_KEY = "AIzaSyYourRealKeyHere"               # Windows PowerShell
# or
# export GOOGLE_API_KEY="AIzaSyYourRealKeyHere"             # Linux/macOS
# or create .env file with: GOOGLE_API_KEY=AIzaSy...
