# 📚 RAG System using n8n Cloud, Google Drive & Qdrant (Free)

A fully working **Retrieval-Augmented Generation (RAG)** system built using **n8n Cloud**, **Google Drive**, **Hugging Face embeddings**, **Qdrant Vector Database**, and **Google Gemini** — all using **free tiers**.

This system allows you to upload documents to Google Drive and ask questions directly from those documents using an AI-powered chat interface.

---

## 🚀 Features

- Automatic document ingestion from Google Drive
- Supports DOCX, PDF, TXT files
- Semantic search using vector embeddings
- Context-aware answers (RAG)
- Fully cloud-based (no local setup)
- Uses only free APIs
- Chat interface inside n8n

---

## 🏗️ Architecture Overview

Google Drive → Text Extraction → Embeddings → Qdrant
↓
User Question → Embedding → Similarity Search → LLM Answer

gherkin
Copy code

---

## 🧰 Tech Stack

| Component | Tool |
|--------|------|
| Workflow Automation | n8n Cloud |
| Document Storage | Google Drive |
| Embeddings | Hugging Face (all-MiniLM-L6-v2) |
| Vector Database | Qdrant Cloud |
| LLM | Google Gemini |
| Framework | LangChain (via n8n nodes) |

---




## ▶️ How to Use (Quick)

1. Import the provided workflow JSON into **n8n Cloud**
2. Configure credentials (Google Drive, Hugging Face, Qdrant, Gemini)
3. Upload documents to Google Drive folder
4. Run ingestion once
5. Ask questions via n8n Chat

👉 For **full step-by-step setup**, see  
📄 **BUILD_FROM_SCRATCH.md**

---

## 👨‍💻 Author

**Nachiket Shinde**  
AI & ML Engineer | AI Automation  
Founder – KodeNeurons

---
