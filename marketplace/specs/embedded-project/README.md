# Enterprise Embedded Project Spec

本 spec 是企业级嵌入式项目通用工程规范，用于约束 MCU/RTOS/裸机嵌入式 C 项目的目录结构、分层架构、模块边界、编码规范、运行时规范、质量策略和 agent 实现行为。

本 spec 不是 LED、UART、RS485、Modbus、Sensor、Flash 或 Watchdog 的专用实现规范。上述模块 MAY 作为分层边界示例出现，但 MUST NOT 成为项目级规范的默认核心。

## 定位

- MUST: 项目级规范负责约束所有模块都必须遵守的工程秩序。
- MUST: 模块级规范只负责补充某个具体模块的实现细节。
- MUST: 当模块级规范与项目级规范冲突时，必须优先遵守项目级规范。
- MUST: 本模板安装后会成为目标项目的 `.trellis/spec/` 起点。
- MUST NOT: 不允许把本 spec 当作某个具体业务功能的实现说明。

## 推荐阅读顺序

1. 先读 `index.md`
2. 再读 `architecture/index.md`
3. 编码任务读 `coding/index.md`
4. 涉及 RTOS、ISR、DMA、状态机时读 `runtime/index.md`
5. 涉及错误处理、测试和 review 时读 `quality/index.md`
6. agent 实现代码前必须读 `agent/index.md`
7. 具体模块设计参考 `modules/index.md`

## 安装路径约束

- MUST: 本模板目录内容必须直接对应最终 `.trellis/spec/` 内容。
- MUST NOT: `marketplace/specs/embedded-project/` 内部不得再额外包含一层 `spec/`。
- MUST NOT: `marketplace/specs/embedded-project/` 内部不得再额外包含一层 `embedded-project/`。

