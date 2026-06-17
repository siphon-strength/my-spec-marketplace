# RTOS 和并发规范

## RTOS task

- MUST: 每个 task 必须有明确职责、优先级、周期或阻塞条件。
- MUST: task 名称必须表达职责，例如 `communication_task`、`diagnostics_task`。
- MUST: task stack size 必须有估算依据或项目默认规则。
- MUST: task 间通信必须通过 queue、event flag、semaphore、stream buffer 或明确封装。
- MUST NOT: 不允许高优先级 task 执行低价值长耗时工作。
- MUST NOT: 不允许多个 task 无保护读写同一共享状态。

## 裸机调度

- MUST: 裸机项目必须定义主循环调度策略。
- MUST: 周期性 poll 函数必须快速返回。
- MUST: poll 函数不得长期阻塞。
- MUST: 超时必须基于系统 tick 判断。
- SHOULD: 每个模块提供 `xxx_init()` 和 `xxx_poll(now_ms)` 类型接口。

## 并发保护

- MUST: 共享数据必须明确是单写者、多读者、锁保护还是消息传递。
- MUST: ISR 与 task 共享变量必须考虑 `volatile`、临界区、原子访问或 RTOS FromISR API。
- MUST: 锁的获取顺序必须稳定，避免死锁。
- MUST NOT: 不允许在持锁状态下执行不可控长耗时操作。

## 超时

- MUST: 所有等待通信、外设、存储或状态转换的路径必须有超时。
- MUST: 超时错误必须返回或上报到明确错误处理路径。
- MUST NOT: 不允许无期限等待信号量、队列、硬件标志或协议响应。

