# habitica-mcp-server（fork）

MCP server for the Habitica API：让 AI 助手读写 Habitica 的任务、习惯、宠物与奖励。

- 原项目：[iBreaker/habitica-mcp-server](https://github.com/iBreaker/habitica-mcp-server)
- 本仓库：[word1230/habitica-mcp-server](https://github.com/word1230/habitica-mcp-server)，下述改动在其基础上做。

## 本次改动（相对上游）

- `create_task` / `update_task` 新增 `tags`：传名称或 ID，名称经 `get_tags` 自动映射为 UUID，未知名称直接报错；全量替换语义。
- `create_task` / `update_task` 新增日期字段：`date`（仅 todo）、`startDate`（仅 daily）。输入 `YYYY-MM-DD`，按 Asia/Shanghai 午夜转 UTC；update 传空串清除；非对应类型传了直接报错。
- `create_task` / `update_task` 新增 daily 周期字段：`frequency`（默认 weekly）/ `repeat`（缺键补 true，update 与现有合并）/ `everyX` / `daysOfMonth` / `weeksOfMonth`（仅 monthly）。
- 难度收敛为单个 `priority`（0.1/1/1.5/2），删除服务端忽略的 `difficulty`。
- 新增 `delete_tag`：按名称或 ID 删除，未知名称报错；服务端自动从所有任务移除该标签。
- 新增 `GLOSSARY.md`：任务、备注、优先级、标签、截止日期、开始日期等术语定义。

## 运行

```bash
HABITICA_USER_ID=... HABITICA_API_TOKEN=... MCP_LANG=zh-CN node index.js
```
