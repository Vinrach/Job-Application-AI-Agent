# 🤖 AI Job Search Agent

### AI-Powered Job Discovery, CV Analysis, Job Matching & Application Prioritization with n8n

<p align="center">

<img src="https://img.shields.io/badge/n8n-Workflow%20Automation-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n">
<img src="https://img.shields.io/badge/Generative%20AI-LLM%20Matching-412991?style=for-the-badge&logo=openai&logoColor=white" alt="Generative AI">
<img src="https://img.shields.io/badge/OpenRouter-LLM-6E56CF?style=for-the-badge" alt="OpenRouter">
<img src="https://img.shields.io/badge/JavaScript-Automation-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript">
<img src="https://img.shields.io/badge/Excel-XLSX-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white" alt="Excel">
<img src="https://img.shields.io/badge/Arbeitnow-Job%20API-111827?style=for-the-badge" alt="Arbeitnow">

</p>

------------------------------------------------------------------------

## 📌 Overview

This project develops a **locally hosted AI Job Search Agent using n8n**
to automate the repetitive parts of searching, filtering, translating,
evaluating, ranking, and organizing relevant job opportunities.

The workflow uses a **master CV** as the source of candidate
information. The CV is converted from DOCX to TXT using **Pandoc**,
extracted by n8n, and analyzed by an OpenRouter-powered LLM to generate
a structured candidate profile.

The system then retrieves job listings from the **Arbeitnow Job Board
API**, filters them according to predefined role and location criteria,
removes jobs older than 48 hours, detects German and English
descriptions, translates German descriptions into English when required,
and evaluates each remaining job against the candidate profile.

The final AI-generated **Job Match Score** is calculated using a
100-point scoring model. Jobs scoring **80 or higher** continue through
the workflow, are ranked from highest to lowest, and the **Top 10**
opportunities are exported to an Excel/XLSX report.

The system is designed primarily for **QA, Software Testing, Test
Automation, Quality Engineering, and related engineering roles in
Germany**.

------------------------------------------------------------------------

# 🎯 Project Objective

The primary objective is to automate the repetitive activities involved
in a technical job search and provide a ranked list of the most relevant
recent opportunities.

The workflow is designed to automate:

-   Extracting candidate information from a master CV.
-   Creating a structured candidate profile.
-   Searching recent job opportunities.
-   Filtering relevant job roles.
-   Filtering jobs based on location.
-   Removing jobs older than 48 hours.
-   Detecting German and English job descriptions.
-   Translating German descriptions into English.
-   Comparing jobs against the candidate's actual CV.
-   Calculating an evidence-based AI Job Match Score.
-   Keeping jobs with a score of 80 or higher.
-   Ranking the remaining jobs.
-   Selecting the Top 10 opportunities.
-   Generating an Excel report containing the selected jobs.

------------------------------------------------------------------------

# 🧩 Business Problem

Searching for jobs manually requires repeatedly performing several
activities:

-   Searching job platforms.
-   Reading job descriptions.
-   Identifying relevant roles.
-   Checking job posting dates.
-   Comparing job requirements with a CV.
-   Translating German job descriptions.
-   Evaluating technical requirements.
-   Identifying missing skills.
-   Evaluating language requirements.
-   Calculating relevance.
-   Copying application links.
-   Maintaining a job-search spreadsheet.

When performed repeatedly across many job postings, this process can
become time-consuming and inconsistent.

The AI Job Search Agent automates the majority of this initial screening
process.

Instead of manually performing:

``` text
Search jobs
     ↓
Read job descriptions
     ↓
Translate German jobs
     ↓
Compare with CV
     ↓
Calculate relevance
     ↓
Copy links
     ↓
Create Excel
```

the workflow provides:

``` text
Master CV
     ↓
Extract Candidate Profile
     ↓
Search Recent Jobs
     ↓
Filter Relevant Roles
     ↓
Filter Location
     ↓
Filter Recent Postings
     ↓
Detect German / English
     ↓
Translate German Descriptions
     ↓
Compare Jobs Against CV
     ↓
Calculate AI Job Match Score
     ↓
Keep Score ≥ 80
     ↓
Rank Jobs
     ↓
Select Top 10
     ↓
Generate Excel
```

------------------------------------------------------------------------

# 🔄 AI Job Search Workflow

