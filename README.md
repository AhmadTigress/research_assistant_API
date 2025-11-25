# research_assistant_API
RAG-powered API for querying research documents with semantic search

# Research Assistant API 🧠

A FastAPI-based Research Assistant that uses Retrieval-Augmented Generation (RAG) to answer questions from your research documents. Built with ChromaDB for vector storage and LangChain for AI orchestration.

## Features

- **Document Ingestion**: Automatically processes markdown files from the `sample_data/` directory
- **Semantic Search**: Finds relevant research content using embeddings
- **AI-Powered Q&A**: Generates answers using Groq's Llama model with RAG
- **RESTful API**: FastAPI endpoints for easy integration
- **Source Attribution**: Returns sources with confidence scores

## Project Structure
```
research_assistant_api/
├── simple_chatbot_API/
│   ├── main_simple_chatbot.py
│   └── service.py
├── main.py              # FastAPI wrapper and API endpoints
├── rag_service.py       # Core RAG logic and question answering
├── database.py          # Embedding model and ChromaDB setup
├── setup_data.py        # Document ingestion and processing
├── requirements.txt     # Python dependencies
├── .gitignore          # Git ignore rules
└── sample_data/         # Folder for your .md research documents
```


## Quick Start

### 1. Prerequisites

- Python 3.8+
- [Groq API Key](https://console.groq.com/) (free account)

### 2. Installation

```bash
# Clone the repository
git clone https://github.com/your-username/research_assistant_api.git
cd research-api

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```
## Environment Setup
Create a .env file in the root directory:
```text
GROQ_API_KEY=your_groq_api_key_here
```

## Add Your Research Documents
Place your markdown files in the sample_data/ directory:
```text
# Example structure
sample_data/
├── machine_learning.md
├── statistics.md
├── research_papers.md
└── notes.md
```

## Initialize the Database
```bash
python setup_data.py
```

This will:
- Process all markdown files in sample_data/
- Split documents into chunks
- Generate embeddings
- Store everything in ChromaDB

## Run the API
```bash
python main.py
```
The API will be available at http://localhost:8000

## API Usage
**Ask a Research Question**
Endpoint: POST /research
```bash
curl -X POST "http://localhost:8000/research" \
  -H "Content-Type: application/json" \
  -d '{
    "question": "What are the best methods for handling class imbalance?"
  }'
```

**Response**
```json
{
  "answer": "Based on the research documents, the best methods for handling class imbalance include...",
  "sources": [
    {
      "title": "machine_learning.md",
      "content": "Class imbalance can be addressed using techniques like SMOTE, random undersampling...",
      "score": 0.85
    }
  ]
}
```

## Check API Status
Endpoint: `GET /`
```bash
curl http://localhost:8000/
```

## Development
## Testing the RAG System
You can test the question-answering directly:
```bash
python rag_service.py
```

## Adding New Documents
Add new ``.md` files to `sample_data/`
Run: `python setup_data.py`

## API Documentation
Once the server is running, visit:
- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc

## Dependencies
- FastAPI: Web framework
- LangChain: AI orchestration
- ChromaDB: Vector database
- Groq: LLM inference
- HuggingFace: Embeddings

## License
MIT License - feel free to use this project for your research needs!

## Contributing
1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Open a pull request