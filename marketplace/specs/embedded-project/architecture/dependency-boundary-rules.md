# 依赖方向和模块边界规范

## 单向依赖

允许的主要依赖方向：

```text
app
  -> services
  -> protocols / middleware / drivers / common
protocols
  -> middleware / common
drivers
  -> bsp / platform / vendor / common
bsp
  -> platform / vendor / common
platform
  -> vendor / common
```

## 强制规则

- MUST: 上层只能通过下层 public API 访问下层能力。
- MUST: 下层不得反向调用上层业务逻辑。
- MUST: 回调接口必须通过抽象 interface 或注册函数表达，不得直接 include 上层头文件。
- MUST: 模块内部状态必须由模块自己拥有和维护。
- MUST NOT: `drivers/` 不得 include `app/` 或 `services/` 的头文件。
- MUST NOT: `protocols/` 不得直接 include `drivers/` 的私有头文件。
- MUST NOT: `common/` 不得依赖任何业务层、协议层或驱动层。
- MUST NOT: 不允许通过全局变量绕过模块边界。

## Public API 边界

- MUST: public API 必须表达模块可提供的能力。
- MUST: public API 参数必须明确所有权、长度、生命周期和错误返回。
- MUST NOT: public API 不得暴露模块 private context 的可写指针，除非该 context 本身就是显式句柄类型。
- SHOULD: 跨层 API 优先使用 `const`、固定宽度整数类型和项目统一错误码。

## 例外处理

- MUST: 如果现有项目结构与本规范冲突，agent 必须标记 `NEED_CONFIRMATION` 并说明冲突。
- MUST: 如果确有性能或实时性原因需要跨层优化，必须写明理由、风险、替代方案和 review 结论。
- MUST NOT: 不允许以“临时调试”为理由提交跨层依赖。

