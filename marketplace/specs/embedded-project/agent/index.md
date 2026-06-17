# Agent 规范索引

本目录专门约束 AI coding agent 的实现行为。

## 必读文件

- `implementation-rules.md`

## 强制规则

- MUST: agent 在实现任何代码前，必须先读取顶层 `index.md`。
- MUST: agent 必须根据任务类型读取对应领域规范。
- MUST: agent 必须先判断代码所属层级。
- MUST: agent 修改完成后必须输出 self-check。
- MUST NOT: agent 不得跳过架构边界直接实现。

## 任务导航

| 场景 | 必须动作 |
|---|---|
| 新增功能 | 回答实现前问题，确认层级和 public API |
| 修改驱动 | 检查 ISR/DMA/硬件边界 |
| 修改协议 | 检查协议层不得直接操作硬件 |
| 修改公共 API | 检查调用方和兼容性 |
| 不确定层级 | 标记 `NEED_CONFIRMATION` |

