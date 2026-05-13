# Asana CRM Automation System
**Technical Documentation for Asana-Zapier-Google Drive Integration**

## 1. Project Overview
A multi-path automation system designed to handle the lead lifecycle within an Asana CRM. The system features conditional branching, AI-driven personalization, and data de-duplication to ensure a resilient workflow.

## 2. Full Workflow Architecture
The following map details the 5-path logic used to route leads based on their current CRM stage: `Ready to Start`, `No Response`, `Quoted`, `Approved`, and `Paid/Closed`.

![Full Automation Architecture](images/workflow_Image1.png)

## 3. Technical Stack
* **Logic Engine:** Zapier Paths (5 distinct branches).
* **CRM:** Asana (Task Update Triggers).
* **Storage:** Google Drive API.
* **Intelligence:** AI by Zapier (GPT-4 Integration).

## 4. Logic Gates & Failsafes

### A. Lead Folder De-duplication (Find or Create)
To prevent storage fragmentation, the system uses a "Search and Fallback" logic gate. Before creating any assets, the system verifies if a project directory already exists.

![De-duplication Logic Configuration](images/workflow_Image2.png)

* **Step:** `Find or Create Lead Folder`.
* **Logic:** Searches Google Drive for a folder matching the `Task Name`. If the search returns null, the system is configured to create a new directory automatically.
* **Impact:** Eliminates duplicate folder creation if a lead is moved between columns multiple times.

### B. Status Validation Filters
* **Step:** `Validate Lead Status`.
* **Logic:** Positioned immediately after **Delay by Zapier** nodes. It re-verifies the task status in Asana before sending any outgoing communication.
* **Impact:** Prevents "Ghost Communications"—automated follow-ups sent after a lead has already moved to a different stage.

## 5. Setup Requirements
1. **Asana:** Columns must match the exact naming convention used in the Zapier filters.
2. **Google Drive:** A "Parent Folder" named `Leads` must be specified for the search node target.
3. **Zapier:** A Professional plan or higher is required to support "Paths" logic.
