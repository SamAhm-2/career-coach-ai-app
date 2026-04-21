

# AI-Powered Career Coach Assistance Application

An AI-powered web application built with **Amazon Q Apps** that automates skill-gap analysis and training recommendations for Career Coaches at Career4All.

---

## Overview

Career4All's coaching team previously relied on a manual, time-consuming process to review CVs, identify skill gaps, and recommend training programs. This project replaces that workflow with an automated, scalable solution using **Amazon Q Business** backed by **Amazon S3** as a dynamic data source.

Coaches upload a learner's CV and a target job description — the application returns:
- A **skill gap analysis**
- **Personalized training recommendations** drawn from the course catalog
- A suggested **learning schedule**
- Support for **coach-driven refinements** via natural language input

---





## Architecture

| Component | Service |
|---|---|
| AI Application | Amazon Q Apps (within Amazon Q Business) |
| Document Index | Amazon Q Business retrieval index |
| Course Catalog Storage | Amazon S3 (`course-catalogueshub`) |
| Identity & Access | AWS IAM Identity Center |
| Access Control | Amazon Q Business ACL (JSON) |
| Content Moderation | Amazon Q Business Global Controls |

---

## Application Cards

The Q App is structured with the following input and output cards:

**Input Cards**
- CV upload
- Job profile / job description upload
- Coach recommendation input (free text)

**Output Cards**
- Skill gap analysis
- Training recommendations
- Suggested learning schedule

---

## Data Sources

Two data sources are connected to the Amazon Q Business index:

1. **Manually uploaded PDF** — Static course catalog uploaded directly into Amazon Q Business.
2. **Amazon S3 bucket** (`course-catalogueshub`) — Coaches upload course catalog files here; a **daily sync** keeps the index up to date automatically.

### S3 Bucket Structure

```
course-catalogueshub/
└── Data/
    ├── Security/     # Accessible to CareerCoaches group (ALLOW)
    └── Medicine/     # Restricted from CareerCoaches group (DENY)
```
### Repository Structure

```
career-coach-ai-app/
│
├── README.md                                                # This file
│
├── docs/
│   ├── project-brief.docx                                   # Original project specification
│   ├── ai-powered-career-coach-assistance-application.md     # Project submission with screenshots and implementation evidence
│   └── screenshots/
│       ├── final-app.png
│       ├── data-sources-sync.png
│       ├── skill-gap-prompt.png
│       ├── blocked-keywords.png
│       ├── acl-applied.png
│       ├── access-allowed.png
│       ├── access-denied.png
│       └── app-shared.png
│
└── config/                                                    # ACL config for S3 data source access control
    └── access-control-list.json


```
### Documents

- [Project Brief](docs/project-brief.md)
- [Project Submission](docs/ai-powered-career-coach-assistance-application.md)
- [ACL Configuration](config/access-control-list.json)
---

## Access Control

Course access is restricted by coach expertise using an ACL configuration file applied to the S3 data source.

**File:** `config/access-control-list.json`


**IAM Identity Center Groups & Users**

| Group | Users |
|---|---|
| CareerCoaches | career.coach.one, career.coach.two |

---

## Content Moderation

Keyword blocking is configured in Amazon Q Business under **Admin Controls and Guardrails → Global Controls**.

Blocked keywords: `Gambling`, `Casino`, `Self-harm`, `Attack`

These words are automatically filtered from all query responses.

---

## Setup Instructions

### Prerequisites
- AWS account with Amazon Q Business access
- IAM Identity Center configured with the `CareerCoaches` group
- An S3 bucket in the same AWS region as the Q Business application

### Steps

1. **Amazon Q Business Application**
   - Open the `CareerCoachAssistant` application in Amazon Q Business.
   - Under *Admin Controls and Guardrails → Global Controls*, enable **Allow end users to send queries directly to the LLM**.

2. **Build the Q App**
   - Create input cards for CV and job profile uploads.
   - Add output cards for skill gap analysis, training recommendations, and schedule.
   - Add an input card for coach refinements.

3. **Connect Data Sources**
   - Upload the PDF course catalog manually to the Q Business index.
   - Create the S3 bucket and upload catalog files.
   - Add the S3 bucket as a data source and configure a **daily sync schedule**.

4. **Apply Access Controls**
   - Upload `config/access-control-list.json` to the S3 bucket.
   - Link the ACL file in the S3 data source configuration within Amazon Q Business.
   - Sync the data source.

5. **Configure Keyword Blocking**
   - Navigate to *Global Controls* in the Q Business admin panel.
   - Add the restricted keywords listed above.

6. **Share the Application**
   - Share the Q App with all users in the account.
   - Apply labels (e.g., `Career Coaching`, `AI-powered`) and mark as a **Verified Q App**.

---

## Submission Checklist

- [x] Screenshot of final application (all input and output cards)
- [x] Screenshot of data sources with last sync time
- [x] Screenshot of Skill Gap Analysis output card prompt
- [x] Screenshot of blocked keywords configuration
- [x] ACL file (`config/access-control-list.json`) uploaded




