# 树莓派（Raspberry Pi）实践

树莓派是 CodeLab 硬件项目的主力平台：Linux 环境 + GPIO + 摄像头，适合做边缘计算和原型。

## 基础准备

- 烧录系统：Raspberry Pi Imager，推荐 Raspberry Pi OS Lite（无桌面，省资源）
- 连接：SSH（`ssh pi@<ip>`），推荐配置静态 IP 或 mDNS
- 换源：国内网络建议配置 apt 镜像，加快安装
- 基本配置：`raspi-config` 开启 SSH / 摄像头 / I2C

## 常用操作

```bash
# 更新系统
sudo apt update && sudo apt upgrade -y

# 查看温度 / 内存
vcgencmd measure_temp
free -h

# GPIO 操作（Python）
python3 -c "import gpiod; print('gpiod ok')"
```

## 典型项目

- **环境监测站**：DHT22 温湿度 + 定时上报 MQTT / 数据库
- **边缘视觉**：USB 摄像头 / CSI 摄像头 + OpenCV + YOLO 检测
- **智能小车**：GPIO 驱动电机 + 摄像头避障
- **内网服务器**：Docker 跑代码仓库、监控面板

## 规范要点

- **Python 项目**按 [python.md](../software/python.md) 规范：uv + ruff + pytest
- **开机自启**：systemd service 管理，不写 crontab 裸脚本
- **远程部署**：Git 拉代码 + systemd / Docker 管理进程
- **备份**：项目代码全在 GitHub，SD 卡只存运行环境
- **日志**：服务日志用 systemd journal（`journalctl -u <service>`）

## systemd 示例

```ini
# /etc/systemd/system/my-app.service
[Unit]
Description=My App
After=network.target

[Service]
User=pi
WorkingDirectory=/home/pi/my-app
ExecStart=/home/pi/my-app/.venv/bin/python -m src.main
Restart=always

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable --now my-app
```

## 下一步

- 嵌入式基础：[embedded.md](embedded.md)
- 无人机：[uav.md](uav.md)
