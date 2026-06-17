# Spec 导航索引

本文件用于帮助 agent 根据当前任务快速定位需要读取的规范文件。

## 必读规则

- MUST: 在实现任何代码前，必须先阅读本文件。
- MUST: 根据任务类型加载对应领域的 `index.md`。
- MUST: 如果任务涉及多个领域，必须同时读取多个领域规范。
- MUST NOT: 不允许只阅读单个模块文件后直接实现代码。
- MUST NOT: 不允许跳过 `architecture/` 中的分层和依赖规则。

## 任务到文档映射

| 任务类型 | 必须阅读 |
|---|---|
| 新建项目结构 | `architecture/index.md`, `agent/index.md` |
| 新增功能模块 | `architecture/index.md`, `modules/index.md`, `agent/index.md` |
| 修改驱动 | `architecture/index.md`, `coding/index.md`, `runtime/index.md`, `modules/index.md` |
| 修改协议解析 | `architecture/index.md`, `coding/index.md`, `runtime/index.md`, `quality/index.md` |
| 涉及 RTOS task | `runtime/index.md`, `quality/index.md` |
| 涉及 ISR / DMA | `runtime/index.md`, `coding/index.md`, `quality/index.md` |
| 涉及错误码 / 日志 / 诊断 | `quality/index.md` |
| 修改公共 API | `coding/index.md`, `architecture/index.md` |
| 修改目录结构 | `architecture/index.md` |
| 代码实现完成后 | `quality/review-checklist.md` |

## Agent 总原则

- MUST: 先判断层级，再设计接口，再实现代码。
- MUST: 新增代码必须放在正确目录。
- MUST: 新增函数必须属于正确模块。
- MUST: 不得破坏单向依赖原则。
- MUST: 修改完成后必须进行 self-check。
- MUST NOT: 不允许为了快速交付而绕过 public API 或模块边界。

