# MID360 Simulation with FAST-LIO

本仓库集成了 **Livox MID360 激光雷达仿真插件** 与 **FAST-LIO**，提供一个完整的仿真环境。  
在 Gazebo 中可以运行 FAST-LIO 并处理来自 MID360 的点云数据，同时支持雷达在仿真环境中运动，便于进行建图与定位实验。

---

## 功能介绍

- 在 **Gazebo** 中加载 Livox MID360 雷达仿真模型。  
- 支持运行 **FAST-LIO**，实时处理仿真点云。  
- 雷达支持运动，可以模拟真实环境中的 UAV 或移动机器人。  
- 提供 **rviz 可视化**，方便查看点云和建图结果。  

---

## 环境要求

- 已编译安装 [FAST-LIO](https://github.com/RightTr/FAST_LIO.git）

---

## 使用步骤

### 1. 启动仿真与 FAST-LIO
运行以下命令：
```bash
roslaunch livox_laser_simulation mid360.launch
```
该命令会：
- 启动 Gazebo 并加载 mid360.world
- 加载 Livox MID360 雷达插件  
- 启动 FAST-LIO 节点进行点云处理
- 启动rviz可视化，选择 `/livox/lidar` 话题即可查看点云。


## 目录结构

```
mid360-FAST_LIO/
├── mid360_simulation_plugin/   # MID360 仿真插件
│   ├── livox_laser_simulation/
│   │   ├── launch/             # 启动文件
│   │   ├── models/             # 模型文件
│   │   ├── worlds/             # Gazebo 世界文件
│   │   └── src/                # 插件源码
└── FAST_LIO/                   # FAST-LIO 算法（集成使用）
```

## 运动方向控制

| 操作 | 键位（平面移动） | 键位（全向移动，Shift） |
|------|------------------|-------------------------|
| 前进 | `i` | `I` |
| 后退 | `,` | `<` |
| 左移 | `j` | `J` |
| 右移 | `l` | `L` |
| 前左斜 | `u` | `U` |
| 前右斜 | `o` | `O` |
| 后左斜 | `m` | `M` |
| 后右斜 | `.` | `>` |
| 上升 | `t` | `t` |
| 下降 | `b` | `b` |
| 停止 | 其它任意键 | 其它任意键 |

## 速度调节

| 操作 | 键位 |
|------|------|
| 增加最大速度 10% | `q` |
| 减小最大速度 10% | `z` |
| 增加线速度 10% | `w` |
| 减小线速度 10% | `x` |
| 增加角速度 10% | `e` |
| 减小角速度 10% | `c` |

## 退出控制
按 `CTRL-C` 退出键盘控制

## 当前默认速度
```
speed 0.5  turn 1.0
```

## 注意事项

- 请确保 `fast_lio/config/mapping/mid360.yaml` 已正确配置雷达参数，需要修改为
```
common:
    lid_topic:  "/livox/lidar"
    imu_topic:  "/livox/imu"
```
- 如果 Gazebo 场景中没有障碍物，可以修改 `worlds/mid360.world` 或 `test_pattern.world` 文件，自定义环境

