# Changelog

各版本条目记录该版本发布时的用户可见变化；当前用法以 README 和 CLI Help 为准。

## v7.1.10

- 新增 ZCode Skill 安装与自动检测支持。
- Kimi Desktop 的安装参数改为 `--harness kimi-work`，已有安装位置不变。
- Python SDK 转为正式可用，同步与异步 API 延续 v7.1.9。
- 整理安装、账号、代理、Windows、更新与卸载指引。

## v7.1.9

- 新增实验性 Python SDK，提供同步与异步客户端、类型化资源、工作负载管理、远程执行和 Notebook 文件传输。
- 支持 SDK 账号管理、会话续期、目录缓存和流式输出。
- **兼容性变化：**六类工作负载的状态统一为大写，缺失或无法识别的状态使用 `UNKNOWN`；Job 的停止状态统一为 `CANCELLED`。依赖旧状态值的脚本需调整。
- **兼容性变化：**`cache status` 按资源身份去重，JSON 增加 `scopes` 和 `size_bytes`；账号凭据与私有状态文件收紧访问权限。
- 修复 Serving 模型查询分页、浏览器验证码判断及日志错误处理。
- 扩展 macOS 与 Windows 支持，改善异步调用和文件传输稳定性。

## v7.1.8

- Serving 列表与详情显示完整 Endpoint；新增 `serving api` 生成调用说明和 curl 示例。
- 新增 `account api-key list/create/export/run/delete`，支持推理密钥管理、文件导出和子进程环境注入。
- 密钥导出支持 Shell、PowerShell、dotenv 和原始格式，使用私有文件权限且不覆盖已有文件。
- 修复长服务地址显示和并发镜像查询的稳定性问题。

## v7.1.7

- 各命令统一支持 `--account <name>` 单次账号选择，并行命令保持各自账号上下文。
- **兼容性变化：**Notebook 不再跨账号自动查找连接，移除 `--account all`；需要其他账号时显式指定。
- 已配置账号的登录名以账号配置为准；默认 SSH Host 别名包含账号信息。
- 修复账号切换、连接复用、GPU 缓存隔离和异常退出后的上下文恢复。
- 表格统一使用 Rich，改善中文对齐和长内容显示；脚本应使用全局 `--json`。

## v7.1.6

- `resources availability` 合并配额余额、实时用量与空闲或可回收整节点容量。
- **兼容性变化：**删除 `resources nodes`，改用 `resources availability`。
- **兼容性变化：**`resources usage` 删除 `--by`，默认按 Project → User 汇总；使用 `--details` 查看任务，并支持 `--project`、`--user`、`--task` 过滤。
- 多节点 Job 要求每节点使用 8 GPU 满节点规格；`--nodes` 指定节点数。
- 修复资源分页、节点状态判断与事件时间线过滤。

## v7.1.5

- **兼容性变化：**移除仓库级配置、路径别名和工作负载 Profile；`inspire init` 只处理账号配置。
- 远端工作目录改用显式绝对路径；Job 默认读取平台日志，SSH 日志需显式指定目录。
- 更新流程支持识别并清理退役配置，账号配置保留；普通模式确认后清理，`--yes` 直接执行。
- 过期会话优先通过已有 SSO 状态续期，减少重复提交凭据。
- JupyterTerminal 执行隔离本地 stdin，修复命令读取输入导致的超时。

## v7.1.4

- 修复 Notebook 删除后重建时，过期名称缓存导致 JupyterTerminal 连接失败。
- JupyterTerminal WebSocket 遵循系统代理的 `NO_PROXY` 设置。
- 恢复 HPC Shell 的默认与显式实例连接。

## v7.1.3

- 名称缓存改为按需读取与更新，减少普通命令的后台请求。
- 镜像、跨工作区列表和资源查询支持并发；批处理复用单次命令内的目录查询。
- 新增原生 Windows 安装、Shell 和连接支持。
- 修复缓存分页、刷新恢复及零保障额度计算组的显示。
- 改善更新包解压安全性与诊断脱敏，更新依赖和 CI 运行时。
- **兼容性变化：**移除冗余的 `cache refresh --full`；账号配置不再缓存项目与资源目录。

## v7.1.2

