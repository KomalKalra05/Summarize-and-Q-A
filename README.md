# Hybrid RAG System for Academic Document Q&A

A sophisticated Retrieval-Augmented Generation (RAG) system that combines vector-based retrieval and knowledge graph technology to answer complex queries about academic papers, research documents, and any PDF content with high accuracy.

## 🎯 Overview

This project addresses the limitations of traditional RAG systems when handling comparison-based and multi-entity queries across diverse academic content. By integrating local vector search with a Neo4j knowledge graph, the system provides accurate answers to both simple factual questions and complex relational queries about research papers, academic documents, technical reports, and any PDF content including mathematical formulas.

## ✨ Features

- **Hybrid Architecture**: Combines local RAG (vector-based) and knowledge-based RAG (graph database)
- **Multi-format Support**: Handles PDF documents, DOC files, web links, and academic papers with mathematical formulas
- **Mathematical Content Processing**: Advanced parsing of mathematical equations, formulas, and scientific notation
- **Universal Document Support**: Works with research papers, technical reports, academic theses, and any PDF content
- **Intelligent Query Routing**: Automatically determines the best retrieval method based on query type
- **Fallback Mechanism**: Uses Google SERP API when local data is insufficient
- **Entity Relationship Analysis**: Leverages Neo4j for complex comparison and relational queries
- **Semantic Search**: Cosine similarity-based retrieval for contextually relevant responses across academic and technical content

## 🏗️ System Architecture & Flow

**RAG Processing Pipeline**

The system follows a comprehensive flow that handles both local data processing and external data retrieval:

**Data Processing Flow:**
1. **Input Stage**: User provides a prompt/query
2. **Data Availability Check**: System determines if relevant data exists locally
3. **External Data Retrieval** (if needed):
   - Google SERP API fetches relevant links
   - LangChain WebBaseLoader scrapes web content
   - Data is extracted and processed
4. **Content Processing**:
   - Documents converted into manageable chunks (10 sentences per chunk, minimum 30 tokens)
   - Text converted into embeddings using encoding models
   - Embeddings stored in MongoDB in Base64 format

**Query Processing Flow:**
1. **Query Analysis**: User prompt is analyzed and converted to embeddings
2. **Similarity Search**: Cosine similarity identifies most relevant chunks from MongoDB
3. **Context Retrieval**: Relevant chunks are decoded and prepared
4. **LLM Generation**: Google Gemini 2B generates response using retrieved context

**Core Components:**
- **Vector Store**: MongoDB with Base64-encoded embeddings and cosine similarity search
- **Knowledge Graph**: Neo4j for entity relationships and complex queries
- **Web Scraping**: LangChain WebBaseLoader for external content extraction
- **External Search**: Google SERP API for additional context when local data is insufficient
- **NLP Processing**: spaCy for text analysis and entity extraction
- **LLM**: Google Gemini 2B for response generation

## 🔄 User Flow

1. **Document Input**: Users upload academic PDFs, research papers, technical documents, or provide web links
2. **Content Processing**: System processes text, mathematical formulas, and scientific notation for comprehensive understanding
3. **Query Processing**: User queries are analyzed and routed to appropriate retrieval method
4. **Local RAG**: Vector search handles factual and content-based queries
5. **Knowledge Graph**: Neo4j processes comparison and relational queries
6. **Fallback**: Google SERP API provides additional context when needed
7. **Response Generation**: Gemini 2B generates comprehensive answers

## 🔧 Technical Details

**Vector Search (Local RAG)**
- **Chunking Strategy**: Documents split into 10-sentence chunks with minimum 30 tokens
- **Embedding Storage**: MongoDB with Base64-encoded embeddings for efficient storage
- **Retrieval Method**: Cosine similarity matching between query and document embeddings
- **Best for**: Factual queries, mathematical content extraction, formula explanations, specific information retrieval

**Knowledge Graph (Neo4j)**
- **Entities**: Papers, authors, methodologies, results, concepts, mathematical models, formulas
- **Relationships**: Citations, comparisons, methodological similarities
- **Query Language**: Cypher queries for complex relationships
- **Best for**: Comparison queries, multi-entity analysis, relationship exploration

**Fallback Mechanism**
- **Trigger**: When local retrieval confidence is below threshold
- **Method**: Google SERP API for external information
- **Integration**: Results combined with local context
