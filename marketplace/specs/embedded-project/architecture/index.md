# Architecture 规范索引

本目录定义项目级架构规则，是所有模块级规范的上位约束。

## 必读文件

- `project-principles.md`: 项目总原则
- `architecture-layers.md`: 标准分层架构
- `directory-structure.md`: 推荐目录结构
- `dependency-boundary-rules.md`: 依赖方向和模块边界规则

## 强制规则

- MUST: 所有代码必须先判断所属层级。
- MUST: 所有新增目录必须符合分层架构。
- MUST: 所有模块必须遵守单向依赖。
- MUST: 模块 public API 必须表达能力边界，而不是暴露内部状态。
- MUST NOT: 不允许模块级规范覆盖项目级架构规则。
- MUST NOT: 不允许上层业务代码直接依赖 MCU 寄存器、vendor HAL 内部实现或板级硬件细节。

## 任务导航

| 任务 | 重点文件 |
|---|---|
| 新建目录或模块 | `directory-structure.md`, `dependency-boundary-rules.md` |
| 判断代码放置位置 | `architecture-layers.md` |
| 检查跨层调用 | `dependency-boundary-rules.md` |
| 拆分已有混乱代码 | `project-principles.md`, `architecture-layers.md` |