``` text
                         Master CV
                            │
                            ▼
                     DOCX → TXT
                       Pandoc
                            │
                            ▼
                    Extract CV Text
                            │
                            ▼
                    AI CV Analysis
                            │
                            ▼
                 Structured CV Profile
                            │
                            ▼
                 Arbeitnow Job Board API
                            │
                            ▼
                    Job Extraction
                            │
                            ▼
                     Role Filtering
                            │
                            ▼
                   Germany Filtering
                            │
                            ▼
                    48-Hour Filtering
                            │
                            ▼
                  Language Detection
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
                    Clean Job Object
                            │
                            ▼
                   Attach CV Profile
                            │
                            ▼
                    AI Job Matcher
                            │
                            ▼
                    Match Score ≥ 80
                            │
                            ▼
                       Sort Jobs
                            │
                            ▼
                       Top 10
                            │
                            ▼
                    Excel / XLSX
```

------------------------------------------------------------------------

# 📊 Technology Stack

  Component                 Technology
  ------------------------- ---------------------
  **Automation Platform**   n8n
  **Hosting**               Local / Self-hosted
  **Runtime**               Node.js
  **CV Format**             DOCX
  **CV Conversion**         Pandoc
  **Job Source**            Arbeitnow API
  **AI Provider**           OpenRouter
  **AI Model**              `openrouter/free`
  **AI Framework**          n8n LangChain nodes
  **Programming**           JavaScript
  **Output**                XLSX / Excel
  **Data Format**           JSON

The workflow currently uses OpenRouter's `openrouter/free` model
configuration for the **CV extraction, German-to-English translation,
and job-matching stages**.

------------------------------------------------------------------------

# 🧠 AI Architecture

The project uses multiple AI stages rather than relying on a single LLM
operation.

``` text
                         Candidate CV
                              │
                              ▼
                     ┌────────────────┐
                     │  CV Extraction │
                     └───────┬────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ AI CV Profiling  │
                    └────────┬─────────┘
                             │
                             ▼
                   Structured CV Profile
                             │
                             ▼
                    Job Description
                             │
                             ▼
                  Language Detection
                             │
                             ▼
                    German Translation
                             │
                             ▼
                       Clean Job Object
                             │
                             ▼
                    Candidate + Job
                             │
                             ▼
                 ┌─────────────────────┐
                 │    AI Job Matcher   │
                 └──────────┬──────────┘
                            │
                            ▼
                       Match Score
                            │
                            ▼
                      Score ≥ 80
                            │
                            ▼
                          Top 10
                            │
                            ▼
                       Excel File
```

------------------------------------------------------------------------

# 📄 Stage 1 --- Master CV Processing

The workflow begins with a master CV stored on the local machine.

The current workflow converts the CV from **DOCX to TXT** using Pandoc.

``` text
Manual Trigger
     ↓
Master CV
     ↓
DOCX → TXT
     ↓
Read TXT File
     ↓
Extract CV Text
     ↓
AI CV Analysis
     ↓
Structured CV Profile
```

The current workflow paths are configured as:

``` text
C:/n8n-files/Master CV/German_CV_MasterQA.docx
C:/n8n-files/Master CV/German_CV_MasterQA.txt
```

These local paths must be changed when the workflow is deployed on
another machine.

------------------------------------------------------------------------

# 🧠 Stage 2 --- AI CV Profiling

The extracted CV text is passed to an OpenRouter-powered LLM.

The AI generates a structured candidate profile containing:

-   Target roles
-   Technical skills
-   QA skills
-   Programming languages
-   Testing tools
-   API testing tools
-   DevOps tools
-   Databases
-   Cloud technologies
-   Years of experience
-   Seniority
-   Industries
-   Certifications
-   Education
-   Languages
-   Location
-   Search keywords

The workflow uses n8n's **Structured Output Parser** to enforce the
expected JSON structure.

The candidate profile becomes the foundation for the later job-matching
process.

------------------------------------------------------------------------

# 👤 Candidate Profile Structure

``` text
Candidate Profile
│
├── Target Roles
├── Technical Skills
├── QA Skills
├── Programming Languages
├── Testing Tools
├── API Testing Tools
├── DevOps Tools
├── Databases
├── Cloud Technologies
├── Years of Experience
├── Seniority
├── Industries
├── Certifications
├── Education
├── Languages
├── Location
└── Search Keywords
```

