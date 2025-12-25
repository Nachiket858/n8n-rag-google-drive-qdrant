

## 🧠 What You Are Building

A system where:

- Documents are uploaded to Google Drive  
- Text is extracted from documents  
- Text is converted into vector embeddings  
- Embeddings are stored in a vector database  
- A user asks a question  
- AI answers using **only the uploaded documents**

---

## 🧰 Accounts Required (Free Tier)

Create accounts for the following services:

- ☁️ **n8n Cloud**  
- 📁 **Google Drive**  
- 🤗 **Hugging Face** (Read access token)  
- 🧠 **Qdrant Cloud** (Free cluster)  
- ✨ **Google Gemini API**

---

## 🧰 Tech Stack

| Component | Tool |
|---------|------|
| Workflow Automation | n8n Cloud |
| Document Storage | Google Drive |
| Text Extraction | n8n Default Data Loader |
| Embeddings | Hugging Face (`all-MiniLM-L6-v2`) |
| Vector Database | Qdrant Cloud |
| LLM | Google Gemini |
| Framework | LangChain (via n8n nodes) |

---

## 🔹 STEP 1: Create Qdrant Collection

Create a collection in Qdrant with the following configuration:

- **Collection Name:** `my_collection`  
- **Vector Size:** `384`  
- **Distance Metric:** `Cosine`  

> ⚠️ Vector size must exactly match the embedding model output.

---

## 🔹 STEP 2: Document Ingestion Workflow

This workflow ingests documents from Google Drive and stores them in the vector database.

### 🔗 Nodes Used

1. Manual Trigger  
2. Google Drive – Search Files  
3. Google Drive – Download File  
4. Default Data Loader  
5. Hugging Face Embeddings  
6. Qdrant Vector Store (Insert Mode)

---

### 📥 Google Drive – Download File

- **Output:** Binary file  
- **Binary Property:** `data`  

This node downloads the document from Google Drive.

---

### 📄 Default Data Loader

- **Data Type:** `binary`  
- Automatically extracts text from:
  - DOCX  
  - PDF  
  - TXT  

This step converts documents into readable text.

---

### 🔢 Hugging Face Embeddings

- **Model:** `sentence-transformers/all-MiniLM-L6-v2`  
- **Embedding Dimension:** `384`  

This node converts text into numerical vectors (embeddings).

---

### 🗄️ Qdrant Vector Store (Insert)

- **Mode:** Insert  
- **Collection:** `my_collection`  

Receives:
- Documents from **Default Data Loader**  
- Embeddings from **Hugging Face**

After this step, documents are indexed and searchable.

---

## 🔹 STEP 3: Question Answering Workflow

This workflow allows users to ask questions and receive answers.

### 🔗 Nodes Used

1. Chat Trigger  
2. Hugging Face Embeddings (Query)  
3. Qdrant Vector Store (Search Mode)  
4. Aggregate  
5. AI Agent  
6. Google Gemini Chat Model  

---

## 🧠 AI Agent Prompt (IMPORTANT)

Use **this exact prompt** in the AI Agent node:

```text
You are a helpful assistant.
Use the provided context to answer the user's question.
If the answer is not contained in the context, say "I don't know".

Context:
{{ $json.pageContent }}

Question:
{{ $('When chat message received').item.json.chatInput }}

Answer:


```

## 🔹 STEP 4: Testing the System

Try asking questions such as:

- ❓ What is mentioned about the admission process?
- 📄 Summarize the uploaded document
- 🔑 What are the key points discussed?

---

## ⚠️ Common Mistakes to Avoid

- Skipping the **Default Data Loader**
- Using different embedding models for ingestion and querying
- Sending full documents directly to the LLM
- Forgetting to re-ingest documents after updates

---

## ✅ Best Practices

- 📏 Keep chunk size between **300–600 characters**
- 🔁 Use the **same embedding model** everywhere
- 🔐 Store API keys using **n8n credentials**
- ♻️ Re-run ingestion whenever documents change

---

## 🎯 Outcome

After completing this project:

- You understand **RAG architecture**
- You can build **production-grade AI workflows**
- You can extend this system for **clients or products**

---

## 🚀 Future Improvements

- File update & delete synchronization
- Frontend chat UI
- Metadata filtering
- Multi-collection support

---

## 👨‍💻 Author

**Nachiket Shinde**  
AI & ML Engineer | AI Automation  
Founder – KodeNeurons
