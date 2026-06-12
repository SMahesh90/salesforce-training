# Admin Day 1: User Management

## 1. What is a Salesforce Administrator?
A Salesforce Admin is the "go-to" person for a company’s Salesforce platform. They don’t just write code; they solve business problems. They make sure the right people have access to the right tools, help pull reports, and keep the system organized so the business runs smoothly.

---

## 2. The Core Four: Key Definitions

| Term | Simple Definition | Analogy |
| :--- | :--- | :--- |
| **User** | A person who logs into Salesforce. | The Person. |
| **Profile** | **What** you can do. It controls your basic permissions (like "Can I delete a file?"). | Your Job Title. |
| **Role** | **Who** you can see. It controls which records you can look at based on your rank. | Your spot on the Org Chart. |
| **Permission Set** | **Extra** powers given to a user without changing their whole profile. | A "VIP Pass." |

---

## 3. College Security Design
Imagine a college system. We use security to make sure data stays private:

*   **Students:** Can see their own grades, but can't see other students' grades.
*   **Professors:** Can see all students in their specific class and enter grades for them.
*   **Registrar (Admin):** Can see every student in the whole college and change their enrollment status.
*   **Security Rule:** A student should never have the "Profile" of a Professor, or they could give themselves straight A's!

---

## 4. Administrator Access Risks
Being an Admin is like having a "Master Key." It is dangerous because:
*   **Human Error:** You could accidentally delete important data that can't be recovered.
*   **Privacy:** Admins can see sensitive info (like salaries or home addresses) that they might not need to see.
*   **System Breaks:** One wrong setting change can stop the entire company from being able to work.

---

## 5. Reflection: Why do systems need strong access control?
Enterprise systems (like Salesforce) hold a massive amount of private data. We need strong access control for three simple reasons:

1.  **Safety:** To keep hackers out and prevent employees from seeing things they shouldn't.
2.  **Accuracy:** If everyone can change everything, the data becomes a mess. Limits keep the data "clean."
3.  **The Law:** In many jobs (like hospitals or schools), it is illegal to let unauthorized people see private records. 

**Bottom Line:** A good Admin follows the "Rule of Least Privilege"—only give people the access they absolutely need to do their job, and nothing more.
