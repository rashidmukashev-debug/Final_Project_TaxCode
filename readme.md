# Tax Code Assistant 🇰🇿

**Course:** CSS4007 Artificial Intelligence
**Team:** Mukashev Rashid, Bairamov Nadir

## About the Project
Tax Code Assistant is an AI-powered application that answers questions about Kazakhstan’s tax legislation. Instead of relying on a general LLM that might hallucinate legal facts, this system uses **Retrieval-Augmented Generation (RAG)** to search through the actual text of the Tax Code of the Republic of Kazakhstan and provides accurate answers with direct citations to the relevant articles.

## Features (MVP)
* Ingests and indexes sections of the Kazakhstan Tax Code.
* Processes user questions regarding tax laws.
* Retrieves relevant context from the legal text.
* Generates an answer with citations using an LLM.

## Setup Instructions

To run this project locally, follow these steps:

**1. Clone the repository:**
```bash
git clone https://github.com/your-username/Final_Project_TaxCode.git
cd Final_Project_TaxCode
```

**2. Create and activate a virtual environment:**
```bash
python -m venv .venv
# On Windows:
.venv\Scripts\activate
# On Mac/Linux:
source .venv/bin/activate
```

**3. Install dependencies:**
*(Requirements file will be added as we build the MVP)*
```bash
pip install -r requirements.txt
```

**4. Set up environment variables:**
Create a `.env` file in the root directory and add your API keys. **Never commit this file to GitHub!**
```text
OPENAI_API_KEY=your_api_key_here
```

**5. Run the application:**
```bash
python main.py
```

## Repository Structure
* `README.md` — Project description and setup guide.
* `PLAN.md` — Project milestones and implementation strategy.
* `AGENTS.md` — Instructions and prompts used for our agentic coding tools.
* `agent-logs/` — Exports of key sessions with our AI coding agent (Codex).
* `DECISIONS.md` — Log of technical decisions, challenges, and agent mistakes.
* `REFLECTION.md` — Final team reflection on the project and AI tool usage.
* `main.py` — The core MVP application script.

## Evaluation
The system will be evaluated against a custom dataset of 30 specific tax-related questions to measure retrieval accuracy, factual correctness, and proper citation format.