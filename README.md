# Phased Verified Development

这是一个用于约束 AI 辅助开发流程的 Skill，核心目标是让 AI 不再“一口气写完然后自称完成”，而是按设计文档、阶段计划、模块验证报告和用户确认一步一步推进。

## 旨在解决什么问题

在使用 AI 做软件开发时，常见问题包括：

- AI 直接开始写代码，缺少设计文档和架构约束。
- 关键技术选择没有经过用户确认。
- 多个模块混在一起开发，出了问题很难定位。
- 测试通过就被 AI 当成“已验收”，但用户没有真正确认。
- 没有中间产物和验证报告，结果不可复查、不可复现。
- 外部 API、模型、数据库等依赖被直接写进业务逻辑，后续难以替换。
- 服务失败、性能问题、异常数据没有被明确记录。
- 换 AI 工具、换线程或隔天继续时，上下文容易丢失。

这个 Skill 的作用，就是把 AI 开发过程变成一个受控的工程流程：先设计，再确认；先验证，再继续；每一步都有记录，每个模块都能复查。

## 核心原则

> 不把“代码已实现”当成完成标准。只有验证报告生成并经用户确认通过后，模块或阶段才算完成。

执行时遵循：

- 设计文档先行。
- 关键决策逐项确认。
- 阶段之间不跨越。
- 每个模块都生成 Markdown 验证报告。
- 验证报告命名跟随阶段计划和任务编号，便于按开发顺序追踪。
- 用户确认通过后才继续下一步。
- 所有外部依赖都通过 provider 抽象隔离。
- 外部服务不可用时必须有降级逻辑，并且要验证。
- 进度、风险、决策和验收状态都要写入文档。

## 适用场景

适合用于：

- 中长期 AI 辅助开发项目。
- 数据处理、文档解析、知识库、API 服务、自动化流程等需要逐步验证的项目。
- 需要用户持续确认关键决策的项目。
- 依赖外部 API、模型、数据库、内部服务的项目。
- 希望跨不同 AI 工具复用同一套开发指挥方法的场景。

不适合用于：

- 一次性的小脚本。
- 不需要验收流程的临时实验。
- 用户明确要求快速原型且接受跳过验证的任务。

## 文件结构

```text
phased-verified-development/
  SKILL.md
  agents/
    openai.yaml
  references/
    document-templates.md
    verification-report-template.md
```

说明：

- `SKILL.md`：主 Skill，定义触发条件、硬规则、开发流程和验证策略。
- `agents/openai.yaml`：面向 Codex/OpenAI 工具的展示元数据。
- `references/document-templates.md`：设计文档、进度文件、API 契约、环境指南、决策日志等模板。
- `references/verification-report-template.md`：模块验证报告模板和状态规范。

## 使用方式

在支持 Skill 的 AI 工具中安装或引用本目录，然后在项目开始时明确要求使用：

```text
Use $phased-verified-development to run this project with design-first planning, module verification reports, and user confirmation before continuing.
```

中文也可以这样说：

```text
使用 phased-verified-development 这套分阶段验证开发方法来推进项目。先写设计文档，关键决策逐项确认，每个模块生成验证报告，用户确认通过后再继续。
```

## 期望产物

使用本 Skill 后，一个项目通常会形成：

```text
docs/
  design.md
  progress.md
  api-contract.md
  environment.md
  decision-log.md
  risks-and-optimizations.md
reports/
  verification/
    phase1_task1_excel_faq_reader_verify.md
    phase1_task3.5_es_setup_verify.md
    phase1_task12_eval_160_verify.md
```

这些文档共同保证项目可以被审阅、复现、恢复上下文和持续推进。

## 开发状态

当前版本是中文主版本，保留英文 Skill 名称和触发描述，方便不同 AI 工具识别。
