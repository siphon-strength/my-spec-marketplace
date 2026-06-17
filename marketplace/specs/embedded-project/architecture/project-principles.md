# 项目总原则

## 1. 分层优先

- MUST: 在实现任何功能前，必须先判断该功能属于哪一层。
- MUST: 新增代码必须放在语义正确的目录中。
- MUST: 每个模块必须有清晰职责、清晰输入输出和清晰依赖。
- MUST NOT: 不允许为了快速实现功能而跨层写代码。

## 2. 驱动只提供能力

- MUST: `drivers/` 只提供硬件访问能力。
- MUST: driver public API 必须屏蔽寄存器细节和平台差异。
- MUST NOT: `drivers/` 不得决定产品业务语义。
- MUST NOT: `drivers/` 不得依赖 `app/` 或 `services/`。

## 3. 协议只处理协议

- MUST: `protocols/` 只处理协议帧、状态机、CRC/checksum、超时和协议错误。
- MUST: 协议层应通过 transport interface 访问传输能力。
- MUST NOT: `protocols/` 不得直接操作 GPIO、UART、DMA 或芯片寄存器。

## 4. 服务组织能力，应用编排业务

- MUST: `services/` 负责组织驱动、协议和公共能力，形成可复用业务服务。
- MUST: `app/` 负责任务编排、产品状态机和最终业务策略。
- MUST NOT: `services/` 不得包含产品启动主流程。
- MUST NOT: `app/` 不得绕过 service 或 protocol 直接操作底层硬件。

## 5. 非阻塞设计

- MUST: 所有周期性逻辑必须设计为非阻塞。
- MUST: 等待外设、通信、存储或传感器结果时必须使用超时机制。
- MUST NOT: 不允许在主循环、RTOS task 或协议轮询函数中使用无超时阻塞等待。

## 6. 可测试设计

- MUST: 纯逻辑模块必须尽量设计为可脱离硬件测试。
- SHOULD: 协议解析、CRC、ring buffer、状态机、参数校验应支持单元测试。
- SHOULD: 硬件相关模块应通过 adapter、mock 或 fake 隔离硬件依赖。

## 7. 可移植设计

- MUST: 与芯片、编译器、板级硬件强相关的代码必须隔离在 `platform/`、`vendor/` 或 `bsp/`。
- MUST NOT: 上层业务代码不得直接依赖具体 MCU 寄存器定义。

