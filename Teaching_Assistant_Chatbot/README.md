# eTA (Electronic Teaching Assistant)

An **LLM + RAG** teaching assistant that lets you upload course materials (PDFs / images), ask questions in a chat interface, and optionally enriches answers with **related images**, **YouTube videos (with transcript-based timestamps)**, and **community knowledge** (Stack Overflow / Piazza).

Built with **Streamlit** + **LangChain** + **FAISS** + **OpenAI**.

## Key features
- **PDF + image upload**: extract text from PDFs (PyPDF2) and images (OCR via pytesseract).
- **RAG chat**: chunk documents, embed into a FAISS vector store, and retrieve relevant context for each question.
- **Model toggle**: switch between `gpt-4` and `gpt-3.5-turbo-0125` in the sidebar.
- **Optional enrichment**:
  - Related images via Google Custom Search (CSE)
  - Related YouTube videos with a short summary + a transcript-based timestamp URL
- **Optional learning sources**:
  - Stack Overflow search + best-answer extraction (HTML cleaned)
  - Piazza post ingestion (adds recent class discussions to reference context)

## How it works
1. You upload PDFs/images in the sidebar.
2. Text is extracted (PDF parsing + OCR), chunked, and embedded.
3. For each question, eTA retrieves the most relevant chunks and calls the LLM to answer.
4. If enabled, it attaches supporting images/videos and community references.

## Requirements
- Python 3.10+ recommended
- A working Tesseract installation (required for OCR)
  - macOS: `brew install tesseract`
  - Ubuntu/Debian: `sudo apt-get install tesseract-ocr`
  - Windows: install from the official Tesseract build and ensure it is on PATH

## Quickstart
```bash
# 1) Install deps
pip install -r requirements.txt

# 2) Create your env file
cp .env.example .env

# 3) Run
streamlit run app.py
```

## Environment variables
Create a `.env` file (see `.env.example`).

### Required
- `OPENAI_API_KEY` — needed to generate answers (and to summarize videos / find timestamps).

### Optional (feature-specific)
- **YouTube enrichment**
  - `YOUTUBE_API_KEY`
- **Google image enrichment**
  - `GOOGLE_API_KEY`
  - `GOOGLE_CSE_ID`
- **Piazza integration**
  - `PIAZZA_EMAIL`
  - `PIAZZA_PASSWORD`

If a feature is enabled in the UI but its credentials are missing, the app will show an error.

## Screenshots
Add screenshots or GIFs under `assets/screenshots/` and then link them here.

## Project structure
```
.
├── app.py
├── htmlTemplates.py
├── requirements.txt
├── .env.example
├── .gitignore
├── LICENSE
└── assets/
    └── screenshots/
        └── README.md
```

## Notes
- **Do not commit secrets**: `.env` and any credential files should never be pushed to GitHub.
- **API cost awareness**: OpenAI and other APIs may incur costs depending on your usage.
- **Transcripts**: some YouTube videos disable transcripts; timestamping will not work in that case.

## License
MIT — see `LICENSE`.
