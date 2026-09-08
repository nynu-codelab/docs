# Java / Spring Boot 实践

CodeLab 软件部的后端主力技术栈。模板见 [java-template](https://github.com/nynu-codelab/templates/tree/main/java-template)。

## 版本基线

- JDK 21（LTS）
- Maven 构建
- Spring Boot 3.x

## 标准结构

```text
src/
├── main/
│   ├── java/com/codelab/xxx/
│   │   ├── controller/    # REST 接口层
│   │   ├── service/       # 业务逻辑层
│   │   ├── repository/    # 数据访问层
│   │   └── config/        # 配置类
│   └── resources/
│       ├── application.yml
│       └── application-local.yml   # 本地配置（gitignore）
└── test/                  # 单元测试
```

## 规范要点

- **分层清晰**：Controller 不写业务逻辑，Service 不碰 SQL 细节
- **配置外置**：数据库、密钥等放环境变量，本地用 `application-local.yml`（不提交）
- **接口风格**：RESTful，统一返回结构，错误有明确状态码
- **测试**：核心 Service 必须有单元测试（JUnit 5）
- **依赖**：`pom.xml` 用版本管理，不随便引入新依赖

## 本地开发

```bash
# application-local.yml.example 复制为 application-local.yml，填入本地配置
mvn spring-boot:run -Dspring-boot.run.profiles=local
# 或 IDE 里配置启动参数 --spring.profiles.active=local
```

## CI（模板自带）

```text
mvn -B compile   # 编译
mvn -B test      # 测试
mvn -B package   # 打包
```

## 下一步

- 用模板建项目：[templates/java-template](https://github.com/nynu-codelab/templates/tree/main/java-template)
- Docker 化：[../docker/dockerfile.md](../docker/dockerfile.md)
