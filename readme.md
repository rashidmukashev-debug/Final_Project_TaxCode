# Tax Code Assistant: AI-Powered Legal Retrieval Agent 🇰🇿

Course project for CSS4007 Artificial Intelligence (Narxoz University).
**Team:** Mukashev Rashid, Bairamov Nadir.

Tax Code Assistant allows accountants, small business owners, and students to ask questions about the tax legislation of the Republic of Kazakhstan in plain language. Instead of relying on a general LLM that might hallucinate legal facts, the agent uses a Retrieval-Augmented Generation (RAG) pipeline to search the actual text of the Tax Code, providing accurate answers with exact citations to the relevant articles.

## The Problem

Navigating the Tax Code of the Republic of Kazakhstan is a complex and time-consuming task. Spreadsheets and keyword searches on standard legal portals often fail to capture the nuance of a user's specific situation. On the other hand, general chatbots (like standard ChatGPT) are prone to "hallucinating" laws, inventing article numbers, or mixing up the legislation of different countries. Our users need reliable, legally grounded insights with exact citations, without having to manually read hundreds of pages of legal text.

## What the Product Does

* **Ingest and Process Legal Text:** Automatically loads, chunks, and indexes the official text of the Kazakhstan Tax Code into a vector database.

* **Answer Specific Legal Questions:** Users can ask questions such as:

  * *"What is the corporate income tax rate for small businesses?"*

  * *"Which article regulates the deadlines for submitting VAT declarations?"*

  * *"What are the penalties for late tax payments?"*

* **Provide Verified Citations:** Every claim in the generated answer is backed by a direct citation (Article, Paragraph) from the retrieved text.

* **Handle Out-of-Scope Queries:** If a user asks a question not covered by the Tax Code (e.g., family law or criminal law), the agent explicitly explains the limitation rather than inventing an answer.

**Project scope:** The agent focuses exclusively on the static text of the Tax Code of the Republic of Kazakhstan. It does not provide certified legal counsel, calculate specific personal taxes based on user documents, or integrate with live government databases (e.g., Egov).

**Stretch goals:** A web-based interface (Streamlit), bilingual support (Russian/Kazakh), and conversational memory for follow-up questions.

## How it Works

The AI feature is a Retrieval-Augmented Generation (RAG) loop:

1. The user submits a natural language question.

2. The system converts the question into a mathematical vector (embedding).

3. The RAG pipeline performs a similarity search against a local vector database containing the chunked Tax Code.

4. The agent retrieves the top *K* most relevant legal chunks.

5. The LLM synthesizes an answer strictly based on the retrieved context, formatting the output with citations.

6. If the retrieved context does not contain the answer, the agent is prompted to decline to answer safely.

```
User Question -> Streamlit App / Terminal -> Embedding Model
                                                  |
                                                  v
                                          Vector Database (FAISS/Chroma)
                                                  | (retrieves relevant chunks)
                                                  v
                                          LLM Generation Prompt
                                                  | (context + query)
                                                  v
                                          Agent Final Answer with Citations

```

## Evaluation

We measure the AI feature using a fixed set of 30 test questions divided into four categories:

1. **Direct Article Retrieval:** Finding a specific, explicitly stated rule.

2. **Multi-Article Synthesis:** Combining information from two or more articles.

3. **Definition and Clarification:** Explaining legal tax terms based on the code.

4. **Unanswerable/Out-of-Scope:** Questions the system must safely refuse.

**Evaluation metrics:**

| Metric | Target | Result | 
| ----- | ----- | ----- | 
| **Retrieval Accuracy** | ≥ 85% | *to be filled* | 
| **Answer Faithfulness** | ≥ 95% | *to be filled* | 
| **Citation Correctness** | ≥ 90% | *to be filled* | 
| **Safe Refusal Rate** | ≥ 80% | *to be filled* | 

*Metric definitions:*

* **Retrieval Accuracy:** Percentage of test cases where the correct underlying article was successfully retrieved from the vector database.

* **Answer Faithfulness:** Percentage of generated answers that contain zero hallucinations (every claim is supported by the retrieved context).

* **Citation Correctness:** Percentage of answers where the cited Article/Paragraph numbers match the actual source text.

* **Safe Refusal Rate:** Percentage of out-of-scope questions correctly handled with a refusal.

