# Refining Project Skill

This repository maintains the Codex skill `refining-project`.

`refining-project` is designed for quickly taking over an existing project. When a user provides a full codebase, partial code, a project structure description, or a specific concern, the skill helps Codex produce a practical handoff document with project understanding, architecture analysis, code review, optimization recommendations, and follow-up development guidance.

## Goals

- Identify project type, technology stack, directory structure, architecture pattern, and core modules.
- Explain module dependencies, data flow, core value, and design focus.
- Review architecture, code quality, maintainability, extensibility, and performance risks from an engineering perspective.
- Focus on duplicated work and reinvented wheels: whether shared modules are reused, whether logic is duplicated, and whether unnecessary new implementations are being introduced.
- Produce executable recommendations, including architecture improvements, code-level improvements, performance work, extensibility improvements, and refactoring paths.
- Prepare future AI development guidance so later work avoids reimplementing existing utilities or stepping into known traps.

## Directory Structure

```text
skills/
  refining-project/
    SKILL.md
    agents/
      openai.yaml
    references/
      architecture-views.md
      handoff-workflow.md
      project-handoff-template.md
      review-checklists.md
README.md
LICENSE
```

`docs/` is intentionally ignored by Git. It is used for local research notes and planning artifacts.

## Core Files

- `skills/refining-project/SKILL.md`: main skill instructions, including trigger description, principles, workflow, output structure, and quality gate.
- `skills/refining-project/references/project-handoff-template.md`: complete project handoff template to adapt when producing a full report.
- `skills/refining-project/references/handoff-workflow.md`: durable documentation workflow for creating or updating target-project handoff and optimization documents.
- `skills/refining-project/references/review-checklists.md`: stack-specific review checklists for frontend, backend/API, database, DevOps, and AI/agent projects.
- `skills/refining-project/references/architecture-views.md`: lightweight architecture view guide for complex projects, including system context, app/service view, module view, and key call chains.
- `skills/refining-project/agents/openai.yaml`: UI metadata, including display name, short description, and default prompt.

## Usage

In an environment that supports Codex skills, invoke it like this:

```text
Use $refining-project to analyze this codebase and produce a project handoff document with architecture review, issue summary, and executable recommendations.
```

More specific example:

```text
Use $refining-project to take over this admin system. Focus on duplicated work, refactoring suitability, and future AI development guidance.
```

## Design Rationale

This skill follows the `$skill-creator` structure:

- Keep `SKILL.md` concise with only the core workflow and decision standards.
- Keep detailed handoff templates, stack-specific checklists, and architecture view guidance under `references/` for on-demand loading.
- Keep UI metadata in `agents/openai.yaml`.
- Do not place a README, installation guide, or changelog inside the skill directory, so the skill remains focused.

## Incorporated Research Outcomes

- Added an evidence index so key judgments must be tied to files, configuration, dependencies, or user-provided information.
- Added repository state and runtime risk so branch state, working tree state, command discovery, and validation status are captured.
- Added engineering maturity ratings to quickly show where project risk is concentrated.
- Strengthened the reinvented wheel check so new implementation recommendations must first explain whether existing modules can be reused.
- Added stack-specific review checklists for frontend, backend/API, database, DevOps, and AI/agent projects.
- Added lightweight architecture views for complex projects, including system context, service view, module view, and key call chains.
- Added a persistent handoff workflow so non-trivial reviews create or update short target-project documents that future AI sessions can resume.

## Persistent Handoff Behavior

For non-trivial reviews, the skill should create or update a durable document in the target project unless the user explicitly asks for chat-only output.

Default behavior:

- Prefer an existing relevant handoff, review, architecture, or optimization document.
- Otherwise create `docs/project-handoff.md` in the target project when appropriate.
- Keep the main handoff short and updateable.
- Track findings, next actions, decisions, and update history with stable IDs.
- During follow-up implementation, update the same document instead of relying on chat memory.

## Language

Project content is standardized in English. The skill still preserves the user's language during actual use: if a user asks in another language, the response may follow that language when appropriate.

## Validation Notes

The following checks were performed manually:

- `SKILL.md` frontmatter includes `name` and `description`.
- `skills/refining-project/agents/openai.yaml` includes `display_name`, `short_description`, and `default_prompt`.
- `references/project-handoff-template.md` can be used as a final handoff template.
- `SKILL.md` references the on-demand files in `references/`.

The local `python.exe` in this environment is an inaccessible Windows Store launcher, so `$skill-creator`'s `quick_validate.py` could not be run. If a working Python runtime is installed, run:

```powershell
python C:\Users\XIAOSIR\.codex\skills\.system\skill-creator\scripts\quick_validate.py skills\refining-project
```
