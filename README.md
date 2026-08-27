<h1 align="center">Xuan Yang · Aldoubt</h1>

<p align="center">
  <strong>Robotics Autonomy · Navigation · LiDAR–IMU Localization · 3D Mapping · ROS 2</strong>
</p>

<p align="center">
  <a href="mailto:xuanyang.robotics@gmail.com"><img src="https://img.shields.io/badge/Email-xuanyang.robotics%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <img src="https://img.shields.io/badge/ROS%202-Humble-22314E?style=flat-square&logo=ros&logoColor=white" alt="ROS 2 Humble" />
  <img src="https://img.shields.io/badge/C%2B%2B-17-00599C?style=flat-square&logo=cplusplus&logoColor=white" alt="C++17" />
  <img src="https://img.shields.io/badge/Focus-Robotics%20Autonomy-2ea44f?style=flat-square" alt="Robotics Autonomy" />
</p>

I am an **Agricultural Machinery and Automation** student at **South China Agricultural University**, building autonomous robot systems for complex structured and semi-structured environments.

我目前聚焦 **机器人自主导航、LiDAR–IMU 定位、3D 点云环境理解与 ROS 2 真机系统**。农业场景是主要验证环境，但目标不是只解决单一农业任务，而是形成可迁移到移动机器人、巡检、割草、无人系统等平台的 **Robotics Autonomy** 能力。

> **What I work on:** make a real robot know **where it is**, understand **where it can go**, plan **how to get there**, and execute the task **reliably**.

---

## System View

```text
LiDAR / IMU / Camera / RTK / Wheel
                |
                v
     Calibration & Synchronization
                |
                v
       State Estimation / LIO
                |
       +--------+--------+
       |                 |
       v                 v
 Localization       Registered Cloud
 Relocalization          |
                         v
                Ground / Traversability
                         |
                         v
                 Navigation Map
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

My current engineering focus is the complete chain from **state estimation and map assets** to **planning, control, mission execution and real-robot validation**.

---

## Featured Engineering Evidence

### 1. [AGT Navigation Runtime](https://github.com/Aldoubt/agt_navigation_runtime) — ROS 2 Autonomous Navigation Runtime

**Role:** main real-robot execution stack.

- Separates robot runtime from offline map / route asset production.
- Integrates sensor adapters, FAST-LIVO2 odometry, ICP/NDT relocalization, local perception, Nav2 planning/control, safety arbitration, chassis adapters, BehaviorTree and mission management.
- Current extracted ROS 2 Humble workspace has completed an **independent 23-package build**.
- Architecture target: `Site Package + Vehicle Profile + Task -> Localization -> Perception -> Planner/Controller -> Mission -> Safety -> Chassis`.

**Evidence to add next:** real-robot navigation GIF, RViz runtime screenshot, failure-recovery demo.

---

### 2. [AGT Map Reconstruction](https://github.com/Aldoubt/Aldoubt-agt_map_reconstruction) — Navigation-oriented 3D Map Reconstruction

**Problem:** agricultural LiDAR maps contain vegetation clutter, repetitive row geometry and navigation-irrelevant points.

```text
LIO PCD
  -> preprocessing
  -> ground segmentation
  -> elevation / traversability
  -> corridor recovery
  -> semantic navigation map
  -> polygon-footprint validation
  -> in-aisle route feasibility search
```

- Compares height threshold, PMF, CSF and Patchwork-style ground segmentation strategies.
- Exports Nav2-compatible trinary static maps with explicit safety semantics.
- Uses the real robot polygon footprint instead of only circular clearance approximations.
- Extends validation from strict aisle centerlines to constant-offset and smooth lateral-route search.

**Evidence to add next:** raw PCD vs traversability vs recovered corridor vs route overlay comparison.

---

### 3. [LIO Benchmark Tools](https://github.com/Aldoubt/lio_benchmark_tools) — Reproducible LiDAR–IMU Evaluation

**Role:** keep SLAM evaluation independent from navigation and robot-control code.

- Unified experiment orchestration for **FAST-LIVO2, Point-LIO, GLIM and DLIO**.
- Records bag, IMU, timestamp handling, parameters, workspace versions and required upstream patches.
- Standardizes run-directory contracts and trajectory evaluation to make algorithm comparisons auditable and reproducible.
- Focuses on failure analysis in repetitive agricultural geometry instead of only successful demos.

**Evidence to add next:** trajectory comparison, APE/RPE summary and representative failure cases.

---

### 4. [AGT Traversability Lab](https://github.com/Aldoubt/agt_traversability_lab) — Local LiDAR Perception & Traversability

**Research focus:** convert online MID360 observations into navigation-relevant local environment representations.

```text
rosbag2 / MID360
  -> point-cloud baseline
  -> ground segmentation
  -> local map
  -> traversability estimation
  -> navigation interface
```

Current work focuses on vegetation growth, corridor deformation, local ground structure and safe-feasibility estimation.

---

## Repository Architecture

The navigation work is intentionally split by responsibility:

```text
agt_navigation_v2
Offline mapping / semantic map / route asset production
                |
                | versioned deployment assets
                v
agt_navigation_runtime
Online localization / perception / planning / control / mission / safety
```

Supporting research repositories validate individual capabilities before they are integrated into the runtime:

```text
lio_benchmark_tools       -> state-estimation evaluation
agt_map_reconstruction    -> offline navigation-map recovery
agt_traversability_lab    -> online local perception experiments
```

---

## Technical Stack

### Engineering / regular use

`ROS 2 Humble` · `Nav2` · `TF2` · `rosbag2` · `RViz2` · `Gazebo` · `C++17` · `Python` · `Eigen` · `PCL` · `OpenCV` · `CMake` · `Docker` · `Git`

### Robotics algorithms / working knowledge

`FAST-LIO2` · `FAST-LIVO2` · `ICP` · `NDT` · `OccupancyGrid` · `Ground Segmentation` · `Traversability` · `Behavior Trees` · `Global Planning` · `Path Tracking`

### Currently deepening

`SO(3) / SE(3)` · `Lie Groups` · `Jacobian Derivation` · `ESKF` · `IMU Modeling` · `Nonlinear Least Squares` · `Factor Graphs` · `Hybrid A*` · `MPC / MPPI`

---

## Hardware & Deployment Experience

`Livox MID360` · `IMU` · `RTK/GNSS` · `Industrial Camera` · `BUNKER` · `Ackermann Chassis`

I prefer **reproducible offline validation before real-robot deployment**, while keeping datasets, parameters, software versions and failure cases traceable.

---

## Current Learning Direction

I am deliberately moving from **framework-level integration** toward **algorithm-level understanding**:

```text
SO(3) / SE(3)
      -> Jacobians
      -> Probability / ESKF
      -> IMU model & preintegration
      -> Nonlinear optimization
      -> LIO internals
      -> Factor-graph optimization
      -> Vehicle-aware planning & control
```

The goal is to connect **mathematical models -> algorithm implementation -> robot behavior -> experimental evidence**.

---

## Contact

- Email: **xuanyang.robotics@gmail.com**
- GitHub: **[@Aldoubt](https://github.com/Aldoubt)**

For technical questions about a repository, opening an Issue is preferred so the context, failure mode and solution remain reproducible.