The workflow instructs the CV analyzer not to invent skills, experience,
certifications, job titles, or technologies that are not supported by
the CV.

------------------------------------------------------------------------

# 🔎 Stage 3 --- Job Collection

The workflow calls the **Arbeitnow Job Board API** and retrieves job
listings.

The current endpoint is:

``` text
https://www.arbeitnow.com/api/job-board-api
```

The returned job array is converted into individual n8n items using
JavaScript:

``` javascript
const jobs = $input.first().json.data;

return jobs.map(job => ({
  json: job
}));
```

This allows each job to move independently through the filtering and
AI-matching stages.

------------------------------------------------------------------------

# 🎯 Stage 4 --- Job Filtering

The system progressively reduces the number of jobs before expensive AI
matching is performed.

## Role Filtering

The workflow filters job titles for relevant roles including:

-   QA
-   Quality Assurance
-   QA Engineer
-   QA Analyst
-   Test Engineer
-   Test Automation Engineer
-   Software Tester
-   Software Test Engineer
-   SDET
-   Quality Engineer
-   Automation QA Engineer
-   Machine Learning
-   Working Student
-   Werkstudent
-   Automation Engineer
-   AI Enablement Engineer
-   Graduate
-   Data Scientist
-   Data Analyst

The current JSON workflow implements a title-based regular-expression
filter.

------------------------------------------------------------------------

## Location Filtering

The project is designed primarily for **Germany**.

The project documentation identifies Germany as the intended target
market and notes that Germany/location filtering is an area being made
more robust.

The current JSON workflow contains a location condition that excludes
`London`. Therefore, the Germany-only location logic should be reviewed
and configured for the deployment environment before treating it as a
fully robust Germany filter.

------------------------------------------------------------------------

## Time Filtering

Jobs older than **48 hours** are removed.

The workflow calculates job age using the `created_at` timestamp and
generates:

``` text
age_hours
```

for each surviving job.

------------------------------------------------------------------------

# 🌍 Stage 5 --- Language Detection

The workflow examines job descriptions and determines whether the
content is:

``` text
German
English
Unknown
```

The German detection logic:

-   Converts text to lowercase.
-   Removes HTML tags.
-   Removes common HTML entities.
-   Normalizes whitespace.
-   Searches for predefined German indicators.
-   Checks whether enough usable text exists.

Examples of German indicators include:

-   der
-   die
-   das
-   den
-   dem
-   des
-   und
-   oder
-   für
-   mit
-   Aufgaben
-   Anforderungen
-   Qualifikationen
-   Erfahrung
-   Kenntnisse
-   Bewerbung
-   Voraussetzungen
-   Wir bieten
-   Du hast
-   Du bist
-   Du verfügst
-   Deine
-   Dein
-   Deutschkenntnisse
-   Abgeschlossenes Studium

This prevents unnecessary translation calls for English jobs.

------------------------------------------------------------------------

# 🇩🇪 Stage 6 --- German → English Translation

If the description is detected as German, it is passed to the AI
translation stage.

The translator is instructed to:

-   Translate the complete job description.
-   Not summarize.
-   Not add information.
-   Not remove information.
-   Preserve technical terminology.
-   Preserve company names.
-   Preserve job titles.
-   Preserve numbers.
-   Preserve experience requirements.
-   Preserve qualifications.
-   Preserve salary information.
-   Preserve locations.

``` text
German Job
    ↓
AI Translator
    ↓
English Job Description
```

If the description is already English, it is passed through unchanged.

------------------------------------------------------------------------

# 🧹 Stage 7 --- Clean Job Object

After translation, the workflow normalizes each job into a consistent
structure.

``` json
{
  "job_title": "...",
  "company_name": "...",
  "location": "...",
  "description_original": "...",
  "description_english": "...",
  "application_link": "...",
  "age_hours": 1.2,
  "created_at": "...",
  "remote": false,
  "tags": [],
  "job_types": [],
  "detected_language": "German"
}
```

This is important because both German and English jobs must have the
same structure before entering the AI matcher.

------------------------------------------------------------------------

# 🔗 Stage 8 --- Attach CV Profile

Each cleaned job is combined with the structured CV profile.

Conceptually:

