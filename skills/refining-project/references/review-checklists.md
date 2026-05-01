# Project Handoff Review Checklists

Use the relevant section when the project has a clear stack or risk area. Do not mechanically copy every checklist item into the final document; keep only findings supported by evidence in the current project.

## General Review

- Are project entry points clear: app entry, route entry, API entry, CLI entry, worker/job entry?
- Are module boundaries clear, or are business modules, shared modules, and infrastructure adapters mixed together?
- Are dependency directions reasonable, or does business logic depend backward on UI or controllers carry too much business logic?
- Is configuration discoverable: environment variables, build config, deployment config, examples, and documentation?
- Is error handling consistent across exceptions, return values, logs, retries, and fallbacks?
- Do tests cover high-risk paths: authentication, authorization, data writes, external services, and core business flows?
- Is there reinvented wheel risk: existing helpers, components, services, schemas, clients, or mature libraries not being reused?
- Is documentation sufficient for handoff: install, run, test, deploy, and troubleshooting?

## Frontend Projects

- Is the routing structure clear, and are pages separated from business modules?
- Is state management centralized with clear boundaries, or is server state incorrectly stored in global client state?
- Is API access centralized through a client wrapper with consistent error handling, loading behavior, retry behavior, and auth?
- Do components reuse the design system, or are buttons, forms, tables, and modals repeatedly reimplemented?
- Performance risks: large bundles, repeated requests, excessive re-rendering, large lists without virtualization, unoptimized images/assets.
- Accessibility: form labels, keyboard navigation, focus states, contrast, and semantic markup.
- Styling consistency: Tailwind, CSS Modules, CSS-in-JS, and component library themes should not be mixed without clear boundaries.
- Do tests cover key interactions, route transitions, form validation, and error states?

## Backend/API Projects

- Are route, controller, service, and model/repository responsibilities clear?
- Are parameter validation and serialization centralized, or repeatedly hand-written?
- Are authentication and authorization handled at consistent boundaries, with no bypass paths?
- Do data writes use transactions, idempotency, and concurrency protection when needed?
- Do external service calls include timeouts, retries, circuit breaking, error mapping, and logs?
- Are API response shapes stable, with consistent status codes and error formats?
- Do background jobs/queues handle retries, deduplication, dead-lettering, and observability?
- Do tests cover core APIs, authorization denial, failure paths, and cross-layer integration?

## Database and Data Layer

- Are schema, migrations, seeds, and fixtures consistent with the code?
- Do queries risk N+1 access, missing indexes, full table scans, large pagination, or unnecessary data loading?
- Are constraints placed at the right layer: database uniqueness/not-null/foreign keys plus application validation?
- Are data migrations reversible and safe for production data volume, locks, and batching?
- Is ORM usage reasonable, or is complex business logic hidden in query construction?
- Is sensitive data minimized, masked, access-controlled, and auditable?
- Do tests cover data boundaries, constraint conflicts, migration safety, and rollback strategy?

## DevOps / Build / Deployment

- Can install, develop, test, build, and deploy commands be identified from scripts/config?
- Does CI run tests, linting, type checks, and builds?
- Are environment variables documented with examples, defaults, required flags, and secret handling?
- Do Docker/container configs distinguish development and production, and are images reasonably sized?
- Are build artifacts, caches, logs, upload files, and generated files excluded from version control?
- Does deployment include rollback, health checks, migration ordering, and monitoring?
- Are dependency versions locked, and are there obviously stale or high-risk dependencies?

## AI / Agent Projects

- Are prompts, skills, tools, and agents separated by responsibility?
- Are trigger conditions clear enough to avoid overly broad invocation?
- Does the project follow progressive disclosure: core workflow in the main file, long templates/checklists in references?
- Are tool boundaries clear: when to read files, when to browse, when to ask the user, and when to request approval?
- Does output have a quality gate and self-check to avoid generic summaries?
- Does the project record evidence, limitations, and unconfirmed items instead of treating inference as fact?
- Is there a reuse check to avoid recreating existing skills, scripts, templates, or helpers?
- Is there a real-task replay or forward-test plan to validate whether the skill is stable?
