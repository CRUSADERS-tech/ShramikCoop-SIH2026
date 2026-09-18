# ShramikCoop — System Architecture & API

**Team:** CRUSADERS  
**Hackathon:** Smart India Hackathon 2026  
**Problem Statement:** SIH26089  
**Theme:** Smart Automation

## 1. Platform Overview

ShramikCoop is a cooperative gig-services platform connecting customers with verified local service workers.

The MVP demonstrates an end-to-end service transaction:

Customer Request  
→ Worker Matching  
→ Job Offer  
→ Worker Acceptance  
→ Travel  
→ Work Started  
→ Completion  
→ Customer Confirmation  
→ Settlement

## 2. Core Architecture

```text
                         SHRAMIKCOOP

                        Customer App
                             |
                             | REST API
                             v
                    +-------------------+
                    |   FastAPI Backend  |
                    +-------------------+
                       |       |       |
                       |       |       |
                       v       v       v
                  PostgreSQL Redis  Settlement
                       |
                       |
             +---------+---------+
             |                   |
             v                   v
       Worker Flutter App    Asterisk IVR
                                  |
                                  | SIP / PJSIP
                                  |
                             Feature Phone
3. MVP Components
Customer App

Used for:

Service request creation
Job tracking
Customer confirmation
Settlement initiation
Viewing payment breakdown
Worker App

Used for:

Worker profile
Availability
New job offers
Accept / refuse
Active job progression
Earnings
Settlement history
FastAPI Backend

Provides the core service APIs for:

Workers
Jobs
Matching
Job progression
Customer confirmation
Settlement
PostgreSQL

Stores the core transactional data:

Workers
Jobs
Settlements
Redis

Used as the platform caching / coordination layer for scalable backend workflows.

Asterisk IVR

Provides feature-phone / SIP access for workers.

The MVP supports:

English
Tamil
Hindi

Workers can select a language using DTMF and accept or refuse a job using keypad input.

4. Job State Machine
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

Alternative states:

REJECTED
TIMEOUT
CANCELLED
DISPUTED
MEDIATION
FINAL_SETTLEMENT
5. REST API Index
Health
GET /

Returns basic API status and version information.

Workers
GET /api/v1/workers/{worker_id}/earnings

Returns worker earnings, pending amount, settled amount and settlement history.

Jobs
POST /api/v1/jobs/

Creates a new service request.

POST /api/v1/jobs/{job_id}/match

Matches an available worker based on the required skill.

POST /api/v1/jobs/{job_id}/accept

Accepts an offered job.

POST /api/v1/jobs/{job_id}/travel

Updates the job to travelling.

POST /api/v1/jobs/{job_id}/start

Starts the job.

POST /api/v1/jobs/{job_id}/complete

Marks work as completed and pending customer confirmation.

POST /api/v1/jobs/{job_id}/confirm

Records customer confirmation.

POST /api/v1/jobs/{job_id}/settle

Creates the settlement and records the payment allocation.

GET /api/v1/jobs/{job_id}

Returns the current job state.

GET /api/v1/jobs/{job_id}/settlement

Returns the settlement details for a job.

GET /api/v1/jobs/worker/{worker_id}/offers

Returns available job offers for a worker.

6. Settlement Model

For the MVP transaction:

Customer Payment        100%
Worker                    95%
Cooperative Welfare        3%
Infrastructure             2%

Example:

Customer pays             ₹1000
Worker receives             ₹950
Cooperative welfare          ₹30
Infrastructure               ₹20

The settlement model is designed around cooperative ownership and transparent allocation.

7. Voice IVR Flow
Incoming Call
      |
      v
Language Selection
      |
      +---- 4 → English
      |
      +---- 5 → Tamil
      |
      +---- 6 → Hindi
                   |
                   v
               Job Offer
                   |
                   v
               Job Action
                /      \
               /        \
          1 → Accept   2 → Refuse
               |
               v
        Backend Job Update
               |
               v
       Confirmation Prompt

The MVP has been validated using an Asterisk SIP environment.

The multilingual IVR currently supports:

English
Tamil
Hindi

The Hindi flow has been validated end-to-end from language selection through job offer, job action selection, backend acceptance and confirmation.

8. Technology Stack
FastAPI
PostgreSQL
Redis
Flutter
Asterisk
SIP / PJSIP
Docker
REST APIs
9. Architecture and Integration Direction

The broader ShramikCoop architecture is designed to support:

Customer
   |
   v
ONDC / Customer Interface
   |
   v
ShramikCoop Platform
   |
   +----------------------+
   |                      |
   v                      v
Worker App             Voice IVR
   |                      |
   +----------+-----------+
              |
              v
        FastAPI Services
              |
       +------+------+
       |             |
       v             v
 PostgreSQL        Redis
       |
       v
Settlement / Escrow Layer

Future-scale integrations include:

ONDC integration
Bhashini-based speech processing
Blockchain-based escrow
Cooperative governance mechanisms
Production-scale telephony infrastructure
Advanced multilingual voice understanding

These components are documented as future / scale architecture unless explicitly marked as implemented.

10. Security and Privacy

The public repository contains documentation and judge-facing technical evidence.

Production credentials, passwords, private keys, environment files and other secrets must not be committed to the repository.

Examples of information that must remain private:

Database passwords
SIP passwords
API keys
Private keys
.env files
Production credentials
11. Implementation Status
Working MVP
Customer service request
Worker matching
Worker job offer
Worker acceptance / refusal
Job progression
Customer confirmation
95/3/2 settlement calculation
Worker earnings
Settlement history
Multilingual IVR
English IVR
Tamil IVR
Hindi IVR
IVR DTMF job acceptance
IVR to backend job acceptance integration
Future Scale Components
ONDC production integration
Bhashini speech processing
Blockchain escrow deployment
Cooperative governance mechanisms
Production-scale telephony
Advanced multilingual voice understanding
12. Evidence Scope

This document is the technical architecture and API documentation index for the ShramikCoop SIH 2026 project.

Additional judge-facing evidence will be maintained under:

docs/
contracts/
ivr/
infrastructure/

The repository is intended to provide transparent technical documentation for the ShramikCoop prototype and its Smart India Hackathon 2026 submission.
