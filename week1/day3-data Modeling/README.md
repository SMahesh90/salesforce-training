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

---

## 4 Formula Fields
