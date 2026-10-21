# Placely — College Placement Management Platform

> **One platform for students preparing for placements and the college teams coordinating them.**
>
> Placely brings student profiles, placement drives, assessments, recruitment operations, notifications, and plan payments together across a mobile app and a shared REST API.

**Mobile app:** Android and iOS (React Native + Expo)  
**Web app:** Plan selection and payments (React + Vite)  
**Project timeline:** November 23, 2025 – approximately June 6, 2026

## At a glance

| Area | What Placely provides |
| --- | --- |
| Students | Account and academic profile workflows, placement-drive discovery and enrollment, notifications, assessments, coding tests, and resume analysis |
| College teams | Role-based administration, student verification, drive management, student reports, and placement analytics |
| Payments | Plan selection, checkout, payment verification, payment history, and payment status handling |
| Platform | A shared Express API, MongoDB persistence, and integrations for payments, files, notifications, and assessment services |

## Screenshots

The following screenshots show the mobile app's student and college-staff experiences. They are grouped by workflow so readers can follow the product from student preparation to college recruitment operations.

### Student experience

| Student profile | Resume analysis and placement drives |
| --- | --- |
| ![Student profile showing verification, academic summary, and personal information](./images/image%20copy.png) | ![Student dashboard showing ATS resume score and placement drives](./images/image.png) |

| Placement preparation and assessments |
| --- |
| ![Student assessment screen with aptitude, technical MCQ, and coding tests](./images/image%20copy%202.png) |

### College verification and analytics

| Department placement overview | Approve student signups |
| --- | --- |
| ![Department placement overview with placement ratio, summary, and actions](./images/image%20copy%203.png) | ![HOD signup approval screen with searchable student list and academic details](./images/image%20copy%204.png) |

| Review class-representative updates | Manage verified students |
| --- | --- |
| ![Class representative verified updates review screen](./images/image%20copy%205.png) | ![Verified students list with academic information and review actions](./images/image%20copy%206.png) |

### Placement officer and recruitment-drive management

| Create a drive | Manage drives |
| --- | --- |
| ![Placement officer dashboard and create-drive form](./images/image%20copy%207.png) | ![Manage drives list with drive details and student actions](./images/image%20copy%208.png) |

| Track drive rounds and selected students | Browse the student directory |
| --- | --- |
| ![Drive management screen with enrollment counts, round progress, and student selection](./images/image%20copy%209.png) | ![Student directory with search, placement status, GPA, ATS score, and backlogs](./images/image%20copy%2010.png) |

| Filter students |
| --- |
| ![Student directory filters for gender, department, semester, and CGPA](./images/image%20copy%2011.png) |

### Recruitment communications

| Mobile enrollment reminder | Placement-round update email |
| --- | --- |
| ![Mobile notifications reminding students about placement-drive enrollment deadlines](./images/image%20copy%2012.png) | ![Email notifying a student about clearing a placement round and interview preparation](./images/image%20copy%2013.png) |

## Product features

### Student mobile app

- **Accounts and onboarding:** Registration, login, password recovery, OTP verification, onboarding, and account logout.
- **Student profile:** View and edit profile and academic information, including GPA and backlog-related records; submit profile changes for review where required.
- **Verification and access:** Student verification states, authorized-student flows, and class-monitor workflows for reviewing eligible student changes.
- **Placement drives:** Browse available drives, view drive details, enroll, and follow application or enrollment status.
- **Placement preparation:** Take assessments, view test results and history, check attempt limits and statistics, and practice using drive- or round-related question sets.
- **Coding assessments:** Run and validate code through the coding-test workflow.
- **Resume support:** Upload a resume, run an ATS-style check, review the score and insights, and support drive-related resume workflows.
- **Notifications:** Receive notifications, mark one or all as read, remove notifications, and subscribe or unsubscribe to drive updates.
- **Student dashboard:** See placement-related information and access the student workflows from the mobile app.
- **Legal and information pages:** About, privacy, and terms information.

### College and placement team workflows

| Role | Supported workflows |
| --- | --- |
| **Administrator** | Sign in; review pending HOD and placement-officer requests; approve or reject those requests |
| **Head of Department (HOD)** | Review department students, verify students and profile updates, and work with department placement drives |
| **Class monitor / authorized student** | Review student changes awaiting verification and approve or reject supported academic-record updates |
| **Placement officer** | Create, edit, and remove drives; manage drive rounds; review students and drive details; view placement analytics and student reports |
| **College authority** | Create and edit college information, retrieve college records, and update college payment status |

### Payments web app

