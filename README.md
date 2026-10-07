# QDjob-Daily

本副本已完成 GitHub 端配置；起点账号配置尚为空。

- 自动任务仓库：[linoomp/QDjob-Daily](https://github.com/linoomp/QDjob-Daily)
- 私有配置与日志仓库：[linoomp/QDjob-Data](https://github.com/linoomp/QDjob-Data)
- 工作流：[QDjob Daily](https://github.com/linoomp/QDjob-Daily/actions/workflows/qdjob-daily.yml)
- 成功的连接验证：[运行记录](https://github.com/linoomp/QDjob-Daily/actions/runs/37582204534)

## 已配置的运行方式

每天北京时间 08:30 调度，随机延迟 0–5 分钟；GitHub 调度可能额外延迟。
账号为空时只检查配置仓库连接并跳过起点任务。

工作流从 `qdjob/QDjob` 获取最新 Linux amd64 Release，同版本通过 Actions 缓存复用。
私有仓库使用专用可读写 Deploy Key 访问，对应私钥已保存为 Actions Secret `DATA_REPO_SSH_KEY`。

程序运行输出保存在私有数据仓库的 `run-logs`，程序日志和刷新后的 `config.json`、`cookies` 也写回该仓库。

## 补齐起点账号配置

1. 使用 [官方 QDjob 编辑器与使用说明](https://github.com/qdjob/QDjob/blob/main/usage.md) 生成自己的账号配置。
2. 将 `config.json`、`cookies` 文件夹放入 **私有** `linoomp/QDjob-Data` 仓库根目录；若使用真实设备资料，可一并导入 `devices.json` 和 `versions.json`。
3. 每个账号需要 User-Agent、ibex 和有效 Cookies，最多支持 3 个账号。
4. 在 Actions 页面选择 **QDjob Daily → Run workflow**。默认勾选 `validate_only`，只检查连接和配置结构。
5. 配置结构检查通过后，取消 `validate_only` 手动执行一次，在私有仓库查看日志确认实际任务结果。后续按日自动调度。

配置结构检查不能证明账号登录仍有效。请把账号配置与 Cookies 保存在私有仓库。

更完整的部署说明见 [SETUP.md](SETUP.md)。

## 项目来源

- 定时任务方案：[2061360308/QDjob-Daily](https://github.com/2061360308/QDjob-Daily)
- QDjob 程序：[qdjob/QDjob](https://github.com/qdjob/QDjob)
