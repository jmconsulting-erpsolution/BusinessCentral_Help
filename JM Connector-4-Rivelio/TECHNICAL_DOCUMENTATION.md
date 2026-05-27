# Technical Documentation

Status: Completed
Date: 2026-05-19
Feature: JM Connector-4-Rivelio

## 1) Technical Summary
AL extension for Business Central runtime `16.0` that manages Rivelio input/output records and executes resilient upload/output processing through report-driven batch pipelines.

## 2) Architecture and Design
- Components:
  - API interaction: `JMRivelioApi.Codeunit.al` via `IJMRivelioApi.Interface.al`.
  - Input domain behavior: `JMRivelioInput.Codeunit.al` via `IJMRivelioInput.Interface.al`.
  - Dependency wiring: `JMRivelioFactory.Codeunit.al`.
  - Scheduled orchestrator: `JMRivelioProcessor.Report.al` (`ProcessingOnly = true`).
  - Output orchestrator: `JMRivelioOutputProcessor.Report.al` (`ProcessingOnly = true`).
  - UI: `JMRivelioInputList.Page.al`, `JMRivelioSetup.Page.al`.
- Design decisions:
  - Factory + interface seams for testability and mock injection.
  - Enum-based status/type modeling (`JMRivelioInputStatus`, `JMRivelioInputType`).
  - Report dataitem pattern for scheduled/batch processing.
  - Controlled retry metadata (`Retry Count`, `Max Retry Count`, `Next Retry DateTime`) with non-blocking per-record continue.

## 3) AL Objects and Files
- Codeunits:
  - `app/src/codeunit/JMRivelioApi.Codeunit.al`
  - `app/src/codeunit/JMRivelioFactory.Codeunit.al`
  - `app/src/codeunit/JMRivelioInput.Codeunit.al`
- Interfaces:
  - `app/src/interface/IJMRivelioApi.Interface.al`
  - `app/src/interface/IJMRivelioInput.Interface.al`
- Tables:
  - `app/src/table/JMRivelioInput.Table.al`
  - `app/src/table/JMRivelioSetup.Table.al`
- Pages:
  - `app/src/page/JMRivelioInputList.Page.al`
  - `app/src/page/JMRivelioSetup.Page.al`
- Report:
  - `app/src/report/JMRivelioProcessor.Report.al`
  - `app/src/report/JMRivelioOutputProcessor.Report.al`
- Enums:
  - `app/src/enum/JMRivelioInputStatus.Enum.al`
  - `app/src/enum/JMRivelioInputType.Enum.al`
  - `app/src/enum/JMRivelioOutputStatus.Enum.al`
- Permission set:
  - `app/src/permissionset/JMPermissionset79000.PermissionSet.al`

## 4) Data Model Changes
- `JM Rivelio Input` table stores imported payload metadata, processing status, returned Rivelio key, and retry/error telemetry.
- `JM Rivelio Setup` table stores endpoint/API key configuration.
- `JM Rivelio Output` table stores downloaded metafile payloads linked to originating input records.
- Enums introduced:
  - `JM Rivelio Input Status`
  - `JM Rivelio Input Type`

## 5) Integration and Dependencies
- External dependency: Rivelio REST API upload endpoint (`data-extraction/uploads/upload`).
- App feature flags include `TranslationFile`, so XLF synchronization/translation is part of maintenance workflow.

## 6) Test and Verification
- Existing tests:
  - `test/src/codeunit/JMRivelioTests.Codeunit.al`
  - `test/src/codeunit/JMRivelioApiMock.Codeunit.al`
- Build verification (2026-05-19):
  - `buildAlPackage`: Success
  - Errors: `0`
  - Warnings: `0`
- No AL source changes were made in this documentation/build task, so no additional coverage/mock/wrapper verification was required.

## 7) Deployment Notes
- Prerequisites:
  - Valid Business Central environment matching app `application` version `27.0.0.0`.
  - Rivelio endpoint and API key configured in setup page.
- Rollout steps:
  1. Build extension package.
  2. Publish extension to target environment.
  3. Configure setup.
  4. Schedule `JM Rivelio Processor` in Job Queue.
- Backout steps:
  1. Disable/delete Job Queue entry.
  2. Unpublish extension version if rollback is required.

## 8) Risks and Technical Debt
- API contract changes in Rivelio may require payload/response adaptations.
- MVP currently lacks enriched retry strategy and detailed operational telemetry.

## 9) Build Command Reference
- Build tool used: `buildAlPackage` with `app/app.json`.
- Last verified build timestamp: 2026-05-15.

## 10) Changefix
- 2026-05-15 | Build: Success | Scope: Technical documentation | Changes: Replaced template with current architecture, object inventory, integration notes, and verified build status.
