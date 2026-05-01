---
name: refining-project
description: Deeply analyze an existing software project, partial codebase, or project description and produce a practical project handoff, architecture review, code quality assessment, optimization plan, and AI-ready follow-up development guide. Use when the user asks to take over a project, understand a codebase, review architecture, detect duplicated work or reinvented wheels, evaluate technology choices, create handoff documentation, or prepare future AI development without reimplementing existing utilities or modules.
---

# Project Handoff Review

Use this skill to turn project code, partial code snippets, or a project description into an evidence-backed handoff and engineering review. The goal is not to summarize files superficially, but to help a future developer or AI agent continue work safely and quickly.

## Principles

- Ground every important judgment in code, configuration, directory structure, dependency manifests, scripts, routes, data models, or information explicitly provided by the user.
- Distinguish confirmed facts from evidence-based inferences. When information is incomplete, state what is known, what is inferred, and what remains unconfirmed.
- Prefer concrete, actionable engineering judgments over generic advice. Every issue must explain location, evidence, why it is a problem, impact, and recommended direction.
- Before recommending new implementation, check whether the project already has shared utilities, components, services, hooks, middleware, constants, schemas, client wrappers, or adapters.
- Every recommendation to add new code must pass a reuse check: determine whether a similar function, component, service, schema, client, or third-party library already exists; if it does, explain how to reuse it instead of creating a new implementation.
- Treat duplicated work and reinvented wheels as first-class review targets: identify repeated logic, custom code that should use an existing library, and internal modules that should be reused.
- External sources may support judgment, but must not override local code evidence. When framework APIs, dependency versions, best practices, or security rules may be outdated, prefer official or current sources and cite them in the output.
- Produce durable project artifacts, not only chat output. For non-trivial reviews, create or update a short handoff/optimization document in the target project so future AI sessions can resume from evidence and decisions.
- Preserve the user's language. If the user asks in English, respond in English.

## Workflow

1. **Inventory the project**
   - Read root files: `README`, dependency/build manifests, lockfiles, framework config, environment examples, Docker/CI config, test config, and AGENTS/CLAUDE/CODEX guidance.
   - Before writing a new report, search the target project for existing handoff, audit, review, or optimization documents. Prefer updating an existing relevant document over creating a duplicate.
   - Use `rg --files` to build a file map, then inspect application logic, tests, shared modules, and configuration directories.
   - Identify runtime entry points: frontend routes/pages, backend server entry points, API routes/controllers, CLI entry points, jobs/workers, serverless handlers, etc.
   - Check repository state and runtime risk: current branch, uncommitted changes, whether dependencies can be installed, whether run/test/build commands are identifiable, and which validations cannot be executed.

2. **Identify project type and stack**
   - Classify the project type: admin system, SaaS, blog/content site, tool, library, API service, mobile app, game, automation script, etc.
   - Extract frontend, backend, build tools, routing, state management, UI library, styling approach, data storage, authentication, testing, linting, and deployment stack from actual files.
   - Do not guess from filenames alone; prefer manifests, config files, imports, and entry points as evidence.

3. **Analyze architecture and modules**
   - Describe the architecture pattern: MVC, layered architecture, modular monolith, microservices, micro-frontend, SSR, CSR, SSG, serverless, event-driven, plugin-based, etc.
   - Break down core modules by responsibility and cite their locations.
   - Explain key dependency flows: UI to state/API, controller to service/model, job to queue, adapter to external service, shared package to business app, etc.
   - Infer the project's core value and design focus from business flows, domain entities, and code organization.
   - When the project has multiple apps, services, workers, databases, or complex external dependencies, read `references/architecture-views.md` and add a lightweight architecture view in the architecture analysis. Do not force diagrams for small projects.

4. **Review code and architecture**
   - Summarize strengths: architecture boundaries, framework conventions, code style, maintainability, extensibility, testability, and developer experience.
   - List concrete issues. Each issue must include location, evidence, why it is a problem, impact, and recommended direction.
   - Focus on duplicated logic, reinvented wheels, unnecessary abstractions, dependency misuse, performance risks, unsafe data flow, and unclear boundaries.
   - Only flag technology choices as unreasonable when code evidence shows mismatch, complexity, risk, maintenance cost, or poor fit for the product.
   - When the project is clearly frontend, backend/API, database-heavy, DevOps/deployment-heavy, or AI/agent-oriented, read the relevant section of `references/review-checklists.md`.

