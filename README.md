# 📄 Retrieval-Augmented Generation (RAG) Pipeline – Document Ingestion & Chunking

This repository contains the **document ingestion and preprocessing pipeline** for a **Retrieval-Augmented Generation (RAG)** system.  
It prepares unstructured PDF documents so they can be efficiently retrieved and used by Large Language Models (LLMs).

---

## 🚀 Overview

Large Language Models cannot directly process PDFs or long documents.  
This pipeline converts real-world documents into **structured, searchable, and AI-ready knowledge chunks** by:

- Loading PDF files
- Extracting text with metadata
- Splitting large text into smaller semantic chunks
- Preparing data for embeddings and vector storage

This pipeline forms the **foundation of any production-grade RAG system**.

---

## 🧠 What is RAG?

**Retrieval-Augmented Generation (RAG)** improves LLM responses by:
1. Retrieving relevant information from external documents
2. Injecting that information into the model during generation

Benefits:
- Reduced hallucinations  
- Improved factual accuracy  
- Domain-specific intelligence  

---

## 🔗 Pipeline Architecture

PDF Documents
↓
Document Loader
↓
LangChain Documents
↓
Text Chunking
↓
Metadata-Preserved Chunks
↓
(Next Step: Embeddings → Vector Database → Retrieval)


---

## 📌 Pipeline Steps (Theory + Implementation)

### 1️⃣ Document Ingestion (PDF Loading)

#### Theory
LLMs cannot read PDFs directly.  
This step converts PDFs into plain text while preserving metadata such as:
- File name
- Page number
- Source path

This makes documents machine-readable and traceable.

#### Implementation
- Iterates through all PDF files in a directory
- Loads PDFs page by page
- Converts each page into a `Document` object
- Stores extracted text along with metadata

**Output:**
List[Document]


---

### 2️⃣ Text Chunking (Splitting Documents)

#### Theory
LLMs and embedding models have context length limits.  
Large documents must be split into **small, overlapping chunks** to ensure:
- Better semantic embeddings
- Accurate retrieval
- Context continuity

Overlapping prevents loss of meaning at chunk boundaries.

#### Implementation
- Uses recursive text splitting
- Splits text based on structure (paragraphs → sentences → words)
- Preserves metadata for every chunk

**Output:**
List[Document] (chunked)


---

### 3️⃣ Metadata Preservation

#### Theory
Metadata is critical for:
- Source attribution
- Page-level citations
- Debugging and trust

Each chunk retains:
- Original file name
- Page number
- Source path

This enables explainable and reliable AI responses.

---

### 4️⃣ Vector Database Readiness

#### Theory
After chunking:
- Each chunk becomes an independent knowledge unit
- These chunks are converted into embeddings
- Stored in a vector database (FAISS, Chroma, Pinecone, etc.)

This repository focuses on **pre-embedding preparation**, following best RAG practices.

---

## 🧩 Core Functions Explained

### `process_all_pdfs(directory)`

**Purpose:**  
Loads all PDFs from a directory and converts them into structured documents.

**How it works:**
- Scans the directory for PDF files
- Extracts text page by page
- Attaches metadata to each page
- Combines all pages into a single document list

**Returns:**
List[Document]


---

### `split_documents(documents)`

**Purpose:**  
Splits large documents into smaller overlapping chunks.

**How it works:**
- Uses a recursive splitting strategy
- Applies configurable chunk size and overlap
- Preserves metadata for each chunk

**Returns:**
List[Document] (chunked)


---

## ✅ Why This Pipeline is Industry-Ready

- Modular and scalable design
- Handles large document collections
- Optimized for semantic search
- Compatible with modern vector databases
- Source-aware and explainable

This architecture closely mirrors **real-world RAG systems used in production**.

---

## 🔮 Future Work

- Generate embeddings using OpenAI / HuggingFace models
- Store embeddings in a vector database (FAISS / Chroma)
- Implement semantic retrieval
- Inject retrieved context into LLM prompts
- Build a full question-answering system

---

## 🧑‍💻 Tech Stack

- Python
- LangChain
- PyPDFLoader
- Recursive Text Splitter
- (Future) Vector Databases & LLMs

---

## 📌 Use Cases

- AI-powered document Q&A
- Chatbots over PDFs
- Knowledge assistants
- Enterprise search systems
- Academic and legal document analysis

---

⭐ If you find this useful, feel free to star the repository!
