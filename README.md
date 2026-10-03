# habitica-mcp-server（fork）

MCP server for the Habitica API：让 AI 助手读写 Habitica 的任务、习惯、宠物与奖励。

- 原项目：[iBreaker/habitica-mcp-server](https://github.com/iBreaker/habitica-mcp-server)
- 本包：[@cheems897/habitica-mcp-server](https://www.npmjs.com/package/@cheems897/habitica-mcp-server)，下述改动在其基础上做。

## 本次改动（相对上游）

- `create_task` / `update_task` 新增 `tags`：传名称或 ID，名称经 `get_tags` 自动映射为 UUID，未知名称直接报错；全量替换语义。
- `create_task` / `update_task` 新增日期字段：`date`（仅 todo）、`startDate`（仅 daily）。输入 `YYYY-MM-DD`，按 Asia/Shanghai 午夜转 UTC；update 传空串清除；非对应类型传了直接报错。
- `create_task` / `update_task` 新增 daily 周期字段：`frequency`（默认 weekly）/ `repeat`（缺键补 true，update 与现有合并）/ `everyX` / `daysOfMonth` / `weeksOfMonth`（仅 monthly）。
- 难度收敛为单个 `priority`（0.1/1/1.5/2），删除服务端忽略的 `difficulty`。
- 新增 `delete_tag`：按名称或 ID 删除，未知名称报错；服务端自动从所有任务移除该标签。
- 新增 `GLOSSARY.md`：任务、备注、优先级、标签、截止日期、开始日期等术语定义。

## 给别人用

凭证是私人的，每人用自己的 User ID + API Token（官网 → 用户 → 设置 → API 页复制）。

### 方式一：全局安装

```bash
npm i -g @cheems897/habitica-mcp-server
```

Claude Code：

```bash
claude mcp add habitica -e HABITICA_USER_ID=... -e HABITICA_API_TOKEN=... -e MCP_LANG=zh-CN -- habitica-mcp-server
```

opencode（`opencode.json`）：

```json
"habitica": {
  "type": "local",
  "command": ["habitica-mcp-server"],
  "environment": {
    "HABITICA_USER_ID": "...", "HABITICA_API_TOKEN": "...", "MCP_LANG": "zh-CN"
  }
}
```

### 方式二：免安装（npx，以发版版本号为准）

Claude Code：

```bash
claude mcp add habitica -e HABITICA_USER_ID=... -e HABITICA_API_TOKEN=... -e MCP_LANG=zh-CN -- npx -y @cheems897/habitica-mcp-server@0.0.5
```

opencode（`opencode.json`）：

```json
"habitica": {
  "type": "local",
  "command": ["npx", "-y", "@cheems897/habitica-mcp-server@0.0.5"],
  "environment": {
    "HABITICA_USER_ID": "...", "HABITICA_API_TOKEN": "...", "MCP_LANG": "zh-CN"
  }
}
```

## 本地开发

```bash
git clone https://github.com/word1230/habitica-mcp-server.git
HABITICA_USER_ID=... HABITICA_API_TOKEN=... MCP_LANG=zh-CN node index.js
```
