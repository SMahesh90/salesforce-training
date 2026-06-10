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
