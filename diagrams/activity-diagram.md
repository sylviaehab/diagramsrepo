# Activity Diagram

## Overview
Activity diagrams show the workflow processes in the Smart Attendance & Employee Management System. This document includes activity diagrams for key processes.

## 1. Leave Request Process

```mermaid
flowchart TD
    Start([Employee Wants Leave]) --> A[Login to Portal]
    A --> B[Navigate to Leave Section]
    B --> C[Fill Leave Request Form]
    C --> D[Select Leave Type]
    D --> E[Enter Start & End Dates]
    E --> F[Provide Reason]
    F --> G{Check Leave Balance}
    
    G -->|Sufficient Balance| H[Submit Request]
    G -->|Insufficient Balance| I[Show Error Message]
    I --> End1([End - Request Not Submitted])
    
    H --> J[System Validates Request]
    J --> K{Validation Successful?}
    
    K -->|No| L[Show Validation Errors]
    L --> C
    
    K -->|Yes| M[Save Request to Database]
    M --> N[Notify Admin]
    N --> O[Update Request Status to 'Submitted']
    O --> P[Send Confirmation to Employee]
    
    P --> Q{Admin Reviews Request}
    
    Q -->|Approve| R[Update Status to 'Approved']
    Q -->|Reject| S[Update Status to 'Rejected']
    Q -->|Request More Info| T[Request Additional Details]
    
    R --> U[Deduct from Leave Balance]
    U --> V[Update Calendar]
    V --> W[Notify Employee - Approved]
    W --> End2([End - Leave Approved])
    
    S --> X[Notify Employee - Rejected]
    X --> End3([End - Leave Rejected])
    
    T --> Y[Notify Employee for Info]
    Y --> Z[Employee Provides Info]
    Z --> M
    
    style Start fill:#4ECDC4
    style End1 fill:#FF6B6B
    style End2 fill:#4CAF50
    style End3 fill:#FF6B6B
    style R fill:#4CAF50
    style S fill:#FF6B6B
```

## 2. Payroll Calculation Process

```mermaid
flowchart TD
    Start([Payroll Period Ends]) --> A[Admin Initiates Payroll]
    A --> B[Select Pay Period]
    B --> C[Fetch All Active Employees]
    C --> D{More Employees?}
    
    D -->|Yes| E[Get Next Employee]
    D -->|No| T[Generate Payroll Summary]
    
    E --> F[Retrieve Attendance Records]
    F --> G[Calculate Days Present]
    G --> H[Calculate Days Absent]
    H --> I[Get Base Salary]
    I --> J[Calculate Gross Salary]
    
    J --> K[Calculate Tax Deductions]
    K --> L[Calculate Other Deductions]
    L --> M[Calculate Net Salary]
    
    M --> N[Create Payroll Record]
    N --> O[Save to Database]
    O --> P[Generate Pay Slip]
    P --> Q{Errors?}
    
    Q -->|Yes| R[Log Error & Skip]
    Q -->|No| S[Mark as Processed]
    
    R --> D
    S --> D
    
    T --> U[Review Summary]
    U --> V{Approve Payroll?}
    
    V -->|No| W[Make Adjustments]
    W --> E
    
    V -->|Yes| X[Mark Payroll as Final]
    X --> Y[Send Pay Slips to Employees]
    Y --> Z[Export Report]
    Z --> End([End - Payroll Completed])
    
    style Start fill:#6C5CE7
    style End fill:#6C5CE7
    style J fill:#00B894
    style M fill:#00B894
    style X fill:#4CAF50
```

## 3. Employee Attendance Tracking

