# C 编码规范

## 命名

- MUST: 文件名、函数名、变量名、宏名、结构体名必须使用英文标识符。
- MUST: 函数名使用 `module_action()` 或 `module_object_action()` 风格。
- MUST: static 函数应使用模块前缀或局部语义清晰的名称。
- MUST: 宏名使用全大写和下划线，例如 `UART_RX_BUFFER_SIZE`。
- MUST NOT: 不允许把代码标识符翻译成中文。

## 类型

- MUST: 固定宽度整数使用 `stdint.h` 类型，例如 `uint8_t`、`uint16_t`、`uint32_t`。
- MUST: 布尔语义使用 `bool`，并包含 `stdbool.h`。
- MUST: 指针参数如果不修改目标对象，必须使用 `const`。
- MUST NOT: 不允许在跨模块 public API 中使用大小不明确的 `int` 表达协议字段、寄存器字段或持久化数据。

## 函数

- MUST: 函数必须职责单一。
- MUST: 可失败函数必须返回统一错误码或明确状态。
- MUST: 输出参数必须在函数注释或命名中明确。
- MUST NOT: 不允许函数通过隐式全局状态返回关键结果。
- SHOULD: 函数长度过长时应按职责拆分，而不是通过注释分段掩盖复杂度。

## 头文件

- MUST: public header 只暴露必要类型、宏和 API。
- MUST: private header 只能被模块内部源文件包含。
- MUST: header 必须具备 include guard 或 `#pragma once`。
- MUST NOT: public header 不得包含无关 vendor/platform 私有头文件。

## 全局变量

- MUST: 全局状态必须有明确所有者。
- MUST: 可被 ISR 或多 task 访问的变量必须有并发保护策略。
- MUST NOT: 不允许新增未受控可写全局变量。
- SHOULD: 模块状态优先封装在 context 结构体或模块私有 static 对象中。

## 注释

- MUST: public API 必须说明参数、返回值和调用约束。
- MUST: 复杂状态机、并发边界和硬件时序必须有简短说明。
- MUST NOT: 不允许用注释替代清晰命名。

