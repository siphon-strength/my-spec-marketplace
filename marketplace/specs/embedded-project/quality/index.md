# Quality 规范索引

本目录约束错误处理、日志、诊断、测试、review 和 self-check。

## 必读文件

- `error-handling-logging-diagnostics.md`
- `testing-and-check-strategy.md`
- `review-checklist.md`

## 强制规则

- MUST: 所有可失败路径必须有错误处理。
- MUST: agent 修改代码后必须输出验证方式。
- MUST: 未实际执行的测试不得声称通过。
- MUST NOT: 不允许静默吞掉错误。

## 任务导航

| 任务 | 重点文件 |
|---|---|
| 新增错误码 | `error-handling-logging-diagnostics.md` |
| 新增日志或诊断 | `error-handling-logging-diagnostics.md` |
| 新增测试或验证 | `testing-and-check-strategy.md` |
| 完成实现自检 | `review-checklist.md` |

