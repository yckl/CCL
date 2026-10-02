# ⚡ CCL: Anthropic Claude Code 架构解析与核心源码深度归档
### Claude Code Deep Architecture Analysis, Runtime Dissection & Source Snapshot

<p align="center">
  <img src="https://img.shields.io/badge/Anthropic-Claude%20Code-D97706.svg?style=flat-square&logo=anthropic" alt="Claude Code" />
  <img src="https://img.shields.io/badge/Package-%40anthropic--ai%2Fclaude--code-blue.svg?style=flat-square&logo=npm" alt="NPM Package" />
  <img src="https://img.shields.io/badge/Target%20Version-v2.1.88-brightgreen.svg?style=flat-square" alt="Version" />
  <img src="https://img.shields.io/badge/Runtime-Node.js%20%3E%3D18-339933.svg?style=flat-square&logo=nodedotjs" alt="Node.js" />
  <img src="https://img.shields.io/badge/UI%20Framework-React%20%2B%20Ink-61DAFB.svg?style=flat-square&logo=react" alt="React Ink" />
  <img src="https://img.shields.io/badge/Architecture-Agentic%20Loop%20%2B%20MCP-purple.svg?style=flat-square" alt="Architecture" />
</p>

---

## 📌 项目定位 (Executive Summary)

**CCL (Claude Code Library / Dissection)** 是一份针对 Anthropic 官方旗舰级终端 AI 编程智能体 **`@anthropic-ai/claude-code` (v2.1.88)** 的**工业级源码重构快照与深度架构剖析智库**。

作为当今全球最为先进的自主 Agentic Coding 生产力工具之一，Claude Code 具备极高的系统工程复杂度。本项目旨在穿透打包混淆层，系统化梳理其底层 **「ReAct 执行主循环、MCP 协议网关、React/Ink 终端反应式渲染、AST 语法分析、子 Agent 协同与上下文主动剪枝」** 的架构机理，为学术研究、开源 Agent 框架演进与前沿代码助手研发提供权威的解剖学样本。

---

## 🏛️ 系统架构全景解剖 (System Architecture Blueprint)

