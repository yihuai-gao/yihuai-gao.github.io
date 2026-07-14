---
layout: page
title: Open Source Projects
permalink: /opensource/
description: Open-source tools I build and maintain for the robotics community.
nav: true
nav_order: 1
---

Good robotics research runs on good infrastructure. Here are some open-source tools I built (and use every day) for real-robot experiments.

### [Real-Env](https://github.com/real-stanford/real-env)

**A shared codebase for real-world robot deployment — from teleop to policy rollout.**

A collection of controllers and peripherals for robotic manipulation research, developed at Stanford REALab during the [Gated Memory Policy](https://gated-memory-policy.github.io/) project. Every component — arm (UR5/UR5e, ARX5), gripper (WSG50, fin-ray fingers), camera (iPhone, webcam, GoPro), and teleop device (SpaceMouse, UMI, iPhUMI) — runs as an independent server process, with Hydra config aggregation for reproducible experiments and multi-process, GPU-accelerated logging. Supports both single-arm and bimanual setups.

### [UMI Data](https://umi-data.github.io/)

**Data is better when universally sharable.**

A community registry of robot manipulation datasets built around the [UMI](https://umi-gripper.github.io/) interface, which is initialized by [Huy Ha](https://github.com/huy-ha) and I am actively maintaining. With just a GoPro and a 3D-printed gripper, any new robot platform can get up and running with UMI policies — no robot-specific data collection required. The registry welcomes contributions beyond the strict UMI spec (different sensors, gripper variants) and ships standardized zarr storage plus a `ReplayBuffer` utility for efficient training.

### [ARX5 SDK](https://github.com/real-stanford/arx5-sdk)

**Full control of your ARX5 robot arm — no ROS, no sudo, no fuss.**

A C++/Python controller for the ARX5 robot arm: a 500 Hz joint controller with ~0.4 ms motor communication latency, Cartesian-space control with keyboard and SpaceMouse teleoperation, teach-and-replay, and multi-arm support from a single process. One `pip install` away, with a clean, fully type-hinted Python API. It powers projects such as [UMI-on-Legs](https://umi-on-legs.github.io/), Vision-in-Action, and DynaGuide.

### [RobotMQ](https://github.com/yihuai-gao/robot-message-queue)

**A robot-centric message queue that never blocks your control loop.**

Lightweight, high-performance messaging for robotics Python applications. All message passing happens on C++ background threads, so the Python GIL never gets in the way of your real-time control. It moves large data through shared memory (~2 GB/s locally) and crosses machines via ZeroMQ, supports both pub-sub and request-reply, and accepts any bytes-serializable data — numpy arrays included. No brokers, no external services: just `RMQServer` and `RMQClient`.

### [RoboLogger](https://github.com/yihuai-gao/robologger)

**Record every modality of your robot at its own frequency — without missing a beat.**

A lightweight, distributed logging library for robot learning. Each modality — arms, cameras, grippers, mobile base — logs in its own process at its own rate (30–125 Hz), buffers in memory during an episode, and batch-writes standardized zarr episodes on stop, so your control loop never stalls on disk I/O. Video is encoded in real time with GPU-accelerated FFmpeg (depth supported), and all loggers are coordinated through [RobotMQ](https://github.com/yihuai-gao/robot-message-queue) with start/stop/pause/resume commands.
