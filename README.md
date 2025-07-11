# Hospital System RAG Chatbot

This project implements a full-stack Retrieval-Augmented Generation (RAG) chatbot that answers natural language queries about a synthetic hospital system. It uses LangChain agents, a FastAPI backend, and a Streamlit frontend.

## Project Structure

```
├── chatbot_api/              # FastAPI backend with LangChain agents
│   ├── agents/
│   ├── chains/
│   ├── models/
│   ├── utils/
│   ├── main.py
│   └── requirements.txt
├── chatbot_frontend/        # Streamlit user interface for chatting
│   ├── main.py
│   └── requirements.txt
├── hospital_neo4j_etl/      # ETL pipeline to populate Neo4j with synthetic data
│   ├── data/
│   └── main.py
├── docker-compose.yml       # Dockerized orchestration of services
└── .env                     # Environment variables (API keys, connection info)
```

## Features

- Retrieval-augmented QA over hospital, patient, physician, and billing data
- Structured + unstructured knowledge integration via LangChain tools
- Modular agent-executor with retry mechanism
- Interactive chat UI with Streamlit using LLM responses
- Dockerized environment with Neo4j, FastAPI, and Streamlit services

## How It Works

1. **ETL Phase**: Loads synthetic CSV data into a Neo4j graph database.
2. **Backend**: Uses LangChain agents to query Neo4j (Cypher) and unstructured data, exposing an API at `/hospital-rag-agent`.
3. **Frontend**: A Streamlit chat UI sends questions to the backend and displays the results with explanations.

## Running Locally

### Step 1: Clone the repository

```bash
git clone https://github.com/your-username/hospital-rag-chatbot.git
cd hospital-rag-chatbot
```

### Step 2: Set up the environment

Create a `.env` file and add your credentials:

```
OPENAI_API_KEY=your-key-here
NEO4J_URI=your_neo4j_bolt_or_http_uri
NEO4J_USERNAME=your_neo4j_username
NEO4J_PASSWORD=your_neo4j_password

HOSPITALS_CSV_PATH=https://raw.githubusercontent.com/hfhoffman1144/langchain_neo4j_rag_app/main/data/hospitals.csv
PAYERS_CSV_PATH=https://raw.githubusercontent.com/hfhoffman1144/langchain_neo4j_rag_app/main/data/payers.csv
PHYSICIANS_CSV_PATH=https://raw.githubusercontent.com/hfhoffman1144/langchain_neo4j_rag_app/main/data/physicians.csv
PATIENTS_CSV_PATH=https://raw.githubusercontent.com/hfhoffman1144/langchain_neo4j_rag_app/main/data/patients.csv
VISITS_CSV_PATH=https://raw.githubusercontent.com/hfhoffman1144/langchain_neo4j_rag_app/main/data/visits.csv
REVIEWS_CSV_PATH=https://raw.githubusercontent.com/hfhoffman1144/langchain_neo4j_rag_app/main/data/reviews.csv

HOSPITAL_AGENT_MODEL=gpt-3.5-turbo-1106
HOSPITAL_CYPHER_MODEL=gpt-3.5-turbo-1106
HOSPITAL_QA_MODEL=gpt-3.5-turbo-0125

```
### Step 3: Run the application

Make sure Docker is installed and running, then:

```bash
docker-compose up --build
```

The following services will start:
- Neo4j at `bolt://localhost:7687`
- FastAPI backend at `http://localhost:8000`
- Streamlit frontend at `http://localhost:8501`



## Requirements

- Python 3.10+
- Docker and Docker Compose
- Neo4j
- OpenAI API Key

## Technologies Used

- LangChain (Agents, Chains)
- FastAPI (Backend)
- Streamlit (Frontend)
- Neo4j (Graph DB)
- OpenAI (LLMs)
- Docker (Orchestration)

