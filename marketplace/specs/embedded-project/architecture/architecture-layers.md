# 分层架构规范

## 标准层级

| Layer | Directory | 主要职责 |
|---|---|---|
| Application Layer | `app/` | 产品状态机、任务编排、业务策略 |
| Service Layer | `services/` | 组合驱动、协议和公共能力形成服务 |
| Protocol Layer | `protocols/` | 协议帧、解析、CRC、协议状态机 |
| Middleware Layer | `middleware/` | 与业务无关的通用软件能力 |
| Driver Layer | `drivers/` | 外设和外部芯片最小可复用驱动 |
| Board Support Layer | `bsp/` | PCB 板级资源映射 |
| Platform Layer | `platform/` | 编译器、启动、链接、RTOS port |
| Vendor Layer | `vendor/` | 芯片厂商库和第三方底层库 |
| Common Layer | `common/` | 公共类型、错误码、工具和纯算法 |
| Config Layer | `config/` | 项目配置、功能开关、编译配置 |

## 1. `app/`

职责：
- 产品状态机
- 任务编排
- 应用级业务策略
- 系统启动后的业务流程组织

规则：
- MUST: `app/` 只负责任务编排、产品状态机和业务策略。
- MUST: `app/` 只能通过 public API 调用下层模块。
- MUST NOT: `app/` 不得直接操作寄存器。
- MUST NOT: `app/` 不得直接操作 GPIO、UART、SPI、I2C、DMA 等底层硬件。
- MUST NOT: `app/` 不得直接拼接协议原始帧。

## 2. `services/`

职责：
- 将驱动、协议和公共能力组合成业务服务
- 设备轮询
- 参数服务
- 故障管理
- 诊断服务
- 通信服务

规则：
- MUST: `services/` 负责形成可复用业务服务。
- MUST: `services/` 可以调用 `protocols/`、`middleware/`、`drivers/`、`common/` 的 public API。
- MUST NOT: `services/` 不得直接访问芯片寄存器。
- MUST NOT: `services/` 不得绕过 driver 直接操作硬件。

## 3. `protocols/`

职责：
- 协议帧构造
- 协议帧解析
- CRC/checksum
- 协议状态机
- 超时和异常码处理

规则：
- MUST: `protocols/` 只负责协议逻辑。
- MUST: 协议输入输出必须通过明确的 buffer、stream 或 transport interface 表达。
- MUST NOT: `protocols/` 不得直接操作 GPIO、UART、DMA 或寄存器。
- MUST NOT: `protocols/` 不得依赖 `app/`。
- SHOULD: 协议层应通过 transport interface 访问传输能力。

## 4. `middleware/`

职责：
- ring buffer
- event bus
- software timer
- 通用状态机框架
- 消息队列封装
- 与业务无关的中间件能力

规则：
- MUST: `middleware/` 必须保持通用性。
- MUST NOT: `middleware/` 不得包含具体产品业务逻辑。
- MUST NOT: `middleware/` 不得依赖 `app/` 或具体业务 service。

## 5. `drivers/`

职责：
- 外设驱动
- 外部芯片驱动
- DMA buffer 管理
- ISR 最小处理
- 硬件初始化和基础收发能力

规则：
- MUST: `drivers/` 只负责硬件外设或外部芯片的最小可复用驱动。
- MUST: 驱动必须通过 public header 向上提供接口。
- MUST NOT: `drivers/` 不得包含业务策略。
- MUST NOT: `drivers/` 不得依赖 `app/` 或 `services/`。
- MUST NOT: UART driver 不得解析 Modbus 功能码。
- MUST NOT: LED driver 不得决定产品状态灯语义。

## 6. `bsp/`

职责：
- board pin map
- board clock
- board peripheral mapping
- PCB 相关硬件资源定义

规则：
- MUST: `bsp/` 只描述当前 PCB 板级硬件资源。
- MUST: 所有板级引脚和外设实例映射必须集中管理。
- MUST NOT: `bsp/` 不得包含产品业务逻辑。
- MUST NOT: `bsp/` 不得解析协议。

## 7. `platform/` 和 `vendor/`

职责：
- startup
- linker script
- CMSIS
- vendor HAL/LL
- compiler port
- RTOS port
- 芯片厂商库

规则：
- MUST: `platform/` 和 `vendor/` 只承载平台、芯片、编译器、启动文件、链接脚本和 RTOS port 相关代码。
- MUST NOT: 不允许在该层写产品业务逻辑。
- MUST NOT: 不允许在该层写协议解析、设备轮询或状态灯策略。

## 8. `common/`

职责：
- common types
- error code
- compiler abstraction
- small utilities
- containers
- pure algorithms

规则：
- MUST: `common/` 只放无业务语义的公共能力。
- MUST NOT: `common/` 不得依赖 `app/`、`services/`、`protocols/` 或 `drivers/`。

## 9. `config/`

职责：
- project config
- feature config
- build config
- compile-time switches

规则：
- MUST: `config/` 只放项目配置、功能开关和编译配置。
- MUST NOT: `config/` 不得包含函数实现和业务流程。

