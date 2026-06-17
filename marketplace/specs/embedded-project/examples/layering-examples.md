# 分层示例

## 示例 1: LED 状态显示

错误做法：

`drivers/led/` 中实现 `led_show_modbus_error()`。

原因：

LED driver 不应该理解 Modbus 错误的业务语义。

正确做法：

- `drivers/led/` 提供 `led_on()`、`led_off()`、`led_toggle()`、`led_set_blink()`。
- `services/led_status_service/` 将系统状态映射为 LED 行为。
- `app/` 根据产品状态调用 `led_status_service`。

## 示例 2: Modbus RTU 通信

错误做法：

`drivers/uart/` 中解析 Modbus 功能码。

正确做法：

- `drivers/uart/` 只负责 UART 字节收发。
- `drivers/rs485/` 负责 RS485 半双工方向控制。
- `protocols/modbus_rtu/` 负责 Modbus RTU 帧构造、解析、CRC 和异常码。
- `services/communication_service/` 负责设备轮询和数据缓存。
- `app/` 负责产品级策略。

## 示例 3: 参数存储

错误做法：

`app/` 中直接操作 Flash 寄存器保存配置。

正确做法：

- `drivers/flash/` 负责 Flash 基础读写。
- `services/parameter_service/` 负责参数格式、校验、默认值和版本迁移。
- `app/` 只调用参数服务 API。

## 示例 4: 传感器采样

错误做法：

`app/` 直接配置 I2C 寄存器并解析传感器原始数据。

正确做法：

- `drivers/i2c/` 负责 I2C 传输能力。
- `drivers/sensor_xxx/` 负责传感器寄存器访问和原始值转换。
- `services/sampling_service/` 负责采样周期、滤波策略和异常统计。
- `app/` 只消费服务输出的业务数据。