```mermaid
flowchart TD
    Start([Employee Arrives at Work]) --> A[Open Employee Portal]
    A --> B[Login with Credentials]
    B --> C{Login Successful?}
    
    C -->|No| D[Show Error Message]
    D --> B
    
    C -->|Yes| E[Navigate to Attendance]
    E --> F[Click 'Clock In' Button]
    F --> G[System Captures Timestamp]
    G --> H{Already Clocked In?}
    
    H -->|Yes| I[Show Error: Already Clocked In]
    I --> End1([End])
    
    H -->|No| J[Create Attendance Record]
    J --> K[Save Clock-In Time]
    K --> L[Display Confirmation]
    L --> M[Show Current Status]
    
    M --> N{Work Day Complete?}
    N -->|No| O[Continue Working]
    O --> N
    
    N -->|Yes| P[Click 'Clock Out' Button]
    P --> Q[System Captures Timestamp]
    Q --> R{Valid Clock-In Exists?}
    
    R -->|No| S[Show Error: No Clock-In Found]
    S --> End2([End])
    
    R -->|Yes| T[Update Attendance Record]
    T --> U[Save Clock-Out Time]
    U --> V[Calculate Hours Worked]
    V --> W[Update Database]
    W --> X[Display Summary]
    X --> Y[Show Total Hours]
    Y --> End3([End - Attendance Recorded])
    
    style Start fill:#4ECDC4
    style End1 fill:#FFA726
    style End2 fill:#FF6B6B
    style End3 fill:#4CAF50
    style V fill:#00B894
```

## 4. Employee Onboarding Process

```mermaid
flowchart TD
    Start([New Employee Hired]) --> A[Admin Logs In]
    A --> B[Navigate to Employee Management]
    B --> C[Click 'Add New Employee']
    C --> D[Fill Employee Details Form]
    
    D --> E[Enter Personal Info]
    E --> F[Enter Contact Info]
    F --> G[Set Hire Date]
    G --> H[Set Base Salary]
    H --> I[Assign Role]
    I --> J{Validate Form}
    
    J -->|Invalid| K[Show Validation Errors]
    K --> D
    
    J -->|Valid| L[Save Employee Record]
    L --> M[Generate Employee ID]
    M --> N[Create User Account]
    N --> O[Generate Login Credentials]
    
    O --> P[Initialize Leave Balance]
    P --> Q[Set Default Permissions]
    Q --> R[Send Welcome Email]
    R --> S[Email Login Credentials]
    
    S --> T{Email Sent Successfully?}
    
    T -->|No| U[Log Error & Notify Admin]
    T -->|Yes| V[Update Status to 'Active']
    
    U --> V
    V --> W[Add to Payroll System]
    W --> X[Display Success Message]
    X --> End([End - Employee Onboarded])
    
    style Start fill:#6C5CE7
    style End fill:#4CAF50
    style V fill:#00B894
```

## Process Descriptions

### Leave Request Process
This workflow shows how employees request leave and how administrators process those requests. Key decision points include leave balance validation and admin approval.

**Key Steps:**
1. Employee submits leave request with details
2. System validates request and checks balance
3. Admin reviews and approves/rejects
4. System updates leave balance and notifies employee

### Payroll Calculation Process
This workflow illustrates the automated payroll calculation for all employees based on attendance records.

**Key Steps:**
1. Admin initiates payroll for pay period
2. System processes each employee individually
3. Calculates gross salary, deductions, and net salary
4. Generates pay slips and reports
5. Admin reviews and approves final payroll

### Attendance Tracking Process
This workflow shows the daily clock-in and clock-out process for employees.

**Key Steps:**
1. Employee logs in to portal
2. Clicks clock-in at start of day
3. System records timestamp
4. Employee clicks clock-out at end of day
5. System calculates total hours worked

### Employee Onboarding Process
This workflow shows how administrators add new employees to the system.

**Key Steps:**
1. Admin enters employee details
2. System creates employee record and user account
3. Generates login credentials
4. Initializes leave balance
5. Sends welcome email to employee

## Decision Points

- **Leave Balance Check**: Ensures employee has sufficient leave days
- **Validation Checks**: Ensures data integrity throughout processes
- **Admin Approval**: Manual review point for leave requests
- **Error Handling**: Proper error handling at critical points

## Parallel Activities

Some processes can occur in parallel:
- Sending notifications while updating database
- Generating reports while processing next employee
- Creating user account while initializing leave balance
