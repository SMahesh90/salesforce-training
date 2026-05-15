# SOQL and Apex Trigger Concepts – Event Management System

## 1. What is SOQL?
**SOQL** stands for **Salesforce Object Query Language**. It is used to retrieve specific data from Salesforce objects such as Events, Attendees, Speakers, and Venues.

**SOQL helps:**
*   **Search records:** Look up specific event details or dates.
*   **Filter data:** Find all attendees who purchased "VIP" tickets.
*   **Access related object information:** See which speakers are assigned to specific sessions.
*   **Generate reports and business logic:** Pull data to calculate total revenue per event.

**Example:** Retrieve all attendees registered for the specific Event.

---

## 2. What is an Apex Trigger?
An **Apex Trigger** is a piece of Apex code that runs automatically when data changes occur in Salesforce objects (DML operations).

**Triggers can execute:**
*   **Before/After inserting** records (e.g., registering a new attendee).
*   **Before/After updating** records (e.g., changing the status of a venue to 'Booked').
*   **Before/After deleting** records (e.g., canceling a session).

**Purpose:** Triggers automate complex actions, enforce data integrity, and handle business logic that cannot be done with standard configurations.

---

## 3. Key Differences

### Flow vs. Apex Trigger
| Feature | Flow | Apex Trigger |
| :--- | :--- | :--- |
| **Type** | No-code/low-code automation | Code-based automation |
| **Creation** | Visual drag-and-drop interface | Requires Apex programming (Java-like) |
| **Best For** | Simple to medium logic | High-performance, complex logic |
| **Flexibility** | Limited to available elements | Highly customizable and powerful |
| **Execution** | Slower for bulk operations | Highly efficient for large data sets |

### Before vs. After Trigger
| Feature | Before Trigger | After Trigger |
| :--- | :--- | :--- |
| **Timing** | Runs before data is saved to the database | Runs after data is saved to the database |
| **Primary Use** | Validation and updating fields on the same record | Notifications and updates to related records |
| **Efficiency** | Faster for modifying the record being processed | Essential when you need the Record ID (e.g., for linking) |
| **Example** | Set ticket price based on "Early Bird" date | Send a PDF Ticket via email after payment is confirmed |

---

## 4. Trigger Use Cases

1.  **Send Confirmation Email After Registration**
    *   **Trigger Event:** After attendee record creation.
    *   **Action:** Automatically send a welcome email with a QR code for entry.
2.  **Update Ticket Inventory After Booking**
    *   **Trigger Event:** After a ticket record is created.
    *   **Action:** Automatically subtract 1 from the "Available Tickets" field on the Event record.
3.  **Notify Organizer When Venue Reaches Capacity**
    *   **Trigger Event:** After available seats reach 0.
    *   **Action:** Send an alert to the Event Manager to stop ticket sales or move to a larger room.
4.  **Speaker Conflict Prevention**
    *   **Trigger Event:** Before a speaker is assigned to a session.
    *   **Action:** Check if the speaker is already scheduled for another session at the same time and block the save if a conflict exists.
5.  **Prevent Duplicate Registrations**
    *   **Trigger Event:** Before a registration record is inserted.
    *   **Action:** Check if the email address is already registered for that specific Event ID to prevent double bookings.

---

## 5. Query Examples (English Query Ideas)

*   **Find all attendees for "Music Festival 2025":** Show a list of everyone who signed up for the specific festival.
*   **Show all events held at "The Grand Ballroom":** Find every event scheduled at a specific venue location.
*   **Find events with a budget exceeding $10,000:** Filter for high-cost events that may require extra management.
*   **Find all speakers specialized in "Cybersecurity":** Search for experts available for a specific technical track.
*   **Find events with no available tickets:** Show all "Sold Out" events where the ticket count is 0.

---

## 6. Reflection – Why Enterprise Systems React Automatically to Data Changes

In an **Event Management System**, data is dynamic and high-volume. Automatic reactions to data changes are critical for maintaining a professional and reliable operation.

**Automatic processing helps:**
*   **Maintain Data Integrity:** Instantly updating ticket counts ensures you never oversell a venue, which protects the company's reputation.
*   **Enhance Customer Experience:** Attendees expect immediate confirmation. Automation provides instant feedback (emails/SMS) without manual staff intervention.
*   **Enforce Complex Business Rules:** Rules like "one speaker cannot be in two places at once" are impossible to track manually at scale; automation handles this instantly.
*   **Operational Efficiency:** By automating routine tasks like seat counting and notifications, staff can focus on the event experience rather than data entry.

**Event-driven behavior** allows enterprise systems to be proactive, ensuring accuracy and speed in a fast-paced business environment.
