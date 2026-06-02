# My Claude Code

从零复现 [Learn Claude Code](https://github.com/shareAI-lab/learn-claude-code) 的动手实践仓库——一步步构建一个真实的 AI 编码 Agent。

## 这是什么

这是一个**教学项目**，通过 19 个递进的模块，从最原始的"一个 bash 工具 + 一个 while 循环"开始，逐步添加工具系统、权限控制、钩子、子代理、记忆、任务系统……最终构建出一个具备生产级特性的 AI 编码 Agent。

每个模块是一个独立的 Python 文件，可以直接运行，修改、调试。

## 核心理念

> Agency 来自于模型的训练，而非外部代码编排。Agent 产品 = 模型 + Harness（工具/知识/观测/行动/权限）。

本仓库教你构建的是 **Harness**——给模型装上手脚、眼睛、记忆和边界。

## 模块索引

| # | 模块 | 核心概念 | 文件 |
|---|---|---|---|
| 01 | Agent Loop | 最简 while 循环：调模型 → 执行工具 → 回传结果 | [01_agent_loop/code.py](01_agent_loop/code.py) |
| 02 | Tool Use | safe_path 沙箱 + read/write/glob 专用工具替代万能 bash | [02_tool_use/code.py](02_tool_use/code.py) |
| 03 | Permission | 三级权限管道：deny list → rules → ask user | [03_permission/code.py](03_permission/code.py) |
| 04 | Hooks | 生命周期钩子系统：PreToolUse / PostToolUse / Stop | [04_hooks/code.py](04_hooks/code.py) |
| 05 | Todo Write | 让模型自己管理任务清单，防止复杂任务中"迷路" | [05_todo_write/code.py](05_todo_write/code.py) |
| 06 | Sub Agent | 子代理隔离：独立 messages 历史，多轮自动收敛 | [06_sub_agent/code.py](06_sub_agent/code.py) |
| 07 | Skill Loading | 技能系统：frontmatter 解析、按需注入 prompt | [07_skills_loading/code.py](07_skills_loading/code.py) |
| 08 | Context Compact | 上下文压缩：摘要生成 + 大输出持久化 + reminder 注入 | [08_context_compact/code.py](08_context_compact/code.py) |
| 09 | Memory | 持久化记忆：检索、写入、反射、维护 | [09_memory/code.py](09_memory/code.py) |
| 10 | System Prompt | 分层 prompt 工程：角色/约束/知识/技能/状态 | [10_system_prompt/code.py](10_system_prompt/code.py) |
| 11 | Error Recovery | 自愈引擎：上下文溢出/工具失败/震荡检测/模型降级 | [11_error_recovery/code.py](11_error_recovery/code.py) |
| 12 | Task System | 任务图：依赖编排、状态持久化、并行执行 | [12_task_system/code.py](12_task_system/code.py) |
| 13 | Background Tasks | 异步任务：后台运行、状态轮询、回调通知 | [13_background_tasks/code.py](13_background_tasks/code.py) |
| 14 | Cron Scheduler | 定时调度：cron 表达式、周期性自动执行 | [14_cron_scheduler/code.py](14_cron_scheduler/code.py) |
| 15 | Agent Team | 多 Agent 协作：并行分发、结果聚合 | [15_agent_team/code.py](15_agent_team/code.py) |
| 16 | Team Protocols | 团队协议：消息总线、角色路由 | [16_team_protocols/code.py](16_team_protocols/code.py) |
| 17 | Autonomous Agents | 自主 Agent：自我规划、持续执行、目标收敛 | [17_autonomous_agents/code.py](17_autonomous_agents/code.py) |
| 18 | Worktree Isolation | git worktree 沙箱隔离 | [18_worktree_isolation/code.py](18_worktree_isolation/code.py) |
| 19 | MCP Plugin | MCP 协议集成、外部工具发现 | [19_mcp/code.py](19_mcp/code.py) |

## 技能目录

```
skills/
├── agent-builder/    # 教你构建 Agent 的 Agent
├── code-review/      # 代码审查技能
├── mcp-builder/      # MCP 服务器构建技能
└── pdf/              # PDF 处理技能
```

每个技能是一个 `SKILL.md`，带 YAML frontmatter 元数据，由 s07 的技能加载系统按需注入。

## 快速开始

### 1. 安装依赖

```bash
pip install anthropic python-dotenv
```

### 2. 配置模型

本项目使用 Anthropic 兼容 API，支持多 Provider。复制并编辑 `.env` 文件：

```env
# DeepSeek
ANTHROPIC_API_KEY=sk-your-deepseek-key
ANTHROPIC_BASE_URL=https://api.deepseek.com/anthropic
MODEL_ID=deepseek-chat

# 或者 Anthropic 官方
# ANTHROPIC_API_KEY=sk-ant-your-key
# MODEL_ID=claude-sonnet-4-6
```

支持的 Provider：Anthropic、DeepSeek、MiniMax、GLM (Zhipu)、Kimi (Moonshot)。

### 3. 运行

```bash
cd my-claude-code
python 01_agent_loop/code.py
```

看到 `s01 >>` 提示符后输入任务，比如：

```
s01 >> 创建一个 hello.py，输出 "Hello, World!"
```

## 学习路线

按数字顺序逐个模块阅读和运行：

1. **01-03**：理解 Agent 的最小闭环（循环 → 工具 → 权限）
2. **04-06**：掌握工程化基础设施（钩子 → 任务管理 → 子代理）
3. **07-09**：建立知识层（技能 → 上下文管理 → 记忆）
4. **10-11**：加固系统（prompt 工程 → 自愈恢复）
5. **12-14**：扩展规模（任务图 → 异步 → 定时调度）
6. **15-17**：多 Agent 协作（团队 → 协议 → 自主运行）
7. **18-19**：隔离与生态（worktree → MCP 外部工具）

## 技术栈

- Python 3.11+
- Anthropic SDK（兼容 DeepSeek / MiniMax / GLM / Kimi）
- 零额外框架依赖，纯标准库 + SDK

## 关于安全

代码中的 `run_bash` 故意保留 `shell=True` 和 denylist 策略——这是**教学基线**，用于展示从"危险"到"安全"的演进过程。生产环境应使用白名单、沙箱隔离、容器化等更强的安全措施。

## 致谢

- [Learn Claude Code](https://github.com/shareAI-lab/learn-claude-code) — 原始教程仓库
- [MiniCode Python](https://github.com/QUSETIONS/MiniCode-Python) — 生产级 Python Agent 实现

## License

MIT
