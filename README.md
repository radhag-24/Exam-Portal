# ExamPortal – Technical Overview

## 1. Project Overview

ExamPortal is a web-based examination management system developed using Google Apps Script and Google Sheets.

It automates the examination workflow, including student registration, examination link generation, online assessments, automated evaluation, result management, retake handling, and certificate generation.

Google Apps Script handles the application logic, while Google Sheets acts as the primary data storage system.

## 2. Technology Stack

| Technology | Purpose |
|---|---|
| Google Apps Script | Backend logic and application processing |
| JavaScript | Application functionality |
| HTML | User interface |
| Google Sheets | Data storage and record management |
| Google Drive | File and certificate storage |
| Google Slides | Certificate template |
| Gmail / MailApp | Email notifications and certificate delivery |

## 3. System Architecture

The application follows a Google Apps Script-based architecture.

### Main Components

- **Frontend:** HTML pages for student registration, examinations, and administrative review.
- **Backend:** Google Apps Script functions for processing requests and managing examination workflows.
- **Database:** Google Sheets workbook for storing registrations, examination settings, invitations, attempts, questions, and results.
- **Email Service:** Sends examination links, notifications, and certificates.
- **Scheduled Triggers:** Handles automatic submission of overdue examination attempts.

### Application Workflow

1. Students access the registration page.
2. Registration details are validated and stored in Google Sheets.
3. Administrators generate and send examination links.
4. The system creates unique invitation tokens.
5. Students access examinations using the generated links.
6. Answers are saved and examinations are submitted.
7. The backend evaluates answers and updates records.
8. Results are generated and passing students receive certificates.
9. Administrators can review attempts and issue retake links.

## 4. Google Sheets Database Structure

The application uses a single Google Sheets workbook containing the following sheets:

| Sheet | Purpose |
|---|---|
| Tests | Examination configuration, time limits, pass percentage, and availability settings |
| Registrations | Student registration details and examination status |
| Results | Examination scores and final results |
| Invites | Unique examination tokens and invitation status |
| Attempts | Examination attempts, answers, scores, and submission details |
| Ethics | Ethics examination question bank |
| Lab Safety | Lab Safety examination question bank |
| README | Workbook usage information |

## 5. Backend Functionality

The main backend implementation is maintained in `Code.gs`.

| Function | Responsibility |
|---|---|
| `doGet()` | Handles application page routing |
| `registerStudent()` | Validates and saves student registration |
| `sendLinks_()` | Generates and sends examination links |
| `createInvite_()` | Creates unique invitation tokens |
| `startExam()` | Starts or resumes an examination attempt |
| `saveAnswers()` | Saves student answers |
| `submitExam()` | Handles examination submission |
| `finalizeAttempt_()` | Evaluates answers and updates examination records |
| `finalizeOverdueAttempts()` | Automatically submits overdue attempts |
| `reviewPage_()` | Generates the administrative review page |
| `makeCertificatePdf_()` | Generates PDF certificates |
| `backupNow_()` | Creates workbook backups |
| `menuResetMonth()` | Resets operational sheets for a new examination cycle |
| `setupSheets()` | Creates and configures workbook sheets |

## 6. Examination Management

### Student Registration

- Collects student information.
- Validates registration details.
- Stores registration records in the Registrations sheet.

### Examination Link Generation

- Generates unique invitation tokens.
- Associates invitations with student registration records.
- Sends examination links through email.
- Supports retake examination links.

### Examination Process

- Loads questions from the relevant question bank.
- Supports configured examination time limits.
- Stores question order and option order for attempts.
- Saves student answers.
- Supports resuming an existing attempt.

### Evaluation and Results

- Evaluates submitted answers.
- Calculates scores and percentages.
- Determines pass or fail status.
- Updates Attempts, Registrations, Invites, and Results sheets.

### Automatic Submission

The scheduled function `finalizeOverdueAttempts()` checks for overdue examination attempts and finalizes them automatically.

A time-driven trigger is used to execute this function periodically.

## 7. Certificate Generation

- Generates PDF certificates for eligible students.
- Uses a certificate template.
- Sends certificates through email.
- Maintains certificate delivery status in the registration records.

## 8. Administrative Features

- Configure examination settings.
- Manage student registrations.
- Generate examination and retake links.
- Review examination attempts.
- Check examination results.
- Generate or resend certificates.
- Create workbook backups.
- Reset operational records for a new examination cycle.

## 9. Project Structure

```text
ExamPortal/
│
├── Code.gs
├── Register.html
├── Exam.html
├── Review.html
├── PickDateTime.html
├── UploadImage.html
├── MailRegistration.html
├── MailTestLink.html
├── MailCertificate.html
├── Certificate.html
├── appsscript.json
├── README.md
│
└── sample-data/
    └── ExamPortal_Sample_Workbook.xlsx
