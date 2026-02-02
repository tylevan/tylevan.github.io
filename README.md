<h1 align="center">
  <img src="https://img.icons8.com/fluency/96/law.png" width="80" alt="Legal RAG"/>
  <br/>
  Legal RAG - Vietnamese Legal AI Assistant
</h1>

<p align="center">
  <strong>AI-Powered Legal Assistant using Retrieval-Augmented Generation</strong>
  <br/>
  <em>Query Vietnamese Decree 13/2023/NĐ-CP and Law No. 91/2025/QH15 of the National Assembly on Personal Data Protection</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Streamlit-Cloud-FF4B4B?style=flat-square&logo=streamlit&logoColor=white"/>
  <img src="https://img.shields.io/badge/Google-Gemini_AI-4285F4?style=flat-square&logo=google&logoColor=white"/>
  <img src="https://img.shields.io/badge/ChromaDB-Vector_DB-00C853?style=flat-square"/>
</p>

<p align="center">
  <a href="#introduction">Introduction</a> •
  <a href="#introduction-to-rag">What is RAG?</a> •
  <a href="#key-features">Key Features</a> •
  <a href="#demo">Demo</a> •
  <a href="#contact">Contact</a>
</p>

## Introduction 🚀

**Legal RAG** is an AI-powered application that helps users query and get answers about Vietnamese legal documents, focusing on **Decree 13/2023/NĐ-CP** - Vietnam's most important regulation on personal data protection.

### Why This Project Matters

With the introduction of Decree 13/2023/NĐ-CP and Law No. 91/2025/QH15 , Vietnamese businesses (especially in **Finance**, **Healthcare**, and **E-commerce**) must comply with strict data protection regulations. However:

| Challenge | Solution |
|-----------|----------|
| 📚 Legal documents are long and hard to read | AI automatically extracts relevant information |
| 🔍 Traditional keyword search is ineffective | **Semantic Search** understands query meaning |
| ⚖️ Requires experts to interpret the law | AI responds with **accurate Article/Clause citations** |
| ⏱️ Time-consuming manual lookup | Response in **< 10 seconds** |

### Who Should Use This?

- **Enterprises** reviewing Decree 13 compliance
- **Lawyers / Legal Compliance** needing quick reference
- **Data Protection Officers (DPO)** providing internal advisory
- **Students / Researchers** learning about AI and Legal Tech

## Introduction to RAG 💡

### What is RAG?

**Retrieval-Augmented Generation (RAG)** combines **information retrieval** and **AI text generation**, helping LLMs (like Google Gemini, ChatGPT) answer more accurately by:

1. **Retrieving** relevant text passages from a knowledge base
2. **Augmenting** the prompt with retrieved information
3. **Generating** responses based on actual context, not hallucinations

> [!NOTE]
> RAG solves the "hallucination" problem of LLMs - when AI fabricates information that doesn't exist in source data. This is **critically important** in the legal domain.

### Legal RAG Workflow

