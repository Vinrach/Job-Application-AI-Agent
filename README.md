# 🤖 AI-Powered Job Search & Matching Automation Agent 

### AI-Powered Job Discovery, CV Analysis & Job Matching with n8n

<p align="center">

<img src="https://img.shields.io/badge/n8n-Workflow%20Automation-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n">
<img src="https://img.shields.io/badge/Generative%20AI-LLM%20Matching-412991?style=for-the-badge&logo=openai&logoColor=white" alt="Generative AI">
<img src="https://img.shields.io/badge/OpenRouter-LLM-6E56CF?style=for-the-badge" alt="OpenRouter">
<img src="https://img.shields.io/badge/JavaScript-Processing-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript">
<img src="https://img.shields.io/badge/Excel-XLSX-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white" alt="Excel">
<img src="https://img.shields.io/badge/Arbeitnow-Job%20API-111827?style=for-the-badge" alt="Arbeitnow">

</p>

---

## 📌 Overview

The **AI Job Search Agent** is a locally hosted **n8n workflow** that automates the initial job-search and screening process.

The workflow takes a master CV, creates a structured candidate profile using an LLM, retrieves recent jobs from the **Arbeitnow Job Board API**, filters relevant opportunities, translates German job descriptions when required, compares each job against the candidate profile, and produces a ranked Excel report.

The project is primarily designed for **QA, Software Testing, Test Automation, Quality Engineering, and related engineering roles in Germany**.

---

# 🎯 Objectives

The system automates:

* CV text extraction and profiling.
* Recent job collection.
* Role and location filtering.
* 48-hour job filtering.
* German-language detection and translation.
* CV-to-job comparison.
* AI Job Match Score calculation.
* Filtering jobs with a score of **80+**.
* Ranking and selecting the **Top 10** jobs.
* Excel report generation.

---

# 🔄 Workflow Architecture

<img width="1122" height="727" alt="image" src="https://github.com/user-attachments/assets/d5b76ebc-ba0b-4150-a9dd-330e059c6612" />

```text
Master CV
   │
   ▼
DOCX → TXT (Pandoc)
   │
   ▼
AI CV Profiling
   │
   ▼
Structured CV Profile
   │
   ▼
Arbeitnow Job API
   │
   ▼
Role / Location Filtering
   │
   ▼
48-Hour Filter
   │
   ▼
Language Detection
   │
   ├── German ──► AI Translation
   │
   └── English
          │
          ▼
     Clean Job Object
          │
          ▼
    Attach CV Profile
          │
          ▼
      AI Job Matcher
          │
          ▼
      Score ≥ 80
          │
          ▼
       Rank Jobs
          │
          ▼
        Top 10
          │
          ▼
      Excel / XLSX
```

---

# 🛠️ Technology Stack

| Component | Technology |
| --------- | ---------- |
| Automation | n8n |
| Hosting | Local / Self-hosted |
| Runtime | Node.js |
| CV | DOCX |
| CV Conversion | Pandoc |
| Job Source | Arbeitnow API |
| AI Provider | OpenRouter |
| AI Model | `openrouter/free` |
| AI Framework | n8n LangChain nodes |
| Programming | JavaScript |
| Output | XLSX / Excel |
| Data Format | JSON |

---

# 📄 1. Master CV Processing

The workflow reads the master CV from the local machine and converts it from DOCX to TXT using Pandoc.

```text
Master CV
   ↓
DOCX → TXT
   ↓
Extract CV Text
   ↓
AI CV Analysis
   ↓
Structured CV Profile
```

The current workflow uses:

```text
C:/n8n-files/Master CV/German_CV_MasterQA.docx
```

Update the path for your own environment.

---

# 🧠 2. AI CV Profiling

The CV is analyzed using an OpenRouter-powered LLM.

The generated profile contains:

