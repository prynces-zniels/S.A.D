# Patient Scheduling & Appointment Management System
A patient portal processes appointment bookings, rescheduling requests, practitioner assignments, and patient records through a central management system.

**Scenario:** During peak morning booking hours, concurrent patient traffic overloads the database. This causes delay and booking failures, preventing patients from rescheduling urgent visits, viewing appointment details, and receiving automated reminders.

---

### Bounded Contexts

#### 1 Patient Portal & Scheduling
Entities: Patient, Appointment, RescheduleRequest, NotificationRule
Ubiquitous Language: Booking Window, Late-Change Flag, Reschedule Window, Slot Availability, Appointment Status

#### 2 Practitioner & Resource Allocation
Entities: HealthcareProvider, ClinicLocation, TimeSlot, Specialization
Ubiquitous Language: Provider Availability, Overbooking Threshold, Room Assignment, Duty Shift

#### 3 Notifications & Communications
Entities: PatientContact, CommunicationLog, ReminderTemplate, DispatchQueue
Ubiquitous Language: Event Trigger, Notification Service, Dispatch Timestamp, Delivery Status

---

### Patient Scheduling - User Stories

#### User Story 1
**As a** patient,  
**I want to** reschedule my scheduled appointment,  
**So that** I can change my appointment time when my availability changes while allowing the system to track late changes.

#### User Story 2
**As a** patient,  
**I want to** view my upcoming appointment details,  
**So that** I can confirm the appointment date, time, healthcare provider, and location before attending.

---

Gherkin Syntax
```gherkin
User Story 1
Scenario: Patient reschedules an appointment within 24 hours of the appointment
 Given a patient has a scheduled appointment for "2026-10-15T10:00:00Z"
 When the patient requests a reschedule to "2026-10-16T14:00:00Z" less than 24 hours before the original appointment
 Then the system should apply a late-change flag
 And emit an "AppointmentRescheduled" event to the Notification Service
 And display a confirmation message with the updated appointment details to the patient.


User Story 2
Scenario 1: Patient views a scheduled appointment
 Given a patient has an upcoming scheduled appointment
 When the patient opens the appointment details
 Then the system should display the appointment date and time
 And display the assigned healthcare provider
 And display the appointment location
 And display the current appointment status.

Scenario 2: Patient has no upcoming appointments
 Given a patient has no scheduled upcoming appointments
 When the patient opens the appointment section
 Then the system should display a message indicating that there are no upcoming appointments.
```