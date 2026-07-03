# analysis-os — AI 协作规范

> 本文件由 github-workflow-master 维护。
> AI 工具（Claude / Cursor / Copilot 等）操作此 repo 前必须完整阅读并遵守。
> 最后更新：2026-07-03

## 项目概述

Analysis OS 是一个 AI-Native 的系统分析方法论框架，核心是 Define → Model → Observe → Explain → Predict → Optimize 六阶段流水线，打包为可复用的 Claude Code Skill，并附带按领域组织的知识包（Android、Camera/ISP、AI Agent 等）。这是一个纯 Markdown 项目，没有构建流程。

## 目录结构

```
analysis-os/
├── .claude/skills/analysis-os/   # 核心 Skill：orchestrator + 六个阶段 reference + prompts/
├── docs/                         # 方法论文档
├── domains/                      # 领域知识包（可扩展）
├── templates/                    # 输出模板
├── examples/                     # 端到端案例
└── diagrams/                     # 可视化参考
```

## 分支规范

| 分支 | 用途 |
|------|------|
| `main` | 稳定分支，随时可作为 Claude Code Skill 使用 |
| `feature/<name>` | 新增领域包 / 模板 / 框架能力 |

单人维护项目，暂不强制 PR review，但仍需遵循 commit 规范。

## Commit 规范（Conventional Commits）

```
feat:     新领域包 / 新模板 / 新阶段能力
fix:      对已有 skill / 领域内容的修正
docs:      纯文档变更
chore:     仓库维护
```

## 新增领域包的规则

1. 放在 `domains/<domain>/<topic>.md`，遵循已有结构：Key objects / Key metrics / Common failure modes / Diagnostic approach。
2. 领域包必须保持"薄"——只提供领域知识，绝不重新实现六阶段流水线本身。
3. 在 `.claude/skills/analysis-os/SKILL.md` 的 domain-detection 表格中登记新领域包。

## 禁止事项

- 禁止在任何阶段文件中跳过 Fact / Inference / Hypothesis / Unknown 的区分要求。
- 禁止领域包重新定义或绕过核心六阶段流水线。
- 禁止在没有 System Model（Phase 2）的情况下直接进入 Explain（Phase 4）——这是整个框架的核心约束，任何 Skill 修改都不能削弱这一点。

## 架构决策记录

- 2026-07-03：初始化仓库，采用 v1.0 结构（Skill-based framework）。v2.0（Analysis Graph）和 v3.0（Multi-Agent）见 `roadmap.md`，暂不实现。
- 2026-07-03：选择 MIT License，仓库设为 public，归属 SoloXLab 组织。
- 2026-07-03：v1.1 — 从 `factor-analyzer` 技能吸收量化严谨性（强制 5Why 深挖、r/β/压缩幅度统计、因子角色分类、跨组稳健性验证、收敛判定标准、横纵向比较发现遗漏因子、强制白话注释、权重编码可视化），同时保留 Analysis OS 无数据也能用的 Tier D 降级路径，不强制要求统计数据。详见 `CHANGELOG.md` [1.1.0]。