``` json
{
  "cv_profile": {
    "target_roles": [],
    "technical_skills": [],
    "qa_skills": [],
    "programming_languages": [],
    "testing_tools": [],
    "api_testing_tools": [],
    "devops_tools": [],
    "databases": [],
    "cloud_technologies": [],
    "years_of_experience": null,
    "seniority": null,
    "industries": [],
    "certifications": [],
    "education": [],
    "languages": [],
    "location": null,
    "search_keywords": []
  },
  "job": {
    "job_title": "...",
    "company_name": "...",
    "description_english": "...",
    "location": "...",
    "application_link": "..."
  }
}
```

This creates a self-contained input for the AI matcher.

------------------------------------------------------------------------

# 🤖 Stage 9 --- AI Job Matching

The AI evaluates the candidate against each job.

The current matching model considers:

1.  Job title and role alignment.
2.  QA and software testing skills.
3.  Test automation.
4.  Programming languages.
5.  Testing tools and frameworks.
6.  API testing.
7.  CI/CD and DevOps.
8.  Databases and cloud technologies.
9.  Required years of experience.
10. Seniority.
11. Education.
12. Certifications.
13. Industry/domain.
14. Language requirements.
15. Location and working arrangement.

The matcher is instructed to evaluate actual requirements rather than
simply counting keyword matches.

The candidate is primarily targeting:

-   QA Engineer
-   Test Engineer
-   Test Automation Engineer
-   Software Testing
-   Quality Assurance
-   API Testing

------------------------------------------------------------------------

# 📊 AI Job Match Scoring Model

The current scoring model is:

  Category                       Maximum Score
  ---------------------------- ---------------
  Role Alignment                            25
  QA / Testing Skills                       25
  Tools & Technologies                      20
  Experience / Seniority                    10
  Language Compatibility                    10
  Education / Certifications                 5
  Other Requirements                         5
  **Total**                            **100**

The final `match_score` must equal the sum of all scoring categories.

The project should refer to this as the **AI Job Match Score**, rather
than an ATS score, because it is the workflow's own 100-point
candidate-to-job matching model and does not reproduce a proprietary ATS
scoring algorithm.

------------------------------------------------------------------------

# 🌐 Language Compatibility

The matcher specifically handles language requirements:

``` text
English
   ↓
Required / Preferred

German
   ↓
Bonus

German B2/C1 requirement
   ↓
Significant penalty
```

The workflow is instructed not to reject a job because German is merely
listed as a nice-to-have.

If German is explicitly required at B2/C1 or higher, the candidate's A1
German level should result in a significant penalty.

The system also distinguishes between:

-   Required
-   Preferred
-   Nice-to-have

requirements.

------------------------------------------------------------------------

# 📈 Stage 10 --- Match Score Filtering

Only jobs with:

``` text
Match Score ≥ 80
```

continue through the workflow.

``` text
                     AI Match Score
                           │
                           ▼
                    ┌──────────────┐
                    │ Score ≥ 80 ? │
                    └──────┬───────┘
                           │
                 ┌─────────┴─────────┐
                 │                   │
                YES                  NO
                 │                   │
                 ▼                   ▼
              Keep                 Remove
```

This reduces the final dataset to jobs considered strong matches
according to the project's scoring model.

------------------------------------------------------------------------

# 🔃 Stage 11 --- Ranking and Top 10

The remaining jobs are sorted from highest to lowest score.

The final workflow keeps only the **Top 10** rather than returning every
job that happens to score above 80.

For example:

``` text
95 → Job A
92 → Job B
89 → Job C
87 → Job D
85 → Job E
84 → Job F
83 → Job G
82 → Job H
81 → Job I
80 → Job J
```

This keeps the final result focused on the strongest recent
opportunities.

------------------------------------------------------------------------

# 📊 Stage 12 --- Excel Output

The final workflow converts the selected jobs into Excel-ready records.

The current output contains:

  -----------------------------------------------------------------------
  Column                    Description
  ------------------------- ---------------------------------------------
  **Job Role**              Job title

  **Company Name**          Hiring company

  **Location**              Job location

  **Job Description**       English job description

  **Match Score**           AI Job Match Score

  **Recommendation**        AI-generated recommendation

  **Matching Skills**       Candidate qualifications matching the job

  **Missing Requirements**  Requirements not sufficiently supported by
                            the CV

  **Language Concerns**     Relevant language compatibility concerns

  **Posted Hours Ago**      Approximate job age

  **Application Link**      Original job/application URL
  -----------------------------------------------------------------------

