<h1 align="center">杨轩 · Aldoubt</h1>

<p align="center">
  <strong>机器人自主系统 · 自主导航 · LiDAR–IMU 定位 · 3D 地图 · ROS 2</strong>
</p>

<p align="center">
  <strong>简体中文 | <a href="./README_EN.md">English</a></strong>
</p>

<p align="center">
  <a href="mailto:xuanyang.robotics@gmail.com"><img src="https://img.shields.io/badge/Email-xuanyang.robotics%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <img src="https://img.shields.io/badge/ROS%202-Humble-22314E?style=flat-square&logo=ros&logoColor=white" alt="ROS 2 Humble" />
  <img src="https://img.shields.io/badge/C%2B%2B-17-00599C?style=flat-square&logo=cplusplus&logoColor=white" alt="C++17" />
  <img src="https://img.shields.io/badge/Focus-Robotics%20Autonomy-2ea44f?style=flat-square" alt="Robotics Autonomy" />
</p>

我是 **华南农业大学农业机械化及其自动化专业** 学生，目前聚焦 **机器人自主导航、LiDAR–IMU 定位、3D 点云环境理解与 ROS 2 真机系统**。

农业场景是我主要的验证环境，但目标并不是只解决单一农业任务，而是形成能够迁移到移动机器人、巡检机器人、割草机器人、无人系统等平台的 **Robotics Autonomy / 机器人自主系统能力**。

> **我关注的问题：让真实机器人知道自己在哪里、理解哪里能走、规划怎么走，并可靠地完成任务。**

---

## 系统视角

```text
LiDAR / IMU / Camera / RTK / Wheel
                |
                v
          标定与时间同步
                |
                v
         状态估计 / LIO
                |
       +--------+--------+
       |                 |
       v                 v
   定位 / 重定位        注册点云
                           |
                           v
                    地面 / 可通行性
                           |
                           v
                      导航地图
                           |
                  +--------+--------+
                  |                 |
                  v                 v
               Planner          Controller
                  \               /
                   \             /
                    v           v
                  Mission / BehaviorTree
                           |
                         Safety
                           |
                         Chassis
```

目前工程重点是打通从 **状态估计与地图资产** 到 **规划、控制、任务执行和真机验证** 的完整自主导航链路。

---

## 核心项目与工程证据

### 1. [AGT Navigation Runtime](https://github.com/Aldoubt/agt_navigation_runtime) — ROS 2 自主导航运行时

**定位：** 当前主要的真机运行与执行系统。

- 将机器人在线运行时与离线地图、语义和路线资产生产解耦。
- 集成传感器适配、FAST-LIVO2 里程计、ICP/NDT 重定位、局部感知、Nav2 规划与控制、安全仲裁、底盘适配、BehaviorTree 与任务管理。
- 当前抽取后的 ROS 2 Humble workspace 已完成 **23 个 package 独立构建验证**。
- 运行链路目标：`Site Package + Vehicle Profile + Task -> Localization -> Perception -> Planner/Controller -> Mission -> Safety -> Chassis`。

---

### 2. [AGT Map Reconstruction](https://github.com/Aldoubt/Aldoubt-agt_map_reconstruction) — 面向导航的 3D 地图恢复

**问题：** 农业 LiDAR 地图中存在大量植被杂波、重复垄行结构和与导航无关的三维点。

```text
LIO PCD
  -> 预处理
  -> 地面分割
  -> 高程 / 可通行性
  -> 通道恢复
  -> 语义导航地图
  -> 机器人多边形足迹验证
  -> 通道内路线可行性搜索
```

- 对比 Height Threshold、PMF、CSF 与 Patchwork-style 等地面分割策略。
- 输出符合 Nav2 使用习惯的三值静态地图，并显式区分静态障碍与不确定区域。
- 使用真实机器人 Polygon Footprint 进行通道验证，而不是只使用等效圆形膨胀近似。
- 从严格中心线验证进一步扩展到 constant-offset 和 smooth lateral route 搜索，用于判断通道内真实可行路线。

---

