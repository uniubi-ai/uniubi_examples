# Uniubi Examples

Uniubi 二次开发示例索引仓。当前版本的基础 demo 随对应代码仓一起维护，本仓提供统一索引，指向 C++ / Python / ROS 2 各自仓库中的版本同步示例。

后续出现跨多个仓库、不能自然归属到单一 SDK 仓的组合 demo 时，放在本仓维护。完整接口教程、DDS 直连接入说明和跨仓开发路径统一维护在 [`uniubi-docs`](https://github.com/uniubi-ai/uniubi-docs)。

## 示例索引

| 示例类型 | 实际位置 | 依赖 | 默认安全级别 |
|---|---|---|---|
| C++ SDK | [`uniubi_robot_sdk/examples`](https://github.com/uniubi-ai/uniubi_robot_sdk/tree/main/examples) | [`uniubi_robot_sdk`](https://github.com/uniubi-ai/uniubi_robot_sdk) | High-level / Low-level 均为交互 CLI，启动不自动执行动作；媒体订阅仅 aarch64 板内 |
| Python SDK | [`uniubi_robot_sdk_py/examples`](https://github.com/uniubi-ai/uniubi_robot_sdk_py/tree/main/examples) | [`uniubi_robot_sdk_py`](https://github.com/uniubi-ai/uniubi_robot_sdk_py) + [`uniubi_robot_sdk`](https://github.com/uniubi-ai/uniubi_robot_sdk) | 高级首跑安全动作；低级零力矩仅限吊架 / 急停条件；媒体订阅仅 aarch64 板内且 `sdk.MEDIA_ENABLED=True` |
| ROS 2 | [`uniubi_ros2`](https://github.com/uniubi-ai/uniubi_ros2/tree/main/src/uniubi_motion_bridge) | [`uniubi_robot_msgs`](https://github.com/uniubi-ai/uniubi_robot_msgs) + [`uniubi_ros2`](https://github.com/uniubi-ai/uniubi_ros2) | Motion bridge 标准 topic；`uniubi_motion_client` 自定义 C++ 流程；默认先做只读验证 |

## 使用方式

先按对应仓库 README 完成安装并运行示例：

- C++ 示例：构建 [`uniubi_robot_sdk`](https://github.com/uniubi-ai/uniubi_robot_sdk)，先运行 `example_highlevel --read-only`，在 `highlevel>` 中做状态/传感器/里程计验证；`example_lowlevel` 启动后同样先用 `status`、`motors` 检查，再执行 `stand`、`lie`、`damping`、`release`，Low-level 姿态命令会按需使能。两个 CLI 均不会自动启动动作；`example_media_frames` 仅用于 aarch64 板内本地部署。
- Python 示例：安装 [`uniubi_robot_sdk_py`](https://github.com/uniubi-ai/uniubi_robot_sdk_py)，并让 `UNIUBI_SDK_ROOT` 指向 [`uniubi_robot_sdk`](https://github.com/uniubi-ai/uniubi_robot_sdk)。`examples/example_highlevel.py --read-only` 是与 C++ 风格一致的 `highlevel>` 交互 CLI，先用 `status`、`motors`、`sensor 5`、`odom 5` 做只读验证，再按需 `take/start/send/stop/release`；`examples/example_lowlevel.py` 仍用于 Low-level 联调。`examples/example_media_frames.py` 仅用于 aarch64 板内本地部署，并要求当前 wheel 的 `sdk.MEDIA_ENABLED=True`。
- ROS 2 示例：先构建 [`uniubi_robot_msgs`](https://github.com/uniubi-ai/uniubi_robot_msgs)，再构建 [`uniubi_ros2`](https://github.com/uniubi-ai/uniubi_ros2) 的 `uniubi_motion_bridge` 和 `uniubi_motion_client` 包；普通业务默认从 Motion bridge 开始。
- DDS 直连接入：按 [`uniubi-docs/docs/uniubi_robot_dds_api.md`](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_robot_dds_api.md) 配置 Domain、QoS、topic 和 `device_id`。

## 安全策略

真实机器人首次联调默认只执行站立、趴下等低风险动作。`walking`、`move`、`bipedStand`、`handstand`、`jump*`、`damp` 等高风险运动动作应单独放入显式确认的示例或测试流程。

Low-level 示例必须将机器狗可靠吊起，保持四脚完全腾空且四肢能够自由活动，不得直接落地测试；测试过程中保持急停可触达并由专人值守。

## 文档

完整接口说明见：

- [`uniubi-docs`](https://github.com/uniubi-ai/uniubi-docs)
- [`uniubi-docs/docs/uniubi_high_level_sdk.md`](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_high_level_sdk.md)
- [`uniubi-docs/docs/uniubi_low_level_sdk.md`](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_low_level_sdk.md)
- [`uniubi-docs/docs/uniubi_media_sdk.md`](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_media_sdk.md)
- [`uniubi-docs/docs/uniubi_robot_dds_api.md`](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_robot_dds_api.md)
- [`uniubi-docs/docs/ros2_dds_interop_overview.md`](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/ros2_dds_interop_overview.md)

## 许可证

本仓库中的 UniUbi 原创示例和文档使用 Apache License 2.0。详见 [LICENSE](LICENSE) 和 [NOTICE](NOTICE)。
