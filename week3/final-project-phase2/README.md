# Final Project Phase 2 - Enterprise Architecture and System Design
## Project Overview: Recruit Management System

The **Recruit Management System** is a Salesforce-based enterprise application designed to streamline the talent acquisition lifecycle. It manages everything from internal job requisitions and candidate sourcing to automated interviewing schedules, multi-level approvals, and final offer generation.

The system leverages Salesforce CRM, Flow Builder, Apex, Lightning Web Components (LWC), and advanced security protocols to ensure a scalable, high-performance recruitment engine.

---

## Final Architecture

### Architecture Overview
```text
+----------------------+
|      Users           |
| Candidates / HR      |
| Hiring Managers      |
+----------+-----------+
           |
           v
+----------------------+
|      LWC UI          |
| Command Center &     |
| Application Forms    |
+----------+-----------+
           |
           v
+----------------------+
| Validation Rules     |
| (Data Integrity)     |
+----------+-----------+
           |
           v
+----------------------+
| Salesforce Flows     |
| Automation Layer     |
+----------+-----------+
           |
           v
+----------------------+
| Apex Classes         |
| (Complex Scoring &   |
| Batch Processing)    |
+----------+-----------+
           |
           v
+----------------------+
| Salesforce Objects   |
| Data Layer           |
+----------+-----------+
           |
           v
+----------------------+
| Notifications        |
| Approvals            |
| Reports & Dashboards |
+----------------------+
```
## Data Model & Relationships

### Core Objects
- **Job Position**: Stores job details, department, and budget.
- **Candidate**: Stores personal profiles, contact info, and CVs.
- **Job Application (Junction)**: Links Candidates to Positions; tracks application status.
- **Interview**: Records schedules, interviewer notes, and technical ratings.
- **Offer Letter**: Tracks salary terms and contract status.

### Entity Relationships
| Object A | Object B | Relationship Type |
| :--- | :--- | :--- |
| Job Position | Job Application | Master-Detail |
| Candidate | Job Application | Master-Detail |
| Job Application | Interview | Master-Detail |
| Job Position | Department | Lookup |
| Offer Letter | Hiring Manager | Lookup |

---

## Hiring Lifecycle Workflow

1. **Candidate Submission**: Applicants use a custom **LWC Application Form**.
2. **Validation**: System checks email syntax and executes a **6-month duplicate check** for the same role.
3. **Flow Automation**: 
    - Creates records.
    - Sends automated confirmation emails.
    - Assigns review tasks to Recruiters.
4. **Apex Processing**: A custom **Suitability Scorer** calculates a candidate's score based on interview ratings and experience.
5. **Database Updates**: Candidate status updates to "In Progress" and the Job Position’s "Applicant Count" increments.
6. **Notification & Approval**: If selected, the system triggers the **Offer Approval Process**.
7. **Analytics**: The **Recruiter Command Center** dashboard refreshes in real-time.

---

## Approval Workflows

### 1. Job Requisition Approval
*   **Path**: Hiring Manager → Dept Head → Finance.
*   **Purpose**: Validates budget availability before a position is posted.

### 2. Salary Offer Approval
*   **Path**: Recruiter → Hiring Manager → HR Director.
*   **Purpose**: Ensures salary equity and prevents over-budget packages.

---

## Reporting & Dashboards

*   **Recruitment Funnel**: Tracks conversion rates from "Applied" to "Hired" to identify drop-off points.
*   **Time-to-Hire**: Measures the average speed of the hiring process for optimization.
*   **Interviewer Productivity**: Monitors feedback turnaround times and interview volume per manager.
*   **Diversity & Sourcing**: Analyzes lead sources (LinkedIn, Referrals) to optimize marketing spend.

---

## Failure Handling & Scalability

### Error Handling
| Scenario | Solution |
| :--- | :--- |
| **Notification Failure** | Notification logs and automated retry logic via Flow. |
| **Duplicate Profiles** | Matching/Duplicate Rules on Name/Phone with UI alerts. |
| **Approval Bottleneck** | Escalation rules redirecting to Directors after 48 hours. |
| **Governor Limits** | **Asynchronous Batch Apex** for processing high-volume (50k+) resumes. |

### Scalability Strategies
*   **Indexing**: Custom indexing on `Email` and `Job ID` for high-speed lookups.
*   **Archiving**: Offloading unsuccessful candidate resumes to **AWS S3** after 2 years.
*   **Selective Queries**: Ensuring Apex code uses indexed fields in `WHERE` clauses to prevent full table scans.

---

## Key Learnings & Reflection

This architecture highlights that high-stakes business processes require a **"Safety-First"** design:

1.  **Data Integrity**: Validation rules are the first line of defense against a cluttered data layer.
2.  **Scalable Automation**: While Flows are ideal for UI logic, **Batch Apex** is non-negotiable for high-volume data imports.
3.  **Governance**: Approval processes are critical for financial control and legal compliance.
4.  **UX Design**: Tailoring interfaces (Mobile for Managers, Dashboards for Recruiters) is essential for system adoption.

---

# TrailHead Profile

<img width="1919" height="1078" alt="Screenshot 2026-06-11 133141" src="https://github.com/user-attachments/assets/33ca7c3e-9162-4966-a2c3-036bebb13011" />

<img width="1919" height="1075" alt="Screenshot 2026-06-11 133243" src="https://github.com/user-attachments/assets/063ba0a5-40ce-48e1-856a-c48b897c416f" />


