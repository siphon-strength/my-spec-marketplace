# 目录结构规范

## 推荐项目目录树

```text
project_root/
├── app/
│   ├── app_main.c
│   ├── app_task.c
│   ├── app_state.c
│   └── app_config.h
├── services/
│   ├── communication_service/
│   ├── parameter_service/
│   ├── fault_manager/
│   └── diagnostics_service/
├── protocols/
│   └── protocol_name/
├── middleware/
│   ├── ring_buffer/
│   ├── event_bus/
│   └── software_timer/
├── drivers/
│   └── peripheral_or_chip/
├── bsp/
│   ├── board_config.h
│   ├── board_pins.h
│   └── board_peripherals.c
├── platform/
│   ├── startup/
│   ├── linker/
│   ├── compiler/
│   └── rtos_port/
├── vendor/
├── common/
│   ├── error_code.h
│   ├── common_types.h
│   └── compiler_abstraction.h
├── config/
│   ├── project_config.h
│   └── feature_config.h
└── tests/
    ├── unit/
    └── mocks/
```

## 目录规则

- MUST: 新增目录必须先判断所属层级。
- MUST: 模块目录名必须表达模块能力或对象，不能表达临时任务。
- MUST: public header 应放在模块对外可见位置，并只暴露必要 API。
- MUST: private source/header 必须保持模块内部可见。
- MUST NOT: 不允许创建 `misc/`、`temp/`、`new/`、`test2/` 等语义不清目录。
- MUST NOT: 不允许把跨层临时文件放在项目根目录。
- SHOULD: 纯逻辑模块应具备 `tests/unit/` 下的最小测试入口。

## 文件命名规则

- MUST: C 源文件和头文件使用小写英文、数字和下划线。
- MUST: 模块内部文件名应以模块名或职责名为前缀，例如 `uart_driver.c`、`parameter_store.c`。
- MUST NOT: 不允许使用中文文件名作为 C 代码文件名。
- SHOULD: 平台或厂商自动生成文件 MAY 保持原厂命名。

