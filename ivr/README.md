# ShramikCoop IVR Validation Evidence

This directory contains sandbox validation evidence for the ShramikCoop multilingual worker IVR.

## IVR scope

The MVP IVR provides a feature-phone based worker interaction flow using DTMF input.

Supported languages:

- English
- Tamil
- Hindi

Primary IVR extension:

- `100`

## Validated interaction flow

The sandbox validation covers:

1. Worker calls the IVR extension.
2. Language selection is presented.
3. Worker selects English, Tamil, or Hindi.
4. A job offer is played in the selected language.
5. Worker can accept or refuse the job using DTMF.
6. Accepting the job triggers the ShramikCoop backend job acceptance endpoint.
7. A confirmation prompt is played.
8. The call ends normally.

## Hindi end-to-end validation

The Hindi flow was specifically validated through MicroSIP:

```text
Call extension 100
        ↓
Language menu
        ↓
Press 6 — Hindi
        ↓
Hindi job offer
        ↓
Hindi job actions
        ↓
Press 1 — Accept
        ↓
Backend acceptance
        ↓
Hindi acceptance confirmation
        ↓
Call completed
Call-log evidence

The file:

microsip-call-log-anonymized.csv

contains an anonymized export of the MicroSIP call history used for sandbox validation.

Summary of the exported log:

Total exported records: 91
Completed calls: 90
Incorrect/non-existent dialing information: 1
Outgoing calls: 88
Incoming calls: 3

The public evidence copy removes SIP call IDs and phone numbers.

Privacy note

This repository copy is intended for technical demonstration and judging evidence.

The public CSV excludes:

SIP call IDs
Phone numbers
Production credentials

The log represents local/sandbox validation evidence and is not presented as production monitoring data.

Implementation notes

The IVR currently uses deterministic DTMF interaction for reliable MVP demonstration.

The architecture is designed to support future integration with:

Bhashini speech services
speech-to-text
local text-to-speech fallback
multilingual voice interaction
Related evidence
System architecture and API documentation: ../docs/architecture-api.md
Smart escrow design: ../contracts/escrow-design.md
PostgreSQL schema: ../docs/database-schema.md
Current implementation status

The multilingual IVR, job offer playback, DTMF accept/refuse flow, and backend acceptance integration have been validated in the local ShramikCoop sandbox.

This evidence should be interpreted as MVP/local validation rather than a claim of production telephony deployment.
