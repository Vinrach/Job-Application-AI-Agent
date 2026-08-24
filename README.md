# 🤖 AI Job Search Agent

### AI-Powered Job Discovery, CV Analysis & Intelligent Job Matching with n8n

<p align="center">

<img src="https://img.shields.io/badge/n8n-Workflow%20Automation-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n">
<img src="https://img.shields.io/badge/AI-Job%20Matching-412991?style=for-the-badge&logo=openai&logoColor=white" alt="AI">
<img src="https://img.shields.io/badge/OpenRouter-LLM-6E56CF?style=for-the-badge" alt="OpenRouter">
<img src="https://img.shields.io/badge/JavaScript-Data%20Processing-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript">
<img src="https://img.shields.io/badge/Excel-Results-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white" alt="Excel">
<img src="https://img.shields.io/badge/Arbeitnow-Job%20API-111827?style=for-the-badge" alt="Arbeitnow">

</p>

---

## 📌 Overview

This project develops an **AI-powered job search and job-matching workflow using n8n** to automate several repetitive steps involved in searching for relevant technology and software engineering jobs.

The workflow analyzes a candidate's CV, extracts a structured professional profile, retrieves recently posted jobs from the **Arbeitnow Job Board API**, filters jobs according to relevant roles and posting age, detects German-language job descriptions, translates German descriptions into English when required, and uses an AI model to evaluate candidate-to-job compatibility.

The final results are ranked by **AI-generated match score** and exported into an Excel file containing relevant job information, matching qualifications, missing requirements, language concerns, recommendations, and application links.

The project is designed to reduce manual job-search effort and provide a more structured approach to prioritizing job opportunities.

---

# 🎯 Project Objective

The primary objective is to build an automated workflow that can transform a candidate CV and a large set of available job postings into a **ranked list of relevant job opportunities**.

The system is designed to help answer questions such as:

* Which newly posted jobs are relevant to the candidate?
* How closely does each job match the candidate's experience?
* Which technical and QA skills match the job requirements?
* What requirements are missing?
* Are there German-language requirements that may affect suitability?
* Which jobs should be prioritized for application?
* Where is the original application link?
* How recently was the job posted?

---

# 🧩 Business Problem

Searching for jobs manually can involve repeatedly performing the same tasks:

* Reading job descriptions.
* Identifying relevant roles.
* Comparing job requirements with a CV.
* Checking posting dates.
* Translating German job descriptions.
* Evaluating technical requirements.
* Identifying missing qualifications.
* Prioritizing applications.
* Maintaining a job-search spreadsheet.

When performed manually across many job postings, this process can become time-consuming and inconsistent.

This project automates the repetitive parts of the workflow and uses an LLM-based evaluation layer to provide **evidence-based job matching**.

---

# 🔄 AI Job Search Workflow

```text
                       Candidate CV
                            │
                            ▼
                    CV Text Extraction
                            │
                            ▼
                 AI CV Profile Extraction
                            │
                            ▼
                 Structured Candidate Profile
                            │
                            ▼
                 Arbeitnow Job Board API
                            │
                            ▼
                     Job Extraction
                            │
                            ▼
                       Role Filter
                            │
                            ▼
                     48-Hour Filter
                            │
                            ▼
                   German Language Detection
                            │
                    ┌───────┴───────┐
                    │               │
                 German          English
                    │               │
                    ▼               │
             AI Translation         │
                    │               │
                    └───────┬───────┘
                            ▼
                     Clean Job Record
                            │
                            ▼
                  Attach Candidate Profile
                            │
                            ▼
                    AI Job Matching
                            │
                            ▼
                     Match Score
                            │
                            ▼
                   Sort by Match Score
                            │
                            ▼
                    Excel Export
