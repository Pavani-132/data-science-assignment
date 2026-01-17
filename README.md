Clinical Summary Generator
Objective

Build a Clinical Summary Generator application that ingests patient data from CSV files and uses a Large Language Model (LLM) to generate a structured, evidence-based clinical summary for home health patients.

Project Overview

This project simulates a simplified Electronic Health Record (EHR) system using CSV files.
The application allows a user to select a patient and automatically generate a concise clinical summary by aggregating diagnoses, medications, vitals, wounds, clinical notes, and functional status data.

The system consists of:

A data ingestion layer that reads CSV files

A backend API that prepares patient context and communicates with an LLM

A Streamlit frontend for user interaction

Data Sources

All patient data is stored as CSV files in the data/ directory.
Each CSV represents a table in a relational database.

diagnoses.csv – Patient diagnoses

medications.csv – Medication list and adherence

vitals.csv – Vital sign measurements over time

notes.csv – Clinical notes

wounds.csv – Active and historical wound data

oasis.csv – Functional status and OASIS assessment data

All data is filtered using patient_id.

Core Functionality
Clinical Summary Generation

The system generates a clinical summary for a given patient by following these steps:

Accept a patient_id as input

Retrieve all related patient data from the CSV files

Format the data into a structured context

Send the context to an LLM

Receive a concise, clinician-style summary

The generated summary focuses on:

Primary diagnoses

Recent vital sign trends

Active wounds (if any)

Medication usage or changes

Functional status based on OASIS data

Access Points
A. Backend API

A Python-based API (FastAPI or Flask) exposes the core functionality.

Endpoint

POST /generate_summary


Input

{
  "patient_id": 1001
}


Output

Generated clinical summary (text or structured JSON)

B. Frontend UI

A simple Streamlit application provides an easy-to-use interface.

Features

Input field for patient_id

“Generate Summary” button

Display of the generated clinical summary

Optional display of citations

LLM Integration

The LLM is instructed to act as a home health clinician.

Prompt Goals

Produce a clear, professional clinical narrative

Use only the provided patient data

Avoid assumptions or hallucinations

Maintain a clinical tone suitable for care documentation

Bonus: Citations & Evidence (Optional Enhancement)
Requirement

Each clinical statement should be verifiable.

Implementation

The LLM is instructed to cite the source CSV and date for each claim

Example:

“Blood pressure remains elevated at 145/88 on 2023-10-01
[Source: vitals.csv]”

Advanced Option

Return structured JSON linking each sentence to its source data

Display citations clearly in the UI

Project Structure
clinical-summary-generator/
├── data/
│   ├── diagnoses.csv
│   ├── medications.csv
│   ├── vitals.csv
│   ├── notes.csv
│   ├── wounds.csv
│   └── oasis.csv
├── app.py              # Streamlit frontend
├── main.py             # API backend
├── requirements.txt    # Python dependencies
└── README.md           # Project documentation

Getting Started
1. Set Up Environment
python -m venv venv
source venv/bin/activate   # macOS/Linux
venv\Scripts\activate      # Windows
pip install -r requirements.txt

2. Run Backend API
python main.py

3. Run Frontend
streamlit run app.py

Deliverables

app.py – Streamlit frontend

main.py – API backend (or unified structure)

requirements.txt

README.md – Instructions and project explanation

Evaluation Criteria

Code Quality – Clean, readable, well-structured

System Design – Clear separation of data, logic, and UI

Prompt Engineering – Effective handling of raw clinical data

User Experience – Simple and intuitive interface

Notes

This project is designed as a clinical data engineering and LLM integration exercise.
The focus is on data grounding, clarity, and trustworthiness rather than visual complexity.
