### 1. What is Salesforce Platform?
The Salesforce Platform is the app development foundation that extends the reach and functionality of the CRM. It is a "metadata-driven" architecture that allows businesses to build, customize, and automate applications quickly.

* It unites different departments (Marketing, Sales, Service, IT) by providing a single, shared view of the customer.
  
* It is designed to be "low-code," meaning most people can build secure, intelligent apps using visual tools, while professional developers can use code to create more complex customizations.

### App

A set of objects, fields, and other functionality (like flows or analytics) grouped together to support a specific business process. 

### Object

These are essentially tables in the Salesforce database that store a particular kind of information. There are standard objects (like Accounts and Contacts) and custom objects created by a user (like the "Property" object).

### Tab

A visual navigation element found within an App. Clicking a tab takes the user to a specific object's list of records or a specific tool (like the "Settings" tab or "Properties" tab).

# Salesforce: Configuration vs. Coding

Salesforce allows you to build apps using either visual tools (**Configuration**) or programming languages (**Coding**).

---

## 🛠 Configuration (No-Code / Low-Code)
*Define behavior using point-and-click visual tools.*

- **Tools:** Flow Builder, Lightning App Builder, Object Manager.
- **Pros:** Fast to build, easy to maintain, and automatically updated by Salesforce.
- **Best For:** Creating fields, simple automation, and standard page layouts.

---

## 💻 Coding (Pro-Code)
*Define behavior using custom-written scripts and frameworks.*

- **Languages:** **Apex** (Back-end logic) and **LWC** (Front-end interface).
- **Pros:** Handles unlimited complexity and connects to external systems.
- **Best For:** Complex math, custom UI, and high-level integrations.

---

## 💡 The Golden Rule
**"Configuration First."** 
Always try to use standard Salesforce tools first. Only use code when the built-in tools cannot meet your specific business requirements.
