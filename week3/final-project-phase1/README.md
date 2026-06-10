# Final Project Phase 1 - Recruit Management System

## Project Overview
The **Recruit Management System (RMS)** is a Salesforce-based enterprise application designed to streamline and automate the end-to-end hiring process. From job requisition and candidate sourcing to interview scheduling and final offer management, this system centralizes data to help HR teams make faster, data-driven hiring decisions.

The project demonstrates the use of Salesforce CRM concepts, custom objects, complex relationships, automation, Apex programming, Lightning Web Components (LWC), and AI-driven recruitment insights.

---

## System Architecture
### High-Level Architecture Diagram
```text
+-------------------+
|  Candidate Portal |
+-------------------+
          |
          v
+-------------------+
|      LWC UI       |
+-------------------+
          |
          v
+-------------------+
| Validation Rules  |
+-------------------+
          |
          v
+-------------------+
| Flow Automation   |
+-------------------+
          |
          v
+-------------------+
|   Apex Classes    |
+-------------------+
          |
          v
+-------------------+
| Salesforce Objects|
+-------------------+
          |
          v
+-------------------+
| Notifications &   |
| Approval Process  |
+-------------------+
          |
          v
+-------------------+
| Reports & Dashboards |
+-------------------+
```
---

# Recruit Management System (Salesforce)

A comprehensive recruitment and talent acquisition solution built on the Salesforce platform. This system manages the end-to-end hiring lifecycle—from job requisition and candidate sourcing to automated interviewing workflows and offer management.

## Objects & Relationships

### Custom Objects
| Object | Purpose |
| :--- | :--- |
| **Job Position** | Stores details of job openings (Title, Department, Budget). |
| **Candidate** | Personal profile and contact info of applicants. |
| **Job Application** | Junction object connecting a Candidate to a specific Job Position. |
| **Interview** | Records interview dates, times, and feedback notes. |
| **Offer Letter** | Tracks the terms of employment offered to the candidate. |

### Relationship Types
*   **Master-Detail Relationships:**
    *   `Job Application` → `Job Position`: Ensures applications are deleted if a position is removed.
    *   `Job Application` → `Candidate`: Links the application history directly to the person.
    *   `Interview` → `Job Application`: Ties feedback to the specific recruitment instance.
*   **Lookup Relationships:**
    *   `Job Position` → `Department`: Organizes positions by internal business units.
    *   `Offer Letter` → `Hiring Manager`: Identifies the approver for the salary package.

## Validation rules 

To maintain data integrity, the following **Validation Rules** are implemented:
*   **Valid Email Format:** Ensures Candidate emails follow standard syntax.
*   **Salary Floor Check:** Prevents Offer Letters from being created with a salary below the Job Position's minimum threshold.
*   **Interview Timeline:** Prevents scheduling interviews for past dates/times.
*   **Duplicate Application:** Prevents a candidate from applying for the same Job Position ID more than once within a 6-month period.

## Flow explanations 

*   **Application Acknowledgment Flow:** 
    *   *Trigger:* New Job Application record.
    *   *Action:* Sends a confirmation email to the candidate and creates a recruiter task for resume review.
*   **Interview Scheduling Flow:** 
    *   *Trigger:* Interview status set to "Scheduled".
    *   *Action:* Updates candidate status and generates a calendar invite for the interviewer.
*   **Position Auto-Close Flow:** 
    *   *Trigger:* Offer status updated to "Accepted".
    *   *Action:* Changes Job Position status to "Closed - Filled" and notifies all other active applicants.

## Apex Logic

*   **Candidate Score Calculator:** A trigger that calculates a "Suitability Score" based on technical assessment ratings and years of experience.
*   **Bulk Application Handler:** A Batch Apex class designed to process thousands of applications from external job boards while staying within governor limits.
*   **Offer PDF Generator:** Custom logic that compiles data from Job Position and Candidate records to generate a standardized employment contract.

## LWC screens 

*   **Recruiter Command Center:** A dashboard for "Applications Pending Review" and "Today's Interview Schedule."
*   **Candidate Application Form:** A modern, multi-step public-facing form for CV submission.
*   **Interview Feedback Panel:** A mobile-friendly interface for hiring managers to submit ratings and comments.
*   **Hiring Funnel Visualizer:** A chart tracking candidate conversion rates from Screening to Offered.

## Workflow explanation 

1.  **Job Creation:** Hiring Manager creates a Job Position.
2.  **Approval:** Position undergoes a **Budget Approval Process** (Manager → Dept Head → Finance).
3.  **Sourcing:** Candidates apply through the LWC Application Form.
4.  **Validation:** System ensures resumes and contact details are present and valid.
5.  **Screening:** Recruiter moves candidates to the Interview stage via Flow.
6.  **Evaluation:** Interviewers submit feedback; Apex logic calculates the suitability score.
7.  **Offer:** Recruiter generates an Offer Letter for **Executive Approval** (Hiring Manager → HR Director).
8.  **Closure:** Upon acceptance, the system closes the position and updates the dashboard.

##  Scaling considerations

*   **Volume:** Built to handle over 200,000 candidate records.
*   **Optimization:** Database indexing on `Candidate Email` and `Job ID` for high-speed searching.
*   **Concurrency:** Asynchronous Apex used for large-scale processing to maintain UI responsiveness.
*   **Storage:** Integration with Salesforce Files for resumes, with a 2-year archival strategy to external storage.

## 🤖 AI Enhancement Ideas

*   **Einstein Resume Ranking:** Automated keyword matching between resumes and Job Descriptions.
*   **Predictive Churn Analysis:** Predict the likelihood of a candidate declining an offer.
*   **Chatbot Integration:** AI-driven bot to answer candidate FAQs regarding application status.

## 📝 Reflection

This project highlights the synergy between data integrity and user experience. 
*   **Data Modeling:** Used junction objects to handle complex M-to-M relationships.
*   **Automation Strategy:** Utilized Flows for maintainability and Apex for high-performance logic.
*   **Governance:** Integrated strict approval processes to ensure fiscal and organizational alignment.


