# Day 14: Flow Governance - Event Management System

## 1. Approval Workflow Examples
Approval workflows make sure that important actions are checked by the right person before they happen.

*   **Speaker Approval:** When a new speaker is added, they are "Pending" until an Event Manager reviews their profile and clicks "Approve." Only then do they appear on the public website.
*   **Venue Budget Approval:** If an organizer books a venue that costs more than $5,000, the system automatically sends a request to the Finance Director. The booking is only confirmed once the Director says "Yes."

## 2. Branching Flow Logic
Branching logic means the system asks a question and takes a different path based on the answer.

*   **Ticket Type Branching:** 
    *   **If VIP:** The system sends a welcome email with a "Special Lounge Pass."
    *   **If General:** The system sends a standard "Thank You" email.
*   **Discount Branching:**
    *   **If Student:** The flow asks the user to upload their ID card.
    *   **If Corporate:** The flow asks for a company tax number.
 
## Complete WorkFlow

<img width="691" height="765" alt="image" src="https://github.com/user-attachments/assets/e439eb61-b2fb-4454-8753-7358dd214946" />


## 3. Governance Explanation
Governance is simply a set of rules to keep the system clean, safe, and easy to fix.

*   **Naming Rules:** We give every flow a clear name (like `Event_Ticket_Booking_Flow`) so everyone knows what it does.
*   **Documentation:** We add descriptions inside the flow to explain why we built it.
*   **Version Control:** We never delete old versions immediately. We keep them so we can go back if a new update has a mistake.
*   **One Flow Per Goal:** Instead of one giant, confusing flow, we build smaller, organized flows that are easier to manage.

## 4. Reflection

*   **Staying Organized**  
    Governance stops the system from becoming a "mess." By following simple rules, any new developer can look at our event system and understand how it works immediately.

*   **Making Smart Decisions**  
    Using branching logic allows our system to be "smart." It treats VIP guests and regular attendees differently without us having to do any manual work.

*   **Ensuring Quality**  
    Approval workflows act as a quality check. They ensure that no unverified speakers or overpriced venues are added to our events by mistake.

*   **Team Safety**  
    Good rules mean that if one person leaves the team, the project doesn't fail. The documentation and standard names act as a map for the next person to follow.
