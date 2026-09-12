# AGENTS.md — AI 代理协作入口

> 本文件面向 AI 代理（Coding Agent）。人类读者请从 [README.md](README.md) 开始。
> README 只保留人类视角的项目介绍（功能 / 环境 / 运行方式 / 目录结构 / 许可）；AI 工作流、行为指令与协作规范集中在本文件。

## 一、必读文档

| 目的 | 文档 |
| --- | --- |
| **AI 辅助开发规划与角色定义（本仓 AI 协作总纲）** | [docs/游戏开发规划与AI辅助系统.md](docs/游戏开发规划与AI辅助系统.md) |
| 通用 AI 主规则：模块化架构、核心行为指令、测试、Git 工作流、命令行规范 | [.trae/rules/rule.md](.trae/rules/rule.md) |
| 项目特定规则：项目名、Godot 根目录、分支、目标平台 | [.trae/rules/rule_local.md](.trae/rules/rule_local.md) |
| Git 分支 / 提交 / 子模块工作流 | [docs/tool-guides/Git工作流程指南.md](docs/tool-guides/Git工作流程指南.md) |
| 架构与工程改进待办（完成一项即删除对应条目） | [docs/架构改进待办项.md](docs/架构改进待办项.md) |
| 错误记忆 / 向量知识库（快速浏览视图，真相来源为 `tools/vector_db/errors.json`） | [docs/working_log.md](docs/working_log.md) |
| 项目结构说明 | [docs/项目结构总览.md](docs/项目结构总览.md) |
| 开发日志 | [docs/桌宠开发日志.md](docs/桌宠开发日志.md) |

## 二、项目速览

- 项目名：**TransparentPet**（内部代号 Project Astra），基于 Godot 4 的桌面桌宠。
- **Godot 工程根目录是 `transparent-pet/`**（`res://` 根）；仓库根只放 `docs/`、`tools/`、`external/` 等仓库级内容。
- 测试框架 **GdUnit4**；CI 平台 **GitHub Actions**；目标平台 **Windows / Web**。
- Godot 主开发分支：**`dev/fan`**；稳定分支 `main`。

## 三、核心行为指令

以下要点摘自 [.trae/rules/rule.md](.trae/rules/rule.md)，冲突时以该文件为准：

1. 用中文思考、回答，并用中文写提交信息与 Git 日志。
2. 不主动创建文件/文档，优先编辑现有文件；仅在用户明确要求时新建文档。
3. 不修改 Godot 工程 `/core/` 下的文件，除非用户明确授权。
4. 生成的功能代码须配套 GdUnit4 单元测试。
5. 模块间通信走 `core/autoload/event_bus.gd` 或模块根 `api.gd` 定义的信号；禁止跨模块 `get_node` 或引用非 API 内部方法。
6. 任务描述不清晰或与架构原则冲突时，先提问，不做危险假设。
7. 每次提交是原子化的最小功能单元；修改 Godot 项目文件后先用 `godot --headless` 验证编译通过再提交。

## 四、提交与 Git 约定

- 提交信息用中文，格式 `类型(模块): 描述`；类型：`feat` / `fix` / `refactor` / `test` / `docs` / `chore`（子模块用 `submodule`）。
  - 示例：`fix(ci): 测试失败阻塞构建`、`docs(gdd): 新增游戏设计文档，更新 README 文档导航`。
- 分支角色：`main` 稳定发布；`dev/<名字>` 个人集成分支；`agent/<任务>` AI 任务分支（合并后删除）。
- 默认不主动 push / 合并，按用户指示执行。

## 五、文档分工

- `README.md`：面向人类读者。
- `AGENTS.md`（本文件）：面向 AI 代理的协作入口与规范索引。
- 详细规范以 [.trae/rules/rule.md](.trae/rules/rule.md) 为准，本文件只做入口与索引。
