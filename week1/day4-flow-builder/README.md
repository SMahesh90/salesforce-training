# Salesforce Flow Builder and Automation: Event Management System

## 1. What is Flow Builder?
Flow Builder is a visual automation tool within Salesforce that allows administrators and developers to automate complex business processes without writing code. It uses a drag-and-drop interface to build logic, update database records, interact with users, and send external communications.

---

## 2. Types of Flows

### Screen Flow
A Screen Flow is a guided process that requires user interaction. It displays screens to collect data from the user or provide them with specific information.
*   **Key Features:** Includes UI elements like text boxes, picklists, and buttons.
*   **Example:** A "Ticket Booking Wizard" where a customer selects their event date, seat number, and meal preference.

### Record-Triggered Flow
This flow runs automatically in the background when a record is created, updated, or deleted. There is no user interface; it simply reacts to data changes.
*   **Key Features:** Operates silently; triggered by database changes.
*   **Example:** Automatically updating an "Event Full" checkbox on an Event record when the number of registered guests reaches the maximum capacity.

---

## 3. Automation Ideas (Event Management System)

1.  **Instant Ticket Confirmation:** Automatically email a PDF ticket and a QR code to a guest the moment their registration payment status is marked as "Paid."
2.  **VIP Tier Graduation:** If a guest’s total spend across all historical events exceeds $1,000, automatically update their "Guest Category" to "VIP" and notify the account manager.
3.  **Low Availability Alert:** Send a notification to the Marketing team when ticket sales reach 90% of capacity so they can run a "Last Chance" campaign.
4.  **Post-Event Survey:** Schedule a flow to send a feedback survey link to all attendees exactly 24 hours after the event "End Time" has passed.
5.  **Vendor Task Creation:** Automatically create a set of tasks for the logistics team (e.g., "Confirm Catering," "Set Up AV") as soon as a new Event record is created.

---

## 4. Flow Diagram Logic
**Selected Automation:** Auto-Assign "Early Bird" Discount

**Logic Steps for Flowchart:**
*   **Start Node:** Record-Triggered Flow (Object: Registration | Condition: Record is Created).
*   **Decision Diamond:** Is the current date > 30 days before Event Start Date?
    *   **Path A (Yes):** Use an Assignment element to apply a 20% discount to the registration fee.
    *   **Path B (No):** Proceed with the Standard Price.
*   **Update Element:** Save the final price to the Registration record.
*   **End Node:** Flow execution completes.

---

## 5. Manual vs. Automated Process
**Process focus:** Managing the Event Waitlist

| Feature | Manual Process | Automated Process (Salesforce) |
| :--- | :--- | :--- |
| **Speed** | Slow; staff must check lists and call guests. | Instant; system detects a vacancy and acts. |
| **Accuracy** | High risk of human error or skipping people. | Precision logic follows the exact order of signup. |
| **Communication** | Messages are sent one by one. | Bulk or individual emails sent automatically. |
| **Effort** | High; requires constant monitoring. | Low; "Set it and forget it" logic. |

**Problems in Manual Process:** 
In a manual system, if a guest cancels at 10:00 PM, the seat stays empty until a staff member checks their email the next morning. This leads to lost revenue and a poor experience for waitlisted guests.

---

## 6. Reflection – Why Automation Matters in Enterprise Systems
Automation is the backbone of modern enterprise systems because it ensures scalability and consistency. As an event management business grows from 50 guests to 5,000, manual processes become a bottleneck that leads to burnout and errors. 

Automation allows the system to handle the "heavy lifting" of data entry and status updates. This frees up human employees to focus on high-value tasks, such as networking with sponsors or improving the onsite event experience. Ultimately, it drives efficiency, reduces operational costs, and provides a faster, more professional service to the end customer.
