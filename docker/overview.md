# Docker 概述

Docker 让"在我电脑上能跑"变成"在哪都能跑"。CodeLab 项目统一用 Docker 打包与运行。

## 核心概念

- **Image（镜像）**：打包好的运行环境 + 代码，只读
- **Container（容器）**：镜像的运行实例，可启停
- **Dockerfile**：描述如何构建镜像
- **docker-compose**：用 YAML 编排多个容器（如 应用 + 数据库）

## 安装

- Windows / macOS：安装 [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Linux：安装 Docker Engine + compose 插件
- 安装后运行 `docker version` 验证

## 常用命令

```bash
docker build -t <name> .          # 构建镜像
docker images                     # 查看镜像
docker run -p 8080:8080 <name>    # 运行容器
docker ps                         # 查看运行中容器
docker logs <container>           # 查看日志
docker compose up -d              # 启动编排（后台）
docker compose down               # 停止并删除
```

## CodeLab 的标准路径

```text
本地开发
  ↓ Docker Build（构建镜像）
  ↓ Docker Compose（本地一键启动）
  ↓ GitHub Actions（CI 中构建）
  ↓ GHCR / Harbor（镜像仓库）
  ↓ 服务器部署（生产环境）
```

新项目请从 [templates](https://github.com/nynu-codelab/templates) 的模板开始，Dockerfile 和 compose 都已内置。

## 下一步

- 怎么写 Dockerfile：[dockerfile.md](dockerfile.md)
- 怎么编排服务：[docker-compose.md](docker-compose.md)
- CI 里怎么用：[../cicd/github-actions.md](../cicd/github-actions.md)
