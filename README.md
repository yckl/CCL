# CCL / CC-Source

> `@anthropic-ai/claude-code` v2.1.88 提取源码归档与结构分析仓库。

这个仓库保存了一份本地提取得到的 Claude Code 源码快照，以及对应的结构化分析文档，方便做代码阅读、架构研究、功能拆解与二次分析。

## 项目元信息

- **Package**: `@anthropic-ai/claude-code`
- **Version**: `2.1.88`
- **Entry**: `cli.js`
- **Runtime**: `Node.js >= 18.0.0`
- **Module Type**: `ESM`
- **Author**: `Anthropic <support@anthropic.com>`
- **Homepage**: <https://github.com/anthropics/claude-code>
- **Extracted At**: `2026-03-31T08:42:29.288Z`
- **Total Sources**: `4756`

## 仓库内容

- `src/`：提取出的主源码目录
- `vendor/`：原生或第三方源码模块
- `node_modules/`：提取时保留的依赖树快照
- `.extract-meta.json`：提取元信息
- `.extract-manifest.json`：提取清单
- `ANALYSIS.md`：本项目的详细分析文档

## 分析结论摘要

根据当前提取结果，这个项目可以概括为一个基于 **Node.js + TypeScript/TSX + React/Ink** 的终端式 AI 编程代理，核心能力主要包括：

1. **AI 对话与查询引擎**
   - 负责和 Claude 模型进行交互
   - 包含主循环、上下文管理、会话历史、成本统计等核心逻辑

2. **丰富的工具系统**
   - 覆盖文件读写编辑、搜索、终端命令、网页抓取、网页搜索、MCP、任务管理、子 Agent 调用等
   - 是 Claude Code 能够“像代理一样工作”的基础

3. **终端 UI 系统**
   - 基于 React + Ink 构建
   - 包含消息渲染、输入组件、Diff 展示、设置、弹窗、状态栏、统计组件等

4. **服务层与扩展能力**
   - 包括 API 通信、OAuth、LSP、MCP、上下文压缩、语音输入、插件、技能、诊断追踪等

5. **多 Agent / 远程协作能力**
   - 包含 Coordinator、Remote/Teleport、IDE Bridge 等子系统
   - 表明该项目不仅是单轮聊天 CLI，而是一个具备工作流和协作能力的完整开发助手

## 目录结构概览

```text
CC-Source/
├── .extract-manifest.json
├── .extract-meta.json
├── node_modules/
├── src/
├── vendor/
├── ANALYSIS.md
└── README.md
```

## 使用说明

这个仓库更适合作为：

- 源码结构学习资料
- CLI Agent 架构分析样本
- 工具系统 / MCP / 终端 UI 的参考案例
- 逆向整理与功能拆解的基础材料

如果你想快速了解整体结构，建议先读：

1. `README.md`
2. `ANALYSIS.md`
3. `src/entrypoints/`
4. `src/tools/`
5. `src/services/`
6. `src/components/`
7. `src/main.tsx`

## 重要说明

- 这是**提取/还原后的源码快照**，不保证与上游官方开发仓库完全一致。
- 某些文件布局、生成产物、依赖形式可能与官方仓库源码状态不同。
- 复用、再分发或进一步公开传播时，请自行确认并遵守上游仓库、包分发与许可证要求。

## 详细分析

详见：[`ANALYSIS.md`](./ANALYSIS.md)