- `job status`、`hpc status` 和 `job events` 支持一次查询多个任务。
- 修复会话失效后的重复认证，减少账号锁定风险。
- 登录失败区分凭据错误、临时限制和验证码要求，并显示可操作的错误提示。
- 默认显示版本更新提醒；修复 `update --check` 在有新版本时误报失败，以及版本查询响应不完整时的异常。
- 修复 Help 示例、参数说明、缩进和终端宽度适配。
- 完成 Browser API v2 迁移，整理使用与开发文档。

## v7.1.1

- 新增 Serving、Ray 和 HPC 的交互式 Shell，支持实例选择。
- `notebook save-image --flatten` 支持将镜像保存为单层。
- 工作负载 Quota 显示每小时点券成本；资源用量支持 `--group` 过滤并显示可抢占容量。
- **兼容性变化：**项目 JSON 的 `remaining_budget` 拆为 `my_remaining_budget` 和 `project_remaining_budget`。
- **兼容性变化：**`cache refresh` 需指定 `--resource`、`--workspace` 或 `--name` 收窄范围。
- 修复空配额缓存、模型分页、重复镜像查询、镜像标签显示和节点容量统计。
- 复用 HTTP 连接，减少重复缓存刷新请求。

## v7.1.0

- 新增数据集目录、版本、标签、校验与申请状态查询；Notebook、Job 和 HPC 支持挂载数据集。
- 新增 TensorBoard 生命周期管理及训练曲线读取。
- 补齐 HPC、Ray、Serving 的日志、实例事件、伸缩与部署观察入口。
- 新增资源用量归因、回收策略、节点事件和 Notebook 即时指标。
- 新增 Ray 启动、Serving 伸缩与回滚、模型部署配置与删除、取消镜像保存等操作。
- 扩展工作负载创建和批处理参数，支持环境变量、保留策略、时长限制及通知。
- **兼容性变化：**`image save` 改为 `notebook save-image`；删除 `config` 命令组，账号相关操作迁入 `account`。
- **兼容性变化：**Project 命令移除 `--workspace`；`--workspace all` 限于支持跨工作区发现的命令。
- **兼容性变化：**事件默认包含工作负载与实例事件；`--workload-level` 可只看工作负载级事件，实例选择使用列表中的标签。
- 修复 Shell 退出、终态等待、日志排序、镜像名称与可见性解析、配额缓存、HPC 规格校验和限流处理。

## v7.0.2

- Notebook 传输方式按实际 GPU 型号判断，并缓存探测结果。
- `cache status` 与 `cache clear` 新增 `--resource` 过滤。
- 自动清理名称索引中退役的资源类型。

## v7.0.1

- 新增 `inspire uninstall` 和安装脚本的 `--uninstall` 入口。
- 默认移除工具拥有的安装内容；`--purge` 可清理账号数据，`--purge-runtime` 可进一步清理运行时。
- 修复安装完成提示的换行。

## v7.0.0

- **兼容性变化：**删除 `notebook url`、`notebook vscode`；`notebook proxy-url` 改为打印地址。
- **兼容性变化：**删除 `user` 命令组，权限查询改用 `account permissions`；移除旧用户配额与密钥查询入口。
- 恢复 `inspire update` 的进度和版本摘要输出。
- 将主要平台操作迁移至 Browser API v2。
- Notebook 执行和 Shell 减少浏览器依赖，改善网关 URL 解析与并发连接建立。
- 修复 Serving 启停、HPC 创建与名称解析、镜像解析、Ray 列表字段及普通成员资源查询。

## v6.3.0

- 新增 Ray 指标及 Serving 事件、实例和启动命令。
- 新增按账号隔离的名称缓存和 `cache status/refresh/clear`。
- **兼容性变化：**删除资源 `id` 命令；`notebook ssh open` 改为 `notebook ssh`；指标参数 `--lcg` 改为 `--group`，Serving 的 `--shm-gib` 改为 `--shm-size`。
- **兼容性变化：**删除 Notebook 执行的旧产物中转参数与 `net-test`；文件传输使用 `notebook scp`。
- **兼容性变化：**凭据改用账号配置；连接 JSON 移除 `public_internet`，资源查询移除 `--no-cache`。
- 统一列表输出预算与名称显示，修复交互字节流、SSH 配置和旧版本更新交接。

## v6.2.0

- GPU Job 支持原生状态通知，并可通过账号配置或 Batch 条目设置。
- 新增 Qoder Work 和 Kimi Desktop 安装支持。
- 修复系统代理与 `NO_PROXY` 继承、依赖安装代理隔离及 Job 容错配置传递。
- 改善代理和登录诊断脱敏。
