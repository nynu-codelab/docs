# 无人机（UAV）实践

CodeLab 无人机方向：从组装调试到自主飞行，结合视觉做落地应用。

## 平台

| 类型 | 用途 | 说明 |
| --- | --- | --- |
| 成品航拍机（DJI） | 航拍、巡检数据采集 | 成熟稳定，SDK 开发 |
| 开源飞控（PX4 / ArduPilot） | 自主飞行、科研 | 可改可学，主流 |
| 自组穿越机 | 竞速 / 花飞 | 偏硬件，进阶 |

## 知识基础

- **飞控**：PX4 / ArduPilot 的架构，姿态估计、控制回路
- **通信**：MAVLink 协议、遥测（数传）
- **地面站**：QGroundControl / Mission Planner
- **机载计算机**：树莓派 / Jetson，跑视觉与决策

## 开发环境

- 仿真优先：PX4 SITL + Gazebo，代码先在仿真里跑
- 实际飞行：先手动 / 定点，再试自主任务
- 日志分析：飞控日志（ulog）用 Flight Review 查看

## 典型项目

- **航线巡检**：按预设航线自动飞行、拍照
- **视觉目标跟踪**：机载相机检测目标，跟随飞行
- **测绘 / 建图**：航拍拼接、正射影像
- **避障**：视觉 / 雷达避障（进阶）

## 规范要点

- **安全第一**：飞行遵守法规与场地要求，远离人群，室外空旷区域
- **仿真先行**：新代码先在 SITL 验证，不直接上真机
- **代码仓库化**：飞控参数、脚本、机载代码分开管理
- **日志留存**：每次飞行保存日志，复盘用
- **分级测试**：单元测试 → 仿真 → 真机低风险科目 → 完整任务

## 工具链

- MAVSDK / pymavlink（程序控制）
- OpenCV + YOLO（机载视觉，参考 [computer-vision.md](../algorithm/computer-vision.md)）
- ROS 2（可选，复杂系统用）

## 下一步

- 机载视觉：[../algorithm/computer-vision.md](../algorithm/computer-vision.md)
- 树莓派机载：[raspberry-pi.md](raspberry-pi.md)