* Target roles
* Technical skills
* QA skills
* Programming languages
* Testing tools
* API testing tools
* DevOps tools
* Databases
* Cloud technologies
* Experience and seniority
* Industries
* Certifications
* Education
* Languages
* Location
* Search keywords

n8n's **Structured Output Parser** is used to maintain a consistent JSON structure.

---

# 🔎 3. Job Collection & Filtering

Jobs are retrieved from:

```text
https://www.arbeitnow.com/api/job-board-api
```

The workflow converts the returned job array into individual items and applies several filters.

### Role Filtering

Relevant roles include:

* QA
* Quality Assurance
* QA Engineer
* QA Analyst
* Test Engineer
* Test Automation Engineer
* Software Tester
* Software Test Engineer
* SDET
* Quality Engineer
* Automation QA Engineer

### Time Filtering

Only jobs posted within the last:

```text
48 hours
```

are retained.

The workflow also calculates:

```text
age_hours
```

for each job.

### Location

The project targets the German job market. The current workflow includes location filtering, but the documentation identifies Germany/location filtering as an area that can still be made more robust.

---

# 🇩🇪 4. Language Detection & Translation

Job descriptions are classified as:

```text
German
English
Unknown
```

German descriptions are translated into English using an LLM.

The translator is instructed to:

* Translate the complete description.
* Preserve technical terminology.
* Preserve company names and job titles.
* Preserve numbers and requirements.
* Preserve salary and location information.
* Not summarize, add, or remove information.

English descriptions pass through unchanged.

---

# 🤖 5. AI Job Matching

Each cleaned job is combined with the structured CV profile and evaluated by the AI Job Matcher.

The scoring model is:

| Category | Points |
| -------- | -----: |
| Role Alignment | 25 |
| QA / Testing Skills | 25 |
| Tools & Technologies | 20 |
| Experience / Seniority | 10 |
| Language Compatibility | 10 |
| Education / Certifications | 5 |
| Other Requirements | 5 |
| **Total** | **100** |

The matcher evaluates actual job requirements rather than simply counting keywords.

The workflow also considers German-language requirements, including stronger penalties when higher German proficiency is explicitly required.

> **Note:** The project uses the term **AI Job Match Score**, not ATS Score, because this is a custom 100-point matching model.

---

# 📈 6. Filtering & Ranking

Only jobs with:

```text
Match Score ≥ 80
```

continue to the final stages.

The remaining jobs are sorted from highest to lowest score, and only the **Top 10** are selected.

```text
95 → Job A
92 → Job B
89 → Job C
87 → Job D
...
80 → Job J
```

---

# 📊 7. Excel Output

The final workflow generates an XLSX report containing:

| Column | Description |
| ------ | ----------- |
| Job Role | Job title |
| Company Name | Hiring company |
| Location | Job location |
| Job Description | English description |
| Match Score | AI Job Match Score |
| Recommendation | AI recommendation |
| Matching Skills | Matching candidate qualifications |
| Missing Requirements | Missing qualifications |
| Language Concerns | Language issues |
| Posted Hours Ago | Job age |
| Application Link | Original job link |

---

# 📂 Repository Structure

```text
AI-Job-Search-Agent/
│
├── workflow/
│   └── AI Job Search Agent.json
│
├── output/
│   └── .gitkeep
│
├── docs/
│   └── workflow-documentation.pdf
│
├── .gitignore
├── README.md
└── LICENSE
```

---

# 🚀 Getting Started

## Prerequisites

* n8n
* Node.js
* Pandoc
* OpenRouter API access
* Arbeitnow API access
* Excel / XLSX-compatible application

## 1. Clone

```bash
git clone https://github.com/<your-username>/AI-Job-Search-Agent.git
cd AI-Job-Search-Agent
```

## 2. Start n8n

```bash
n8n
```

## 3. Import Workflow

Import:

```text
workflow/AI Job Search Agent.json
```

into n8n.

## 4. Configure CV

