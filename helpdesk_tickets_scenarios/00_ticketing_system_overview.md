# Ticketing System Lab Using Jira Service Management
---

## Overview

This lab demonstrates the implementation and use of **Jira Service Management** to simulate a real-world IT Help Desk ticketing environment.

In enterprise organizations, ticketing systems are critical for tracking user-reported issues, managing service requests, assigning responsibilities, enforcing service-level expectations, and maintaining documentation of all support activities.

Within this home lab environment, **Jira Service Management** is integrated alongside **Active Directory and Windows client systems** to replicate how IT support teams log, triage, troubleshoot, and resolve technical issues in a structured and accountable manner.

This lab bridges the gap between technical system administration skills and operational IT service management workflows.

## Objectives

The objectives of this lab are to:

- Configure and set up a functional Jira Service Management project.

- Create and manage support tickets related to Active Directory and Windows administration tasks.

- Simulate real-world Help Desk workflows including ticket creation, assignment, prioritization, troubleshooting, resolution, and closure.

- Document troubleshooting steps and maintain clear resolution notes within each ticket.

- Demonstrate understanding of structured incident management processes used in enterprise IT environments.

- Practice accountability and audit tracking through proper ticket lifecycle management.

By completing this lab, the focus is not only on resolving technical issues, but also on demonstrating professional documentation, process discipline, and familiarity with industry-standard IT service management tools.

---

## How a Ticketing System Works:

A ticketing system is a essential tool/resource used by IT teams, designed to:
1. **Capture Issues** - Log reported problems or service requests
2. **Organize Requests** - Categorize and prioritize tickets written by end users.
3. **Assign Responsiblity** - Ensure an IT Technician is assigned and owns the issue.
4. **Track Progress** - Monitor status throughout the resolution process.
5. **Document Actions** - Record troubleshooting steps and outcomes.
6. **Close and Archive** - Preserve records for auditing and knowledge reference.

**Jira Service Management** supports this lifecycle through structured workflows and customizable ticket fields.

---

## Ticket Attributes and Properties In Jira

Every ticket (Issue) in Jira contains structured fields that ensure consistency and clarity.

 These fields allow IT teams to track responsbility, prioritize workload, and maintain an audit trail of all support activites.

Below are the core properites configured and used in this lab.

![TicketAttributes](/images/JiraTicket.png)

##### Request Type:
- Specificies the type of issue/request the end user is asking for.
- **Examples:** Get IT Help, Onboard new employees, Request new account, Request admin access, etc
- **Purpose:** Let IT Support staff to get a general sense of what the issue is about.

### Issue Key (Ticket ID)
- Automatically generated unique identifier (e.g., IT-1, SP-2).
- **Purpose:** Used for tracking, referencing, and reporting.

##### Summary(Subject):
- A short, clear description of the issue
- **Example**: User unable to log in - account locked"
- **Purpose:** Allows technicians to quickly understand the nature of the issue without reading the full description.

##### Description:
- A detailed explanation of the problem provided by the requester or technician.
- **Purpose:** Captures context, error messages, and relevant information necessary for troubleshooting.

##### Assignee:
- The IT Technician/Specialist assigned with handling the ticket and solving the end user's issue.
- **Purpose**: Establishes ownership and accountability for the issue.

##### Creator:
- The individual reporting the issue.
- **Purpose:** Identifies who is affected and who should receive updates regarding resolution.

##### Priority:
- Defines urgency and impact. Common levels include: **Highest, High, Medium, Low, and Lowest**.
- **Purpose:** Helps IT teams allocate resources and respond according to business impact.

##### Status:
- Indicates where the ticket is in its lifecycle:
    - **Open**
    - **Waiting**
    - **Assigned**
    - **In Progress**
    - **Escalated**
    - **Closed**
- **Purpose:** Tracks progress and ensures no issue is left unattended.

![JiraTicketExpanded](/images/JiraTicketExpanded.png)

---

## Part 1: Setting Up Jira Service Management

### Step 1: Create an Atlassian Account

1. Navigate to the Atlassian website.
2. Sign up for a free account.
3. Once logged in, select **Create Project**.
4. Choose **Service Management Project**.
5. Select the **IT Service Management** template.

This creates a structured help desk project with predefined workflows.

