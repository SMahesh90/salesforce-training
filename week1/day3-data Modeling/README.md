# Event Management System & Salesforce Concepts

## 1. Difference Between App, Object, Record, and Field

| Concept | Meaning | Example in Event Management System |
|--------|---------|------------------------------------|
| App | A collection of related objects, tabs, and features used for a specific purpose | Event Planner App |
| Object | A database table that stores related data | Event Object, Venue Object |
| Record | A single entry inside an object | "Annual Tech Conference 2025" (A specific event) |
| Field | A single piece of information inside a record | Event Date, Ticket Price, Capacity |

---

## 2. Standard vs. Custom Objects

| Standard Objects | Custom Objects |
|------------------|----------------|
| Pre-built objects provided by Salesforce | Objects created by users based on specific business needs |
| Already available in Salesforce | Created manually by the Admin |
| Examples: Account (Sponsoring Company), Contact (Attendee) | Examples: Event, Venue, Speaker, Registration |
| Cannot be deleted | Can be modified or deleted |
| Used for common CRM processes | Used for organization-specific requirements |

---

## 3. Event Data Model

### Objects

#### Event
Stores information about the specific event.

**Fields:**
- Event ID
- Event Name
- Event Date
- Total Capacity
- Tickets Sold
- Venue ID

#### Venue
Stores information about the location where events are held.

**Fields:**
- Venue ID
- Venue Name
- Address
- Maximum Capacity
- Rental Cost

#### Attendee (Contact)
Stores personal information of people attending the events.

**Fields:**
- Contact ID
- First Name
- Last Name
- Email
- Phone Number

#### Speaker
Stores details about individuals speaking at the events.

**Fields:**
- Speaker ID
- Speaker Name
- Bio
- Expertise
- Assigned Event

---

### Relationships

| Parent Object | Child Object | Relationship Type |
|--------------|-------------|------------------|
| Venue | Event | One-to-Many |
| Event | Speaker | One-to-Many |
| Event | Registration | One-to-Many |
| Attendee | Registration | One-to-Many |

---

### Data Model Diagram

```text
+----------------------+
|        Venue         |
+----------------------+
| Venue ID             |
| Venue Name           |
| Max Capacity         |
+----------------------+
           |
           | One-to-Many
           |
+----------------------+
|        Event         |
+----------------------+
| Event ID             |
| Event Name           |
| Total Capacity       |
| Tickets Sold         |
+----------------------+
     /       |       \
    /        |        \
   /         |         \
+---------+ +--------------+ +------------------+
| Speaker | | Registration | |    Attendee      |
+---------+ +--------------+ +------------------+
|SpeakerID| | Reg ID       | | Contact ID       |
| Name    | | Event ID     | | First Name       |
|Expertise| | Attendee ID  | | Last Name        |
+---------+ +--------------+ | Email            |
                             +------------------+

```

---

## 4. Formula Fields 

## Available Tickets

**Formula** = Total_Capacity__c - Tickets_Sold__c

**Explanation:** Automatically calculates how many tickets are left for an event. This prevents staff from selling more tickets than the venue can hold.

## Occupancy Percentage

**Formula** = (Tickets_Sold__c / Total_Capacity__c) * 100

**Explanation:** Shows what percentage of the event is booked. This helps the marketing team decide if they need to push more advertisements.

## Event Revenue

**Formula** = Tickets_Sold__c * Ticket_Price__c

**Explanation:** Automatically calculates total revenue from ticket sales without manual calculation.

---

**In Salesforce, __c indicates a custom field or custom object.**

**Why this exists:**

Salesforce needs a way to distinguish built-in (standard) components from user-created ones.

__c literally means custom.

---

## 5. Validation Rules

## Event Date Must Be Future

**Rule:**

Event_Date__c < TODAY()

**Explanation:** Prevents users from creating an event in the past.

## Cannot Exceed Capacity

**Rule:**

Tickets_Sold__c > Total_Capacity__c

**Explanation:** Prevents overbooking beyond venue capacity.

## Email Required for Registration

**Rule:**

ISBLANK(Email__c)

**Explanation:** Ensures every attendee provides an email address so tickets and updates can be sent.

---

## 6. Reflection – Why Structured Enterprise Data Matters

Structured enterprise data allows organizations to manage complex operations like event management efficiently and accurately.

## Benefits

**Track Logistics:** Instantly see which venue is booked for which event.

**Improve Accuracy:** Automated formulas keep ticket counts and revenue calculations correct.

**Ensure Safety:** Validation rules prevent unsafe overbooking.

**Enhance Communication:** Structured relationships help send targeted updates to attendees.

**Scalability:** Supports growth from managing a few events to hundreds while keeping data organized.
