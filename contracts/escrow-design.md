# ShramikCoop — Smart Escrow Design

**Team:** CRUSADERS  
**Hackathon:** Smart India Hackathon 2026  
**Problem Statement:** SIH26089  
**Theme:** Smart Automation

## 1. Purpose

ShramikCoop is designed with a cooperative settlement architecture in which a
customer payment can be held until the service transaction reaches the required
completion and confirmation conditions.

The long-term architecture uses an EVM-compatible smart contract / escrow layer
for transparent settlement.

The current MVP demonstrates the escrow and settlement logic at the application
layer. The production blockchain contract is a future-scale component and is not
claimed as deployed in the current MVP.

## 2. Escrow Concept

The intended transaction flow is:

```text
Customer Payment
       |
       v
   Escrow Layer
       |
       v
 Worker completes job
       |
       v
 Customer confirms completion
       |
       v
 Settlement released
       |
       +------------------+
       |                  |
       v                  v
 Worker             Cooperative
  95%                   3%
                         |
                         +---- Infrastructure 2%

The escrow layer is intended to prevent settlement from being released before the
required service-completion conditions are satisfied.

3. Settlement Model

ShramikCoop uses the following allocation model:

Customer Payment       100%
Worker                  95%
Cooperative Welfare      3%
Infrastructure           2%

For a ₹1000 customer payment:

Worker                 ₹950
Cooperative Welfare      ₹30
Infrastructure           ₹20
Total                  ₹1000

The allocation is represented explicitly in the application settlement model.

4. Proposed EVM Escrow Lifecycle

The future smart-contract lifecycle is designed around these states:

CREATED
   |
   v
FUNDED
   |
   v
JOB_ACCEPTED
   |
   v
JOB_IN_PROGRESS
   |
   v
COMPLETION_PENDING
   |
   v
CUSTOMER_CONFIRMED
   |
   v
RELEASED
   |
   v
SETTLED

Exceptional conditions may include:

CANCELLED
DISPUTED
MEDIATION
REFUNDED
5. Proposed Contract Responsibilities

A future Solidity escrow contract would be responsible for:

Deposit

Record the amount associated with a service transaction.

Job Association

Associate the escrow record with a unique ShramikCoop job identifier.

Completion Condition

Prevent final release until the service reaches the required completion and
customer-confirmation state.

Settlement Allocation

Calculate or enforce the agreed settlement distribution:

95% → Worker
3%  → Cooperative Welfare
2%  → Infrastructure
Release

Release the escrowed amount only after the required conditions are satisfied.

Dispute Handling

Support a future dispute / mediation pathway instead of automatically releasing
funds when a transaction is contested.

6. Proposed Contract Interface

A future implementation may expose functions conceptually similar to:

createEscrow()
fundEscrow()
markJobAccepted()
markCompletionPending()
confirmCompletion()
releaseEscrow()
openDispute()
resolveDispute()
refundEscrow()

The exact Solidity interface will be finalized during the blockchain implementation
phase.

7. Application-Level MVP Settlement

The current MVP already demonstrates the settlement workflow at the backend
application layer.

The transaction flow is:

Customer creates job
       |
       v
Worker matched
       |
       v
Worker accepts
       |
       v
Job progresses
       |
       v
Worker completes
       |
       v
Customer confirms
       |
       v
Settlement created
       |
       v
95 / 3 / 2 allocation recorded

The backend provides settlement information associated with the job and worker
earnings.

8. Blockchain Integration Direction

The intended production architecture is:

Customer App
      |
      v
ShramikCoop Backend
      |
      +----------------------+
      |                      |
      v                      v
PostgreSQL              EVM Escrow
      |                      |
      |                      v
      |                 Settlement
      |                      |
      +----------+-----------+
                 |
                 v
            Worker App

The backend remains responsible for application workflow and transaction state,
while the future blockchain layer can provide an independently verifiable
settlement record.

9. Transparency Model

The proposed escrow architecture is intended to make important settlement events
verifiable:

Job ID
  |
  +-- Escrow created
  |
  +-- Funding recorded
  |
  +-- Completion confirmed
  |
  +-- Settlement released
  |
  +-- Worker allocation
  |
  +-- Cooperative allocation
  |
  +-- Infrastructure allocation

This supports transparent cooperative settlement rather than relying solely on
private internal records.

10. Security Considerations

A production smart-contract implementation must address:

Access control
Unauthorized settlement attempts
Replay protection
Reentrancy protection
Integer / arithmetic safety
Dispute handling
Refund conditions
Contract upgrade strategy
Emergency controls
Wallet and key management
Transaction verification

The contract must be independently tested and audited before handling real
customer funds.

11. Current Implementation Status
Implemented in MVP
Application-level settlement workflow
Job completion state
Customer confirmation state
Worker earnings calculation
95/3/2 settlement allocation
Settlement record associated with a job
Worker settlement history
Future Implementation
Solidity escrow contract
EVM deployment
On-chain escrow funding
On-chain settlement release
On-chain dispute resolution
Blockchain transaction verification
Production wallet/key management

No deployed smart-contract address is claimed by this document.

12. Evidence Policy

This document describes the planned EVM smart-escrow architecture and the
application-level escrow/settlement implementation currently demonstrated by the
MVP.

Actual Solidity source code and a deployed contract address will be added to this
repository only after the blockchain implementation is completed and verified.
