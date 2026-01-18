📄 Retrieval-Augmented Generation (RAG) Pipeline – Document Ingestion & Chunking

This repository implements the document ingestion and preprocessing pipeline for a Retrieval-Augmented Generation (RAG) system.
The pipeline prepares unstructured PDF documents so they can be efficiently retrieved and used by Large Language Models (LLMs) for question answering and knowledge-based generation.

🚀 Overview

Large Language Models cannot directly understand raw PDFs or large documents.
This pipeline converts real-world documents into structured, searchable, and AI-ready knowledge units by:

Loading PDF files

Extracting text with metadata

Splitting large text into smaller semantic chunks

Preparing data for vector embedding and retrieval

This forms the foundation of any production-grade RAG system.

🧠 What is RAG?

Retrieval-Augmented Generation (RAG) enhances LLMs by allowing them to:

Retrieve relevant information from external documents

Use that information while generating accurate responses

This approach:

Reduces hallucinations

Improves factual accuracy

Enables domain-specific AI systems

🔗 Pipeline Architecture
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

📌 Pipeline Steps (Theory + Implementation)
1️⃣ Document Ingestion (PDF Loading)
Theory

LLMs cannot process PDFs directly.
The first step converts PDFs into plain text while preserving metadata such as:

File name

Page number

Source path

This makes documents machine-readable and traceable.

Implementation

Iterates through all PDF files in a directory

Loads PDFs page by page

Converts each page into a Document object

Stores extracted text along with metadata

Output:
A list of structured Document objects.

2️⃣ Text Chunking (Splitting Documents)
Theory

Embedding models and LLMs have context length limits.
Large documents must be split into small, overlapping chunks to ensure:

Better semantic embeddings

Accurate retrieval

Context continuity

Overlapping prevents loss of meaning between chunk boundaries.

Implementation

Uses recursive text splitting

Splits text based on structure (paragraphs → sentences → words)

Preserves metadata for every chunk

Output:
A list of smaller, searchable document chunks.

3️⃣ Metadata Preservation
Theory

Metadata is critical for:

Source attribution

Page-level citations

Debugging and trust

Each chunk retains:

Original file name

Page number

Source path

This enables explainable and reliable AI responses.

4️⃣ Vector Database Readiness
Theory

After chunking:

Each chunk becomes a standalone knowledge unit

These chunks are converted into embeddings

Stored in a vector database (e.g., FAISS, Chroma, Pinecone)

This repository focuses on pre-embedding preparation, following best RAG practices.

🧩 Core Functions Explained
process_all_pdfs(directory)

Purpose:
Loads all PDFs from a given directory and converts them into structured documents.

How it works:

Scans the directory for PDF files

Extracts text page by page

Attaches metadata to each page

Combines all pages into a single document list

Returns:

List[Document]

split_documents(documents)

Purpose:
Splits large documents into smaller overlapping chunks.

How it works:

Uses recursive splitting strategy

Applies configurable chunk size and overlap

Preserves metadata for each chunk

Returns:

List[Document] (chunked)
