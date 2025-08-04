# 📄 SDA-RAG: Structured Data-Aware Retrieval-Augmented Generation

**SDA-RAG** is a document-grounded Question-Answering (QA) pipeline designed to extract answers from both scanned and searchable PDFs, even if they contain complex structured data like tables or images. It enhances standard RAG by introducing structured data parsing, fine-tuned reranking (RAFT), and support for scanned documents — enabling accurate and faithful answers from technical manuals and general documents.

![Methodology](https://github.com/ShadmanSobhan/SDA-RAG/blob/main/Methodology.png)

---

## 🧠 Key Features

- ✅ Supports both **searchable** and **scanned** PDFs
- 📑 Extracts and summarizes **tables** and **images**
- 🧾 Uses **semantic search** with **LLM-based reranking**
- 🪄 Generates answers using a **fine-tuned Gemma-2-9b-it** model
- 📦 Built-in **OCR**, **chunking**, and **vector storage**
- 🧪 Evaluated using **RAGas** and **DeepEval**

---


## 🔍 How It Works

### 1. **Document Processing**
- Scanned PDFs are converted to searchable text using OCR.
- Tables are extracted using YOLO and converted to HTML, then described using a language model.
- Images are extracted and described using multimodal LLMs.
- All texts are merged into a unified format for embedding.

### 2. **Retrieval**
- **Stage 1:** FAISS-based semantic similarity search using BAAI/bge-small-en-v1.5 embeddings.
- **Stage 2:** Top-K chunks are reranked using a **fine-tuned reranker** based on the RAFT method.

### 3. **Answer Generation**
- Final top-N chunks are passed to the **Gemma-2-9b-it-GPTQ** LLM for answer generation.

---

## 📊 Evaluation Highlights

- **Faithfulness**: 96% (DeepEval), 94% (RAGas)
- **Answer Relevancy**: 93% (DeepEval), 87% (RAGas)
- Proven improvement over standard RAG, especially in handling structured data and hallucination resistance.

---

## 📚 Technical Highlights

| Component       | Model / Library Used                     |
|----------------|-------------------------------------------|
| Embedding       | `BAAI/bge-small-en-v1.5`                 |
| Vector Store    | `FAISS`                                  |
| Reranker        | Fine-tuned `Gemma-2-9b-it` (via RAFT)    |
| Table Extractor | `YOLO` via `unstructured`                |
| Image Describer | `llama-3.2-90b-vision-preview`           |
| Generation LLM  | `Gemma-2-9b-it-GPTQ`                     |
| OCR             | `pytesseract`                            |

---


