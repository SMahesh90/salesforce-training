# Day 9: Component Communication & Dashboard Architecture - Event Management System

## 1. Dashboard Design
The Event Management System utilizes three specialized dashboards to cater to different user roles, ensuring a streamlined experience for attendees, staff, and administrators.

### Attendee Dashboard
*   **Components:** 
    *   `headerNav`: Branding and navigation links.
    *   `myTicketList`: Displays all tickets purchased by the user.
    *   `sessionScheduler`: Shows personalized event timelines.
    *   `eventMap`: Interactive venue locations.
    *   `realTimeAlerts`: Instant notifications for schedule changes.
*   **Purpose:** Provides attendees with a central hub to manage their event journey and access digital entry passes.

### Organizer Dashboard
*   **Components:** 
    *   `salesOverview`: Real-time charts for ticket sales and revenue.
    *   `guestManager`: List of registrants with filtering capabilities.
    *   `checkInTerminal`: Tool for scanning and marking attendee arrival.
    *   `speakerPortal`: Interface to update session details and bios.
*   **Purpose:** Enables event planners to manage logistics, monitor sales, and handle on-site operations.

### Admin Dashboard
*   **Components:** 
    *   `capacityAnalytics`: Tracks venue occupancy versus safe limits.
    *   `permissionControl`: Manages user roles for staff and organizers.
    *   `financeAudit`: Detailed reports on payouts and transaction history.
    *   `broadcastCenter`: Sends push notifications across the entire platform.
*   **Purpose:** Offers high-level oversight for system health, financial auditing, and global platform management.

## 2. Component Communication
In this system, components interact using modern LWC communication patterns to ensure data remains synchronized across the dashboard.

### Communication Patterns Used:
1.  **Parent to Child (`@api`):** The `Organizer Dashboard` (Parent) passes specific Event IDs to the `Sales Overview` (Child) so it knows which data to fetch.
2.  **Child to Parent (Custom Events):** When a staff member clicks "Check-In" in the `CheckInTerminal` component, it dispatches a `checkedin` event. The Parent dashboard listens for this event to refresh the `Guest Manager` list.
3.  **Unrelated Component Communication (LMS):** We use **Lightning Message Service (LMS)** to communicate between the `Session Scheduler` and the `RealTimeAlerts`. If a session is delayed, the scheduler publishes a message that the alert component receives, even if they aren't in the same hierarchy.

## 3. Data Flow Explanation
**Selected Process: Ticket Booking & Registration**

1.  **Step 1 – UI Layer (LWC):** The user selects a ticket tier (e.g., VIP) and enters guest information into an LWC form.
2.  **Step 2 – Validation Layer:** The component performs client-side checks (e.g., ensuring the email format is correct and required fields are not empty).
3.  **Step 3 – Apex Logic:** The LWC calls an Apex method to perform a "Server-side Check" to ensure ticket inventory is still available before processing.
4.  **Step 4 – Database Storage:** Upon validation, a new **Registration Record** is inserted into the Salesforce Database.
5.  **Step 5 – Flow Automation:** A background Salesforce Flow triggers to generate a unique QR code and send an automated confirmation email to the attendee.
6.  **Step 6 – UI Update:** The LWC receives a success callback, clears the form, and shows a "Booking Successful" Toast message to the user.

## Complete Data Flow

   <img width="827" height="657" alt="image" src="https://github.com/user-attachments/assets/5aa48245-92ad-492b-8cb1-57a36d1aab35" />


## 4. Aura vs LWC

| Feature | Aura Components | Lightning Web Components (LWC) |
| :--- | :--- | :--- |
| **Architecture** | Proprietary Metadata framework | Modern Web Standards (ES6+) |
| **Performance** | Slower (requires more browser processing) | Fast (runs natively in the browser) |
| **Logic** | Uses `$A.get()` and unique Aura syntax | Standard JavaScript (Import/Export) |
| **Security** | Locker Service | Lightning Security / LWS (Enhanced) |
| **Maintainability** | Higher complexity; harder to debug | Modular; easier to maintain and test |

### Why Salesforce Moved to LWC
Salesforce transitioned to LWC to align with the modern web stack. By building on standard Web Components, LWC offers significantly better performance, lower memory usage, and allows developers to use skills that are transferable across the entire web development industry.

## 5. Reflection
**Why Enterprise Applications Need Modular Architecture**

In an **Event Management System**, requirements are constantly shifting. One event might require a "Social Media Feed" component, while another might need a "Live Polling" feature. 

Modular architecture is essential for several reasons:
*   **Reusability:** A `TicketCard` component can be used for concerts, conferences, or workshops without changing the underlying code.
*   **Scalability:** As the system grows from managing 100 attendees to 100,000, we can optimize individual components (like the search bar) without needing to overhaul the entire application.
*   **Parallel Development:** Different developers can work on the "Payment Gateway" and the "Map Interface" simultaneously because the components are isolated.
*   **Simplified Maintenance:** If there is an issue with the "Check-in Scanner," the developer knows exactly which component to fix, reducing the risk of breaking the "Sales Reports."

