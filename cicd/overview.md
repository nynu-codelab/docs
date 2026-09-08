# CI/CD 概述

CI（持续集成）指代码合并前自动检查；CD（持续部署）指自动发布。CodeLab 目前先做 **基础 CI**，部署后续扩展。

## CodeLab 的 CI 管线

```text
Pull Request
  ↓ Lint（代码规范）
  ↓ Test（自动化测试）
  ↓ Build（构建产物）
Merge
  ↓ Docker Build（构建镜像）
  ↓ Tag（打版本标签）
  ↓ GHCR / Harbor（推送到镜像仓库）
  ↓ 服务器部署（后续阶段）
```

## 现状（已完成的部分）

| 环节 | 状态 |
| --- | --- |
| PR → Lint → Test → Build → Merge | 已通过模板 CI 落地 |
| Docker 镜像 Build → Tag → GHCR | 预留工作流，按需启用 |
| 自动部署到服务器 | 暂不做，后续扩展 |

## 原则

- **CI 必须通过才能合并**（`main` / `develop` 分支保护）
- 优先复用模板中的工作流，不为复杂而复杂
- 不引入 Kubernetes / Terraform 等重型设施，用 Docker Compose 足够

## 下一步

- GitHub Actions 怎么写：[github-actions.md](github-actions.md)
- 项目模板自带 CI：[templates](https://github.com/nynu-codelab/templates)