The workflow converts these records to XLSX.

The configured output filename is:

``` text
QA_Job_Search_Reasults.xlsx
```

------------------------------------------------------------------------

# 🧩 Structured AI Outputs

The workflow uses n8n Structured Output Parser nodes to enforce
consistent AI responses.

## Candidate Profile

``` json
{
  "target_roles": [],
  "technical_skills": [],
  "qa_skills": [],
  "programming_languages": [],
  "testing_tools": [],
  "api_testing_tools": [],
  "devops_tools": [],
  "databases": [],
  "cloud_technologies": [],
  "years_of_experience": null,
  "seniority": null,
  "industries": [],
  "certifications": [],
  "education": [],
  "languages": [],
  "location": null,
  "search_keywords": []
}
```

## Job Match

``` json
{
  "match_score": 0,
  "role_alignment_score": 0,
  "qa_testing_score": 0,
  "tools_technology_score": 0,
  "experience_score": 0,
  "language_score": 0,
  "education_certification_score": 0,
  "other_requirements_score": 0,
  "recommendation": "Strong Match",
  "matching_qualifications": [],
  "missing_requirements": [],
  "language_concerns": [],
  "reason": ""
}
```

Structured outputs make the workflow easier to process programmatically
and export into a consistent Excel report.

------------------------------------------------------------------------

# 🛠️ Technology Stack

  -----------------------------------------------------------------------
  Technology                                Purpose
  ----------------------------------------- -----------------------------
  **n8n**                                   Workflow automation and
                                            orchestration

  **OpenRouter**                            LLM access for CV analysis,
                                            translation, and job matching

  **Arbeitnow API**                         Job posting data source

  **JavaScript**                            Job filtering,
                                            transformation, sorting, and
                                            processing

  **Pandoc**                                DOCX-to-TXT CV conversion

  **Excel / XLSX**                          Job-search result reporting

  **JSON**                                  Workflow configuration and
                                            structured AI outputs

  **Large Language Models**                 CV profiling, translation,
                                            and candidate-job evaluation
  -----------------------------------------------------------------------

### Primary Skills Demonstrated

-   Generative AI
-   Large Language Models
-   Prompt Engineering
-   n8n Workflow Automation
-   AI Job Matching
-   CV Parsing
-   Natural Language Processing
-   API Integration
-   JavaScript
-   Data Transformation
-   Structured AI Outputs
-   Job Recommendation
-   Requirement Analysis
-   Excel Reporting
-   Workflow Design

------------------------------------------------------------------------

# 📂 Repository Structure

A recommended GitHub repository structure is:

``` text
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

### `workflow/`

Contains the exported n8n workflow.

### `AI Job Search Agent.json`

The primary project file containing the n8n workflow configuration,
nodes, prompts, JavaScript processing logic, structured output parsers,
and workflow connections.

### `output/`

Optional directory for generated XLSX job-search results.

### `docs/`

Optional directory for workflow documentation and diagrams.

### `.gitignore`

Prevents credentials, personal CV files, generated output, temporary
files, and environment-specific data from being committed.

### `README.md`

Contains the project documentation and setup instructions.

------------------------------------------------------------------------

# 🚀 Getting Started

## Prerequisites

To run the project, install or configure:

-   n8n
-   Node.js
-   Pandoc
-   OpenRouter API access
-   Arbeitnow Job Board API access
-   Microsoft Excel or an XLSX-compatible application

The workflow is designed to run locally/self-hosted.

------------------------------------------------------------------------

## 1. Clone the Repository

``` bash
git clone https://github.com/<your-username>/AI-Job-Search-Agent.git

