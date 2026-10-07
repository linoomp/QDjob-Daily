# QDjob GitHub 端配置

仓库及工作流已部署；账号配置为空，需补齐真实账号配置。

本地校验：YAML 解析通过，10 段 Bash 脚本语法检查通过，7 个模拟账号配置场景通过。尚未运行远程 GitHub Actions，也未执行真实起点账号任务。

## 部署位置

- 项目副本：`linoomp/QDjob-Daily`，公开，来自 `2061360308/QDjob-Daily`。
- 数据仓库：`linoomp/QDjob-Data`，私有，仅保存账号配置、Cookies 和运行日志。
- `qdjob-daily.yml` 安装到项目副本的 `.github/workflows/qdjob-daily.yml`。
- `config.json` 安装到私有数据仓库根目录。初始账号列表为空。

## 运行设置

每天北京时间 08:30 调度，并随机延迟 0–5 分钟。GitHub 的调度可能额外延迟。

手动运行默认勾选 `validate_only`：只检查私有仓库连接与配置结构，不执行起点任务。
账号列表为空时，定时运行也只报告“账号配置尚为空”，不下载或执行 QDjob。

工作流使用 `qdjob/QDjob` 最新 Linux amd64 Release。同一版本通过 GitHub Actions 缓存复用；无需创建或删除二进制版本分支。

执行输出保存在私有数据仓库的 `run-logs`，不会主动打印到公开 Actions 日志。程序刷新后的 `config.json` 与 `cookies` 也写回私有仓库。

## 访问方式

在私有数据仓库创建一把可读写 Deploy Key，将对应私钥保存为项目副本的 Actions Secret `DATA_REPO_SSH_KEY`。该密钥仅用于这个私有数据仓库，无需将个人 GitHub 登录令牌交给工作流。

SSH 主机密钥从 GitHub 官方 `meta` API 获取，使用严格主机密钥检查。

## 账号配置仍需补充

用官方 QDjob 编辑器生成真实 `config.json` 和 `cookies` 文件夹，必要时一并保存 `devices.json` 和 `versions.json`，放入私有数据仓库根目录。

每个账号需要 username、User-Agent、ibex，以及包含官方必需字段的 Cookies；最多 3 个账号。可选 tokenid 与推送服务由用户自行设置。

配置结构检查不能证明账号仍处于登录状态。补齐配置后，取消 `validate_only` 手动执行一次，查看私有运行日志确认实际任务结果。

## 参考

- 项目说明：https://github.com/2061360308/QDjob-Daily
- 官方使用说明：https://github.com/qdjob/QDjob/blob/main/usage.md
- 官方 Release：https://github.com/qdjob/QDjob/releases/latest
