Clinical Summary Generator
Overview

The Clinical Summary Generator is a Python-based application that generates concise, evidence-based clinical summaries for home health patients.
It simulates a simplified Electronic Health Record (EHR) system using CSV files and leverages a Large Language Model (LLM) to transform raw patient data into a structured clinical narrative.

The project includes:

A FastAPI backend for summary generation

A Streamlit frontend for user interaction

A CSV-based data layer representing EHR tables

Objective

To build a system that:

Ingests patient data from multiple CSV files

Aggregates data by patient_id

Uses an LLM to generate a clinician-style summary

Optionally includes citations for data traceability

Features

Patient-level data filtering using patient_id

Structured clinical summaries

REST API for summary generation

Streamlit UI for easy usage

Evidence-based summaries with optional citations

Modular design (Data Layer, API, UI, LLM)

Data Sources

All patient data is stored in the data/ directory as CSV files:

File	Description
diagnoses.csv	Patient diagnoses
medications.csv	Medication details
vitals.csv	Vital sign history
notes.csv	Clinical notes
wounds.csv	Wound assessments
oasis.csv	Functional status (OASIS)

Each file is queried using patient_id.

System Architecture
Streamlit UI
     |
FastAPI Backend
     |
Data Layer (CSV Files)
     |
LLM (Clinical Summary Generation)

Tech Stack

Python 3.8+

FastAPI – Backend API

Streamlit – Frontend UI

Pandas – Data processing

Google Gemini / OpenAI – LLM integration

Uvicorn – ASGI server

Project Structure
clinical-summary-generator/
├── data/

│   ├── diagnoses.csv

│   ├── medications.csv

│   ├── vitals.csv

│   ├── notes.csv

│   ├── wounds.csv

│   └── oasis.csv

├── src/

│   ├── data_layer.py

│   └── llm_service.py

├── app.py              # Streamlit frontend

├── main.py             # FastAPI backend

├── requirements.txt

├── .env.example

└── README.md

Installation & Setup
1. Create Virtual Environment
python -m venv venv
source venv/bin/activate      # macOS/Linux
venv\Scripts\activate         # Windows

2. Install Dependencies
pip install -r requirements.txt

3. Configure Environment Variables
cp .env.example .env


Add your LLM API key in .env:

GEMINI_API_KEY=your_api_key_here
# Optional
OPENAI_API_KEY=your_openai_key_here

Running the Application
Start Backend API
python main.py


API will be available at:

http://localhost:8000

Docs: http://localhost:8000/docs

Start Frontend UI
streamlit run app.py


UI will open at:

http://localhost:8501

API Endpoints
Health Check
GET /health

List Patients
GET /patients

Generate Clinical Summary
POST /generate_summary


Request Body

{

  "patient_id": 1001,
  "include_citations": true
  
}

Clinical Summary Content

The generated summary focuses on:

Primary diagnoses

Recent vital sign trends

Active wounds

Medications and adherence

Functional status (OASIS)

When enabled, each statement includes citations referencing the source CSV file and date.

Example Output
Patient presents with chronic pressure ulcers and requires assistance
with activities of daily living. Recent vital signs remain stable.
[Source: vitals.csv, oasis.csv]

Evaluation Focus

Code quality and organization

Clear separation of concerns

Effective prompt engineering

Usable and intuitive interface

Data-grounded LLM responses