cd AI-Job-Search-Agent
```

Replace `<your-username>` with your GitHub username.

------------------------------------------------------------------------

## 2. Start n8n

For a local n8n installation:

``` bash
n8n
```

Alternatively, n8n can be deployed using Docker.

------------------------------------------------------------------------

## 3. Import the Workflow

Open the n8n interface and import:

``` text
workflow/AI Job Search Agent.json
```

The imported workflow contains the complete pipeline and node
connections.

------------------------------------------------------------------------

## 4. Configure the Master CV

The current workflow expects:

``` text
C:/n8n-files/Master CV/German_CV_MasterQA.docx
```

The workflow uses Pandoc to convert the DOCX CV into:

``` text
C:/n8n-files/Master CV/German_CV_MasterQA.txt
```

If the CV is stored in a different location, update the corresponding
file paths in n8n.

------------------------------------------------------------------------

## 5. Configure OpenRouter

Configure your OpenRouter credentials inside n8n.

The workflow currently uses:

``` text
openrouter/free
```

for:

-   CV profiling.
-   German-to-English translation.
-   AI job matching.

Do not commit OpenRouter API credentials to GitHub.

------------------------------------------------------------------------

## 6. Execute the Workflow

The current workflow starts with the manual trigger:

``` text
When clicking "Execute workflow"
```

Execute the workflow from n8n.

The workflow then:

1.  Extracts the CV.
2.  Builds the candidate profile.
3.  Retrieves jobs.
4.  Filters relevant roles.
5.  Applies location filtering.
6.  Filters jobs posted within 48 hours.
7.  Detects German descriptions.
8.  Translates German descriptions.
9.  Builds clean job objects.
10. Attaches the CV profile.
11. Matches jobs using AI.
12. Applies the 80-point threshold.
13. Sorts the remaining jobs.
14. Selects the Top 10.
15. Generates the Excel report.

------------------------------------------------------------------------

# 🔁 Reproducing the Analysis

``` text
Candidate CV
     │
     ▼
DOCX → TXT
     │
     ▼
CV Text Extraction
     │
     ▼
AI Candidate Profile
     │
     ▼
Structured Candidate Data
     │
     ▼
Arbeitnow Job API
     │
     ▼
Job Listings
     │
     ▼
Role Filtering
     │
     ▼
Location Filtering
     │
     ▼
48-Hour Filtering
     │
     ▼
Language Detection
     │
     ├── German ──► AI Translation
     │
     └── English ─► Continue
                         │
                         ▼
                  Clean Job Record
                         │
                         ▼
                 Candidate + Job
                         │
                         ▼
                   AI Matching
                         │
                         ▼
                   Match Score
                         │
                         ▼
                    Score ≥ 80
                         │
                         ▼
                      Ranking
                         │
                         ▼
                      Top 10
                         │
                         ▼
                  Excel Results
```

------------------------------------------------------------------------

# 📋 Example Output

A typical final job record contains:

``` text
Job Role
Company Name
Location
Job Description
Match Score
Recommendation
Matching Skills
Missing Requirements
Language Concerns
Posted Hours Ago
Application Link
```

This makes it possible to move from:

``` text
Large Number of Job Listings
          │
          ▼
      Role Filtering
          │
          ▼
    Recent Job Filtering
          │
          ▼
      AI Job Matching
          │
          ▼
       Score ≥ 80
          │
          ▼
        Top 10
          │
          ▼
