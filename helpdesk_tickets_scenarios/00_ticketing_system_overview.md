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

##### Urgency:
- 

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

---

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














