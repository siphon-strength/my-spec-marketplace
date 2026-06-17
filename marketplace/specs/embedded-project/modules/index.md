# Modules 规范索引

本目录用于存放具体模块级 spec。

模块级 spec 只能补充项目级规范，不能覆盖项目级规范。

## 典型模块

- UART driver
- RS485 driver
- Modbus RTU protocol
- LED driver
- Flash driver
- Sensor driver
- Watchdog
- Parameter storage
- Diagnostics service

## 强制规则

- MUST: 模块级 spec 必须遵守项目级分层架构和依赖方向。
- MUST: 模块级 spec 必须明确所属层级。
- MUST: 模块级 spec 必须明确允许职责和禁止职责。
- MUST: 模块级 spec 必须说明 public API、状态所有权、并发规则和验证方式。
- MUST NOT: 模块级 spec 不得允许 `drivers/` 依赖 `app/`。
- MUST NOT: 模块级 spec 不得允许 `protocols/` 直接操作硬件寄存器。
- MUST NOT: 不允许把所有模块细节都堆进项目级 spec。

## 模板

新增模块规范时，MUST 复制并填写 `module-spec-template.md` 的结构。