<!-- 📌 REPLACE WITH YOUR WORKFLOW IMAGE -->
![Legal RAG Workflow](https://github.com/tylevan/tylevan.github.io/blob/main/images/workflow.png)

## Key Features ⚙️

This project applies advanced RAG techniques to ensure high accuracy:

| Technique | How It Works | Benefit |
|-----------|--------------|---------|
| **Semantic Chunking** | Split PDF by legal structure (Điều, Khoản, Chương) using regex patterns instead of fixed character count | Preserve complete legal context within each chunk |
| **Rich Metadata** | Each chunk stores: `law_name`, `article_id`, `issued_date`, `issuing_body`, and pre-formatted `citation` string | Enable accurate Article/Clause citations in responses |
| **Hybrid Search** | Vector search (Gemini Embedding) finds semantic matches + BM25 finds exact keyword matches, then merge results | Balance semantic understanding with exact term matching |
| **Query Expansion** | LLM generates 3 query variations: typo-corrected, legal terminology, keyword-focused | Improve recall by 20-30% on legal queries |
| **Cross-Encoder Reranking** | mMARCO multilingual model re-scores all candidates by query-document relevance | Improve precision by pushing most relevant docs to top |
| **Contextualized Query** | LLM rewrites query to resolve pronouns ("nó", "điều này") based on chat history | Enable natural multi-turn conversations |
| **Anti-Hallucination Prompt** | Strict system prompt: only use provided context, cite specific Article/Clause, refuse if info not found | Prevent AI from fabricating legal information |

> [!IMPORTANT]
> **Anti-Hallucination** is the most critical feature in the legal domain. The AI is designed to refuse answering if information is not found in source documents.

## Demo 🎬

### 🔗 Live Demo

<p align="center">
  <a href="YOUR_STREAMLIT_URL">
    <img src="https://static.streamlit.io/badges/streamlit_badge_black_white.svg" height="50"/>
  </a>
</p>

```
🌐 https://******.app
```

### 📱 Screenshots

<!-- 📌 REPLACE WITH ACTUAL SCREENSHOT -->
<p align="center">
  <img src="https://github.com/tylevan/tylevan.github.io/blob/main/images/chat-interface-demo.png" alt="Chat Interface" width="80%"/>
</p>

### 💬 Example Conversation

```
👤 User: Dữ liệu cá nhân là gì?

🤖 AI: Theo Điều 2 Nghị định 13/2023/NĐ-CP, dữ liệu cá nhân là thông tin 
       dưới dạng ký hiệu, chữ viết, chữ số, hình ảnh, âm thanh hoặc dạng 
       tương tự trên môi trường điện tử gắn liền với một con người cụ thể 
       hoặc giúp xác định một con người cụ thể...

👤 User: Vậy dữ liệu nhạy cảm khác gì?

🤖 AI: Theo khoản 4 Điều 2, dữ liệu cá nhân nhạy cảm là dữ liệu cá nhân 
       gắn liền với quyền riêng tư mà khi bị xâm phạm sẽ gây ảnh hưởng 
       trực tiếp đến quyền và lợi ích hợp pháp của chủ thể dữ liệu, bao gồm:
       - Quan điểm chính trị, tôn giáo
       - Tình trạng sức khỏe
       - Dữ liệu di truyền, sinh trắc học
       - Đời sống tình dục
       ...
```

## Tech Stack 🛠️

| Component | Technology |
|-----------|------------|
| **Frontend** | Streamlit |
| **LLM** | Google Gemini 2.5 Flash |
| **Embedding** | Gemini Embedding |
| **Vector DB** | ChromaDB |
| **Keyword Search** | BM25 (rank_bm25) |
| **Reranking** | Cross-Encoder (mMARCO) |
| **Vietnamese NLP** | PyVi |


## About 👨‍💻

<table>
<tr>
<td width="120" align="center">
<img src="https://via.placeholder.com/100/4F46E5/FFFFFF?text=TL" width="80" style="border-radius:50%"/>
</td>
<td>

**Ty Le Van**

Product Manager with experience in digital platforms and customer engagement solutions.

</td>
</tr>
</table>

## Contact 📬

<p align="center">
  <a href="mailto:your.email@example.com">
    <img src="https://img.shields.io/badge/Email-Contact-D14836?style=for-the-badge&logo=gmail&logoColor=white"/>
  </a>
  <a href="https://linkedin.com/in/tylevan">
    <img src="https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/>
  </a>
  <a href="https://github.com/tylevan">
    <img src="https://img.shields.io/badge/GitHub-Follow-181717?style=for-the-badge&logo=github&logoColor=white"/>
  </a>
</p>

<p align="center">
  Made with ❤️ by <strong>Ty Le Van</strong>
  <br/>
  <sub>© 2026 Legal RAG Project</sub>
</p>
