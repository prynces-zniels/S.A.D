# Legacy University Portal Modernization
A legacy monolithic University Portal processes applications and admissions, student tuition billing and allows student access to assignments and learning materials through a single centralized database.

**Scenario:** During peak hours, concurrent web traffic overloads the monolithic database. This exhaustion crashes the entire platform, thereby preventing applicants from submitting forms, students from turning in coursework, and the finance office from processing payments.

---

### Bounded Contexts

#### 1 Student applications and admissions
Entities: Applicant, ApplicationForm, VerificationDocument, WaitlistEntry
Ubiquitous Language: Cutoff Point, Application Deadline, WASSCE Verification, Waitlist,  Application Status

#### 2 Student Billing & Finance
Entities: StudentAccount, Invoice, ScholarshipAward, PaymentReceipt
Ubiquitous Language: Payment Deadline, Lab Fee, Scholarship Disbursement, Invoice

#### 3 Course Content & Assignments
Entities: CourseModule, Assignment, Submission, GradingSystem
Ubiquitous Language: Assignment Prompt, Submission Timestamp, Grading, Attachment

---

### Course Content and Assignment - User Stories

#### User Story 1
**As a** lecturer,
**I want to** view a student's submission timestamp, deadline, and course material access logs,
**So that** I can identify learning gaps and provide targeted academic support.

#### User Story 2
**As a** proctor,
**I want to** track tab-switching events, time spent per question, and click activity during online assignments,
**So that** I can flag suspicious assessment activity and uphold academic honesty standards.

---

Gherkin Syntax
```gherkin
User Story 1
Scenario: Instructor views student submission and engagement dashboard for an assignment
 Given an instructor is logged into the "Discrete Math" course portal
 And a student has submitted "Truth Table Assignment" 10 minutes before the deadline
 When the instructor opens the engagement analytics dashboard for "Truth Table Assignment"
 Then the system displays the submission timestamp and deadline proximity log
 And shows the course material access logs


User Story 2
Scenario: System flags an assignment submission for further review due to suspicious activity
 Given a student is currently taking the online assessment "S.A.D Quiz 3"
 And the assessment has an active monitoring rule for browser tracking
 When the student switches away from the test tab 3 or more times
 And completes a 10-question section in less than 30 seconds
 Then the system should record the exact browser timestamps and question duration logs
 And mark the final submission status as "Flagged for Review"
 And emit an "AssessmentFlagged" event to the Proctor Dashboard
```
