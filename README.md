# Hospital Management - DevOps Project

## 1. Project overview

## 2. Requirement analysis
### 2.1 Functional requirements
#### PATIENTS
Register, search, view, edit. Deactivate a record
while preserving past appointments.
#### DOCTORS
Register, view, update, deactivate. Track
specialisation and availability.
#### APPOINTMENTS
Create with patient, doctor, date, time and reason.
Status: scheduled, completed, cancelled. No
double-booking.
#### MEDICAL RECORDS
A doctor records visit date, diagnosis and notes.
Records are retained and readable by authorised
staff.
#### AUTHENTICATION
Users log in before reaching protected
functionality. The system distinguishes three roles.
#### ACCESS AND EXPORT
Functionality restricted by role. A doctor exports
authorised data as a CSV report.
### 2.2 Non-functional requirements
**Performance** Requests processed within two seconds under the expected demonstration workload.

**Availability** Available during normal operation; recovers automatically from an application or container failure.

**Security — storage** Passwords must not be stored in plain text.

**Security — access** Authentication before protected functionality; role permissions enforced.

**Deployability** A change on the main branch produces a published container image without manual steps.

**Testability** Automated unit and end-to-end tests run in CI on every pull request.

**Observability** Application and system metrics exposed and visible on a dashboard.

**Maintainability** A documented branching strategy and a versioning scheme for artefacts.

## 3. Roles and access control

| Capability | Receptionist | Doctor | Administrator |
|---|---|---|---|
| Register, search and edit a patient | Yes | No | Yes |
| Deactivate a patient record | Yes | No | Yes |
| Register, update or deactivate a doctor | No | No | Yes |
| Schedule an appointment | Yes | No | Yes |
| View appointments | All | Own only | All |
| Update or cancel an appointment | Yes | No | Yes |
| Record diagnosis and visit notes | No | Yes | No |
| Read a patient's medical history | No | Own patients | No |
| Export authorised data to CSV | No | Yes | No |
| Manage user accounts and roles | No | No | Yes |

Only Receptionist should be able to edit appointments because if a doctor could do so they might start managing their appointments without notifying people.

The Administrator should not be able to read or modify a patient's medical records because that information is private and not relevant to the administrator's job

The Administrator should not be able to export even authorized patient data because that's not something relevant to his job.

## 4. Product backlog
### US-01 — Register a patient
**As a receptionist, I want to register a patient so that their details are stored in the system.**

- Receptionist can enter patient details.
- Required fields must be completed.
- A patient record is created.

### US-02 — Schedule an appointment
**As a receptionist, I want to schedule an appointment so that patients can see a doctor.**

- Select patient, doctor, date, and time.
- Prevent double bookings.
- Confirm the appointment.

### US-03 — Record visit notes
**As a doctor, I want to record diagnosis and visit notes so that the patient's record is up to date.**

- Doctor can enter diagnosis and notes.
- Notes are linked to the patient.
- Notes are saved with the visit date.

### US-04 — View appointments
**As a doctor, I want to view my appointments so that I know which patients I need to see.**

- Doctor can view their appointments.
- Patient, date, and time are shown.
- Doctor cannot view other doctors' appointments.

### US-05 — Search for a patient
**As a receptionist, I want to search for a patient so that I can quickly find their record.**

- Search by name or patient ID.
- Matching patients are displayed.
- Receptionist can open a record.

### US-06 — View medical history
**As a doctor, I want to view my patients' medical history so that I have relevant information during a visit.**

- Doctor can view their patients' history.
- Previous diagnoses and notes are shown.
- Other patients' histories are restricted.

### US-07 — Update or cancel an appointment
**As a receptionist, I want to update or cancel appointments so that the schedule stays accurate.**

- Change appointment date or time.
- Cancel an appointment.
- Schedule updates immediately.

### US-08 — Deactivate a patient
**As a receptionist, I want to deactivate a patient record so that inactive patients are clearly identified.**

- Receptionist can deactivate a record.
- Confirmation is required.
- Record remains stored as inactive.

### US-09 — Register a doctor
**As an administrator, I want to register a doctor so that they can use the system.**

- Enter doctor details.
- Create a doctor account.
- Assign the doctor role.

### US-10 — Manage users and roles
**As an administrator, I want to manage user accounts and roles so that users have the correct access.**

- Create and deactivate accounts.
- Assign roles.
- Access follows the assigned role.

### US-11 — Export data to CSV
**As a doctor, I want to export authorised data to CSV so that I can use it for permitted purposes.**

- Export only authorised data.
- Generate a CSV file.
- Exclude unauthorised information.

### US-12 — Deactivate a doctor
**As an administrator, I want to deactivate a doctor so that they can no longer access the system.**

- Deactivate the doctor account.
- Prevent login.
- Keep existing records.

| Priority | ID | Story | Role |
|---:|---|---|---|
| 1 | US-01 | Register a patient | Receptionist |
| 2 | US-02 | Schedule an appointment | Receptionist |
| 3 | US-03 | Record visit notes | Doctor |
| 4 | US-04 | View appointments | Doctor |
| 5 | US-05 | Search for a patient | Receptionist |
| *6* | US-06 | View medical history | Doctor |
| *7* | US-07 | Update or cancel appointment | Receptionist |
| 8 | US-08 | Deactivate a patient | Receptionist |
| 9 | US-09 | Register a doctor | Administrator |
| 10 | US-10 | Manage users and roles | Administrator |
| 11 | US-11 | Export data to CSV | Doctor |
| 12 | US-12 | Deactivate a doctor | Administrator |

### Top-three justification

The first three stories cover the basic patient workflow: registering a patient, booking an appointment, and recording the visit. They provide the core functionality needed for a patient visit before adding additional features.

## 5. Process and ceremonies

We will use 2-week sprints because they provide enough time to complete useful features while allowing regular feedback.

### Sprint Plan
| Sprint | What we will deliver |
|---|---|
| Sprint 1 | Patient registration, patient search, and appointment scheduling |
| Sprint 2 | View, update, and cancel appointments |
| Sprint 3 | Record diagnosis, visit notes, and view medical history |
| Sprint 4 | User accounts, roles, doctor management, and CSV export |

### Sprint Ceremonies
| Ceremony | When | What we do | Output |
|---|---|---|---|
| Sprint Planning | Start of each sprint | Select stories and split them into tasks | Sprint backlog |
| Daily Stand-up | Every day | Discuss progress, plans, and blockers | Updated task board |
| Sprint Review | End of sprint | Demonstrate completed features | Feedback |
| Sprint Retrospective | After review | Discuss what went well and what to improve | Improvement actions |

### Backlog Refinement Triggers
- A story is unclear or missing acceptance criteria.
- A story is too large for one sprint.
- Requirements or priorities change.
- New information is discovered during development.
- A story is approaching the top of the backlog.