### 3. [LIO Benchmark Tools](https://github.com/Aldoubt/lio_benchmark_tools) — 可复现 LiDAR–IMU 评测

**定位：** 将 SLAM / LIO 评测与导航、控制代码解耦，建立独立实验资产。

- 为 **FAST-LIVO2、Point-LIO、GLIM、DLIO** 建立统一运行与实验编排方式。
- 记录 rosbag、IMU、时间戳处理、参数、workspace 版本及必要上游补丁。
- 统一 Run Directory Contract 和轨迹评价流程，使横向算法比较可审计、可复现。
- 不只展示成功 Demo，更关注重复农业结构和退化场景中的漂移、失效与边界条件。

---

### 4. [AGT Traversability Lab](https://github.com/Aldoubt/agt_traversability_lab) — 局部 LiDAR 感知与可通行性

**研究重点：** 将 MID360 在线观测转换为能够直接服务导航的局部环境表达。

```text
rosbag2 / MID360
  -> 点云显示基线
  -> 地面分割
  -> 局部地图
  -> 可通行性估计
  -> 导航接口
```

当前重点关注植被生长、通道变形、局部地面结构与安全通行性的实时判断。

---

## 仓库架构

导航相关代码按职责进行拆分：

```text
agt_navigation_v2
离线建图 / 语义地图 / 路线资产生产
                |
                | 版本化部署资产
                v
agt_navigation_runtime
在线定位 / 感知 / 规划 / 控制 / 任务 / 安全
```

支持研究仓库用于在进入运行时之前独立验证具体能力：

```text
lio_benchmark_tools       -> 状态估计与 LIO 评测
agt_map_reconstruction    -> 离线导航地图恢复
agt_traversability_lab    -> 在线局部感知实验
```

---

## 技术栈

### 日常工程使用

`ROS 2 Humble` · `Nav2` · `TF2` · `rosbag2` · `RViz2` · `Gazebo` · `C++17` · `Python` · `Eigen` · `PCL` · `OpenCV` · `CMake` · `Docker` · `Git`

### 机器人算法与工程认知

`FAST-LIO2` · `FAST-LIVO2` · `ICP` · `NDT` · `OccupancyGrid` · `Ground Segmentation` · `Traversability` · `Behavior Trees` · `Global Planning` · `Path Tracking`

### 当前重点进深

`SO(3) / SE(3)` · `Lie Groups` · `Jacobian Derivation` · `ESKF` · `IMU Modeling` · `Nonlinear Least Squares` · `Factor Graphs` · `Hybrid A*` · `MPC / MPPI`

---

## 硬件与部署经验

`Livox MID360` · `IMU` · `RTK/GNSS` · `Industrial Camera` · `BUNKER` · `Ackermann Chassis`

工程上优先采用 **离线可复现验证 -> 真机部署** 的方式，并尽量保证数据、参数、软件版本与失败案例可追溯。

---

## 当前学习进深路线

我正在有意识地从 **框架级集成** 向 **算法级理解** 深入：

```text
SO(3) / SE(3)
      -> Jacobian
      -> 概率模型 / ESKF
      -> IMU 模型与预积分
      -> 非线性优化
      -> LIO 内部机制
      -> 因子图优化
      -> 车辆约束规划与控制
```

目标是把 **数学模型 -> 算法实现 -> 机器人行为 -> 实验佐证** 串成一条完整能力链。

---

## 作品集与视觉佐证

后续会持续把结果图、GIF 和完整演示视频整理到 [`assets/`](./assets/) 并接入主页，优先展示：

- 温室真机自主导航与任务执行
- RViz 中的定位、规划、控制与状态变化
- 原始点云到导航地图的恢复对比
- LIO 多算法轨迹与 APE / RPE 评测
- 局部地面分割与可通行性感知

---

## 联系方式

- 邮箱：**xuanyang.robotics@gmail.com**
- GitHub：**[@Aldoubt](https://github.com/Aldoubt)**

如果是某个具体仓库的技术问题，建议优先通过对应仓库的 Issue 交流，便于保留问题背景、失效模式与解决过程。
