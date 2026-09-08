# Dockerfile 实践

Dockerfile 描述如何构建镜像。CodeLab 要求：**多阶段构建 + 精简镜像 + 不泄露密钥**。

## 基本结构

```dockerfile
# 阶段一：构建
FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /app
COPY pom.xml .
RUN mvn -B dependency:go-offline
COPY src ./src
RUN mvn -B package -DskipTests

# 阶段二：运行（只拷贝产物，镜像小）
FROM eclipse-temurin:21-jre
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

这是 Java 项目的标准写法：构建阶段大，运行阶段小。

## Python 示例

```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

## 规范要点

- **多阶段构建**：构建产物与运行环境分离，镜像体积小
- **尽量用官方基础镜像**：`python:3.12-slim`、`eclipse-temurin:21-jre`、`node:22-alpine`
- **先复制依赖文件再复制代码**：利用层缓存，改代码不用重新装依赖
- **不要 COPY .env / 密钥**：运行时用环境变量注入
- **固定基础镜像版本**：不用 `latest`，保证可复现

## 本地构建

```bash
docker build -t my-app .
docker run --rm -p 8080:8080 my-app
```

## 常见问题

- 镜像太大：检查是否把 `.git`、`node_modules`、`target` 复制进去了（用 `.dockerignore`）
- 构建慢：调整 COPY 顺序，利用缓存
- 容器启动即退出：看日志 `docker logs <container>`，通常是入口命令问题

## 下一步

- 多容器编排：[docker-compose.md](docker-compose.md)
- CI 中构建并推送：[../cicd/github-actions.md](../cicd/github-actions.md)
