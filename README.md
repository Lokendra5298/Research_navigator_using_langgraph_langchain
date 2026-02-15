**Project Name**  
**Scholarly Research Navigator**  
(or a slightly shorter/catchier alternative: **ArXiv Navigator**, **PaperLens**, **Research Compass**)

Below is a ready-to-use `README.md` file you can copy-paste directly into your repository root.

```markdown
# Scholarly Research Navigator

**AI-powered academic paper discovery, filtering, semantic search and literature review generator**  
using ArXiv metadata (~2M papers), LangChain/LangGraph agents, Google Gemini, and local embeddings.

<p align="center">
  <img src="https://via.placeholder.com/800x400/2c3e50/ecf0f1?text=Scholarly+Research+Navigator" alt="Scholarly Research Navigator" />
  <br/>
  <em>(replace this placeholder with a real screenshot later)</em>
</p>

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
```

### 3. Download Data

Download the arXiv metadata file (~1.2 GB compressed) from:  
https://www.kaggle.com/datasets/Cornell-University/arxiv

Place the file as:  
`arxiv-metadata-oai-snapshot.json`  
(in the same folder as `data_loader.py`)

For quick testing you can use a tiny subset (4–20 papers) — see example in project discussions.

### 4. Run

```bash
# Option A – Web interface (recommended)
streamlit run streamlit_app.py

# Option B – Console test run
python main.py
```

**First run** will:
- Load & clean metadata
- Create SQLite database (~several GB)
- Build FAISS vector index (can take 15–90 min on full dataset)

Subsequent runs are fast.

## 📁 Project Structure

```
.
├── data_loader.py          # Loads & cleans arXiv JSON metadata
├── data_base.py            # SQLite setup & connection
├── rag.py                  # FAISS vector store with local embeddings
├── tools.py                # SQL filter, vector search, PDF fetch tools
├── llm.py                  # Gemini model + HuggingFace embeddings factory
├── agent.py                # LangGraph agent & workflow definition
├── streamlit_app.py        # Web UI
├── main.py                 # Simple console runner for testing
├── utils.py                # Small helpers
├── requirements.txt
├── .env.example            # Copy to .env and fill API key
└── arxiv-metadata-oai-snapshot.json    (you provide this)
```

## Example Queries to Try

- "Recent papers in cs.AI after 2023"
- "Show me papers by Ashish Vaswani on transformers"
- "Find papers about Low-rank Adaptation and compare to full fine-tuning"
- "Summarize the main ideas in the most cited attention papers"

## Important Notes

- **PDF fetching** is done live from arXiv → respect rate limits (small delays are already added)
- **Gemini free tier** has strict rate & token limits — monitor usage
- Full 2M paper indexing requires significant RAM & time
- Current router prompt is basic → can be significantly improved

## Roadmap / Possible Improvements

- [ ] Conversation memory (multi-turn chat)
- [ ] Better tool selection & parallel tool calling
- [ ] Local LLM fallback (Ollama / LM Studio)
- [ ] Citation graph & related papers
- [ ] Cached PDFs & summaries
- [ ] Export literature review as markdown / LaTeX
- [ ] Support other sources (Semantic Scholar, PubMed…)


Built with curiosity & too much coffee  
© 2025–2026 Lokendra  
```
