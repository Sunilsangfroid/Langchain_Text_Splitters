# LangChain Text Splitters

A collection of text splitting methods using LangChain for various document types and use cases. Text splitting is a crucial preprocessing step when working with large documents and LLMs, allowing you to break down content into manageable chunks for effective embedding, retrieval, and processing.

## Features

This repository demonstrates several text splitting strategies:

### Length-Based Splitting
- Simple chunking based on character count
- Configurable chunk size and overlap
- Works with any text but may break semantic meaning
- Example: [`length_based.py`](length_based.py)

### Text Structure-Based Splitting
- Uses natural text separators (paragraphs, sentences, etc.)
- Preserves readability of content
- Configurable separators for custom formatting
- Example: [`text_structure_based.py`](text_structure_based.py)

### Document Format-Specific Splitting
- Specialized handling for different document types:
  - Markdown: [`markdown_splitting.py`](markdown_splitting.py)
  - Python Code: [`python_code_splitting.py`](python_code_splitting.py)
- Language-aware splitting that respects document structure

### Semantic-Based Splitting
- Advanced splitting based on meaning rather than length
- Uses embeddings to identify natural semantic boundaries
- Keeps related content together regardless of length
- Example: [`semantic_based_splitting.py`](semantic_based_splitting.py)

## Getting Started

### Prerequisites
- Python 3.7+
- API keys for the LLM services you plan to use

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/Sunilsangfroid/langchain_text_splitters.git
   cd langchain_text_splitters
   ```

2. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install requirements:
   ```bash
   pip install -r requirements.txt
   ```

4. Set up environment variables:
   Create a `.env` file in the root directory with the following API keys:
   ```
   OPENAI_API_KEY="your_openai_api_key"
   ANTHROPIC_API_KEY="your_anthropic_api_key"
   GOOGLE_API_KEY="your_google_api_key"
   HUGGINGFACEHUB_ACCESS_TOKEN="your_huggingface_token"
   GROQ_API_KEY="your_groq_api_key"
   ```
   (Only add keys for services you plan to use)

## Usage Examples

### Length-Based Splitting
```python
from langchain.text_splitter import CharacterTextSplitter

splitter = CharacterTextSplitter(
    chunk_size=200,
    chunk_overlap=0,
    separator=""
)

result = splitter.split_text(your_text)
```

### Text Structure-Based Splitting
```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(
    chunk_size=100,
    chunk_overlap=0,
    separators=["\n\n", "\n", " ", ""]
)

chunks = splitter.split_text(your_text)
```

### Code Splitting (Python)
```python
from langchain.text_splitter import RecursiveCharacterTextSplitter, Language

splitter = RecursiveCharacterTextSplitter.from_language(
    language=Language.PYTHON,
    chunk_size=300,
    chunk_overlap=0,
)

chunks = splitter.split_text(your_code)
```

### Semantic-Based Splitting
```python
from langchain_experimental.text_splitter import SemanticChunker
from langchain_google_genai.embeddings import GoogleGenerativeAIEmbeddings

text_splitter = SemanticChunker(
    GoogleGenerativeAIEmbeddings(model="models/embedding-001"),
    breakpoint_threshold_type="standard_deviation",
    breakpoint_threshold_amount=1
)

docs = text_splitter.create_documents([your_text])
```

## When to Use Each Method

- **Length-Based**: Quick and simple, best for homogeneous text
- **Text Structure-Based**: Good for preserving natural breaks in content
- **Document Type-Specific**: Ideal when working with specialized formats
- **Semantic-Based**: Best for preserving meaning and topical coherence, but more computationally expensive

## License

This project is open-source - feel free to use and modify as needed.

## Acknowledgements

- [LangChain](https://github.com/langchain-ai/langchain) for the base libraries
- Various embedding and LLM providers for their services