# RAG Learning Resources

A hands-on notebook for building a **local, private RAG (Retrieval-Augmented Generation)** pipeline using open-source tools — no API keys, no data sent to the cloud.

---

## What You'll Build

A conversational agent that can read any PDF and answer questions about it — using only tools running on your machine.

---

## Stack

| Component | Tool |
|-----------|------|
| LLM | Gemma 2 2B via [Ollama](https://ollama.com) |
| Embeddings | `sentence-transformers/all-MiniLM-L6-v2` (HuggingFace) |
| Vector Store | ChromaDB |
| Orchestration | LangChain |
| Document Loader | PyPDFLoader |

---

## Prerequisites

### 1. Install Ollama

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

### 2. Pull Gemma 2 2B (~1.6 GB)

```bash
ollama pull gemma2:2b
```

### 3. Create a virtual environment and install dependencies

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

---

## Usage

Open the notebook in Jupyter or PyCharm:

```bash
jupyter lab
```

Then open `Summarizing_Private_Documents_Using_RAG_LangChain_and_Ollama.ipynb` and run cells top to bottom.

The notebook will:
1. Auto-start the Ollama server if it's not running
2. Download the sample PDF
3. Split, embed, and index it in ChromaDB
4. Let you query it with natural language — with memory across turns

To use your own PDF, replace the `filename` and `url` in the load cell with your file path.

---

## Hardware Requirements

| Resource | Minimum |
|----------|---------|
| RAM | 4 GB free (Gemma 2 2B needs ~1.6 GB) |
| Disk | 3 GB free (model + dependencies) |
| GPU | Not required — runs on CPU |

Tested on Intel Core i5-1235U, 14 GB RAM, no GPU.

---

## Notebook Structure

1. **Setup** — install dependencies, start Ollama
2. **Preprocessing** — load PDF, split into chunks, embed into ChromaDB
3. **LLM Construction** — connect to local Gemma 2 via Ollama
4. **RetrievalQA** — simple Q&A over the document
5. **Prompt Template** — prevent hallucination with a grounded prompt
6. **Conversation Memory** — follow-up questions with context
7. **Interactive Agent** — chat loop over your document
8. **Exercises** — try your own PDF, return source chunks, swap models

---

## Sample Document

The notebook uses the [Sentinel Kiln DB paper](https://openreview.net/pdf?id=efGzsxVSEC) as a demo document — a research paper on satellite-based brick kiln detection in South Asia.

---

## Why Local?

| | Cloud LLM API | This Notebook |
|---|---|---|
| LLM | Remote model via API | Gemma 2 2B via Ollama (local) |
| Auth | API key required | None |
| Data leaves machine? | Yes | No |
| Cost | Per-token billing | Free |