### Step 2: Project Configuration

After project creation, configure the basic settings. 
- Navigate to the space settings by going to **Support** tab under the **Recent** section. 
- Click on the three dots next to **Support** and select the **Space Settings** option to open settings.

#### Project Details

- Project Name (e.g., IT-HomeLab-ServiceDesk)
- Project Key (e.g., IT)

![JiraSettings](/images/JiraProjectSettings.png)

#### Configure Request Types

Request types determine how users submit support requests through the help desk portal.

To configure request types:

1. While still under **Space Settings**, navigate to **Request Management** > **Request Types** > **Service Requests**.
2. Click **Create Request Type** > **Create blank**.
3. Provide a **Name, Description, and Icon** for the request type.
4. Select which **Portal Groups** this request falls under.
5. Customize the fields users must fill out when submitting the request.
6. Finally, select the appropriate **Work Type** (e.g. Service Request, Incident, Access Request)

![RequestCreation](/screen-recordings/RequestCreation.gif)

Here, you can add new request types for tickets/issues like:
- Password Resets
- Account Unlock
- Remote Desktop Issue
- Network Connectivity Issue

![RequestType](/images/RequestType.png)

---

## Part 2: Creating and Managing Tickets

### Step 1: Create a Ticket

1. Click the blue **Create** button that is on the header.
2. Select the Service Management project that you created.
3. Choose the **Work Type** for this ticket (e.g. Service Request).
4. Select the **Request Type** that fits the ticket best.
5. Fill in the necessary information:
    - **Summary**
    - **Description**
    - **Attachments**(e.g. Screenshots)
    - **Organization**

The system will generates a unique Issue Key and a new ticket will appear in the ticket queue after refreshing the page.

![CreateTicket](/screen-recordings/CreateTicket.gif)

---

### Example Ticket for Installing New Software:

- **Space:** Support(e.g. Name of space)
- **Work Type:** Service Request
- **Request Type:** Request new software
- **Summary:** User needs Adobe license and software installed on their workstation
- **Reason Why:** The end user uses Adobe frequently for their job.

---

### Step 2: Assign and Begin Work

1. Be in the **Ticket Queue** page of your Jira project.
2. Open the ticket by clicking the ticket's key or summary to see more details.
3. To assign a ticket to a techincian or yourself, hover over the **Assignee** field in the **Details** section on the right side of the page.
4. To change the status of the ticket, click on the blue button above the details section and select the status that best represents its status.
    - By default, the status of the ticket will be **Waiting for support**.
5. After changing the status, a modal will appear to add **Internal comments** about the ticket or directly reply to the end user to provide an update.

![TicketAssign](/screen-recordings/TicketAssign.gif)

### Step 3: Resolve and Close:

1. After resolving the requester's ticket, change the status of the ticket to **Resolved**.
2. A modal will open to add resolution notes for the ticket like:
    - **Resolution:** How the issue was resolved(Done, Won't Do, Declined, Duplicate)
    - **Linked Issues:** Whether the ticket is linked to any issues previously.
    - **Issue:** Specifiy the issue that is linked to current ticket.
    - **Comments:** Add internal notes on ticket and/or reply to the customer
3. Click **Resolve this issue** button to finalize changes.
4. The ticket will now be marked as **"Resolved"** and it will disappear from the ticket queue.

![ResolveTicket](/images/ResolveTicket.png)

---
## Skills Demonstrated

This lab demonstrates several key skills relevant to IT Support and Help Desk roles:

- Configuring and operating a **Jira Service Management** project
- Managing the full **ticket lifecycle** including creation, assignment, status updates, and resolution
- Categorizing and prioritizing support requests using **request types and priority levels**
- Documenting troubleshooting steps and resolution notes within tickets
- Understanding structured **IT support workflows** used in professional help desk environments

These skills reflect common responsibilities of IT technicians who rely on ticketing systems to track, organize, and resolve user issues.

## Conclusion

This lab demonstrated the setup and use of **Jira Service Management** within a simulated IT support environment.

By configuring request types, creating service tickets, and managing them through the resolution process, this project replicates how IT teams handle user requests in real-world help desk operations.

The exercise reinforces the importance of structured workflows, proper documentation, and accountability when managing technical support issues.