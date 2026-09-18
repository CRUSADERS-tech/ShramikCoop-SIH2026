# ShramikCoop — PostgreSQL Database Schema

**Team:** CRUSADERS  
**Hackathon:** Smart India Hackathon 2026  
**Problem Statement:** SIH26089  
**Theme:** Smart Automation

## 1. Purpose

ShramikCoop uses PostgreSQL as the primary transactional database for the MVP.

The database stores the core entities required to execute a cooperative gig-service
transaction:

- Workers
- Jobs
- Settlements

The schema is designed around the service-job lifecycle and transparent settlement
records.

## 2. Current MVP Schema

```text
+---------------------------+
|          workers          |
+---------------------------+
| id              PK        |
| worker_id       UNIQUE    |
| name                      |
| phone           UNIQUE    |
| primary_skill             |
| verification_level       |
| is_available              |
+-------------+-------------+
              |
              | worker_id
              |
              v
+---------------------------+
|           jobs            |
+---------------------------+
| id              PK        |
| job_id          UNIQUE    |
| customer_name             |
| customer_phone            |
| required_skill            |
| description               |
| location                  |
| customer_price            |
| worker_payout             |
| status                    |
| worker_id                 |
+-------------+-------------+
              |
              | job_id
              |
              v
+---------------------------+
|       settlements         |
+---------------------------+
| id              PK        |
| job_id          FK UNIQUE |
| total_amount              |
| worker_amount             |
| cooperative_amount        |
| infrastructure_amount    |
| status                    |
+---------------------------+
3. Worker Entity

The workers table represents workers registered on the platform.

Fields
Field	Type	Description
id	Integer	Primary database identifier
worker_id	String	Public worker identifier
name	String	Worker name
phone	String	Worker phone number
primary_skill	String	Main service skill
verification_level	String	Worker verification state
is_available	Boolean	Current availability
Current verification state

The MVP supports verification information through the worker profile and
verification_level field.

Example:

REGISTERED
VERIFIED

The exact verification workflow can be extended as the platform scales.

4. Job Entity

The jobs table represents customer service requests and their lifecycle.

Fields
Field	Type	Description
id	Integer	Primary database identifier
job_id	String	Unique public job identifier
customer_name	String	Customer name
customer_phone	String	Customer contact number
required_skill	String	Required worker skill
description	String	Service request description
location	String	Service location
customer_price	Integer	Customer payment amount
worker_payout	Integer	Worker allocation
status	String	Current job state
worker_id	String	Matched worker identifier
5. Job Lifecycle

The database status field represents the current position of a job in the
application workflow.

REQUESTED
    |
    v
MATCHING
    |
    v
OFFERED
    |
    v
ACCEPTED
    |
    v
TRAVELLING
    |
    v
IN_PROGRESS
    |
    v
COMPLETION_PENDING
    |
    v
CUSTOMER_CONFIRMATION
    |
    v
COMPLETED
    |
    v
ESCROW_RELEASED
    |
    v
SETTLED

Additional states may include:

REJECTED
TIMEOUT
CANCELLED
DISPUTED
MEDIATION
FINAL_SETTLEMENT
6. Settlement Entity

The settlements table stores the final allocation associated with a job.

Fields
Field	Type	Description
id	Integer	Primary database identifier
job_id	String	Associated job identifier
total_amount	Integer	Total customer payment
worker_amount	Integer	Worker allocation
cooperative_amount	Integer	Cooperative welfare allocation
infrastructure_amount	Integer	Infrastructure allocation
status	String	Settlement state

The job_id field is unique in the settlement table so that a job has one
corresponding settlement record in the current MVP model.

7. Settlement Calculation

The MVP uses the cooperative allocation model:

Customer Payment       100%
Worker                  95%
Cooperative Welfare      3%
Infrastructure           2%

Example transaction:

Customer Payment       ₹1000
Worker Allocation       ₹950
Cooperative Welfare      ₹30
Infrastructure           ₹20

The values are stored explicitly in the settlement record.

8. Entity Relationship

Conceptually:

WORKER
  |
  | worker_id
  |
  v
JOB
  |
  | job_id
  |
  v
SETTLEMENT

A worker can participate in multiple jobs over time.

A completed job can have one settlement record in the current MVP.

9. Data Flow
Customer
   |
   v
Create Job
   |
   v
jobs
   |
   v
Worker Matching
   |
   v
worker_id assigned
   |
   v
Worker Accepts
   |
   v
Job Progression
   |
   v
Customer Confirmation
   |
   v
Settlement Created
   |
   v
settlements
10. Transactional Consistency

The database is used as the source of truth for the MVP transaction lifecycle.

Important transaction records include:

Unique worker identifiers
Unique job identifiers
Worker-job assignment
Job status
Customer payment amount
Worker payout
Settlement allocation
Settlement status

The application layer controls valid state transitions before settlement is
recorded.

11. Privacy and Sensitive Data

The database contains customer and worker contact information required for
service operations.

Production deployments must apply appropriate controls for:

Access management
Encryption in transit
Encryption at rest
Credential management
Data retention
Audit logging
Personal-data protection

The public repository must never contain production database credentials,
passwords, connection strings containing secrets, or customer/worker personal
records.

12. Multi-Tenant Architecture Direction

The current MVP uses a single application database schema.

For future production-scale deployment, the database can be extended to support
multiple cooperative or regional tenants.

A possible future model is:

+---------------------------+
|          tenants          |
+---------------------------+
| id              PK        |
| tenant_code     UNIQUE    |
| name                      |
| region                    |
+-------------+-------------+
              |
       +------+------+
       |             |
       v             v
   workers         jobs
       |             |
       +------+------+
              |
              v
        settlements

Tenant-aware records can then carry a tenant_id and appropriate database
access controls can be applied.

This multi-tenant design is a future-scale architecture and is not claimed as
fully implemented in the current MVP.

13. Technology

Current database technology:

PostgreSQL

The application accesses PostgreSQL through the FastAPI backend.

The database is containerized as part of the local development environment.

14. Implementation Status
Implemented
PostgreSQL database
Worker table
Job table
Settlement table
Worker/job association
Job lifecycle status
Settlement records
95/3/2 allocation fields
Worker earnings derived from settlement data
Future Scale
Multi-tenant database isolation
Advanced audit logging
Database-level tenant policies
Production encryption strategy
Automated retention policies
Analytics warehouse
Geographic partitioning / sharding where required
15. Evidence Scope

This document describes the PostgreSQL schema used by the ShramikCoop MVP and
the planned direction for multi-tenant production scaling.

Additional database diagrams can be added to this repository as the architecture
is expanded.
