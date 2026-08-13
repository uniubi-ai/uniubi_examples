# Uniubi Examples

[简体中文](README.zh-CN.md)

Examples for developing applications with Uniubi robots. Choose an entry point by control mode or programming language. Complete applications that combine multiple SDKs, ROS 2, or several robot capabilities can be added to this repository as standalone examples.

## Choose a Development Path

| Goal | Recommended starting point |
|---|---|
| Call built-in robot capabilities such as standing, laying, and walking | [High-level development guide](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/how-to/high-level-control.md) |
| Run a custom control policy and command joint positions or torques directly | [Low-level development guide](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/how-to/low-level-control.md) |
| Use robot motion capabilities through ROS 2 topics and services | [ROS 2 Motion Bridge guide](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/how-to/ros2-motion-bridge.md) |
| Subscribe to camera, microphone, or encoded media frames | [Media SDK documentation](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_media_sdk.md) |
| Train, export, and deploy a Low-level policy | [Policy training, export, and replay](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/how-to/train-export-replay.md) |

## C++ Examples

See [`uniubi_robot_sdk/examples`](https://github.com/uniubi-ai/uniubi_robot_sdk/tree/main/examples) for complete build and run instructions.

- [High-level interactive control](https://github.com/uniubi-ai/uniubi_robot_sdk/blob/main/examples/example_highlevel.cpp): query state, sensor data, and odometry, and invoke built-in robot actions.
- [Low-level posture control](https://github.com/uniubi-ai/uniubi_robot_sdk/blob/main/examples/example_lowlevel.cpp): inspect the motor layout and validate standing, laying, and damping control.
- [Low-level TensorRT policy](https://github.com/uniubi-ai/uniubi_robot_sdk/blob/main/examples/example_lowlevel_tensorrt.cpp): load an ONNX model, build an FP32 TensorRT engine on every start, and run the policy at 50 Hz.
- [MediaBus frame subscription](https://github.com/uniubi-ai/uniubi_robot_sdk/blob/main/examples/example_media_frames.cpp): subscribe to and save audio and video frames locally on an aarch64 board.

[Open the C++ SDK](https://github.com/uniubi-ai/uniubi_robot_sdk)

## Python Examples

See [`uniubi_robot_sdk_py/examples`](https://github.com/uniubi-ai/uniubi_robot_sdk_py/tree/main/examples) for complete installation and run instructions.

- [High-level interactive control](https://github.com/uniubi-ai/uniubi_robot_sdk_py/blob/main/examples/example_highlevel.py): query state, sensor data, and odometry, and invoke built-in robot actions.
- [Low-level control](https://github.com/uniubi-ai/uniubi_robot_sdk_py/blob/main/examples/example_lowlevel.py): demonstrate a Low-level connection, observations, and control-frame transmission.
- [Low-level TensorRT policy](https://github.com/uniubi-ai/uniubi_robot_sdk_py/blob/main/examples/example_lowlevel_tensorrt.py): build an FP32 TensorRT engine from ONNX on Orin without PyTorch.
- [MediaBus frame subscription](https://github.com/uniubi-ai/uniubi_robot_sdk_py/blob/main/examples/example_media_frames.py): subscribe to and save audio and video frames locally on an aarch64 board.

[Open the Python SDK](https://github.com/uniubi-ai/uniubi_robot_sdk_py)

## ROS 2 Examples

- [`uniubi_motion_bridge`](https://github.com/uniubi-ai/uniubi_ros2/tree/main/src/uniubi_motion_bridge): expose High-level motion capabilities through ROS 2 topics and services.
- [`uniubi_motion_client`](https://github.com/uniubi-ai/uniubi_ros2/tree/main/src/uniubi_motion_client): query state and control the robot through the ROS 2 interfaces.
- [`uniubi_robot_msgs`](https://github.com/uniubi-ai/uniubi_robot_msgs): robot message, service, and action definitions.

[Open the ROS 2 repository](https://github.com/uniubi-ai/uniubi_ros2)

## Developer Documentation

- [Uniubi developer documentation](https://github.com/uniubi-ai/uniubi-docs)
- [SDK build and installation](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/BUILD.md)
- [High-level SDK API](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_high_level_sdk.md)
- [Low-level SDK API](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_low_level_sdk.md)
- [Media SDK API](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/uniubi_media_sdk.md)
- [DDS and ROS 2 interoperability](https://github.com/uniubi-ai/uniubi-docs/blob/main/docs/ros2_dds_interop_overview.md)

## Real-Robot Safety

Begin the first real-robot session with read-only queries and low-risk postures. Keep the emergency stop within reach and an operator present at all times.

Run general Low-level posture and zero-torque examples on a secure safety rig with all feet clear. Validate a TensorRT policy that includes `walk` in two stages: run only `stand` and `lay` on the rig; after confirming the posture and joint directions, place the robot on clear, level, obstacle-free ground and run `stand` → `walk` → `stop` → `lay`. Never execute `walk` while the robot's feet are suspended.

## License

Original Uniubi examples and documentation in this repository are licensed under the Apache License 2.0. See [LICENSE](LICENSE) and [NOTICE](NOTICE).
