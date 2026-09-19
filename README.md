# ShramikCoop — SIH 2026

**Open-Source Platform Cooperative Infrastructure & Distributed Ledger Escrow Rails for Unorganized Workforce Pools**

**Team CRUSADERS**  
**Smart India Hackathon 2026**  
**Problem Statement ID: SIH26089**  
**Problem Statement: Cooperative Gig Services Platform for Household & Community Services**  
**Theme: Smart Automation**

---

## About ShramikCoop

ShramikCoop is a **platform-cooperative infrastructure layer for unorganized blue-collar workforce pools**.

It is not simply a service-booking application.

The core idea is to provide workers with a common cooperative digital infrastructure that connects:

- Customers and open-network commerce
- Verified local workers
- Smartphone and feature-phone access
- Multilingual voice/IVR interaction
- Automated job matching and lifecycle management
- Transparent cooperative settlement
- Welfare contribution mechanisms
- Auditable distributed-ledger escrow architecture

The smartphone application, customer interface, and worker IVR are **access channels to the same underlying platform and business logic**.

---

# Core Architecture

The ShramikCoop platform is organized as a common backend infrastructure layer with multiple worker and customer access channels.

### Customer / Open Commerce

Customer-side discovery and service interaction can operate through customer applications and ONDC-oriented open-network integration.

### ShramikCoop Core

The common platform layer provides:

- FastAPI backend
- Job lifecycle management
- Worker matching
- Job state transitions
- Settlement calculation
- Worker earnings
- Customer confirmation
- Cooperative settlement logic

### Worker Access Channels

Workers can access the same platform through:

- Smartphone application
- Feature phone
- Multilingual IVR
- English
- Tamil
- Hindi

### Data and Infrastructure Layer

The MVP uses:

- PostgreSQL
- Redis
- Asterisk
- HAProxy

### Settlement Layer

The cooperative settlement model distributes the customer payment as:

- 95% Worker
- 3% Cooperative Welfare
- 2% Infrastructure

The architecture is designed to support future distributed-ledger and EVM escrow integration.

---

# Judge Evidence & Verification

The following links provide direct access to the project's architecture, technical evidence, validation records, and working prototype.

## 1. System Architecture & API Documentation

[Open Architecture & API Documentation](docs/architecture-api.md)

Contains the implemented system architecture, platform components, job state machine, REST API endpoint index, IVR flow, technology stack, implementation status, security/privacy considerations, and future integration direction.

---

## 2. Smart Escrow Contract Architecture

[Open Smart Escrow Architecture & Settlement Design](contracts/escrow-design.md)

Documents the proposed Polygon/EVM smart escrow lifecycle, cooperative settlement model, contract responsibilities, transparency model, security considerations, and future on-chain integration.

**Important:** The current MVP demonstrates settlement at the application layer. A deployed smart-contract address is not claimed.

---

## 3. PostgreSQL Database Schema

[Open PostgreSQL Database Schema Documentation](docs/database-schema.md)

Documents the implemented PostgreSQL MVP schema covering:

- Workers
- Jobs
- Settlements
- Relationships
- Job lifecycle
- Settlement calculations
- Privacy considerations
- Current implementation
- Future multi-tenant architecture direction

---

## 4. Multilingual IVR Validation Evidence

[Open Multilingual IVR Validation Evidence](ivr/README.md)

Contains anonymized MicroSIP validation evidence for the local telephony sandbox.

The demonstrated IVR supports:

- English
- Tamil
- Hindi
- DTMF language selection
- Worker job offer playback
- Accept / refuse actions
- Backend job-acceptance integration

### Validated Hindi Flow

Language selection  
↓  
Hindi job offer  
↓  
Job action prompt  
↓  
Worker acceptance  
↓  
Backend job update  
↓  
Acceptance confirmation

The IVR evidence represents local/sandbox validation rather than production telephony monitoring.

The public evidence copy excludes SIP call IDs and phone numbers.

---

## 5. Working Prototype Demonstration

[Open Working Prototype Demo](demo/README.md)

