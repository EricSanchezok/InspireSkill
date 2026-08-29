# Changelog

各版本条目记录该版本发布时的用户可见变化；当前用法以 README 和 CLI Help 为准。

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