- Student login and protected plan selection and checkout.
- Selection of a plan, creation of a payment order, and payment verification.
- Success, processing, and failure states, with payment history and failed-payment handling in the API.
- Informational pages covering privacy, cookies, terms, contact, refunds, security, and service status.
- An app-download request flow.

### Platform services and operations

- Role-aware API route groups with authentication middleware on protected workflows.
- MongoDB models for students, colleges, staff roles, drives, tests, questions, resumes, payments, and notifications.
- Razorpay order, verification, and webhook handling.
- Resume and file upload/storage integrations using configured object-storage providers.
- Firebase-backed notification services and enrollment reminders.
- Assessment integrations for AI-assisted resume analysis and remote code evaluation, when their credentials and services are configured.
- Scheduled plan-expiration and resume-cleanup jobs.

> Integrations that require external credentials are deployment-dependent. The feature areas above describe the code paths present in the project, not a guarantee that every third-party service is configured in every environment.

## End-to-end workflows

### 1. Student onboarding, verification, and placement-drive enrollment

```mermaid
flowchart TD
    A[Student registers or signs in] --> B[Complete onboarding and student profile]
    B --> C{Does the profile require review?}
    C -- Yes --> D[Submit profile or academic update]
    D --> E[Class monitor or authorized reviewer checks the update]
    E --> F{Approve?}
    F -- Yes --> G[Verified profile data is available to placement workflows]
    F -- No --> H[Update is rejected for correction]
    H --> B
    C -- No --> G
    G --> I[Browse placement drives]
    I --> J[Open drive details and check eligibility]
    J --> K[Enroll in the drive]
    K --> L[Track drive or enrollment status]
    L --> M[Receive relevant notifications and reminders]
```

### 2. College staffing and recruitment-drive management

```mermaid
flowchart TD
    A[HOD or placement officer submits an access request] --> B[Administrator reviews pending request]
    B --> C{Approve request?}
    C -- No --> D[Request rejected]
    C -- Yes --> E[Staff member signs in with role access]
    E --> F{Staff role}
    F -- HOD --> G[Review department students and verification requests]
    G --> H[Verify eligible students or profile changes]
    G --> I[View department drives]
    F -- Placement officer --> J[Create or edit a placement drive]
    J --> K[Configure drive rounds and details]
    K --> L[Students discover and enroll in the drive]
    L --> M[Review drive students and recruitment progress]
    M --> N[View analytics and student reports]
    H --> L
```

### 3. Assessment and resume-analysis workflow

```mermaid
flowchart LR
    A[Student opens preparation tools] --> B{Choose a workflow}
    B --> C[Start an assessment]
    C --> D[Answer questions and submit]
    D --> E[API records result]
    E --> F[Review score, history, statistics, and report]
    B --> G[Start a coding assessment]
    G --> H[Submit code]
    H --> I[API calls configured code-evaluation service]
    I --> J[Show validation or execution result]
    B --> K[Upload a resume]
    K --> L[Resume analysis service evaluates it]
    L --> M[Review ATS score and resume insights]
```

### 4. Plan purchase and payment confirmation

```mermaid
sequenceDiagram
    actor Student
    participant Web as Payment web app
    participant API as Placely API
    participant RP as Razorpay
    participant DB as MongoDB

    Student->>Web: Sign in and select a plan
    Web->>API: Request payment order
    API->>RP: Create order
    RP-->>API: Order details
    API-->>Web: Checkout details
    Web->>RP: Complete checkout
    RP-->>Web: Payment response
    Web->>API: Submit payment verification
    API->>API: Verify payment signature
    API->>DB: Record payment and plan state
    API-->>Web: Success or failure status
    RP->>API: Payment webhook event
    API->>DB: Reconcile payment event
    Web-->>Student: Show processing, success, or failure page
```

## Architecture

```mermaid
flowchart TB
    subgraph Clients
        Mobile[React Native mobile app<br/>Student and college staff]
        Payment[React payment web app]
    end

    subgraph Backend[Node.js backend]
        API[Express REST API]
        Auth[Authentication and role middleware]
        Routes[Route groups]
        Controllers[Controllers]
        Services[Services and integrations]
        Jobs[Scheduled jobs]
    end

    DB[(MongoDB<br/>Mongoose models)]
    Razorpay[Razorpay]
    Firebase[Firebase notifications]
    Storage[Cloudflare R2 / AWS S3]
    Assessments[Gemini / code evaluation provider]
    Email[Email and messaging providers]

    Mobile -->|HTTPS / JSON| API
    Payment -->|HTTPS / JSON| API
    API --> Auth --> Routes --> Controllers --> Services
    Services <--> DB
    Services <--> Razorpay
    Services <--> Firebase
    Services <--> Storage
    Services <--> Assessments
    Services <--> Email
    Razorpay -->|Signed webhook| API
    Jobs --> Services
    Jobs --> DB
```

