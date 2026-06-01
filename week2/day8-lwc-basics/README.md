# LWC Basics - Event Management System

## 1. What is LWC?
**Lightning Web Components (LWC)** is a modern Salesforce UI framework used to build fast, reusable, and component-based web applications for managing events and attendee experiences.

LWC is built using:
*   **HTML:** For defining the structure of the event pages.
*   **JavaScript:** For managing event logic and user interactions.
*   **CSS:** For styling the dashboard and registration forms.

It follows modern web standards, helping developers create high-performance interfaces that handle real-time event data natively inside Salesforce.

## 2. Why Salesforce Uses LWC
Salesforce uses LWC for the Event Management System to ensure:
*   **Faster Performance:** Provides a smooth experience for users browsing high-traffic event schedules.
*   **Reusable Components:** Use the same "Ticket Card" or "Speaker Bio" component across multiple event pages.
*   **Better Scalability:** Easily handles thousands of attendee registrations and real-time updates.
*   **Modern UI Development:** Allows for the creation of sleek, mobile-responsive event dashboards.
*   **Easier Maintenance:** Standardized code makes it simple to update event rules or pricing logic.

## 3. UI Screens in Event Management System

### 1. Event Registration Screen
*   **Purpose:** Allows guests to register for specific events and choose ticket types.
*   **Features:** Guest name input, Ticket type selection (VIP/General), and "Register Now" button.

### 2. Event Dashboard
*   **Purpose:** Provides a high-level overview of all upcoming events.
*   **Features:** Event list, dates, venue locations, and total tickets sold vs. remaining.

### 3. Attendee Check-in Screen
*   **Purpose:** Used by staff at the venue to check in guests.
*   **Features:** QR code scanner interface, check-in status toggle, and VIP status indicators.

### 4. Speaker & Vendor Panel
*   **Purpose:** Allows organizers to manage performers, speakers, and third-party vendors.
*   **Features:** Speaker profiles, session timings, and vendor contact management.

### 5. Real-time Notification Panel
*   **Purpose:** Displays urgent updates during a live event.
*   **Features:** Schedule change alerts, venue move notifications, and emergency announcements.

## 4. Component Breakdown
**Chosen Screen:** Event Detail Dashboard

| Component Name | Purpose |
| :--- | :--- |
| **Header Component** | Displays the event logo, navigation links, and user login status. |
| **Event Info Component** | Shows specific details like Event Name, Date, Time, and Venue Map. |
| **Ticket Status Component** | Displays a progress bar of tickets sold and remaining capacity. |
| **Speaker Component** | A reusable card showing the photo, name, and bio of event speakers. |
| **Alert Component** | A pop-up or banner used for reminders (e.g., "Event starting in 10 mins"). |

### Why Reusable Components Are Important
*   **Reduce Duplicate Code:** A "Ticket Summary" component can be used on both the Admin dashboard and the Attendee receipt page.
*   **Improve Maintainability:** Update the "Venue Layout" component once, and it reflects across all event pages.
*   **Increase Development Speed:** Quickly assemble new events by dragging and dropping existing UI components.
*   **Consistent UI Design:** Ensures the branding and buttons look the same for every event in the system.

## 5. Frontend vs Backend Logic

| Functionality | Frontend (LWC/UI) | Backend (Apex) |
| :--- | :---: | :---: |
| Button Clicks (Register/Check-in) | ✅ Yes | ❌ No |
| Capturing Attendee Details | ✅ Yes | ❌ No |
| Displaying Success/Error Toasts | ✅ Yes | ❌ No |
| Basic Field Validation | ✅ Yes | ⚠️ Partial |
| Ticket Price Calculation | ❌ No | ✅ Yes |
| Updating Registration Records | ❌ No | ✅ Yes |
| Processing Payments | ❌ No | ✅ Yes |
| Sending Confirmation Emails | ❌ No | ✅ Yes |
| Complex RSVP Business Logic | ❌ No | ✅ Yes |

### Responsibilities:
*   **Frontend (LWC):** Focuses on the user journey—handling clicks, showing modals, and making the event registration process intuitive.
*   **Backend (Apex):** Focuses on the data—calculating taxes on tickets, ensuring the database isn't overbooked, and securing attendee information.

## 6. Reflection
**Why Modern Enterprise Systems Use Component-Based UI Architecture**

Modern enterprise systems, such as an **Event Management System**, utilize component-based UI architecture because it mirrors the complexity of real-world operations. 

In an event context, requirements change rapidly—you might need to add a "Sponsor Section" or a "Virtual Link" button at the last minute. 
1.  **Scalability:** We can add new features for a "Mega-Conference" without breaking the logic for a "Small Webinar."
2.  **Faster Development:** By using a library of components (Buttons, Inputs, Cards), we can launch new event pages in hours instead of days.
3.  **Easier Testing:** We can test the "Payment Component" individually to ensure it works perfectly before adding it to the main site.
4.  **Consistency:** Whether a user is looking at a concert or a corporate seminar, the interface feels familiar and professional.

