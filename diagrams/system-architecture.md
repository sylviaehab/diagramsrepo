# System Architecture Diagram

## Overview
This diagram illustrates the three-tier architecture of the Smart Attendance & Employee Management System, showing how the client layer, application layer, and data layer interact with each other.

## Architecture Layers

- **Client Layer**: User-facing portals (Admin and Employee)
- **Application Layer**: Core business logic services
- **Data Layer**: Database for persistent storage

## Diagram

```mermaid
graph TB
    subgraph "Client Layer"
        AP[Admin Portal]
        EP[Employee Portal]
    end
    
    subgraph "Application Layer"
        AUTH[Authentication Service]
        EMS[Employee Management Service]
        ATS[Attendance Tracking Service]
        LMS[Leave Management Service]
        PRS[Payroll Service]
        RS[Reporting Service]
    end
    
    subgraph "Data Layer"
        DB[(Database)]
    end
    
    AP --> AUTH
    EP --> AUTH
    
    AUTH --> EMS
    AUTH --> ATS
    AUTH --> LMS
    AUTH --> PRS
    AUTH --> RS
    
    EMS --> DB
    ATS --> DB
    LMS --> DB
    PRS --> DB
    RS --> DB
    
    style AP fill:#4CAF50
    style EP fill:#2196F3
    style DB fill:#FF9800
```

## Key Components

### Client Layer
- **Admin Portal**: Interface for administrators to manage the system
- **Employee Portal**: Interface for employees to track attendance and request leave

### Application Layer
- **Authentication Service**: Handles user login and authorization
- **Employee Management Service**: CRUD operations for employee records
- **Attendance Tracking Service**: Manages clock-in/out and attendance records
- **Leave Management Service**: Processes leave requests and approvals
- **Payroll Service**: Calculates salaries based on attendance
- **Reporting Service**: Generates various reports and exports

### Data Layer
- **Database**: Centralized data storage for all system information

## Data Flow
1. Users access the system through their respective portals
2. All requests pass through the Authentication Service
3. Authenticated requests are routed to appropriate services
4. Services interact with the database for data operations
5. Results are returned to the user through the portal