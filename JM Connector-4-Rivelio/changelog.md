# Changelog

## 2026-05-19

- Added Phase 2 reliability fields and status model on `JM Rivelio Input` (`Failed`, retry counters, next retry datetime, last-attempt/error metadata).
- Updated both processor reports to use non-blocking retry logic with processing telemetry counters and summary messages.
- Added `Process Now`, `Requeue`, `Clear Error`, and `Open Last Error` actions to `JM Rivelio Input List` with guarded transitions.
- Hardened setup with endpoint/API key validation on save and a `Test Setup` action on `JM Rivelio Setup`.
- Completed unfinished output-processing task: `JM Rivelio Output Processor` now marks input records as `Processed` only after a fully successful collection cycle and when outputs exist for the input.
- Added `CollectOutputsForInputCycle` to `IJMRivelioOutputMgt` / `JM Rivelio Output Mgt` and expanded tests to cover cycle-completion true/false paths, duplicates-only cycles, and malformed/invalid list payload handling.
- Fixed `JM Rivelio Api` metafile list payload generation to emit valid JSON for `doc_id` filtering.
- Implemented Rivelio Output feature: added `JM Rivelio Output` table (79011), `JM Rivelio Output Status` enum (79010), Output and OutputMgt Logic codeunits (79012, 79014) with full TDD coverage (7 tests across 2 test codeunits).
- Extended `IJMRivelioApi` with `ListMetafilesByDocId` and `GetMetafileDownload` methods for Rivelio metafile discovery and download.
- Created `IJMRivelioFileAction` interface and wrapper codeunit (79016) to enable testable file download; added mock (79904) for unit test coverage of `DownloadBlob` paths.
- Refined mock pattern: applied writing-mocks skill rules to `JMRivelioApiMock` for canonical stub/spy surface (`Expect_*`, `IsInvoked_*`, `IsInvokedWith_*`).
- Added `JM Rivelio Output List` page (79013) with `Download JSON` action and `JM Rivelio Output Processor` report (79015) for status update processing.
- Updated Factory (79006) with Output, OutputMgt, and FileAction interface getters; updated permission sets for all new objects.

## 2026-05-18

- Updated [.github/prompts/generate-documentation.prompt.md](.github/prompts/generate-documentation.prompt.md): Aligned with docs-update skill, replaced build + Changefix staging with 8-step workflow (classify → changelog → setup → getting-started → user-guide → README → docs index → archive plans → cross-check → report).
