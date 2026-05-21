# Event Management System: LWC Architecture Overview

---

### 1. What is LWC?
*   **Modern Web Standard:** Built on ES6+ and native Web Components, ensuring it runs efficiently in modern browsers.
*   **Lightweight Core:** It features a minimal "engine" layer, making it significantly faster than legacy frameworks like Aura.
*   **Reusable Logic:** Allows developers to build modular elements (like a "Register" button) that can be reused across different pages.
*   **Example:** In an Event App, LWC is used to build the interactive "Speaker Profile" cards and "Live Seat Map."

### 2. Why Salesforce Uses LWC
*   **Performance:** By leveraging the browser's native capabilities, components render and update faster, providing a smoother user experience.
*   **Standardization:** It uses standard HTML, CSS, and JavaScript, allowing developers to apply general web skills without learning proprietary languages.
*   **Enhanced Security:** Includes built-in security features like Lightning Locker and Lightning Web Security (LWS) to protect sensitive event data.
*   **Example:** Salesforce uses LWC so that an organizer viewing a dashboard of 5,000 attendees sees real-time updates without page lag.

### 3. Your UI Screens
*   **Event Explorer Dashboard:** The landing page where users browse all available conferences, concerts, and workshops.
*   **Attendee Registration Form:** A dynamic input screen where users enter details, select ticket tiers, and provide dietary preferences.
*   **Speaker Detail Side-Panel:** A contextual view that appears when a speaker is selected, showing their bio and scheduled sessions.
*   **Real-Time Schedule:** A list view that updates live as sessions start or finish during the event.

### 4. Component Breakdown
*   **`eventTile` (Child):** Displays a summary of a single event (Image, Title, Date). It dispatches a `tileclick` event when selected.
*   **`eventList` (Parent):** Iterates through data to render multiple `eventTile` components and manages the layout (grid vs. list).
*   **`eventDetail` (Detail View):** Receives an Event ID via a public property (`@api`) and displays the full description and speaker list.
*   **`eventApp` (Container):** The top-level component that acts as the "orchestrator," handling event communication between the List and the Detail view.

### 5. Frontend vs. Backend Logic
*   **Frontend (LWC/JavaScript):** Handles "Client-Side" logic such as UI animations, input validation (e.g., checking if an email is valid), and firing events.
*   **Backend (Apex/Salesforce):** Handles "Server-Side" logic such as querying the database for available tickets (SOQL) and saving new attendee records (DML).
*   **Data Bridge:** LWC uses the `@wire` service or imperative Apex calls to request data from the backend and bring it into the frontend UI.
*   **Example:** When a user clicks "Book Now," the **Frontend** shows a loading spinner while the **Backend** runs a script to deduct a ticket from the inventory.

### 6. Reflection
*   **The "Events Up, Properties Down" Pattern:** This architecture keeps the Event App organized. Children notify parents of actions (clicks), and parents pass data (event details) down to children.
*   **Modularity:** Because components are decoupled, we can change the `eventTile` design without breaking the `eventList` logic.
*   **Scalability:** This system is easy to grow; we can add a "Sponsor" component or a "Feedback" form by simply dropping new LWCs into the existing container.
*   **Efficiency:** Using standard JS and CSS makes debugging easier and ensures the app remains compatible with future web browser updates.