**Baseline comparison:** We will compare our RAG system against a baseline LLM (without retrieval tools) fed the same questions, measuring the reduction in hallucinations and incorrect citations.

## Data

**Main Dataset:** The official text of the Tax Code of the Republic of Kazakhstan (parsed from public sources like *adilet.zan.kz*).

* Formats: Processed into markdown or plain text files.

* The text is chunked into logical units (e.g., by Article or Paragraph) to optimize vector search.

**Data limitations:**

* The data is static and represents the Tax Code at the time of download. It will not automatically update if new amendments are passed during the project timeframe.

## Setup Instructions

**Requirements:** Python 3.11+, an LLM API Key (OpenAI/Gemini), and dependencies in `requirements.txt`.

**1. Clone the repository:**

```
git clone <repository-url>
cd Final_Project_TaxCode

```

**2. Virtual environment:**

```
python -m venv .venv
source .venv/bin/activate  # Mac/Linux
.venv\Scripts\activate     # Windows

```

**3. Install dependencies:**

```
pip install -r requirements.txt

```

**4. Configure API access:**
Create a `.env` file in the root directory. **Never commit this to GitHub.**

```
OPENAI_API_KEY=your_api_key_here

```

**5. Run the application:**

```
python main.py

```

## LLM Provider and Limits

* **Product API:** We utilize an LLM API (e.g., OpenAI or Gemini) for text embeddings and generating the final responses. API keys are safely stored in environment variables.

* **Agentic Development:** We use **Codex (Paid)** and other agentic tools for planning, implementation, and debugging. Limits are monitored carefully to avoid exhausting daily quotas.

## Repository Structure

```
.
├── app.py                 # Streamlit interface (stretch goal)
├── main.py                # Core MVP terminal script
├── rag/                   # Embeddings, vector DB, and retrieval logic
├── data/                  # Raw and chunked Tax Code documents
├── evaluation/            # 30-question test set, evaluation script, and metrics
├── agent-logs/            # Selected agentic coding sessions
├── requirements.txt
├── .env.example
├── PLAN.md
├── AGENTS.md
├── DECISIONS.md
├── REFLECTION.md
└── README.md

```

## Team and Responsibilities

| Team Member | Owned Module and Deliverables | 
| ----- | ----- | 
| **Mukashev Rashid** | **Data & RAG Pipeline:** Data scraping/parsing from *adilet.zan.kz*, text chunking strategies, vector database initialization, embedding generation, and retrieval logic. | 
| **Bairamov Nadir** | **Application & Evaluation:** System architecture, terminal/Streamlit interface, formulation of the 30 test questions, manual baseline comparison, and evaluation metrics reporting. | 
| **Shared** | Joint evaluation of results, maintaining agent logs (`agent-logs/`), tracking tool decisions in `DECISIONS.md`, and writing the final `REFLECTION.md`. Both members commit code and understand the full pipeline. | 

## How We Built It (Agentic Development)

This project is developed primarily using agentic coding tools.

* **Codex (Paid)** is used for core logic, complex implementation, and architectural planning.

* We maintain the required development process documentation:

  * `PLAN.md` — Project milestones.

  * `AGENTS.md` — Instructions used to prompt our coding agents.

  * `agent-logs/` — Transcripts of critical coding sessions.

  * `DECISIONS.md` — Log of technical pivots, challenges, and instances where the agent failed and required human correction.

  * `REFLECTION.md` — Final team reflection.

## Roadmap

**Checkpoint (16 November 2026):**

* Tax Code data is downloaded and cleaned.

* Vector database is set up with a small sample of the law.

* Terminal MVP: User asks "What is the VAT rate?", system retrieves the text, and prints the answer.

* Initial 10 test questions evaluated.

* `PLAN.md`, `AGENTS.md`, and first logs uploaded.

**Final Release (13 December 2026):**

* Full Tax Code processed and indexed.

* Complete 30-question evaluation with baseline comparison.

* Robust citation formatting.

* `README.md`, `DECISIONS.md`, and `REFLECTION.md` finalized.

* Code freeze at tag `v1.0`.

## Limitations

* The system is an educational tool and is not a substitute for professional legal or accounting advice.

* The retrieval system relies on semantic similarity; highly ambiguous questions may retrieve sub-optimal legal clauses.

* API rate limits may restrict the speed of bulk evaluations.
