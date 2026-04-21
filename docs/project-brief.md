# Project Brief
## AI-Powered Career Coach Assistance Application — Career4All

---

## Project Details

| | |
|---|---|
| **Organisation** | Career4All |
| **Platform** | Amazon Q Apps (Amazon Q Business) |
| **Cloud Provider** | Amazon Web Services (AWS) |
| **Role** | Cloud Engineer |
| **Stakeholder** | Emma — Lead Career Coach |
| **Repository** | career-coach-ai-app |

---

## 1. Project Overview

Career coaching at Career4All involves skill-gap analysis and training recommendations. The current manual process is inefficient and inconsistent. This project builds a web-based application using Amazon Q Apps — a no-code solution — to automate skill-gap analysis by comparing student CVs against job descriptions and recommending relevant training from Career4All's digital catalog. Coaches can fine-tune recommendations using natural language inputs, ensuring consistency and up-to-date guidance for students.

---

## 2. Problem Statement

### Current Workflow

- **Resume Review & Skill Gap Analysis** — coach manually reviews the learner's CV and compares it against a job description to identify skill gaps
- **Training Recommendations** — coach selects relevant training programs from a catalog and creates a personalised learning schedule
- **Customisation** — coaches fine-tune recommendations based on learner skill level, time availability, and preferred learning format

### Key Challenges

- **Manual & Time-Consuming** — significant manual effort across every coaching engagement
- **Scalability** — learner volume has doubled in six months; the team cannot keep pace
- **Keeping Resources Updated** — coaches struggle to stay current with evolving training programs and technologies

---

## 3. Project Goal

Develop an automated solution that streamlines the career coaching process, improves efficiency, and enables scalability — leveraging AWS services.

---

## 4. Solution Architecture

| Component | Service |
|---|---|
| AI Application | Amazon Q Apps (within Amazon Q Business) |
| Document Index | Amazon Q Business retrieval index |
| Course Catalog Storage | Amazon S3 (`course-catalogueshub`) |
| Identity & Access | AWS IAM Identity Center |
| Access Control | Amazon Q Business ACL (JSON) |
| Content Moderation | Amazon Q Business Global Controls |

---

## 5. Application Design

### Input Cards
- CV upload
- Job profile / job description upload
- Coach recommendation input (free text)

### Output Cards
- Skill gap analysis
- Training recommendations
- Suggested learning schedule

---

## 6. Build Instructions

### Section 1 — Setup Amazon Q Business

Use the provided AWS sandbox. If using the Udacity-provided Amazon Q Business, the following resources are pre-created: Amazon Q Business application, IAM Identity Center group, and IAM Identity Center users.

Navigate to **CareerCoachAssistant → Admin Controls and Guardrails → Global Controls → Edit**. Enable **Allow end users to send queries directly to the LLM** and save.

---

### Section 2 — Create the Application

#### Task 1 — Basic Application
- Step 1.1 — Create a basic application
- Step 1.2 — Add input cards for CV and job profile uploads
- Step 1.3 — Add output card for skill gap analysis
- Step 1.4 — Add output card for training recommendation
- Step 1.5 — Verify the application

#### Task 2 — Customise the Application
- Step 2.1 — Add output card for learning schedule
- Step 2.2 — Add input card for coach recommendation (free text)

---

### Section 3 — Enhance with PDF Course Catalog

#### Task 3 — Use Existing Data Source
- Step 3.1 — Access the already-uploaded PDF course catalog in Amazon Q Business
- Step 3.2 — Verify queries retrieve training recommendations from this source
- Step 3.3 — Confirm results integrate seamlessly with other data sources

---

### Section 4 — Connect Amazon S3 as a Data Source

#### Task 4 — Add S3 Data Source
- Step 4.1 — Create an Amazon S3 bucket and upload static course catalog
- Step 4.2 — Sync the data source
- Step 4.3 — Verify recommendations include training from the new source
- Step 4.4 — Configure a daily sync schedule

---

### Section 5 — Security & Access Control

#### Task 5 — Restrict Course Access by Coach Expertise
- Step 5.1 — Use the existing `CareerCoaches` group in IAM Identity Center (users: `career.coach.one`, `career.coach.two`)
- Step 5.2 — Upload restricted course files to the S3 bucket under `Data/Medicine/` and `Data/Security/`
- Step 5.3 — Create the ACL configuration file and associate it with the data source

**ACL Rules**

| S3 Path | Group | Access |
|---|---|---|
| `s3://.../Data/Security/` | CareerCoaches | ALLOW |
| `s3://.../Data/Medicine/` | CareerCoaches | DENY |

#### Task 6 — Keyword Blocking
- Step 6.1 — Block keywords: `Gambling`, `Casino`, `Self-harm`, `Attack`
- Configure under **Admin Controls and Guardrails → Global Controls**

---

### Section 6 — Share the Application

#### Task 7 — Share the App
- Step 7.1 — Share the application with all users in the account
- Apply custom labels: `Career Coaching`, `AI-powered`
- Endorse and mark as a **Verified Q App**

---

## 7. Submission Requirements

- Screenshot of the final application showing all input and output cards
- Screenshot of data sources showing the last sync time
- Screenshot of the Skill Gap Analysis output card prompt
- Screenshot of the blocked keywords configuration
- ACL file 

---

## 8. Assessment Rubric

| Criterion | What is Assessed |
|---|---|
| Create & Customise Amazon Q Application | Q App built with correct input/output cards; advanced components added and tested |
| Upload Static PDF & Connect Amazon S3 | PDF catalog uploaded; S3 bucket created, connected, synced, and daily sync configured |
| Secure the Application | ACL applied to restrict Medicine content; keyword blocking configured and verified |
| Publish & Share the Application | App shared with all users; labels applied; marked as Verified Q App |

---






