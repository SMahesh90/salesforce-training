# Event Management System – Salesforce & Apex Concepts

## 1. What is Apex?
Apex is a strongly typed, object-oriented programming language developed by Salesforce. It allows developers to execute flow and transaction control statements on the Salesforce platform API. It acts as the "brain" for complex operations that standard configuration cannot handle.

**Apex is mainly used for:**
*   **Custom Automation:** Complex ticket booking workflows.
*   **Complex Calculations:** Dynamic tax, multi-currency handling, and tiered discounts.
*   **External Integrations:** Connecting to payment gateways (Stripe) or QR code generators.
*   **Advanced Validations:** Checking speaker availability across multiple time zones.
*   **Trigger-based Operations:** Executing logic automatically when a registration is created.

---

## 2. Comparisons: Automation & Customization

### Flow vs. Apex
| Feature | Flow | Apex |
| :--- | :--- | :--- |
| **Type** | No-code/low-code tool | Programming language (Code) |
| **Interface** | Visual drag-and-drop | Text-based coding |
| **Complexity** | Best for simple to moderate logic | Best for high-complexity logic |
| **Maintenance** | Easier for Admins | Requires Developer expertise |
| **Performance** | Good for standard tasks | Superior for large data volumes |

### Configuration vs. Coding
| Feature | Configuration (Clicks) | Coding (Apex/LWC) |
| :--- | :--- | :--- |
| **Method** | Clicks and settings | Writing logic/scripts |
| **Speed** | Very fast for standard setup | Slower; requires testing/deployment |
| **Flexibility** | Limited by Salesforce UI | Unlimited customization |
| **Examples** | Validation Rules, Page Layouts | Apex Triggers, API Callouts |

---

## 3. Real Examples Where Apex Is Needed

### 1. Dynamic Ticket Pricing Logic
*   **Example:** Automatically calculating ticket prices based on "Early Bird" dates, group size (e.g., 10+ people get 15% off), and membership status.
*   **Why Apex?** This involves cross-referencing multiple criteria and performing real-time math that exceeds the capabilities of standard formula fields.

### 2. External QR Code Generation
*   **Example:** Upon successful payment, Salesforce calls an external API to generate a unique QR code for the attendee's badge and saves the image link back to the record.
*   **Why Apex?** Securely handling HTTP Callouts and parsing JSON data from external web services requires Apex.

### 3. Multi-Resource Conflict Checker
*   **Example:** Ensuring that a specific Room (Venue) and a specific Speaker are not booked for two different sessions at the same time.
*   **Why Apex?** This requires querying multiple objects (Sessions, Venues, and Speakers) and comparing time ranges in a single transaction.

---

## 4. Integrated System Design

### CRM
The Event Management System (EMS) leverages Salesforce CRM to manage:
*   Attendee relationships and communication history.
*   Sponsor tracking and contract management.
*   Lead generation for future events.

### Objects
*   **Event:** Stores name, date, venue, and total capacity.
*   **Attendee:** Stores personal details (Name, Email, Ticket Type).
*   **Speaker:** Stores bio and expertise.
*   **Session:** Individual workshops or talks within an event.
*   **Registration:** A junction object connecting Attendees to Events.

### Relationships
*   **1 Event → Many Sessions** (Master-Detail)
*   **1 Venue → Many Events** (Lookup)
*   **Event ↔ Attendee** (Many-to-Many via Registration object)
*   **Session ↔ Speaker** (Many-to-Many via Session-Speaker junction)

### Validation
*   **No Past Dates:** Event Start Date cannot be in the past.
*   **Capacity Guard:** Prevent Registration if "Seats Available" is 0.
*   **Purpose:** Ensures data integrity and prevents overbooking or scheduling errors.

### Flow
*   **Confirmation Email:** Sent automatically after a registration record is created.
*   **Status Update:** Updates Event status to "Sold Out" when capacity hits 100%.
*   **Reminder:** Notifications sent to Speakers 24 hours before their session starts.

### Apex Usage
*   **Payment Integration:** Processing credit card data via Stripe API.
*   **Bulk Check-in:** A custom interface to check in hundreds of attendees per minute.
*   **Complex Tax Engine:** Calculating VAT/Sales tax based on the attendee's country of origin.

---

## 5. Pseudocode Examples

### Example 1 – Capacity Check

    IF (Registration_Count >= Max_Capacity) {
       THEN Display Error: "Event is at full capacity."
    } ELSE {
       Allow Registration and Update Available_Seats.
    }

---

### Example 2 – Early Bird Discount

    IF (Current_Date <= Early_Bird_Deadline) {
       Apply 20% Discount to Ticket_Price.
    } ELSE {
       Apply Standard_Price.
    }

---

### Example 3 – Speaker Conflict

    IF (Speaker_Schedule.contains(New_Session_Time)) {
       THEN Block Creation: "Speaker is already assigned to another session."
    } ELSE {
       Assign Speaker to Session.
    }

---

## 6.Reflection – Why Enterprise Systems Eventually Need Programming

As an Event Management System scales from a local meetup to a global conference, it inevitably outgrows "out-of-the-box" configuration.

### Programming becomes essential for:

**Complexity:** Managing multi-layered pricing and global tax compliance.
**Scalability:** Handling thousands of concurrent registrations without data errors.
**Connectivity:** Seamlessly integrating with external marketing, payment, and logistics tools via APIs.
**Customization:** Delivering a unique, branded user experience that standard layouts cannot provide.