### Request lifecycle

```text
Mobile app or payment website
        |
        | HTTP request (JSON, upload, or webhook)
        v
Express middleware
  CORS -> body parsing -> authentication / role checks (where required)
        |
        v
Route -> Controller -> Service
                    |          |
                    |          +---- External integrations (as configured)
                    v
              Mongoose model
                    |
                    v
                MongoDB
                    |
                    v
          JSON response to client
```

### Main API areas

| API prefix | Responsibility |
| --- | --- |
| `/students` | Student accounts, profiles, onboarding, academic updates, dashboard, and authorization workflows |
| `/hods` | HOD and department workflows |
| `/placeofficers` | Placement-officer operations |
| `/drives` | Drive creation, discovery, details, and enrollment |
| `/notifications` | Notification retrieval, read state, delivery, and drive subscriptions |
| `/admin` | Administrator access and staff-request decisions |
| `/test` | Assessment attempts, results, history, practice, statistics, and reports |
| `/code` | Code execution and validation |
| `/resumes` | Resume upload and drive-related resume access |
| `/payments` | Orders, verification, failures, history, and app-download requests |
| `/collegeauthority` | College records and payment-status workflows |
| `/webhooks/razorpay` | Razorpay payment-event processing |

## Technology stack

| Layer | Technologies and libraries |
| --- | --- |
| Backend runtime and API | Node.js, Express 5 |
| Persistence | MongoDB, Mongoose |
| Authentication and security building blocks | JSON Web Tokens, bcrypt, CORS middleware |
| Mobile application | React Native 0.81, Expo SDK 54, Expo Router 6, React Navigation |
| Mobile capabilities | Expo Notifications, document and image pickers, AsyncStorage, encrypted storage, Firebase |
| Payment web application | React 19, Vite 7, React Router 7, TanStack Query, Axios |
| Payments | Razorpay |
| File and document handling | Multer, AWS SDK for S3, PDF utilities, ExcelJS |
| Assessment integrations | Google Generative AI SDK and configured code-evaluation service |
| Background work | node-cron |
| Development and delivery | npm, ESLint, Docker configuration, Expo/EAS configuration, Git |

## Codebase map

```text
Placely/
├── Backend/
│   ├── app.js, server.js       # Express setup, route mounting, and server startup
│   ├── routes/                 # REST endpoints and webhook entry point
│   ├── controllers/            # HTTP request and response handling
│   ├── services/               # Business workflows and external integrations
│   ├── models/                 # MongoDB / Mongoose schemas
│   ├── middleware/             # Authentication, uploads, errors, webhook checks
│   ├── config/                 # Database and provider clients
│   └── jobs/                   # Plan expiration and resume cleanup
├── Mobile/
│   ├── app/                    # Expo Router screens grouped by user role
│   ├── components/             # Shared interface components
│   ├── context/, lib/, utils/  # App state, API client, and supporting helpers
│   └── app.json, eas.json      # Expo and build configuration
├── Payment/
│   ├── src/App.jsx             # Browser routes and guarded checkout routes
│   ├── src/pages/              # Dashboard, plans, checkout, status, and policy pages
│   └── src/lib/api.js          # Backend API client
└── placely-project-showcase.md # This project overview
```

## Recruiter walkthrough

Placely is a multi-client product rather than a single mobile screen: the mobile app serves students and college staff, while the browser app handles plan selection and payments. Both use a shared API, which owns role-aware workflows, persistence, payment verification, and integrations.

For a technical walkthrough, useful areas to explore are:

1. **Role-based workflows:** student verification, HOD and placement-officer access, and administrator approval.
2. **Drive lifecycle:** drive setup and rounds through student discovery, enrollment, and staff reporting.
3. **Assessment services:** test history and reporting, code evaluation, and resume analysis.
4. **Payment consistency:** order creation, verification, webhook events, and recorded payment status.
5. **Cross-client design:** mobile and web clients sharing API capabilities while keeping their user experiences separate.

---

*Feature and technology descriptions reflect the application code and manifests in this repository. Availability of external integrations depends on deployment configuration and credentials.*

## Payment website

Plan selection and checkout are available at [web.placely.space](https://web.placely.space/).

---

**Usage notice:** The screenshots and other project materials on this page are provided for viewing as a project showcase. Do not copy, reproduce, redistribute, or use them without prior permission from the project owner.


## Source Code Access

The source-code repository is private. Source code is available to recruiters upon request, subject to project ownership and access permissions.