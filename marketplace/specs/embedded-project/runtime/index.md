# Runtime 规范索引

本目录约束 RTOS、裸机调度、ISR、DMA、状态机和非阻塞运行时设计。

## 必读文件

- `rtos-and-concurrency.md`
- `interrupt-and-dma-rules.md`
- `scheduler-and-state-machine.md`

## 强制规则

- MUST: 所有周期性任务必须有明确调度方式。
- MUST: 涉及共享状态时必须说明并发保护方式。
- MUST: ISR 和 DMA 必须保持边界清晰。
- MUST: 长流程必须优先使用状态机或事件驱动设计。
- MUST NOT: 不允许通过长时间阻塞或忙等实现业务流程。

## 任务导航

| 任务 | 重点文件 |
|---|---|
| 新增 RTOS task | `rtos-and-concurrency.md`, `scheduler-and-state-machine.md` |
| 修改 ISR | `interrupt-and-dma-rules.md` |
| 修改 DMA buffer | `interrupt-and-dma-rules.md`, `memory-resource-rules.md` |
| 新增状态机 | `scheduler-and-state-machine.md` |