```
┌────────────────────────────────────────────────────────────────────────┐
│                        终端反应式呈现层 (Terminal UI Layer)            │
│               React 18/19 + Ink + Marked-Terminal + Yoga Layout        │
├────────────────────────────────────────────────────────────────────────┤
│  - 沉浸式流式 Markdown 增量渲染       - 实时双向 Unified Diff 审查面板 │
│  - 响应式多行命令输入与历史回溯 (Prompt)- 任务步进转轮与 Token 计费看板│
└────────────────────────────────────┬───────────────────────────────────┘
                                     │ User Actions & Stream Events
┌────────────────────────────────────▼───────────────────────────────────┐
│                        执行核心编排调度器 (Core Agent Loop)            │
├────────────────────────────────────────────────────────────────────────┤
│  [Query Engine]         主思考循环驱动 / 多轮对话自迭代 / 状态机递归   │
│  [Context Compactor]    上下文自动修剪 / 智能记忆衰减 / 窗口超限平滑压缩│
│  [Permission Guard]     高危 Shell/写操作敏感度评估与用户即时确认机制  │
│  [Subagent Coordinator] 任务解耦派发 / 独立沙箱子 Agent 孵化与结果归并  │
└────────────────────────────────────┬───────────────────────────────────┘
                                     │ Tool Execution Bus / RPC
┌────────────────────────────────────▼───────────────────────────────────┐
│                        外设与系统能力总线 (Extensibility & Tools)      │
├────────────────────────────────────────────────────────────────────────┤
│  - File System Ops (Read/Write/Patch) - Shell Execution (Sandbox PTY)  │
│  - AST Codebase Search (Ripgrep/Glob) - Web Browser / Fetch Services   │
│  - Model Context Protocol (MCP Client)- LSP Language Server 协议桥接   │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 🔬 五大核心机制深度拆解 (Deep Insights)

### 1. 终端 TUI 反应式渲染体系 (`src/components/`)
* 彻底打破传统 CLI 单向 `console.log` 的桎梏，基于 **React/Ink** 将终端屏幕抽象为 DOM 树结构。
* 实现了组件级别的局部状态重绘、Flexbox 盒模型终端自适应（基于 Facebook Yoga 引擎）以及细腻的代码 Diff 高亮对照。

### 2. 强类型受控工具链与 MCP 网关 (`src/tools/`)
* 系统中的每一个功能调用（读文件、正则搜索、Git 操作、终端命令）均遵循统一的生命周期标准；
* 原生实现 **MCP (Model Context Protocol)** 客户端协议，不仅能调用内置工具，还能无缝挂载本地与网络 MCP Server 工具池。

### 3. 自适应上下文感知与记忆压缩引擎 (`src/services/context/`)
* 面对超长代码库浏览时，系统通过启发式压缩算法监控 Token 消耗水位；
* 在接近模型上下文上限（Context Window Limit）时，自适应触发中间记忆折叠（Compaction），保留核心系统提示词与最终任务目标，防止灾难性遗忘。

### 4. 协同子智能体机制 (Subagent Delegation)
* 内置 Coordinator 协同体系，可根据任务复杂度将庞大工程任务切分为多个子任务，动态唤起隔离的 Subagent 并发执行，最终将产出物向上汇报聚合。

### 5. 开发者工具链整合 (IDE & LSP Integration)
* 通过语言服务器协议（LSP）与 IDE Bridge，打通与本地编辑器（VSCode / Cursor 等）的跨进程联动，精准获取代码符号、定义跳转与诊断错误。

---

## 📂 源码模块结构导览 (Directory Organization)

```text
CCL/
├── src/                                   # 核心源码还原目录 (4,750+ 源码文件)
│   ├── components/                        # React/Ink 终端 UI 组件库
│   ├── entrypoints/                       # 各种模式启动入口 (CLI、IPC、Server)
│   ├── services/                          # 核心底层业务驱动
│   │   ├── api/                          # Claude API 客户端与网络层
│   │   ├── context/                      # 会话上下文与 Token 压缩中枢
│   │   ├── mcp/                          # Model Context Protocol 协议实现
│   │   ├── lsp/                          # 语言服务器协议桥接器
│   │   └── telemetry/                    # 性能指标与链路追踪
│   ├── tools/                             # 全量原子工具实现 (File, Terminal, Web)
│   └── main.tsx                           # TUI 主生命周期挂载入口
├── vendor/                                # 第三方依赖或原生嵌入模块
├── ANALYSIS.md                            # 详细模块分析白皮书
├── .extract-manifest.json                 # 提取文件指纹清单
└── README.md                              # 项目技术全景说明
```

---

## 📖 核心研读推荐路线 (Study Guide)

想要深入吸收其工程精华，建议按以下路线循序阅读：

1. **宏观理解**：精读 [`ANALYSIS.md`](./ANALYSIS.md)，全面了解模块间耦合关系。
2. **启动与入口**：查看 `src/entrypoints/` 与 `src/main.tsx`，理解 CLI 参数解析与环境初始化的全过程。
3. **Agent 核心主循环**：深入 `src/services/` 下的查询引擎与状态机运转机理。
4. **工具实现范式**：参考 `src/tools/`，学习大模型调用工具（Function Calling）的参数校验规范与安全确认拦截。
5. **终端交互美学**：研读 `src/components/`，学习如何利用 React/Ink 构建现代终端交互界面。

---

## ⚠️ 免责声明与知识产权 (Disclaimer)

* 本仓库代码为研究分析目的而归档的源码结构快照，旨在推动软件工程与 AI 代理架构的技术交流；
* 相关商标、核心算法及版权归原作者 **Anthropic, PBC** 所有；
* 任何商业使用或二次分发请务必遵守上游官方授权与相关许可协议。