The recorded MVP demonstrates the complete end-to-end service transaction:

Customer request  
↓  
Worker matching  
↓  
Worker job offer  
↓  
Worker acceptance  
↓  
Travel  
↓  
Work started  
↓  
Work completed  
↓  
Customer confirmation  
↓  
Settlement

### Settlement Demonstration

For a ₹1000 customer payment:

| Allocation | Amount |
|---|---:|
| Worker payout | ₹950 |
| Cooperative welfare | ₹30 |
| Infrastructure | ₹20 |
| **Total** | **₹1000** |

The demonstration uses separate customer and worker interfaces while both operate against the same backend transaction state.

The working prototype demonstrates the MVP application-layer settlement flow.

---

## 6. Official Smart India Hackathon Registry

[Open Official Smart India Hackathon Portal](https://www.sih.gov.in/)

**Problem Statement ID:** `SIH26089`

The official SIH portal is provided as the authoritative registry destination.

A specific deep-link is not claimed unless independently verified.

---

# Cooperative Settlement Model

ShramikCoop uses the following MVP settlement model:

**Customer Payment → 95% Worker + 3% Cooperative Welfare + 2% Infrastructure**

For a ₹1000 customer payment:

| Allocation | Percentage | Example |
|---|---:|---:|
| Worker | 95% | ₹950 |
| Cooperative Welfare | 3% | ₹30 |
| Infrastructure | 2% | ₹20 |
| **Total** | **100%** | **₹1000** |

The design aims to keep the worker payout transparent while creating a cooperative welfare contribution and a defined infrastructure allocation.

The application-layer MVP calculates and records this distribution through the backend settlement workflow.

The distributed-ledger escrow architecture is documented separately for future EVM integration.

---

# Worker Access Model

ShramikCoop is designed around **multiple access channels rather than a single application interface**.

## Smartphone

The worker application provides:

- Job offers
- Acceptance / refusal
- Active job progression
- Earnings visibility
- Profile and verification
- Job history

## Feature Phone / Voice

Multilingual IVR provides access for workers who may not depend on smartphones or text-heavy interfaces.

### Current MVP Languages

- Tamil
- English
- Hindi

The same worker language selection is used across the worker application and IVR architecture.

## Open Network Direction

The architecture is designed to integrate customer-side discovery and service lifecycle flows with **ONDC-oriented open commerce infrastructure**.

---

# Mesthri-as-a-Hub

The architecture supports a **Mesthri-as-a-Hub** model for local workforce coordination.

The Mesthri role is intended for:

- Worker onboarding
- Local verification support
- Workforce coordination
- Operational assistance
- Local workforce support

The Mesthri does **not** control worker pricing, customer payments, or cooperative settlement.

The platform retains the common business logic and settlement rules.

---

# Job Lifecycle

The implemented MVP job lifecycle is:

REQUESTED  
↓  
MATCHING  
↓  
OFFERED  
↓  
ACCEPTED  
↓  
TRAVELLING  
↓  
IN_PROGRESS  
↓  
COMPLETION_PENDING  
↓  
CUSTOMER_CONFIRMATION  
↓  
COMPLETED  
↓  
ESCROW_RELEASED  
↓  
SETTLED

Alternative states include:

- REJECTED
- TIMEOUT
- CANCELLED
- DISPUTED
- MEDIATION
- FINAL_SETTLEMENT

The lifecycle is shared by the customer-side and worker-side interactions through the common backend.

---

# Multilingual Worker Access

The worker access layer uses a shared language model across the worker application and IVR.

Current supported language codes:

| Language | Code |
|---|---|
| Tamil | `ta` |
| English | `en` |
| Hindi | `hi` |

The selected language controls worker-facing UI and IVR prompts.

The current IVR MVP uses deterministic DTMF language selection.

The broader architecture can support future speech recognition and multilingual voice automation.

---

# Voice / IVR Architecture

The current telephony sandbox uses Asterisk for worker voice interaction.

The MVP IVR flow is:

Incoming worker call  
↓  
Language selection  
↓  
Job offer playback  
↓  
Accept / Refuse selection  
↓  
Backend job action  
↓  
Confirmation prompt  
↓  
Call completion

The current MVP validates English, Tamil, and Hindi worker interaction.

Future versions can integrate speech recognition and multilingual voice services such as Bhashini-oriented language infrastructure.

---

# Customer and Worker Transaction Model

The customer-side and worker-side interfaces operate against the same backend transaction state.

A typical transaction is:

Customer requests service  
↓  
Backend creates job  
↓  
Worker matching  
↓  
Worker receives offer  
↓  
Worker accepts  
↓  
Worker travels  
↓  
Work begins  
↓  
Work completes  
↓  
Customer confirms completion  
↓  
Settlement is calculated  
↓  
95 / 3 / 2 distribution is recorded  
↓  
Worker earnings become visible

This common transaction model allows different access channels to participate in the same cooperative workflow.

---

# Key Technology

- FastAPI
- PostgreSQL
- Redis
- Flutter
- Asterisk
- HAProxy
- Multilingual voice / IVR architecture
- ONDC-oriented commerce integration
- Polygon / EVM escrow architecture
- REST API
- Cooperative settlement logic

---

# MVP Implementation Status

The current MVP demonstrates:

- Customer service request
- Worker matching
- Worker job offer
- Worker acceptance
- Job travel state
- Work started state
- Work completed state
- Customer confirmation
- 95 / 3 / 2 settlement
- Worker earnings visibility
- Multilingual worker IVR
- Backend integration between IVR and job lifecycle
- Separate customer and worker interfaces
- End-to-end transaction demonstration

The escrow smart-contract layer and broader open-network integrations are documented as architecture / future integration components where they are not yet deployed in the MVP.

The current MVP should therefore be understood as a working application-layer demonstration of the broader ShramikCoop cooperative infrastructure architecture.

---

# Security & Privacy Direction

The platform architecture considers:

- Tokenized worker identity representation
- Privacy-aware data handling
- Anonymized public IVR evidence
- Separation of application data from future ledger records
- Controlled access to worker information
- Auditable settlement records

The current repository does not expose production credentials, private keys, SIP credentials, or sensitive worker/customer identifiers.

---

# Repository Structure

```text
ShramikCoop-SIH2026/
│
├── backend/
│   └── FastAPI backend
│
├── frontend/
│   └── Worker Flutter application
│
├── customer_app/
│   └── Customer application
│
├── infrastructure/
│   └── Infrastructure configuration
│
├── contracts/
│   └── Smart escrow architecture and settlement design
│
├── docs/
│   ├── Architecture and API documentation
│   └── PostgreSQL database schema
│
├── ivr/
│   ├── Multilingual IVR validation evidence
│   └── Anonymized MicroSIP call log
│
└── demo/
    ├── Working prototype demo documentation
    └── Working prototype demonstration video

Implementation Boundaries

The repository distinguishes between what is demonstrated in the MVP and what is part of the future-scale architecture.

Demonstrated in MVP
Customer transaction flow
Worker application
Worker matching
Job lifecycle
Customer confirmation
Application-layer settlement
95 / 3 / 2 distribution
Worker earnings
Multilingual IVR
Backend IVR integration
Local telephony validation
Recorded working prototype
Architecture / Future Integration
Deployed Polygon/EVM smart escrow
Production ONDC integration
Distributed ledger settlement
Large-scale telephony deployment
Advanced speech recognition
Production-scale multilingual voice automation
Broader cooperative governance infrastructure

This distinction is maintained so that the repository does not claim deployed infrastructure that is currently represented as architecture or future integration.

Why ShramikCoop

ShramikCoop focuses on infrastructure for worker-owned digital participation, rather than only providing another service marketplace.

The platform architecture brings together:

Open-network commerce
Cooperative workforce organization
Multichannel worker access
Voice-first participation
Automated job lifecycle
Transparent settlement
Welfare allocation
Auditable financial architecture

The goal is to provide a reusable cooperative infrastructure layer that can support different unorganized workforce pools and community service categories.
