# Changelog

各版本条目记录该版本发布时的用户可见变化；当前用法以 README 和 CLI Help 为准。

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
