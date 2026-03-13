# Skills 规范

本仓库用于存放日记相关的 skills，并以统一格式适配多个 agent，例如 Codex、Claude、OpenClaw。

## 设计原则

1. GitHub 仓库是唯一真源。
2. 每个 skill 只有一份规范化主定义，agent 适配为可选附加层。
3. skill 核心内容保持 agent 无关。
4. agent 特定行为必须隔离在适配文件中。
5. 每个 skill 都应具备版本、可审查性和可验证性。

## 目录结构

```text
skills/
  <skill-id>/
    skill.yaml
    SKILL.md
    templates/
    examples/
    tests/
    adapters/
      claude.yaml
      codex.yaml
      openclaw.yaml
```

## 必备文件

### `skill.yaml`

用于索引、校验、打包和适配生成的机器可读元数据。

必填字段示例：

```yaml
id: reflect-daily
name: 每日复盘
version: 0.1.0
category: journal
entry: SKILL.md
tags:
  - diary
  - reflection
compatibility:
  codex: supported
  claude: supported
  openclaw: planned
triggers:
  - 写日记
  - daily reflection
```

字段规则：

- `id`：全局唯一，使用 kebab-case
- `name`：简短、清晰的人类可读名称
- `version`：使用语义化版本
- `category`：稳定分类，如 `journal`、`review`、`emotion`、`planning`
- `entry`：通常固定为 `SKILL.md`
- `tags`：用于搜索和分类的简洁标签
- `compatibility`：声明各 agent 的支持状态，可用值为 `supported`、`partial`、`planned`、`unsupported`
- `triggers`：代表性触发语句，反映用户会如何调用该 skill

推荐可选字段：

```yaml
description: 将原始日记笔记整理为结构化反思内容。
inputs:
  - raw_notes
  - date
  - mood
outputs:
  - polished_journal
  - action_items
dependencies: []
author: whit-ziji-skills
license: MIT
```

## `SKILL.md`

这是 skill 的规范主文本，也是后续各 agent 适配的来源。

必备章节：

```md
# Skill 名称

## 目标

## 使用时机

## 输入

## 工作流程

## 输出格式

## 示例

## 边界情况

## 安全与隐私
```

章节要求：

- `目标`：说明 skill 的核心用途
- `使用时机`：说明适合触发的场景和不适用场景
- `输入`：说明必填输入、可选输入、默认值和降级策略
- `工作流程`：使用稳定、可复现的步骤定义行为
- `输出格式`：明确输出结构和格式约束
- `示例`：至少给出一个真实、可理解的示例
- `边界情况`：说明输入缺失、噪声、矛盾、过长等情况的处理方式
- `安全与隐私`：说明如何避免泄露隐私、臆造事实或过度推断

## `templates/`

用于存放可复用模板，例如：

- `daily.md`
- `weekly-review.md`
- `emotion-checkin.md`
- `concise.md`

模板应尽量保持通用，不绑定某一个 agent。

## `examples/`

用于存放示例输入输出，便于贡献者理解 skill，也便于后续做测试。

推荐文件：

- `input.md`
- `output.md`
- `notes.md`

## `tests/`

用于预留验证样例、回归测试或结构校验数据。

推荐文件：

- `cases.yaml`
- `expected-output.md`

## `adapters/`

用于定义 skill 在不同 agent 中的映射方式。

规则：

- 适配文件不能重新定义 skill 的核心逻辑，除非目标 agent 有明确限制
- 适配文件只描述 agent 相关内容，例如安装位置、调用方式、环境要求、格式补丁
- 如果暂不支持某 agent，可以先不创建对应 adapter 文件，但要在 `skill.yaml` 里声明兼容状态

推荐结构：

```yaml
agent: codex
status: supported
entry: ../SKILL.md
install:
  mode: manual
invoke:
  triggers:
    - 写日记
    - polish my journal
notes:
  - 保持主 skill 的核心流程不变。
```

## 命名规则

- skill 目录名必须与 `id` 一致
- 文件和目录名优先使用 kebab-case
- 命名应具体，优先使用 `weekly-review`，而不是过于宽泛的 `review`
- `id` 建议使用动作导向命名，例如 `capture-daily`、`polish-journal`、`monthly-retrospective`

## 兼容状态

- `supported`：当前已有可用适配
- `partial`：核心 skill 可用，但适配尚未完整
- `planned`：计划支持，但尚未实现
- `unsupported`：明确不作为支持目标

## 提交前检查清单

新增 skill 前应检查：

1. `skill.yaml` 存在且结构合法
2. `SKILL.md` 存在且包含全部必备章节
3. `id` 与目录名一致
4. `version` 符合语义化版本规则
5. `triggers` 具体且具有代表性
6. 隐私和安全预期有明确说明
7. agent 特定逻辑已隔离到 `adapters/`

## 外部 Skill 归一化规则

当把来自其他 agent、个人笔记或零散 prompt 的 skill 整理进本仓库时，遵循以下流程：

1. 提取核心意图，移除主定义中的 agent 特定措辞
2. 按规范章节重写为结构化 `SKILL.md`
3. 将平台相关说明迁移到 `adapters/`
4. 创建 `skill.yaml`，补齐稳定 `id`、`version`、`triggers` 和兼容状态
5. 补充至少一个示例，以及该 skill 用到的模板文件

这就是后续所有新 skill 进入本仓库时的统一整理标准。