Prioritized Opportunities
```

------------------------------------------------------------------------

# 💡 Business Value

The AI Job Search Agent provides an automated decision-support layer for
job searching.

The workflow can help reduce repetitive manual effort associated with:

-   Job discovery.
-   Job filtering.
-   Job recency checking.
-   CV-to-job comparison.
-   German job translation.
-   Requirement analysis.
-   Skill matching.
-   Language requirement analysis.
-   Job ranking.
-   Excel report preparation.

The final system is intended as a **personal AI-powered job discovery
and ranking agent** rather than an autonomous application-submission
system.

------------------------------------------------------------------------

# 🔐 Data Privacy & Security

The workflow processes CV information that may contain personal and
professional data.

For safe public GitHub usage:

-   Do not commit the actual CV file.
-   Do not commit API keys.
-   Do not commit n8n credentials.
-   Do not commit `.env` files containing secrets.
-   Do not commit generated job-search reports containing personal data.
-   Do not expose private local file paths unnecessarily.
-   Use n8n credential management for API credentials.
-   Review external LLM provider data-handling policies before
    processing private CV information.

The workflow contains local Windows paths and credential references.
These should be replaced with environment-specific configuration before
public deployment.

------------------------------------------------------------------------

# ⚠️ Current Limitations

## Job Sources

The current workflow specifically retrieves jobs from the **Arbeitnow
Job Board API**.

LinkedIn, StepStone, XING, and other job platforms are not currently
represented as separate sources in this workflow.

## Location Filtering

Germany is the intended target market, but the current JSON contains a
location condition that excludes London rather than implementing a
complete Germany-only semantic location filter.

## Role Filtering

The current workflow uses predefined job-title keywords. Relevant jobs
with unconventional titles may therefore be excluded before reaching the
AI matching stage.

## Job Recency

The current workflow considers jobs posted within the previous **48
hours**.

## Language Detection

German language detection uses heuristic word and phrase indicators
rather than a dedicated language-classification model.

## AI Match Score

The score is generated by an LLM using the project's own 100-point
scoring model. It should be treated as an **AI-assisted ranking
signal**, not as a guaranteed probability of receiving an interview.

## Application Automation

The current workflow does not automatically submit job applications. It
provides the original application link for manual review and
application.

## CV Tailoring

The current workflow analyzes the CV but does not automatically generate
a job-specific tailored CV.

## Cover Letter Generation

The current workflow does not currently generate cover letters.

------------------------------------------------------------------------

# 🔮 Future Improvements

## 🔍 Job Discovery

-   Add multiple job APIs.
-   Add additional job-board integrations.
-   Add company career-page discovery.
-   Add configurable job sources.
-   Add semantic job searching.
-   Add duplicate job detection.
-   Add configurable posting-age filters.
-   Add configurable target locations.
-   Add remote/hybrid/on-site preferences.

## 📍 Location Intelligence

-   Implement robust Germany-wide location detection.
-   Detect German cities and regions.
-   Support multiple target countries.
-   Identify remote positions.
-   Distinguish remote, hybrid, and on-site roles.
-   Support radius-based location filtering.

## 🤖 AI Matching

-   Introduce embedding-based semantic similarity.
-   Combine deterministic scoring with LLM evaluation.
-   Add configurable scoring weights.
-   Improve required/preferred/nice-to-have classification.
-   Add skill-gap analysis.
-   Add seniority-aware matching.
-   Add industry/domain matching.
-   Add explainable scoring for individual requirements.
-   Improve multilingual job analysis.

## 📄 CV & Application Generation

A future version could extend the workflow with:

``` text
Matched Job
     │
     ▼
Select Appropriate Master CV
     │
     ▼
AI CV Tailoring
     │
     ▼
ATS Optimization
     │
     ▼
Tailored CV
     │
     ▼
AI Cover Letter
     │
     ▼
Application Package
```

This would transform the current job-discovery system into a broader
AI-assisted job-application platform.

## 📊 Job Search Analytics

Future versions could track:

-   Total jobs discovered.
-   Jobs passing role filters.
-   Jobs passing location filters.
-   Jobs passing the 48-hour filter.
-   Average AI Job Match Score.
-   Number of jobs scoring 80+.
-   Most frequently missing skills.
-   Most requested technologies.
-   Most relevant job titles.
-   Most common language requirements.
-   Applications submitted.
-   Interview conversion rate.
-   Rejection rate.

## ⚙️ Workflow Automation

The current workflow uses a manual trigger.

A future version could introduce scheduled execution:

``` text
Scheduled Trigger
       │
       ▼
Daily Job Search
       │
       ▼
Job Filtering
       │
       ▼
AI Matching
       │
       ▼
Score ≥ 80
       │
       ▼
Top 10
       │
       ▼
Email / Notification
```

------------------------------------------------------------------------

# 📊 Potential End-to-End Architecture

``` text
                         AI JOB SEARCH AGENT
                                  │
          ┌───────────────────────┼────────────────────────┐
          │                       │                        │
          ▼                       ▼                        ▼
      Candidate CV            Job Sources             Preferences
          │                       │                        │
          ▼                       ▼                        ▼
      CV Analyzer           Arbeitnow API          Target Roles
          │                       │                  Location
          ▼                       ▼                  Job Age
 Candidate Profile         Job Filtering           Preferences
          │                       │                        │
          └───────────────┬───────┘                        │
                          ▼                                │
                  Language Processing                      │
                          │                                │
                          ▼                                │
                    AI Job Matcher ◄──────────────────────┘
                          │
                          ▼
                    Match Scoring
                          │
                          ▼
                      Score ≥ 80
                          │
                          ▼
                       Ranking
                          │
                          ▼
                        Top 10
                          │
                          ▼
                    Excel Results
