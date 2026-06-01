# Day 10: Mini-Project – Event Management System

## 1. System Overview
The **Event Management System** is a Salesforce-based platform designed to manage the full lifecycle of corporate events. It streamlines venue booking, speaker assignments, and attendee registrations, providing a centralized hub for organizers to track real-time event performance and guest engagement.

## 2. CRM Concepts
*   **Lead & Contact Management:** Captures prospects as Leads and converts them to Contacts upon registration.
*   **Campaign Tracking:** Links events to Salesforce Campaigns to measure marketing effectiveness.
*   **Account Management:** Manages relationships with Venues, Catering Vendors, and Corporate Sponsors.
*   **Activity Management:** Tracks tasks and meetings with speakers to ensure event readiness.

## 3. Data Model
| Object Name | Type | Relationship |
| :--- | :--- | :--- |
| **Event__c** | Custom | Master object for all event details. |
| **Venue__c** | Custom | Lookup to Event; stores location and capacity. |
| **Attendee__c** | Custom | Junction object linking Contacts to Events. |
| **Speaker__c** | Custom | Lookup to Event sessions; stores bios and expertise. |
| **Registration__c**| Custom | Master-Detail to Event; tracks tickets and payments. |

## 4. Validation Rules
*   **End Date Check:** Prevents saving an event if the End Date is earlier than the Start Date.
*   **Sold Out Guard:** Blocks new registrations if the `Tickets_Sold__c` equals `Venue_Capacity__c`.
*   **Email Requirement:** Ensures all attendees have a valid email for ticket delivery.

## 5. Flows (Automation)
*   **Confirmation Flow:** Automatically emails a digital ticket and QR code upon successful payment.
*   **Capacity Alert:** Notifies organizers via email when an event reaches 90% capacity.
*   **Guest Check-in:** A Screen Flow that guides on-site staff through the attendee check-in process.

## 6. Apex Logic
*   **Speaker Conflict Trigger:** Prevents a speaker from being assigned to multiple sessions at the same time.
*   **Dynamic Pricing:** Calculates ticket costs based on "Early Bird" or "Last Minute" timeframes.
*   **Revenue Batch:** A nightly process that aggregates total revenue from all registrations.

## 7. UI Screens
*   **Public Registration Form:** Multi-step LWC for guest sign-ups.
*   **Organizer Dashboard:** Visual charts showing ticket sales, revenue, and attendance.
*   **Check-in Terminal:** A simplified LWC for staff to scan and verify attendees quickly.

## 8. Complete Data Flow

Event Ticket Booking
          ↓
LWC Screen (Registration Form)
          ↓
Validation Rules (Checks Capacity & Dates) 
          ↓
Apex Logic (Calculates Dynamic Pricing/Discounts)
          ↓
Database Storage (Saves Registration & Attendee Records)
          ↓
Flow Automation (Generates QRCode & Ticket ID)
          ↓
Notifications (Sends Confirmation Email)

## 9. Reflection

This modular architecture ensures high data integrity by combining automated validations with custom Apex logic. By utilizing LWC for the interface and Flows for automation, the system remains scalable and provides a professional, seamless experience for both organizers and attendees.
