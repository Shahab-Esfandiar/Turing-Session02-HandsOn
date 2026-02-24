# 🧠 The Amnesia Test (Vector Memory)
**Advanced Retrieval-Augmented Generation (RAG) Engine with Pinecone**

This project is an educational and high-performance AI engineering tool designed to demonstrate and overcome the stateless nature of Large Language Models (LLMs). It bridges the gap between isolated prompts and continuous conversations by implementing a sophisticated long-term vector memory system using Pinecone.

---

## 🏗️ System Architecture
Built with modern AI development principles, the architecture focuses on a "Memory-First" philosophy to ensure context retention and prevent agent amnesia.

* **Vector Memory Engine:** A specialized module (`VectorMemory` class) that handles embedding generation, unique ID assignment, and semantic retrieval of past messages.
* **Namespace Isolation Pattern:** Decouples user sessions by generating unique `session_id`s, strictly separating data between different chats to prevent index pollution and context overlap.
* **Robust Retry Logic:** Implements an exponential backoff system (`get_embedding_with_retry`) to elegantly manage API rate limits (HTTP 429) and network latency.
* **Dynamic Context Assembly:** Dynamically constructs the LLM prompt by prepending relevant historical context retrieved from the database before the current user query.

### 🧠 Stateless vs. Stateful Testing
* **Amnesia Test:** Actively demonstrates the default memory limitations of standard LLM APIs by forcing a context-loss scenario.
* **Stateful Integration:** Utilizes semantic search (`top_k=5`) to retrieve highly relevant past conversations from the vector space and inject them into the LLM's context window.

### 🧬 Semantic Data Processing
* **Automated Embedding Generation:** Converts user and assistant messages into 1536-dimensional dense vectors using OpenAI's `text-embedding-3-small` model.
* **Temporal Sorting:** Automatically extracts timestamps from Pinecone metadata and sorts retrieved messages chronologically to maintain a logical conversation flow.

---

## 💎 Execution & Data Features

* **Serverless Indexing:** Seamlessly connects to Pinecone's serverless architecture on AWS, automatically creating the required index if it doesn't exist.
* **Synchronized States:** Implements intelligent `time.sleep()` mechanisms to ensure cloud-based serverless vectors are fully synchronized before retrieval.

### 🔒 Security & Standards
* **Environment Management:** Uses `python-dotenv` to keep API keys (`PINECONE_API_KEY`, `OPENAI_API_KEY`) completely secure and out of the source code.
* **Type Hinting:** Fully annotated with Python typing (`List`, `Dict`, `Any`, `Optional`) for enterprise-grade readability and maintainability.

---

## 🚀 How to Run

1. **Clone the Repo**
2.  **Install Requirements:**
    
    ```bash
    pip install openai pinecone-client python-dotenv
    ```
3.  **Setup Environment:**
    Create a `.env` file in the root directory and add your credentials:
    
    ```env
    PINECONE_API_KEY=your_pinecone_api_key
    OPENAI_API_KEY=your_openai_api_key
    OPENAI_BASE_URL=[https://api.avalai.ir/v1]
    ```
4.  **Launch:**
    
    Open and run the Jupyter Notebook (.ipynb) cells sequentially to observe the contrast between the stateless and stateful chatbot implementations.

---

## 🛠️ Tech Stack
* **Language:** Python 3.12+
* **AI Providers:** OpenAI API (`gpt-4o`, `text-embedding-3-small`)
* **Vector Database:** Pinecone (`pinecone-client`, ServerlessSpec)
* **Core Libraries:** `time`, `random`, `uuid`, `typing`
