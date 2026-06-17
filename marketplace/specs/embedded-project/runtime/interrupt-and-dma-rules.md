# ISR 和 DMA 规范

## ISR

- MUST: ISR 只允许执行最小化处理，例如清中断标志、搬运少量数据、记录状态、发送事件。
- MUST: ISR 调用 RTOS API 时必须使用对应 FromISR 版本。
- MUST NOT: 不允许在 ISR 中执行复杂业务逻辑。
- MUST NOT: 不允许在 ISR 中调用 `printf()`、`malloc()`、`free()` 或阻塞 API。
- MUST NOT: 不允许在 ISR 中执行完整协议解析，除非该解析极小且有明确实时性理由。
- SHOULD: ISR 中产生的复杂工作应转移到 task、service 或 poll 函数中处理。

## DMA

- MUST: DMA buffer 必须有明确所有者。
- MUST: DMA 完成、半完成、错误中断必须有明确处理路径。
- MUST: DMA 与 CPU 共享 buffer 时必须考虑 cache、`volatile`、memory barrier 或平台等价机制。
- MUST: DMA buffer 的长度、对齐和生命周期必须被文档化。
- MUST NOT: 不允许多个模块无边界地直接操作同一个 DMA buffer。

## 中断与模块边界

- MUST: driver 层负责硬件中断最小处理。
- MUST: protocol 或 service 层的后续处理必须通过事件、queue、callback 或 poll 触发。
- MUST NOT: ISR 不得直接调用 `app/` 业务策略函数。

