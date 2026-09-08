# 硬件方向概述

CodeLab 硬件部：嵌入式、树莓派、无人机，把软件和硬件结合起来做真实系统。

## 工作内容

- **嵌入式**：单片机（MCU）开发、传感器采集、控制逻辑（见 [embedded.md](embedded.md)）
- **树莓派**：Linux 单板电脑，跑 Python / 边缘 AI（见 [raspberry-pi.md](raspberry-pi.md)）
- **无人机**：飞控、航线、机载视觉（见 [uav.md](uav.md)）
- 软硬结合项目：上位机、通信协议、数据上云

## 常见项目形态

```text
传感器 / 设备
  ↓ 采集（MCU / 树莓派）
数据 / 控制指令
  ↓ 通信（串口 / MQTT / HTTP）
上位机 / 云端（Python / FastAPI）
  ↓ 展示、存储、决策
```

## 工程规范

- **代码与硬件分离**：固件、驱动、上位机分别建仓库
- **接口文档先行**：串口协议、MQTT 主题、API 先写清楚再联调
- **版本管理**：硬件改动（接线图、原理图）也要记录版本
- **日志与调试**：设备侧记录日志，出问题可回溯
- **安全**：先断电再接线；无人机飞行遵守规定，室内 / 空旷场地

## 常用工具链

- 单片机：Arduino / PlatformIO / STM32CubeIDE
- 树莓派：Raspberry Pi OS、GPIO、Camera、Docker
- 无人机：PX4 / ArduPilot、QGroundControl、MAVSDK
- 通用：串口工具（PuTTY / minicom）、逻辑分析仪、万用表

## 下一步

- 树莓派：[raspberry-pi.md](raspberry-pi.md)
- 嵌入式：[embedded.md](embedded.md)
- 无人机：[uav.md](uav.md)
