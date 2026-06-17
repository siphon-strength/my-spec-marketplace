# Coding 规范索引

本目录约束 C 语言编码风格、public API 设计、内存和资源管理。

## 必读文件

- `c-coding-standard.md`
- `api-design-rules.md`
- `memory-resource-rules.md`

## 强制规则

- MUST: 新增 C 代码必须遵守项目统一命名、类型、返回值和错误处理规则。
- MUST: public API 必须清晰表达输入、输出、错误和所有权。
- MUST: 所有 buffer 操作必须带长度边界。
- MUST NOT: 不允许新增无边界字符串或内存写入。
- MUST NOT: 不允许在嵌入式运行时核心路径中随意使用动态内存。

## 任务导航

| 任务 | 重点文件 |
|---|---|
| 新增 C 文件 | `c-coding-standard.md` |
| 设计 public API | `api-design-rules.md` |
| 使用 buffer / queue / context | `memory-resource-rules.md` |
| 修改错误返回 | `api-design-rules.md`, `quality/error-handling-logging-diagnostics.md` |

