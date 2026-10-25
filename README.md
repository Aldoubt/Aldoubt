# 杨轩 · Aldoubt

**机器人定位与导航研发｜ROS 2｜LiDAR–IMU SLAM｜移动机器人系统工程**

华南农业大学农业机械化及其自动化专业。主要方向是移动机器人自主导航，重点关注 3D LiDAR–IMU 里程计、全局重定位、导航地图构建，以及将算法集成到 ROS 2 / Nav2 并在真实底盘上验证。

我希望解决的问题是：**机器人如何可靠地定位自己、理解可通行环境，并持续执行导航任务？**

- **方向：** LiDAR–IMU SLAM、全局重定位、点云地图处理、Nav2、ROS 2 系统集成
- **平台：** Livox MID360、Bunker 履带底盘、FW-mini 舵轮底盘
- **环境：** Ubuntu 22.04、ROS 2 Humble、C++、Python、Linux
- **求职方向：** 激光 SLAM / 定位导航算法 / 机器人软件研发

[Email](mailto:xuanyang.robotics@gmail.com) · [LinkedIn](https://www.linkedin.com/) · [所有仓库](https://github.com/Aldoubt?tab=repositories)

---

## 精选项目

我把作品集集中在几个能体现不同工程能力的项目上。仓库中的功能状态、测试证据和限制以各项目 README 为准；**已实现、离线验证、仿真验证和真实机器人验收不是同一件事。**

### 1. [AGT Navigation V3](https://github.com/Aldoubt/agt_navigation_v3) — ROS 2 定位与导航栈

**展示能力：系统集成、定位接口设计、Nav2 接入与现场验收。**

面向 MID360 与 Bunker 类履带底盘，围绕局部里程计、全局重定位、统一 TF 校正和 Nav2 组织导航运行链路。

- 明确区分局部里程计与全局定位校正的职责。
- 通过定位、TF、传感器时序与导航启动检查约束运行状态。
- 文档记录当前启动方式、地图资产准备、现场验收门槛及未通过项。

**阅读入口：** [README 与启动说明](https://github.com/Aldoubt/agt_navigation_v3)

### 2. [AGT Field Test Workbench](https://github.com/Aldoubt/agt_field_test_workbench) — 机器人现场测试工作台

**展示能力：测试流程工程化、传感器与底盘集成、实验可追溯性。**

目标是把建图数据准备、地图与路线检查、导航测试、受监督运动和录包分析组织成一致的工作流，减少现场调试对零散命令和个人记忆的依赖。

**阅读入口：** [README 与当前功能状态](https://github.com/Aldoubt/agt_field_test_workbench)

### 3. [AGT Map Reconstruction](https://github.com/Aldoubt/agt_map_reconstruction) — 3D 点云到导航地图

**展示能力：点云处理、地面与可通行性分析、几何验证。**

研究如何将 LIO 输出的 PCD 转换为可检查的导航地图，包含高程分析、农业行/走廊恢复、语义障碍表达、Nav2 地图导出，以及机器人多边形 footprint 和路线几何验证。

**阅读入口：** [README、实验阶段与限制](https://github.com/Aldoubt/agt_map_reconstruction)

### 4. [LIO Benchmark Tools](https://github.com/Aldoubt/lio_benchmark_tools) — LiDAR / LIO 可复现实验

**展示能力：算法评测、实验编排、数据分析与失败诊断。**

提供统一的离线实验组织方式，记录算法配置、版本、参数、轨迹健康和资源使用。项目明确区分算法成功运行、轨迹质量检查与有真值支持的精度评估，不将没有 ground truth 的结果包装成绝对精度排名。

**阅读入口：** [README 与实验协议](https://github.com/Aldoubt/lio_benchmark_tools)

### 5. [proc-lens](https://github.com/Aldoubt/proc-lens) — Linux / ROS 2 进程诊断工具

**展示能力：Linux 系统开发、Rust、可观测性与工具产品化。**

通过 Linux `/proc` 检查进程、资源占用和父子进程来源，并结合 ROS 2 工作空间与开发项目线索辅助定位后台任务。仓库提供安装和发布说明。

**阅读入口：** [README、截图与安装方法](https://github.com/Aldoubt/proc-lens)

---

## 我的工程工作流

```text
传感器 / 底盘接入
      ↓
时间同步、TF 与外参检查
      ↓
LiDAR–IMU 里程计与建图
      ↓
地图清洗、可通行性与导航资产
      ↓
全局重定位 + 局部跟踪
      ↓
Nav2 规划、控制与任务执行
      ↓
录包、指标、失败分析与回归测试
```

我重视的不只是让 Demo 跑起来，也包括明确模块边界、保存复现实验条件、区分证据与假设，以及记录系统在哪些条件下会失败。

## 如何阅读这些仓库

- **想看端到端导航工程：** 从 [AGT Navigation V3](https://github.com/Aldoubt/agt_navigation_v3) 开始。
- **想看点云与地图算法：** 查看 [AGT Map Reconstruction](https://github.com/Aldoubt/agt_map_reconstruction)。
- **想看算法对比与实验设计：** 查看 [LIO Benchmark Tools](https://github.com/Aldoubt/lio_benchmark_tools)。
- **想看测试工作流和系统诊断：** 查看 [Field Test Workbench](https://github.com/Aldoubt/agt_field_test_workbench) 与 [proc-lens](https://github.com/Aldoubt/proc-lens)。

上游算法、驱动和依赖的 fork 主要用于集成、复现或补丁维护；它们不代表我从零实现了对应的上游算法。涉及现场运行的项目会在 README 中说明验证范围和已知限制。

## 联系

欢迎交流机器人定位导航、LiDAR–IMU SLAM、ROS 2 系统集成和移动机器人现场测试。

- Email: xuanyang.robotics@gmail.com
- GitHub: [@Aldoubt](https://github.com/Aldoubt)
