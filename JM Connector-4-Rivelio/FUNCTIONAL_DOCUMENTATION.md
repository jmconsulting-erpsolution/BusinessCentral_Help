# Functional Documentation

Status: Completed
Date: 2026-05-19
Feature: JM Connector-4-Rivelio

## 1) Business Goal
Provide a production-ready integration between Microsoft Dynamics 365 Business Central and Rivelio so users can import files, process them asynchronously, retrieve outputs, and recover safely from transient failures.

## 2) Scope
### In scope
- Manage Rivelio setup values (endpoint and API key).
- Upload and store input files in table `JM Rivelio Input`.
- Process imported records through scheduled batch execution.
- Persist the returned Rivelio key when upload succeeds.
- Retrieve and store output metafiles as `JM Rivelio Output` records.
- Support retry/error visibility and safe requeue actions.

### Out of scope
- Parsing Rivelio extraction results.
- Automatic downstream processing to final business documents.
- Immutable integration event log (deferred).

## 3) User Roles and Actors
- Business Central user importing files.
- Administrator configuring setup and scheduling the processor.
- Job Queue running the background report.

## 4) Functional Behavior
- Setup is maintained on page `JM Rivelio Setup`.
- Users add records and inspect statuses on page `JM Rivelio Input List`.
- Imported records are processed by report `JM Rivelio Processor`.
- On successful API call, status changes to `Send to Rivelio` and `Rivelio Key` is stored.
- Sent records are processed by report `JM Rivelio Output Processor` and produce one or more output records.
- On failed processing, records move to `Failed` with retry metadata and remain recoverable.

## 5) User Flows
- Entry point: open `JM Rivelio Setup` to configure endpoint/API key, then open `JM Rivelio Input List`.
- Main flow: import file -> status `Imported` -> upload processor -> `Send to Rivelio` -> output processor -> `Processed`.
- Recovery flow: `Failed` records can be handled with `Process Now`, `Requeue`, `Clear Error`, and `Open Last Error` actions.

## 6) Rules and Validations
- Status and Type are enum-based (no `Option` usage).
- Batch processing is implemented as `ProcessingOnly` report with dataitem iteration.
- Processing uses status-based scoping so only eligible records are sent.
- Setup save validates endpoint format and required API key.

## 7) Acceptance Criteria
- [x] AC-1 User can configure Rivelio endpoint and API key.
- [x] AC-2 User can create/import input records.
- [x] AC-3 Scheduled processor handles imported records.
- [x] AC-4 Successful sends persist key and update status.
- [x] AC-5 Failed sends do not block processing of other records.
- [x] AC-6 Output metafiles are downloaded and persisted without duplicates.
- [x] AC-7 Failed records expose retry/error metadata and can be requeued safely.

## 8) Known Limitations
- No retrieval/parsing of extraction results yet.
- Error handling focuses on MVP continuity rather than rich diagnostics dashboards.

## 9) Build Verification
- App build completed successfully on 2026-05-19.
- Result: 0 errors.

## 10) Changefix
- 2026-05-15 | Build: Success | Scope: Functional documentation | Changes: Replaced template with implemented MVP behavior, flows, acceptance criteria, and build verification.