```

------------------------------------------------------------------------

# 🧠 Skills Demonstrated

## Artificial Intelligence

-   Generative AI
-   Large Language Models
-   Prompt Engineering
-   Structured LLM Outputs
-   AI-Based Job Matching
-   Natural Language Processing
-   AI-Assisted Decision Support

## Workflow Automation

-   n8n
-   Workflow orchestration
-   Conditional workflow execution
-   API integration
-   Automated file processing
-   Data transformation

## Software Engineering

-   JavaScript
-   JSON
-   REST API integration
-   Data processing
-   Structured data handling
-   Workflow architecture

## Job Intelligence

-   CV parsing
-   Candidate profiling
-   Job classification
-   Job matching
-   Requirement analysis
-   Skill-gap identification
-   Language compatibility analysis
-   Job ranking

## Data Processing

-   DOCX-to-TXT conversion
-   Timestamp processing
-   Job filtering
-   Data normalization
-   Sorting
-   XLSX generation
-   Structured JSON processing

------------------------------------------------------------------------

# 📚 Project Resources

### Workflow

The primary project artifact is:

``` text
AI Job Search Agent.json
```

This file contains the exported n8n workflow.

### Job Data Source

The workflow currently uses:

**Arbeitnow Job Board API**

### AI Provider

The workflow currently uses:

**OpenRouter**

### AI Model Configuration

``` text
openrouter/free
```

------------------------------------------------------------------------

# 📌 Final Project Goal

The completed system is a personal AI-powered job discovery and ranking
agent designed to answer:

> **"Give me the newest relevant QA/testing jobs in Germany, compare
> them against my actual CV, and give me the best opportunities in an
> Excel report."**

The current workflow automates the core pipeline:

``` text
CV Extraction
      ↓
Structured CV Profiling
      ↓
Job API Retrieval
      ↓
Role Filtering
      ↓
Location Filtering
      ↓
48-Hour Filtering
      ↓
German Detection
      ↓
German → English Translation
      ↓
CV + Job Combination
      ↓
AI Job Matching
      ↓
80% Match Threshold
      ↓
Ranking
      ↓
Top 10
      ↓
Excel Generation
```

------------------------------------------------------------------------

# 🚧 Project Status

``` text
┌─────────────────────────────────────────────┐
│             AI JOB SEARCH AGENT             │
├─────────────────────────────────────────────┤
│                                             │
│  ✓ CV Text Extraction                       │
│  ✓ Structured CV Profiling                  │
│  ✓ Job API Retrieval                        │
│  ✓ Role Filtering                           │
│  ✓ 48-Hour Job Filtering                    │
│  ✓ German Language Detection                │
│  ✓ German → English Translation              │
│  ✓ Clean Job Object Generation              │
│  ✓ CV + Job Profile Combination             │
│  ✓ AI Job Matching                          │
│  ✓ 100-Point Match Scoring                  │
│  ✓ 80% Match Threshold                      │
│  ✓ Job Ranking                              │
│  ✓ Top-10 Selection                         │
│  ✓ Excel Generation                         │
│                                             │
│  ○ Multiple Job Sources                     │
│  ○ More Robust Germany Filtering            │
│  ○ Semantic Job Search                      │
│  ○ Advanced Skill-Gap Analysis              │
│  ○ Tailored CV Generation                   │
│  ○ Cover Letter Generation                  │
│  ○ Automated Notifications                  │
│  ○ Application Tracking                     │
│                                             │
└─────────────────────────────────────────────┘
```

The core pipeline is documented as working across CV extraction,
structured profiling, job API retrieval, role filtering, 48-hour
filtering, German detection, translation, CV/job combination, AI
matching, 80% filtering, Top-10 ranking, and Excel generation.

The major remaining development areas are expanding job sources and
making Germany/location and language filtering increasingly robust.

------------------------------------------------------------------------

# 👨‍💻 Author

**Vineeth Racharla**

Master of Science in AI & Data Analytics

GitHub: **[@Vinrach](https://github.com/Vinrach)**

LinkedIn: **[Vineeth
Racharla](https://linkedin.com/in/vineeth-racharla/)**

------------------------------------------------------------------------

::: {align="center"}
### Generative AI • n8n • LLMs • Job Matching • Workflow Automation

**Turning Job Search into an AI-Assisted Decision Workflow**
:::
