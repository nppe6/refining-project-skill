# Refining Project Skill

这个仓库用于维护 Codex skill：`refining-project`。

`refining-project` 面向“快速接手项目”的场景：当用户提供完整代码库、局部代码、项目结构说明或具体问题时，帮助 Codex 输出可直接用于交接的项目理解、架构分析、代码评审、优化建议和后续开发指南。

## 能力目标

- 分析项目类型、技术栈、目录结构、架构模式和核心模块。
- 梳理模块依赖、数据流、核心价值和设计重点。
- 从工程角度评审架构、代码质量、可维护性、可扩展性和性能隐患。
- 重点检查“重复造轮子”：已有公共模块是否被复用、是否存在重复逻辑、是否引入了不必要的新实现。
- 输出可执行优化建议，包括架构优化、代码层优化、性能优化、可扩展性改进和重构路径。
- 沉淀后续 AI 开发指南，避免继续开发时重复实现已有工具或踩已知坑点。

## 目录结构

```text
skills/
  refining-project/
    SKILL.md
    agents/
      openai.yaml
    references/
      architecture-views.md
      project-handoff-template.md
      review-checklists.md
docs/
  plans/
    2026-05-01-001-update-refining-project-skill-plan.md
    2026-05-01-002-apply-refining-project-research-plan.md
  research/
    refining-project-optimization.md
    similar-skills-distillation.md
README.md
LICENSE
```

## 核心文件

- `skills/refining-project/SKILL.md`：skill 主说明，包含触发描述、使用原则、分析流程、输出结构和评审检查清单。
- `skills/refining-project/references/project-handoff-template.md`：项目交接文档模板，在需要完整交接报告时读取并套用。
- `skills/refining-project/references/review-checklists.md`：按技术栈拆分的专项评审检查表，复杂项目或明确技术栈项目按需读取。
- `skills/refining-project/references/architecture-views.md`：复杂项目的轻量架构视图指南，用于输出系统上下文、服务视图、模块视图和关键调用链。
- `skills/refining-project/agents/openai.yaml`：UI 元数据，包括展示名称、简短描述和默认调用提示。
- `docs/plans/2026-05-01-001-update-refining-project-skill-plan.md`：本次统一语言和补齐文档的轻量计划。
- `docs/plans/2026-05-01-002-apply-refining-project-research-plan.md`：将调研沉淀应用到 skill 本体的实施计划。
- `docs/research/similar-skills-distillation.md`：相似 skill 与 GitHub 实践的调研、蒸馏和可借鉴模式。
- `docs/research/refining-project-optimization.md`：基于调研结果形成的当前 skill 改造优化建议。

## 使用方式

在支持 Codex skills 的环境中，可以这样调用：

```text
使用 $refining-project 分析这个代码库，并输出包含架构评审、问题总结和可执行优化建议的项目交接文档。
```

也可以提供更具体的输入：

```text
使用 $refining-project 接手这个后台管理系统，重点检查是否重复造轮子、是否适合重构，并给出后续 AI 开发指南。
```

## 设计依据

该 skill 按照 `$skill-creator` 的要求创建和整理：

- `SKILL.md` 保持精简，只放核心工作流和判断标准。
- 详细交接模板、专项检查表和架构视图指南放在 `references/`，按需读取，避免主 skill 过长。
- `agents/openai.yaml` 单独维护 UI 展示信息。
- 不在 skill 目录内额外放 README、安装指南或变更日志，避免干扰 skill 本体。

## 当前已吸收的调研成果

- 增加证据索引，要求关键判断绑定文件、配置、依赖或用户提供的信息。
- 增加仓库状态与运行风险，记录分支、工作区、命令识别和验证情况。
- 增加工程成熟度评级，帮助快速判断项目风险集中在哪里。
- 强化重复造轮子检查，要求新增实现建议先说明是否可复用已有模块。
- 增加技术栈专项检查表，覆盖前端、后端/API、数据库、DevOps、AI/agent 项目。
- 增加复杂项目轻量架构视图，按需输出系统上下文、服务视图、模块视图和关键调用链。

## 语言规范

当前 skill 面向中文项目接手与中文工程评审场景，因此主要内容统一为中文。保留少量英文技术术语，例如 `hook`、`schema`、`serverless`、`bundle`、`worker`，是因为这些术语在代码库和工程沟通中更常见。

## 验证说明

本地已手工检查以下内容：

- `SKILL.md` frontmatter 包含 `name` 和 `description`。
- `skills/refining-project/agents/openai.yaml` 包含 `display_name`、`short_description` 和 `default_prompt`。
- `references/project-handoff-template.md` 可作为最终交接文档模板使用。

当前环境中的 `python.exe` 是不可访问的 Windows Store 占位入口，因此未能运行 `$skill-creator` 自带的 `quick_validate.py`。如果安装了可用 Python，可执行：

```powershell
python C:\Users\XIAOSIR\.codex\skills\.system\skill-creator\scripts\quick_validate.py skills\refining-project
```
