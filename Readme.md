# PDF_QA

A Flask-based API for uploading PDF documents, extracting and chunking their content (including tables), generating embeddings, and answering user questions about the documents using Retrieval-Augmented Generation (RAG) with Sentence Transformers and Ollama.

## Features

- **PDF Upload**: Upload PDF files for processing.
- **Text & Table Extraction**: Extracts text and tables from PDFs, converting tables to Markdown.
- **Chunking**: Splits extracted content into overlapping chunks for better context retrieval.
- **Embeddings**: Generates embeddings for all chunks using Sentence Transformers.
- **RAG QA**: Answers user questions by retrieving relevant chunks and querying an LLM via Ollama.
- **Sample Prompts**: Provides predefined prompts for common document queries.
- **File Management**: List and delete uploaded files and their processed data.
- **CORS Support**: Allows frontend access from `http://127.0.0.1:5500`.

## Requirements

- Python 3.8+
- [Ollama](https://ollama.com/) running locally with the `phi3:mini` model (or adjust in code)
- [sentence-transformers](https://www.sbert.net/)
- [pdfplumber](https://github.com/jsvine/pdfplumber)
- Flask, Flask-CORS, numpy, werkzeug

## Setup

1. **Clone the repository:**
   ```sh
   git clone https://github.com/yourusername/PDF_QA.git
   cd PDF_QA
   ```

2. **Create a virtual environment:**
   ```sh
   python -m venv env
   env\Scripts\activate   # On Windows
   # Or
   source env/bin/activate  # On Mac/Linux
   ```

3. **Install dependencies:**
   ```sh
   pip install -r requirements.txt
   ```

4. **(Optional) Download and run Ollama with the required model:**
   - [Install Ollama](https://ollama.com/download)
   - Pull the model:
     ```sh
     ollama pull phi3:mini
     ```
   - Start the Ollama server (usually runs automatically).

5. **Run the Flask API:**
   ```sh
   python main.py
   ```

6. **Frontend**
   - Serve your frontend (e.g., with Live Server in VS Code) at `http://127.0.0.1:5500`.

## API Endpoints

| Method | Endpoint                  | Description                        |
|--------|--------------------------|------------------------------------|
| GET    | `/api/health`            | Health check                       |
| POST   | `/api/upload`            | Upload and process a PDF           |
| POST   | `/api/question`          | Ask a question about a PDF         |
| GET    | `/api/files`             | List uploaded files                |
| DELETE | `/api/files/<file_id>`   | Delete a file and its data         |
| GET    | `/api/sample_prompts`    | Get sample prompts for the UI      |

## File Structure

- `main.py` - Main Flask API code
- `uploads/` - Uploaded PDF files
- `processed/` - Processed chunks and embeddings
- `env/` - (Ignored) Python virtual environment

## .gitignore

Make sure your `.gitignore` includes:
```
env/
uploads/
processed/
*.pyc
__pycache__/
```

## Notes

- The API is configured for local development. Adjust CORS settings as needed for production.
- Maximum PDF file size is set to 50MB.
- For best results, ensure Ollama and the required model are running before asking questions.

## License