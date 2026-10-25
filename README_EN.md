# Xuan Yang · Aldoubt

**Robotics Localization & Navigation | ROS 2 | LiDAR–IMU SLAM | Mobile Robot Systems**

I study Agricultural Machinery and Automation at South China Agricultural University. My work focuses on mobile robot autonomy, especially 3D LiDAR–IMU odometry, global relocalization, navigation-map construction, and integrating these components into ROS 2 / Nav2 systems for real-platform evaluation.

**The problem I work on:** How can a mobile robot localize reliably, understand traversable environments, and execute navigation tasks continuously?

- **Focus:** LiDAR–IMU SLAM, global relocalization, point-cloud mapping, Nav2, ROS 2 integration
- **Platforms:** Livox MID360, Bunker tracked robot, FW-mini steering-wheel robot
- **Stack:** Ubuntu 22.04, ROS 2 Humble, C++, Python, Linux
- **Roles:** LiDAR SLAM, localization/navigation algorithms, robotics software engineering

[Email](mailto:xuanyang.robotics@gmail.com) · [Repositories](https://github.com/Aldoubt?tab=repositories)

---

## Featured Projects

This portfolio highlights a small set of projects that demonstrate different engineering skills. For each project, refer to its README for the exact status and evidence. **Implemented, offline-tested, simulation-tested, and field-validated are different levels of evidence.**

### 1. [AGT Navigation V3](https://github.com/Aldoubt/agt_navigation_v3) — ROS 2 Localization & Navigation

**Demonstrates:** System integration, localization interfaces, Nav2 integration, and field acceptance workflows.

A ROS 2 navigation stack targeting MID360 and Bunker-class tracked robots. It organizes local odometry, global relocalization, a single global TF correction authority, and Nav2 navigation.

The repository documents launch procedures, map-asset preparation, TF and sensor-timing checks, acceptance gates, and known limitations.

### 2. [AGT Field Test Workbench](https://github.com/Aldoubt/agt_field_test_workbench) — Field-Test Workflow

**Demonstrates:** Test workflow engineering, sensor/chassis integration, and experiment traceability.

The project aims to organize map preparation, map and route checks, navigation trials, supervised motion, and rosbag-based diagnostics into a consistent workflow.

### 3. [AGT Map Reconstruction](https://github.com/Aldoubt/agt_map_reconstruction) — Point Clouds to Navigation Maps

**Demonstrates:** Point-cloud processing, terrain/traversability analysis, and geometric validation.

An offline toolkit for turning LIO-generated PCD maps into inspectable navigation assets, including elevation analysis, agricultural corridor recovery, semantic obstacle representation, Nav2 map export, and polygon-footprint route validation.

### 4. [LIO Benchmark Tools](https://github.com/Aldoubt/lio_benchmark_tools) — Reproducible LiDAR/LIO Experiments

**Demonstrates:** Algorithm evaluation, experiment orchestration, data analysis, and failure diagnosis.

The framework organizes offline experiments and records configurations, versions, parameters, trajectory-health checks, and resource usage. It distinguishes a successful run from a valid accuracy evaluation and does not claim absolute accuracy without ground truth.

### 5. [proc-lens](https://github.com/Aldoubt/proc-lens) — Linux / ROS 2 Process Diagnostics

**Demonstrates:** Linux systems programming, Rust, observability, and software packaging.

A lightweight process inspector based on Linux `/proc`, with resource monitoring and process-provenance clues for ROS 2 workspaces and development projects. The repository includes installation and release instructions.

---

## Engineering Workflow

```text
Sensor and chassis integration
             ↓
Time synchronization, TF and extrinsic checks
             ↓
LiDAR–IMU odometry and mapping
             ↓
Map cleanup, traversability and navigation assets
             ↓
Global relocalization + local tracking
             ↓
Nav2 planning, control and mission execution
             ↓
Rosbags, metrics, failure analysis and regression tests
```

I care not only about getting a demo to run, but also about module boundaries, reproducible experiments, separating evidence from assumptions, and documenting failure conditions.

## Where to Start

- **End-to-end navigation engineering:** [AGT Navigation V3](https://github.com/Aldoubt/agt_navigation_v3)
- **Point-cloud and map processing:** [AGT Map Reconstruction](https://github.com/Aldoubt/agt_map_reconstruction)
- **Algorithm evaluation:** [LIO Benchmark Tools](https://github.com/Aldoubt/lio_benchmark_tools)
- **Test workflow and system diagnostics:** [Field Test Workbench](https://github.com/Aldoubt/agt_field_test_workbench) and [proc-lens](https://github.com/Aldoubt/proc-lens)

Forks of upstream algorithms, drivers, and dependencies are used for integration, reproduction, or patch maintenance; they should not be interpreted as algorithms implemented from scratch. Repositories involving field operation document their validation scope and known limitations.

## Contact

Open to conversations about robot localization/navigation, LiDAR–IMU SLAM, ROS 2 integration, and real-world mobile robot testing.

- Email: xuanyang.robotics@gmail.com
- GitHub: [@Aldoubt](https://github.com/Aldoubt)
