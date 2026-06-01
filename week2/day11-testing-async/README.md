# Day 11: Testing & Asynchronous Processing - Event Management System

## 1. Why Testing Matters
In an **Event Management System**, testing is essential to ensure a high-quality user experience and financial accuracy.
*   **Accuracy in Transactions:** Ensures that ticket prices and discounts are calculated correctly to avoid revenue loss.
*   **System Stability:** Prevents the application from crashing during high-traffic periods, such as when ticket sales first open.
*   **Data Integrity:** Guarantees that validation rules (like venue capacity) are enforced, preventing overbooking.
*   **User Trust:** Reliable check-in and registration processes build confidence for both attendees and event organizers.

## 2. What is Asynchronous Processing?
Asynchronous processing refers to tasks that run in the background without making the user wait for the process to finish. In Salesforce, this allows the system to handle long-running tasks (like generating a PDF or calling an external payment API) while keeping the user interface fast and responsive.

## 3. Important Test Cases
To maintain system reliability, we focus on these critical test scenarios:

| Test Case | Scenario | Expected Result |
| :--- | :--- | :--- |
| **Capacity Enforcement** | Attempting to register for a "Sold Out" event. | System blocks the registration and displays a "Sold Out" message. |
| **Discount Logic** | Applying an "EARLYBIRD" promo code. | The total price is reduced by the correct percentage. |
| **Speaker Conflict** | Assigning a speaker to two overlapping sessions. | The system throws an error and prevents the assignment. |
| **Check-in Update** | Toggling the "Checked-In" status on a guest record. | The Attendee record updates and the dashboard count increases. |
| **Bulk Registration** | Registering 200 attendees at once. | The system processes all records without hitting Governor Limits. |

## 4. Async Use Cases
We utilize asynchronous processing for the following tasks in the Event Management System:
*   **Queueable Apex:** Generating unique QR codes for tickets immediately after a successful booking.
*   **Batch Apex:** Automatically closing past events and archiving attendee data at the end of every month.
*   **Future Methods:** Making secure callouts to third-party payment gateways (e.g., Stripe) to verify ticket payments.
*   **Scheduled Apex:** Sending a "Daily Summary Report" to event organizers every morning.

## 5. Reliability Discussion
To ensure the system remains reliable under heavy loads, we implement:
*   **Governor Limit Management:** Asynchronous tasks have higher limits for CPU time and memory, allowing us to process larger sets of data.
*   **Error Handling:** Using `try-catch` blocks in Apex and "Fault Paths" in Flows to ensure that if one process fails, it doesn't crash the entire system.
*   **Bulkification:** Writing all code to handle multiple records simultaneously, ensuring performance remains stable during mass registrations.

## 6. Reflection
Testing and asynchronous processing are fundamental to building a professional-grade enterprise system. Testing provides the "safety net" that ensures business rules are never violated, while asynchronous processing provides the "engine" that keeps the system fast and scalable. Together, they allow the Event Management System to handle thousands of users while maintaining speed, security, and accuracy.
