# whit-ziji-skills

一个面向个人成长场景的开源日记 skills 仓库，用于统一整理和沉淀与日记、反思、复盘相关的 AI 能力。

## 项目目标

`whit-ziji-skills` 的出发点很简单：用AI记日记的方式，帮助个人成长

曾国藩通过日记和“修身十二条”长期自我监督，核心方法就是“每天记录，每天反省，每天改一点点”。蒋把日记进一步发展成一套复盘系统，不只有每日记录，也有每周、每月、每年的反省，并按不同主题持续整理。

这些方法放到今天依然成立。不同的是，在 AI 时代，我们可以借助 AI 让这套过程更稳定、更结构化、更容易坚持。例如：

- 根据模板生成每日日记和 checklist
- 自动补充天气、睡眠等结构化信息
- 从日记中整理周记、月记、年记
- 提取行动项、反思点和阶段性主题

但这个项目有一个明确前提：**AI 只是辅助工具，个人成长真正关键的仍然是持续反思与行动。**

这个仓库不是一个零散 prompt 的集合，而是一个面向多 agent 的 journaling skill registry。它把 GitHub 仓库作为唯一真源，在仓库中定义规范化 skill，再通过轻量适配层映射到 Codex、Claude、OpenClaw等不同环境。

## 项目范围

本仓库主要存放：

- 每日日记类 skills
- 周复盘、月复盘类 skills
- 情绪记录与反思类 skills
- 润色、总结、提取类 skills
- 面向多 agent 的统一 skill 定义与适配文件

## 设计思路

仓库围绕四层结构组织：

1. 内容层：skill 本体、模板、示例
2. 规范层：元数据与结构约束
3. 适配层：不同 agent 的映射配置
4. 发布层：后续的校验、同步、打包流程

## 目录结构

```text
whit-ziji-skills/
├─ README.md
├─ docs/
│  └─ skills-spec.md
└─ skills/
   └─ <skill-id>/
      ├─ skill.yaml
      ├─ SKILL.md
      ├─ templates/
      ├─ examples/
      ├─ tests/
      └─ adapters/
```

## Skill 规范

仓库中的所有 skill 都应遵循统一规范，详见：

`docs/skills-spec.md`

核心要求：

- 每个 skill 都有独立目录
- 每个 skill 都有标准化的 `skill.yaml` 和 `SKILL.md`
- skill 核心逻辑保持 agent 无关
- 平台差异放在 `adapters/` 中
- 外部导入的 skill 必须先归一化，再进入仓库

## 工作流程

推荐流程如下：

1. 在仓库中新增或修改 skill
2. 审查规范主定义
3. 补充或更新 agent 适配文件
4. 后续再同步到目标 agent

这样可以避免不同 agent 中长期出现内容漂移。

## 新 Skill 的整理方式

后面你发送原始 skill 时，会按照以下方式整理：

1. 提取稳定、通用、agent 无关的核心能力
2. 生成清晰的 kebab-case skill 目录名
3. 编写 `skill.yaml`
4. 重写为结构化 `SKILL.md`
5. 将各 agent 特有内容拆分到 `adapters/`
6. 按需要补充模板和示例

## 当前状态

当前仓库处于初始化阶段：

- 已建立规范文档
- 已完善 README
- 具体 skills 将逐步补充

