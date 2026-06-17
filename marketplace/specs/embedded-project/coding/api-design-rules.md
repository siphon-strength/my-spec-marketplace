# API 设计规范

## Public API

- MUST: public API 必须只暴露模块承诺长期维护的能力。
- MUST: public API 必须稳定、命名一致、参数语义清晰。
- MUST: 可失败 API 必须返回项目统一错误码，例如 `error_code_t`。
- MUST: API 必须说明是否可在 ISR 中调用。
- MUST: API 必须说明是否线程安全。
- MUST NOT: public API 不得暴露模块内部状态的可写地址。
- MUST NOT: public API 不得要求调用者理解底层寄存器位含义。

## 参数和返回值

- MUST: 指针参数必须允许性明确，若不允许 `NULL` 必须检查并返回参数错误。
- MUST: buffer 参数必须同时传入指针和长度。
- MUST: 输出 buffer 必须传入容量，函数必须返回实际写入长度或明确状态。
- MUST NOT: 不允许使用无长度的裸数组参数表达可写 buffer。
- SHOULD: 枚举参数应提供非法值检查。

## 初始化和生命周期

- MUST: 每个有状态模块必须定义初始化顺序。
- MUST: `xxx_init()` 必须可报告失败原因。
- MUST: 资源释放或反初始化 API 必须说明何时需要调用。
- MUST NOT: 不允许 API 在未初始化状态下静默工作。

## 兼容性

- MUST: 修改 public API 时必须评估所有调用方。
- MUST: 删除或改变 API 行为必须在 review 中说明影响。
- SHOULD: 对外 API 的结构体应预留版本或 size 字段，以支持未来扩展。

