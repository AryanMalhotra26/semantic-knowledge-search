# Semantic Developer Knowledge Search

A semantic search engine for developer documentation using Retrieval-Augmented Generation (RAG), LangChain, OpenAI embeddings, and ChromaDB.

## Overview

Standard keyword search fails when developers use different terminology than the documentation. This RAG-powered search engine bridges that gap — returning contextually relevant answers grounded in actual documentation chunks.

## Tech Stack

- **Language:** Python 3.10+
- **Embeddings:** OpenAI `text-embedding-ada-002`
- **Vector Store:** ChromaDB
- **RAG Framework:** LangChain
- **LLM:** GPT-4 (answer generation)
- **API Layer:** FastAPI
- **Retrieval:** Semantic similarity search over embedded documentation chunks

## Architecture

```
Query → OpenAI Embeddings → ChromaDB Similarity Search → Top-K Chunks → GPT-4 → Grounded Answer
```

1. Documentation is chunked and embedded with OpenAI's embedding model
2. Chunks are stored in ChromaDB as a persistent vector store
3. At query time, the query is embedded and matched against stored chunks via cosine similarity
4. Top-K retrieved chunks are passed as context to GPT-4
5. GPT-4 generates a grounded answer with strict context constraints to minimize hallucinations

## Key Features

- Natural-language engineering queries over structured documentation
- Retrieval + generation failure mode analysis (context fragmentation, weak chunk ranking, prompt sensitivity)
- Targeted improvements at each pipeline stage
- FastAPI backend for easy integration

## Setup

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=your_key_here
python ingest.py        # embed and store docs
uvicorn app:app --reload  # start API server
```

## Results

Implemented RAG significantly reduced hallucinations vs. standalone GPT-4 responses by grounding every answer in retrieved documentation context.
