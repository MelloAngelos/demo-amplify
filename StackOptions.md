**Use of AWS Services in the Implementation of a Procurement Workflow Application for a Thesis Project**

---

### 1. Introduction

This report outlines how AWS services can be utilized to support the implementation of a procurement workflow system for a thesis project. The system is designed to handle multi-step procurement procedures involving various departments (Unit Managers, Budget Office, Procurement Office, Legal, etc.), including electronic form submissions, approvals, document uploads, and integration with external platforms like the Greek KIMDIS portal. Additionally, a crucial part of the thesis includes the analysis and visualization of usage data related to the application.

---

### 2. Overview of Application Requirements

The application should support:

* Role-based access and authentication
* Multi-step approval workflows
* Document upload and secure storage
* Notifications and scheduled reminders
* Audit trails and logs
* Integration with external systems (e.g., KIMDIS)
* **Data visualization and usage analytics**

---

### 3. AWS Services Overview

AWS provides several managed services that align with the technical and functional requirements of the procurement workflow application. Two possible architectural paths are proposed:

---

### 4. Option A: Serverless with AWS Amplify (Gen 2)

This option leverages AWS Amplify Gen 2's full-stack capabilities to rapidly build, deploy, and scale a serverless application.

#### Key Services:

* **AWS Amplify (Gen 2)**: Code-first approach using TypeScript to define backend resources.
* **Amazon Cognito**: For user authentication and role-based access.
* **AppSync (GraphQL API)**: Auto-generated API from data models.
* **Amazon DynamoDB**: NoSQL database for storing requests and workflow states.
* **AWS Lambda**: For custom logic (e.g., notifications, workflow transitions).
* **Amazon S3**: Secure file uploads (e.g., signed PDFs, contracts).
* **Amazon EventBridge**: Schedule-based or event-based Lambda invocation (e.g., reminders, cleanup).
* **Amazon SES**: For sending email notifications to departments/users.
* **Amazon QuickSight** (optional): For **interactive dashboards and data visualizations** based on logged actions and usage metrics.

#### Benefits:

* Fully serverless and scalable
* Fast development using Amplify CLI and code-first modeling
* Simple integration of authentication, APIs, and storage
* Integrated analytics and visualization tools with QuickSight (optional)

#### Example Use Cases:

* Run scheduled Lambdas for stale request cleanup
* Store documents in S3 and link them to specific workflow steps
* Send automatic emails when approval deadlines are near
* Visualize frequency of procurement requests per department or step completion times

---

### 5. Option B: Custom Backend with PostgreSQL + AWS Integrations

For more complex or traditional architectures requiring a relational database, this option allows using a custom backend while still leveraging AWS services for specific needs.

#### Core Stack:

* **Frontend**: React + Vite + TypeScript
* **Backend**: Node.js (Express) or NestJS
* **Database**: PostgreSQL (hosted on AWS RDS or externally)

#### AWS Services (Modular Usage):

* **Amazon Cognito**: Authentication and JWT token issuance
* **Amazon S3**: File storage with access control
* **AWS Lambda**: Used selectively for:

  * Email sending (via SES)
  * PDF generation
  * Scheduled tasks (e.g., overdue steps)
  * S3 file validation
* **Amazon EventBridge**: Scheduling Lambda invocations (e.g., daily cleanup)
* **Amazon SES**: Email service for system notifications
* **Amazon QuickSight** or custom charting (e.g., Chart.js, Recharts): for usage **data visualization and reporting** from PostgreSQL

#### Benefits:

* Full control over database schema and complex queries
* Can use existing backend architecture and ORM (e.g., Prisma, Sequelize)
* Amplify Hosting can still be used for frontend deployment

#### Example Use Cases:

* A Lambda triggered every morning to remind budget approvers of pending tasks
* A Lambda that generates a signed procurement summary PDF
* Upload files to S3 and save metadata in PostgreSQL
* Generate bar charts showing average time spent per approval step or number of requests per unit

---

### 6. Comparative Summary

| Feature                     | Option A: Amplify Gen 2 | Option B: Custom Backend        |
| --------------------------- | ----------------------- | ------------------------------- |
| Auth & User Management      | Cognito                 | Cognito or custom               |
| API Layer                   | AppSync (GraphQL)       | Express/NestJS REST API         |
| Database                    | DynamoDB                | PostgreSQL                      |
| Custom Logic                | Lambda                  | Native code + Lambda (optional) |
| Scheduled Jobs              | EventBridge + Lambda    | EventBridge + Lambda            |
| File Storage                | S3                      | S3                              |
| PDF Generation, Email, etc. | Lambda                  | Lambda                          |
| Frontend Hosting            | Amplify Hosting         | Amplify Hosting / Vercel        |
| Data Visualization          | QuickSight (optional)   | QuickSight or custom frontend   |

---

### 7. Recommendation

For a thesis-level project with an emphasis on **cloud-native architecture**, fast deployment, and minimal ops, **Option A (Amplify Gen 2)** is highly recommended. It enables rapid iteration, integrates authentication, file storage, APIs, background processing, and optionally data analytics and visualization.

However, if the application must follow strict relational logic, support SQL-based reporting, or integrate with legacy systems, **Option B** offers more flexibility and architectural control, while still enabling rich visual analytics using PostgreSQL + QuickSight or frontend tools.

---

### 8. Conclusion

Both approaches provide robust AWS-powered solutions to build a modern, secure, and scalable procurement workflow system. AWS services like **Cognito, Lambda, S3, EventBridge, SES, QuickSight**, and **Amplify Hosting** remain valuable building blocks in either architecture.

The final decision depends on technical complexity, familiarity with tools, and academic or operational requirements, including the necessity for **usage analytics and data visualization** as part of the thesis deliverables.
