# Docker Compose 实践

Compose 用 YAML 一次性启动多个容器。CodeLab 的本地开发环境和数据库都靠它。

## 最小示例

```yaml
# docker-compose.yml
services:
  app:
    build: .
    ports:
      - "8080:8080"
    env_file:
      - .env
    depends_on:
      - db

  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_USER: ${DB_USER}
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_DB: ${DB_NAME}
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

## 环境变量：.env 与 .env.example

- 真实配置写在本地 `.env`（**已被 .gitignore 忽略**，不进 git）
- 仓库里只提交 `.env.example`，填示例值：

```bash
# .env.example
DB_USER=codelab
DB_PASSWORD=change-me
DB_NAME=codelab
```

```bash
# 本地实际操作
cp .env.example .env   # 复制并填入真实值
docker compose up -d
```

## 常用命令

```bash
docker compose up -d          # 启动（后台）
docker compose up --build     # 改代码后重建
docker compose ps             # 查看状态
docker compose logs -f app    # 跟踪应用日志
docker compose down           # 停止
docker compose down -v        # 停止并删除数据卷（慎用！数据会丢）
```

## 规范要点

- 服务名用短横线小写：`api-server`、`mysql-db`
- 密钥一律走 `.env` / 环境变量，禁止写死在 compose 文件
- `depends_on` 只保证启动顺序，不代表数据库已就绪（应用层做重试）
- 数据库数据用命名卷持久化（上面的 `pgdata`）

## 下一步

- 本地流程：`cp .env.example .env` → `docker compose up -d` → 本地开发
- 发布流程：[../cicd/overview.md](../cicd/overview.md)
