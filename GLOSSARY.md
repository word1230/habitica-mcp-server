# Habitica 任务管理

本语境覆盖通过 MCP 创建/更新 Habitica 任务时的领域语言。

## Language

**任务**:
用户在 Habitica 中的 habit / daily / todo / reward 四类事项的统称。
_Avoid_: 工单，事项卡

**备注**:
任务的 `notes` 纯文本补充说明，随任务创建/更新一起写入。
_Avoid_: 注释，评论，清单

**优先级**:
任务难度，唯一字段 `priority`，取值为 0.1=琐碎 / 1=简单 / 1.5=中等 / 2=困难。
_Avoid_: 难度，difficulty

**标签**:
用户为任务打的分类标记；用户侧用名称，API 侧用 UUID。
_Avoid_: tagId 直传，自动建标签

**截止日期**:
仅 `todo` 有效的 `date` 字段，用户侧输入 `YYYY-MM-DD`，按 Asia/Shanghai 午夜理解后转 UTC 发给 Habitica。
_Avoid_: 开始日期，重复规则，每日任务日期