Update the local CV path in the workflow:

```text
C:/n8n-files/Master CV/German_CV_MasterQA.docx
```

## 5. Configure OpenRouter

Add your OpenRouter credentials in n8n.

The current model configuration is:

```text
openrouter/free
```

Do not commit API keys or credentials to GitHub.

## 6. Run

Execute the workflow using the manual trigger:

```text
When clicking "Execute workflow"
```

The workflow will produce the final Top-10 Excel report.

---

# 🔐 Privacy & Security

The workflow processes personal CV information.

For a public repository:

* Do not commit your actual CV.
* Do not commit API keys.
* Do not commit n8n credentials.
* Do not commit `.env` files containing secrets.
* Do not commit personal job-search results.
* Replace local file paths before sharing the workflow.

---

# ⚠️ Current Limitations

* **Job sources:** Currently uses Arbeitnow; LinkedIn, StepStone, XING, etc. are not separate sources.
* **Location:** Germany filtering can be improved further.
* **Role filtering:** Primarily keyword/title based.
* **Recency:** Limited to jobs posted within 48 hours.
* **Language detection:** Uses heuristic indicators.
* **AI scoring:** A ranking signal, not a guaranteed interview probability.
* **Applications:** Does not automatically submit applications.
* **CV tailoring:** Does not currently generate tailored CVs.
* **Cover letters:** Not currently generated.

---

# 🔮 Future Improvements

* Add multiple job sources.
* Add semantic job search.
* Improve Germany/location detection.
* Add duplicate-job detection.
* Add embedding-based job/CV similarity.
* Improve skill-gap analysis.
* Add automated CV tailoring.
* Add AI cover-letter generation.
* Add email/notification support.
* Add application tracking and analytics.
* Add scheduled daily execution.

Future application workflow:

```text
Matched Job
    ↓
Select Master CV
    ↓
AI CV Tailoring
    ↓
ATS Optimization
    ↓
Tailored CV
    ↓
AI Cover Letter
    ↓
Application Package
```

---

# 🚧 Project Status

```text
✓ CV Extraction
✓ AI CV Profiling
✓ Job API Retrieval
✓ Role Filtering
✓ 48-Hour Filtering
✓ German Detection
✓ German → English Translation
✓ CV + Job Combination
✓ AI Job Matching
✓ 100-Point Scoring
✓ 80% Threshold
✓ Job Ranking
✓ Top-10 Selection
✓ Excel Generation

○ Multiple Job Sources
○ Advanced Location Filtering
○ Semantic Job Search
○ Skill-Gap Analysis
○ CV Tailoring
○ Cover Letter Generation
○ Notifications
○ Application Tracking
```

---

# 🧠 Skills Demonstrated

### AI & Data

* Generative AI
* LLMs
* Prompt Engineering
* Structured LLM Outputs
* NLP
* AI Job Matching
* Recommendation Systems

### Automation & Development

* n8n
* JavaScript
* JSON
* REST APIs
* Workflow Automation
* Data Transformation
* Pandoc
* Excel/XLSX Generation

### Job Intelligence

* CV Parsing
* Candidate Profiling
* Job Classification
* Requirement Analysis
* Skill Matching
* Language Analysis
* Job Ranking

---

# 📚 Project Resources

**Workflow:** `AI Job Search Agent.json`

**Job Source:** Arbeitnow Job Board API

**AI Provider:** OpenRouter

**Model:** `openrouter/free`

---

# 👨‍💻 Author

**Vineeth Racharla**

Master of Science in AI & Data Analytics

GitHub: **[@Vinrach](https://github.com/Vinrach)**

LinkedIn: **[Vineeth Racharla](https://linkedin.com/in/vineeth-racharla/)**

---

<div align="center">

### Generative AI • n8n • LLMs • Job Matching • Workflow Automation

**Turning Job Search into an AI-Assisted Decision Workflow**

</div>
