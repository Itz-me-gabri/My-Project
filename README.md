# 🚀 Streamlining IT Procurement: Automating Standard Laptop Orders with Flow Designer

![ServiceNow](https://img.shields.io/badge/ServiceNow-Flow%20Designer-00A1E0?style=for-the-badge\&logo=servicenow)
![Automation](https://img.shields.io/badge/Automation-Workflow-green?style=for-the-badge)
![Project](https://img.shields.io/badge/Project-MY%20PROJECT-purple?style=for-the-badge)

> **A ServiceNow Flow Designer automation project that streamlines Standard Laptop procurement by automatically creating, routing, and managing Catalog Tasks after approval.**

---

## 📌 Project Overview

This project is implemented in **ServiceNow** and demonstrates workflow automation using **Flow Designer**.

The solution streamlines the IT procurement lifecycle by automatically creating and routing **Catalog Tasks (`sc_task`)** for **Standard Laptop** requests once the required approval conditions are satisfied.

### 🎯 Objective

* Automate Catalog Task creation.
* Eliminate manual ticket triaging.
* Route laptop requests to the correct fulfillment team.
* Dynamically transfer request information to fulfillment tasks.
* Improve consistency and reduce processing delays.

---

## 👥 Team Details

| Role              | Details         |
| :---------------- | :-------------- |
| **Team Name**     | MY PROJECT      |
| **Team Member 1** | Gabrian J       |
| **Team Member 2** | Chaandru E      |
| **Team Member 3** | Jetson Samuel S |

---

## 🏗️ Main Modules

### 1️⃣ Service Catalog Module

The Service Catalog module handles the initial laptop request.

**Components:**

* 🖥️ **Catalog Item Configuration**

  * Standard Laptop catalog item.
* 📝 **Variable Definition**

  * Location
  * Urgency
  * Laptop model
  * Other user requirements
* ✅ **Approval Integration**

  * Requests must satisfy organizational approval requirements before fulfillment begins.

---

### 2️⃣ Flow Designer Automation Engine

The **Flow Designer** acts as the automation engine for the project.

**Components:**

* ⚡ **Trigger Configuration**

  * Flow monitors the `sc_req_item` table.
  * Flow executes when the Standard Laptop request reaches the required approved state.
* 🔧 **Action Configuration**

  * Automatically creates a `sc_task` record.
* 💊 **Data Pills**

  * Dynamically transfers information from the Requested Item to the Catalog Task.
* 🔄 **Dynamic Field Mapping**

  * Maps requested user information and descriptions into the generated fulfillment task.

---

### 3️⃣ Task Management & Assignment Module

This module manages fulfillment after the request has been approved.

**Components:**

* 👨‍💻 **Assignment Rules**

  * Automatically assigns the task to the **Hardware** assignment group.
* 📋 **Task Management**

  * Generated tasks contain the required request information.
* 🔒 **State Management**

  * Task completion is connected to the fulfillment lifecycle of the parent Requested Item.

---

## ✨ Features Implemented

### ⚡ Automated Flow Trigger

The flow listens for changes to the **`sc_req_item`** table and executes when the Standard Laptop request satisfies the configured approval condition.

### 📝 Dynamic Task Creation

A **Catalog Task (`sc_task`)** is automatically generated, eliminating the need for a service desk agent to manually create a fulfillment task.

### 🎯 Intelligent Routing

The generated task is automatically assigned to the **Hardware** assignment group for laptop configuration and deployment.

### 🔄 Dynamic Field Mapping

Important information from the original request is transferred to the generated Catalog Task, including:

* Requested For
* Short Description
* Catalog Variables
* Request-related information

---

## 🔄 Project Workflow

```text
┌──────────────────────────┐
│ Service Request          │
│ Submission               │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│ Approval Process         │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│ Flow Designer Trigger    │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│ Catalog Task Generation  │
│       (sc_task)          │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│ Field & Variable Mapping │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│ Hardware Group Assignment│
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│ Fulfillment & Closure    │
└──────────────────────────┘
```

---

## 🧪 Validation & End-to-End Testing

Testing was performed using impersonation to verify that the flow behaves correctly under different request conditions.

| Test Case                   | User / Role         | Operation        | Condition                | Expected Result                                                 | Actual Result |
| :-------------------------- | :------------------ | :--------------- | :----------------------- | :-------------------------------------------------------------- | :-----------: |
| **Flow Trigger - Approved** | End User / Approver | Submit & Approve | Request State = Approved | Flow triggers and `sc_task` is created and assigned to Hardware |     ✅ Pass    |
| **Flow Trigger - Rejected** | End User / Approver | Submit & Reject  | Request State = Rejected | Flow does not create a task and request is closed incomplete    |     ✅ Pass    |
| **Task Assignment Check**   | ITIL Fulfiller      | View Task        | Task generated by Flow   | Assignment Group is Hardware                                    |     ✅ Pass    |
| **Variable Mapping**        | End User            | Submit Request   | Variables populated      | Variables are available on generated Catalog Task               |     ✅ Pass    |

---

## 🛠️ Technology Stack

| Technology                         | Purpose                        |
| :--------------------------------- | :----------------------------- |
| **ServiceNow**                     | IT Service Management Platform |
| **Flow Designer**                  | Workflow Automation            |
| **Service Catalog**                | Laptop Request Management      |
| **Catalog Task (`sc_task`)**       | Fulfillment Task               |
| **Requested Item (`sc_req_item`)** | Request Record                 |
| **Data Pills**                     | Dynamic Data Mapping           |
| **Update Sets**                    | Deployment                     |

---

## 🚀 How to Import / Deploy

To deploy the Flow Designer implementation using a ServiceNow Update Set:

### Step 1: Import Update Set

Navigate to:

```text
System Update Sets
        ↓
Local Update Sets
        ↓
Import Update Set from XML
```

Upload the provided XML file.

### Step 2: Preview

Open the imported Update Set and select:

```text
Preview Update Set
```

Review any preview errors or missing dependencies.

### Step 3: Resolve Dependencies

Check for potential issues such as:

* Missing dictionary entries
* Missing assignment groups
* Missing catalog items
* Missing application dependencies
* Missing Flow Designer components

### Step 4: Commit

After successful validation:

```text
Commit Update Set
```

### Step 5: Verify Flow

Navigate to:

```text
Flow Designer
```

Verify that the flow is:

* ✅ Imported
* ✅ Active
* ✅ Published
* ✅ Configured with the correct trigger and actions

### Step 6: End-to-End Test

Impersonate an end user and:

```text
Service Portal
      ↓
Standard Laptop
      ↓
Submit Request
      ↓
Approval
      ↓
Flow Execution
      ↓
Catalog Task
      ↓
Hardware Assignment Group
```

---

## 📊 Expected Automation Result

When a **Standard Laptop** request is approved:

```text
Approved Request
       │
       ▼
Flow Designer
       │
       ▼
Create sc_task
       │
       ├── Requested For
       ├── Short Description
       ├── Variables
       └── Request Information
       │
       ▼
Assignment Group
     Hardware
       │
       ▼
Laptop Fulfillment
```

---

## 🎯 Project Outcome

This project demonstrates how **ServiceNow Flow Designer** can replace repetitive manual administrative activities with structured, codeless automation.

The solution provides:

* ⚡ Faster task creation
* 🎯 Automatic task routing
* 🔄 Dynamic data transfer
* 📋 Standardized fulfillment
* 🚫 Reduced manual intervention
* 🖥️ Improved hardware procurement workflow
* 📈 Better process consistency

By dynamically generating and routing fulfillment tasks based on approval conditions, the solution creates a streamlined handoff between **request submission, approval, and hardware fulfillment**.

---

## 📁 Suggested GitHub Repository Structure

```text
MY-PROJECT/
│
├── README.md
│
├── update-set/
│   └── standard-laptop-flow.xml
│
├── screenshots/
│   ├── catalog-item.png
│   ├── flow-designer.png
│   ├── trigger.png
│   ├── catalog-task.png
│   └── hardware-assignment.png
│
└── documentation/
    └── project-documentation.pdf
```

---

## 👨‍💻 Team

**MY PROJECT**

* **Gabrian J**
* **Chaandru E**
* **Jetson Samuel S**

---

## ⭐ Project Highlights

> **Service Catalog → Approval → Flow Designer → Catalog Task → Hardware Assignment → Fulfillment**

**Built with ServiceNow Flow Designer 🚀**
