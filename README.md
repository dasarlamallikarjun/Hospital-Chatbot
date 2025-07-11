# 🏥 Hospital System RAG Chatbot

An AI-powered chatbot for hospital data exploration, built with **LangChain**, **Neo4j**, **FastAPI**, and **Streamlit**. It supports natural language queries about hospitals, physicians, patients, insurance payers, visits, billing details, reviews, and wait times — using **retrieval-augmented generation (RAG)** over structured and unstructured data.

---

## 🚀 Features

- ⚙️ **ETL Pipeline**: Loads synthetic hospital data into a Neo4j graph database
- 🧠 **LangChain Agent**: Combines Cypher querying with unstructured document search
- 💬 **Chat Interface**: Streamlit-based frontend for interactive question answering
- 📊 **Multi-modal Retrieval**: Structured (Neo4j) + Unstructured (docs, reviews)
- 🔄 **RAG Pipeline**: Retrieval-Augmented Generation with intermediate explanation steps

---

## 🧱 Architecture

```plaintext
User (Streamlit)
   ⬇
Chatbot Frontend (Python)
   ⬇ HTTP Request
FastAPI API (/hospital-rag-agent)
   ⬇
LangChain Agent Executor
   ↙️               ↘️
Neo4j (Cypher)   Document Retriever
   ⬇
Answer with reasoning steps
```

---

## 📂 Project Structure

```
Chatbot_api/
│
├── agents/
│   └── hospital_rag_agent.py      # Main LangChain agent definition
│
├── chains/
│   └── hospital_cypher_chain.py   # Custom Cypher chain logic
│
├── models/
│   └── hospital_rag_query.py      # Pydantic models for request/response
│
├── utils/
│   └── async_utils.py             # Retry logic wrapper
│
├── hospital_neo4j_etl/            # ETL loader for Neo4j graph
├── chatbot_api/                   # FastAPI app code
├── chatbot_frontend/              # Streamlit app UI
│
├── .env                           # Environment config
├── docker-compose.yml             # Service orchestration
├── requirements.txt               # Python dependencies
└── README.md                      # 📘 This file
```

---

## 🧪 Example Questions

- What is the current wait time at Wallace-Hamilton Hospital?
- What is the average billing amount for Medicaid visits?
- Which hospitals are in the hospital system?
- Which physician has the shortest average visit duration?
- What are patients saying about the nursing staff at Castaneda-Hardy?

---

## 🛠️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/hospital-chatbot.git
cd hospital-chatbot
```

### 2. Configure Environment

Create a `.env` file in the root:

```env
OPENAI_API_KEY=sk-xxxxxxxxxxxx
NEO4J_URI=bolt://your_neo4j_host:7687
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=yourpassword
```

### 3. Build and Run with Docker

```bash
docker-compose up --build
```

- 🌐 Streamlit UI: `http://localhost:8501`
- 🔗 FastAPI endpoint: `http://localhost:8000/hospital-rag-agent`
- 🧠 Neo4j Browser: `http://localhost:7474`

---

## 📦 Tech Stack

| Layer           | Tool/Lib            |
|----------------|---------------------|
| LLM Backend     | OpenAI GPT          |
| Framework       | LangChain           |
| Graph DB        | Neo4j               |
| API             | FastAPI             |
| Frontend        | Streamlit           |
| Deployment      | Docker Compose      |

---

## 📌 Deployment on Streamlit Cloud (Optional)

Yes, you can deploy this project directly to [Streamlit Community Cloud](https://streamlit.io/cloud), **but note**:

- Streamlit Cloud does **not support Docker Compose**
- You must **split** the frontend and backend
- Use `st.experimental_connection` or `requests.post()` to connect to an external backend (e.g., hosted on [Render](https://render.com), [Fly.io](https://fly.io), or [Railway](https://railway.app))

### Recommended Steps:

1. Host `chatbot_api` (FastAPI backend) using:
   - [Render](https://render.com)
   - [Railway](https://railway.app)

2. In `chatbot_frontend`, update:
   ```python
   CHATBOT_URL = "https://your-fastapi-backend-url/hospital-rag-agent"
   ```

3. Deploy `chatbot_frontend` on Streamlit Cloud:
   - Push it to GitHub
   - Go to: https://streamlit.io/cloud
   - Connect your repo and deploy