5. **Provide executable optimization recommendations**
   - Architecture recommendations must address observed problems; avoid unnecessary large rewrites.
   - Code-level recommendations should include examples in the project's actual technology stack when useful.
   - Performance recommendations must connect to verifiable paths: rendering, queries, network calls, caching, bundle size, startup time, loops, IO, concurrency, or data loading.
   - Extensibility recommendations should reuse existing project patterns.
   - Decide whether refactoring is appropriate. If so, provide a phased, low-risk refactoring path.
   - Each recommendation should ideally include: evidence -> proposal -> execution steps -> validation method -> risk. If evidence is missing, mark it as a hypothesis to verify.

6. **Prepare future AI development**
   - Summarize coding style, naming habits, directory conventions, testing approach, common scripts, and local commands.
   - List reusable utilities, shared modules, components, services, schemas, and client wrappers, and explain when to use them.
   - Call out traps: hidden coupling, generated files, environment dependencies, migration risks, brittle tests, framework lifecycle concerns, and areas where duplicated implementation is likely.
   - Include a "before adding new code" checklist to help future AI agents avoid reinventing existing behavior.

7. **Persist and maintain the handoff**
   - Read `references/handoff-workflow.md` before writing or updating project documentation.
   - For a first review, create a concise handoff document in the target project unless the user explicitly asks for chat-only output.
   - For follow-up optimization work, update the existing handoff or action document as work progresses: mark completed items, add new evidence, record decisions, and keep next actions current.
   - Avoid one ever-growing document. Keep the main handoff short and split deep notes only when the topic is large enough to justify a separate file.

## Output Structure

Unless the user requests a different format, use this structure:

- Project Overview
- Evidence Index
- Repository State and Runtime Risk
- Architecture Analysis
- Engineering Maturity Rating
- Module Breakdown
- Issue Summary
- Optimization Recommendations
- Future Development Guide

For a complete handoff document, read and adapt `references/project-handoff-template.md`. Do not keep empty sections; place unknowns in "Unconfirmed Items".

## On-Demand References

- `references/project-handoff-template.md`: read when generating a complete project handoff document.
- `references/handoff-workflow.md`: read before creating or updating durable handoff/optimization documents in the target project.
- `references/review-checklists.md`: read relevant sections when the project has a clear stack or needs deeper review.
- `references/architecture-views.md`: read when the project has multiple apps, services, workers, databases, or complex external dependencies and needs a lightweight architecture view.

## Evidence Standards

Good examples:

- `src/api/user.ts` defines user-related API calls and is consumed by `src/pages/users/*`.
- `package.json` shows React + Vite + Zustand, so the project can be identified as a CSR frontend with client-side state management.

Weak examples:

- "The project probably uses React" without checking dependencies, config, or imports.
- "Extract a helper function" without first checking whether a similar helper already exists.

When the user only provides partial code or a project description:

- Ask for key missing files if the missing information would make the analysis materially misleading.
- If analysis is still possible, state conclusions, limitations, and the next files or commands to inspect.

## Review Checklist

- Are entry points and routes clear?
- Are domain module boundaries clear?
- Can data flow be traced from UI/API to persistence or external services?
- Are shared utilities, components, and services discoverable and reused?
- Are error handling, loading states, logging, validation, authentication, and authorization boundaries placed appropriately?
- Do tests cover high-risk paths and verify behavior rather than implementation trivia?
- Do performance-sensitive paths avoid repeated computation, N+1 queries, large bundles, excessive re-rendering, blocking IO, and unbounded loops?
- Are configuration and environment requirements discoverable?
- Do build, test, and deployment scripts match the architecture?
- Do recommendations fit the current stack and avoid heavy tools without clear payoff?

## Final Quality Gate

Before delivering, check:

- Did you explain project type, core value, and design focus?
- Did you list key entry points, core modules, and dependency relationships?
- Did you provide an evidence index and distinguish facts, inferences, and unconfirmed items?
- Did you explain repository state, runtime risk, and identified validation commands?
- Did you include a module table, dependency explanation, or lightweight architecture view?
- Does every issue explain why it is a problem?
- Does every optimization recommendation include execution steps or validation?
- Did you list reusable modules and a reuse check for new code?
- Did you create or update a durable target-project handoff/optimization document, or explicitly state why output is chat-only?
- Did you mark refactors or changes that should not be done yet, with reasons?
