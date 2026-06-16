# Smart Onboarding Automation

An automated onboarding workflow built with **n8n**, **Google Sheets**, and **Gmail** that streamlines applicant processing based on city-specific hiring capacity.

## Overview

Managing onboarding manually can become difficult when multiple locations have different hiring limits.

This workflow automatically:

* Receives new onboarding applications from Google Forms
* Checks current employee counts per city
* Compares counts against predefined hiring thresholds
* Sends onboarding emails when capacity is available
* Places applicants on a waiting list when locations are full
* Maintains a queue for future openings

---

## Workflow Architecture

```text
Google Form Submission
          │
          ▼
Google Sheets Trigger
          │
          ▼
Read Employee Database
          │
          ▼
Read City Thresholds
          │
          ▼
Capacity Validation Logic
          │
    ┌─────┴─────┐
    ▼           ▼
Capacity      Full
Available     Capacity
    │           │
    ▼           ▼
Send         Send
Onboarding   Waitlist
Email        Email
                │
                ▼
         Add to Queue
```

---

## Features

### Automatic Capacity Checking

The workflow:

1. Retrieves the applicant's selected city.
2. Counts existing employees in that city.
3. Fetches the city's maximum employee threshold.
4. Determines whether additional onboarding slots are available.

### Automated Applicant Communication

#### Accepted Applicants

When capacity is available:

* Sends an onboarding email
* Confirms city and contract type
* Shares next onboarding steps
* Displays remaining available positions

#### Waitlisted Applicants

When capacity is full:

* Sends a polite notification email
* Informs the applicant they have been added to a queue
* Stores applicant details for future contact

### Queue Management

Waitlisted candidates are automatically stored in a dedicated Google Sheet including:

* Name
* Email
* City
* Contract Type
* Contact Date

---

## Technologies Used

* n8n
* Google Forms
* Google Sheets
* Gmail API
* JavaScript

---

## Google Sheets Structure

### Employee List Sheet

| Name     | City   | Contract  |
| -------- | ------ | --------- |
| John Doe | Berlin | Full-Time |

### Threshold Sheet

| City    | Threshold |
| ------- | --------- |
| Berlin  | 50        |
| Hamburg | 30        |
| Munich  | 40        |

### Queue Sheet

| Name | Email | City | Contract | Contacted |
| ---- | ----- | ---- | -------- | --------- |

---

## Business Logic

```javascript
capacityAvailable =
currentEmployees < cityThreshold
```

If:

```javascript
true
```

Applicant receives onboarding email.

If:

```javascript
false
```

Applicant is waitlisted and stored in the queue.

---

## Use Cases

* Employee onboarding
* Fleet recruitment
* Driver onboarding
* Contractor management
* Multi-city hiring operations
* Franchise workforce management

---

## Setup

### Prerequisites

* n8n instance
* Google Account
* Gmail OAuth credentials
* Google Sheets OAuth credentials

### Configuration Steps

1. Import the workflow into n8n.
2. Connect Google Sheets credentials.
3. Connect Gmail credentials.
4. Create:

   * Employee List Sheet
   * Threshold Sheet
   * Queue Sheet
5. Connect a Google Form to the response sheet.
6. Activate the workflow.

---

## Future Improvements

* Slack notifications
* HR dashboard
* Approval workflows
* Multi-level capacity rules
* Automated interview scheduling
* PDF onboarding packet generation
* Analytics and reporting

---

## License

MIT License

Feel free to modify and extend the workflow for your organization's onboarding and recruitment process.
