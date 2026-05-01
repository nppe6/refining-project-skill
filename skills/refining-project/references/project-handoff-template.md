# Project Handoff Document Template

Use this template for the final handoff document. Every conclusion should be tied to code, configuration, directories, dependencies, or information provided by the user. Delete sections that do not apply; do not leave empty shells.

## Project Overview

- Project type:
- Core value:
- Design focus:
- Technology stack:
  - Frontend:
  - Backend:
  - Build/runtime:
  - State management:
  - UI/styling:
  - Data/storage:
  - Testing/quality:
- Key entry points:
- Run and build commands:
- Confirmed facts:
- Evidence-based inferences:

## Evidence Index

| Judgment | Evidence file/location | Conclusion | Confidence |
| --- | --- | --- | --- |
| Technology stack |  |  | High / Medium / Low |
| Entry points |  |  | High / Medium / Low |
| Core modules |  |  | High / Medium / Low |
| Build/test/deploy |  |  | High / Medium / Low |
| External dependencies |  |  | High / Medium / Low |

## Repository State and Runtime Risk

- Current branch:
- Working tree state:
- Dependency installation status:
- Identified commands:
  - Install:
  - Development:
  - Test:
  - Build:
  - Lint/format:
- Validations executed:
- Validations not executed and why:
- Runtime risks:

## Architecture Analysis

- Architecture pattern:
- Rendering/runtime mode:
- Directory structure:
- Core dependency relationships:
- Data flow/call chain:
- Key design tradeoffs:
- Are architecture boundaries clear?

### Lightweight Architecture View (For Complex Projects)

Fill this section when the project has multiple apps, services, workers, databases, or complex external dependencies. Delete it for small projects.

- System context:
- App/service view:
- Module/component view:
- External dependencies:
- Key call chain:

## Engineering Maturity Rating

| Dimension | Rating | Evidence | Main Risk |
| --- | --- | --- | --- |
| Architecture clarity | High / Medium / Low / Unconfirmed |  |  |
| Code consistency | High / Medium / Low / Unconfirmed |  |  |
| Test coverage | High / Medium / Low / Unconfirmed |  |  |
| Performance risk | High / Medium / Low / Unconfirmed |  |  |
| Security/authorization boundaries | High / Medium / Low / Unconfirmed |  |  |
| Documentation and developer experience | High / Medium / Low / Unconfirmed |  |  |
| Extensibility | High / Medium / Low / Unconfirmed |  |  |

## Module Breakdown

| Module | Location | Responsibility | Depends on / Used by | Notes |
| --- | --- | --- | --- | --- |

## Issue Summary

Sort issues by severity. Every issue must explain why it is a problem. Use either P0/P1/P2/P3 or High/Medium/Low consistently throughout the document.

| Severity | Issue | Location/Evidence | Why It Is a Problem | Impact | Recommended Direction | Validation |
| --- | --- | --- | --- | --- | --- | --- |

### Reinvented Wheel / Duplication Check

- Existing reusable capabilities:
- Suspected duplicated implementations:
- Recommended reuse path:
- Why new implementation is not recommended:
- Pre-new-code reuse check result:

### Technology Choice Assessment

- Reasonable choices:
- Unreasonable or high-cost choices:
- Alternatives:

## Optimization Recommendations

### Architecture Optimization

- Current state:
- Evidence:
- Recommendation:
- Execution steps:
- Risk:
- Validation:

### Code-Level Optimization

Provide examples in the current technology stack when useful. Examples must serve a concrete issue; do not include examples just for display.

- Current state:
- Evidence:
- Recommendation:
- Example code:
- Validation:

### Performance Optimization

- Performance risk:
- Evidence:
- How to verify:
- Optimization plan:

### Extensibility Improvements

- Short-term improvements:
- Mid-term improvements:
- Not recommended yet:
- Why not recommended:

### Refactoring Decision

- Is refactoring appropriate?
- Refactoring scope:
- Phased plan:
- Regression validation:

## Future Development Guide

- Code style and structure conventions:
- Existing utilities/shared modules:
- Reusable modules:
- Best places to reference before adding features:
- Special traps or gotchas:
- Pre-development checklist:
  - Does a similar utility, component, service, or hook already exist?
  - Does the change fit existing directory boundaries?
  - Does it reuse existing API/client/schema/validation patterns?
  - Does it include necessary tests or validation steps?
  - Does it introduce an unnecessary new dependency?

## External Sources and Version Evidence

If external sources, official documentation, or current best practices were used, list them here. Delete this section if the analysis is fully based on local code.

| Source | Purpose | Conclusion |
| --- | --- | --- |

## Unconfirmed Items

List anything that could not be confirmed because code is incomplete, configuration is missing, commands could not be run, or the user did not provide enough information.
