# Day 15: Data Management (Event Management System)

This module focuses on the integrity, migration, and maintenance of data within the Event Ticket Booking application. High-quality code (LWC/Apex) is ineffective if the underlying data is compromised.

## ⚠️ Data Quality Problems

In an Event Management context, poor data quality often manifests as:

*   **Incomplete Attendee Profiles:** Missing mandatory fields like Email or Phone, preventing ticket delivery via Flow.
*   **Formatting Inconsistency:** Phone numbers entered as `(555) 123-4567` vs `5551234567`, making SMS notifications fail.
*   **Invalid Reference Data:** Event records linked to non-existent venues or inactive organizers.
*   **Stale Data:** Registrations that remain in "Pending" status indefinitely due to failed payment triggers, skewing capacity reports.

## 🔄 Migration Discussion

When migrating legacy event data (e.g., from an old Excel tracker or SQL database) into Salesforce:

*   **Mapping Strategy:** Legacy `Old_Ticket_ID` must be mapped to a custom field marked as **External ID** in Salesforce to maintain relationships.
*   **Load Order:** Data must be imported in a specific sequence to maintain referential integrity:
    1.  **Accounts/Contacts:** (Organizers & Attendees)
    2.  **Events:** (The parent records)
    3.  **Registrations:** (Linking Attendees to Events)
*   **Data Scrubbing:** Before the Insert operation, we must use tools like Excel or OpenRefine to remove "test" records and standardize date formats to ISO-8601.

## 🛡️ Duplicate Prevention Ideas

To ensure a single attendee doesn't accidentally register five times for the same session:

*   **Salesforce Matching & Duplicate Rules:**
    *   **Criteria:** Match Email AND Event_ID.
    *   **Action:** Block the creation of a second registration record if a match exists.
*   **Apex Pre-Processing:** Within the Registration LWC, the Apex controller should perform a "Pre-Check" SOQL query:
    ```sql
    SELECT Id FROM Registration__c 
    WHERE Attendee_Email__c = :email 
    AND Event__c = :eventId
    ```
*   **Unique Keys:** Use a formula field or a text field (populated by Flow) that concatenates `Email + EventID` and set it to **Unique (Case-Insensitive)** at the database level.

## 📉 Enterprise Risks of Bad Data

For a large-scale event organization, bad data leads to:

*   **Financial Loss:** Inaccurate dynamic pricing logic (Apex) might apply discounts to users who don't qualify, or over-calculate tax.
*   **Operational Chaos:** If "Capacity Checks" fail due to bad data, an event might be overbooked, leading to venue safety violations.
*   **Reputational Damage:** Sending a QR code for "Event A" to an attendee who registered for "Event B" results in a poor customer experience and brand distrust.
*   **Compliance Risks:** Failure to accurately track "Opt-in" status for marketing emails can lead to GDPR or CAN-SPAM violations.

## 🧠 Reflection

Data Management is not a one-time task but a continuous cycle. In building the Event Ticket Booking system, I realized that **Validation Rules** and **Apex Logic** are the "Gatekeepers," but the **Database Schema** is the "Foundation."

Technical features like QR Code generation (Flow) and Dynamic Pricing (Apex) are entirely dependent on the data being clean and structured. Moving forward, I will prioritize "Data-First" thinking—validating the shape of the data before writing the logic to process it.

---
**Next Steps:** Implement a Custom Metadata Type to manage event-specific validation constants.
