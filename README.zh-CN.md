# Uniubi Examples

[English](README.md)

Uniubi 机器人二次开发示例。你可以从控制方式或开发语言选择合适的入口；需要组合多个 SDK、ROS 2 或机器人能力的完整应用时，可以在本仓库中扩展为独立示例。

## 选择开发入口

| 开发目标 | 推荐入口 |
|---|---|
| 调用站立、趴下、行走等机器人内置能力 | [High-level 开发导读](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/how-to/high-level-control.md) |
| 运行自己的控制策略，直接控制关节位置或扭矩 | [Low-level 开发导读](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/how-to/low-level-control.md) |
| 通过 ROS 2 topic / service 使用机器人运动能力 | [ROS 2 Motion Bridge 导读](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/how-to/ros2-motion-bridge.md) |
| 订阅摄像头、麦克风或编码帧 | [Media SDK 文档](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_media_sdk.md) |
| 训练、导出并部署 Low-level 策略 | [策略训练、导出与回放](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/how-to/train-export-replay.md) |

## C++ 示例

完整构建和运行说明见 [`uniubi_robot_sdk/examples`](https://github.com/uniubi-ai/uniubi_robot_sdk/tree/main/examples)。

- [High-level 交互控制](https://github.com/uniubi-ai/uniubi_robot_sdk/blob/main/examples/example_highlevel.cpp)：查询状态、传感器和里程计，调用机器人内置动作。
- [Low-level 姿态控制](https://github.com/uniubi-ai/uniubi_robot_sdk/blob/main/examples/example_lowlevel.cpp)：读取电机布局，验证站立、趴下和阻尼控制。
- [Low-level TensorRT 策略](https://github.com/uniubi-ai/uniubi_robot_sdk/blob/main/examples/example_lowlevel_tensorrt.cpp)：输入 ONNX，每次启动构建 FP32 TensorRT engine，并以 50 Hz 运行策略。
- [MediaBus 帧订阅](https://github.com/uniubi-ai/uniubi_robot_sdk/blob/main/examples/example_media_frames.cpp)：在 aarch64 板内订阅和保存音视频帧。

[进入 C++ SDK](https://github.com/uniubi-ai/uniubi_robot_sdk)

## Python 示例

完整安装和运行说明见 [`uniubi_robot_sdk_py/examples`](https://github.com/uniubi-ai/uniubi_robot_sdk_py/tree/main/examples)。

- [High-level 交互控制](https://github.com/uniubi-ai/uniubi_robot_sdk_py/blob/main/examples/example_highlevel.py)：查询状态、传感器和里程计，调用机器人内置动作。
- [Low-level 控制](https://github.com/uniubi-ai/uniubi_robot_sdk_py/blob/main/examples/example_lowlevel.py)：演示 Low-level 连接、观测和控制帧下发。
- [Low-level TensorRT 策略](https://github.com/uniubi-ai/uniubi_robot_sdk_py/blob/main/examples/example_lowlevel_tensorrt.py)：在 Orin 上从 ONNX 构建 FP32 TensorRT engine，不依赖 PyTorch。
- [MediaBus 帧订阅](https://github.com/uniubi-ai/uniubi_robot_sdk_py/blob/main/examples/example_media_frames.py)：在 aarch64 板内订阅和保存音视频帧。

[进入 Python SDK](https://github.com/uniubi-ai/uniubi_robot_sdk_py)

## ROS 2 示例

- [`uniubi_motion_bridge`](https://github.com/uniubi-ai/uniubi_ros2/tree/main/src/uniubi_motion_bridge)：将 High-level 运动能力映射为 ROS 2 topic 和 service。
- [`uniubi_motion_client`](https://github.com/uniubi-ai/uniubi_ros2/tree/main/src/uniubi_motion_client)：使用 ROS 2 接口查询状态和控制机器人。
- [`uniubi_robot_msgs`](https://github.com/uniubi-ai/uniubi_robot_msgs)：机器人消息、service 和 action 定义。

[进入 ROS 2 仓库](https://github.com/uniubi-ai/uniubi_ros2)

## 开发文档

- [Uniubi 开发文档](https://github.com/uniubi-ai/uniubi-docs)
- [SDK 构建与安装](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/BUILD.md)
- [High-level SDK API](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_high_level_sdk.md)
- [Low-level SDK API](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_low_level_sdk.md)
- [Media SDK API](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_media_sdk.md)
- [DDS 与 ROS 2 互操作](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/ros2_dds_interop_overview.md)

## 实机安全

首次实机联调应从只读查询和低风险姿态开始，并始终保持急停可触达、有人值守。

通用 Low-level 姿态和零力矩示例应在安全吊架上验证，保持四脚完全腾空。包含 `walk` 的 TensorRT 策略采用分阶段验证：吊架上只执行 `stand` 和 `lay`；确认姿态及关节方向正常后，将机器狗放到空旷、平整、无障碍地面，再执行 `stand` → `walk` → `stop` → `lay`。不要在四脚腾空时执行 `walk`。

## 许可证

本仓库中的 Uniubi 原创示例和文档使用 Apache License 2.0。详见 [LICENSE](LICENSE) 和 [NOTICE](NOTICE)。
