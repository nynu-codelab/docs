# CodeLab Docs

本仓库只放两类文档：**codelab-admin 怎么维护项目**、**software（软件研发）怎么协作提 PR**。技术栈教程按需查，不作为入门必读。

## 我是 codelab-admin → 项目维护

| 文档 | 内容 |
| --- | --- |
| [新仓库四步配置](github/repository-setup.md) | 建仓库、加 team、CODEOWNERS、分支保护 |
| [仓库命名与权限模型](github/repository.md) | 三 team 模型、可见性、默认分支保护 |
| [工程安全基线](engineering/security.md) | 密钥、CI、依赖安全；泄露事件响应 |
| [项目与技术资产交接](engineering/handover.md) | 人员变动时仓库、权限、密钥怎么交 |

## 我是 software 开发者 → 怎么协作

| 文档 | 内容 |
| --- | --- |
| [Git 概述](git/overview.md) / [分支模型](git/branching.md) / [Commit 规范](git/commit-convention.md) | 日常 Git |
| [Issue 规范](github/issue.md) | 怎么写 Issue |
| [PR 流程](github/pull-request.md) | 怎么提 PR |
| [Code Review](github/code-review.md) | 怎么审、怎么被审 |
| [工程流程总览](engineering/overview.md) | 需求 → 发布全流程 |
| [技术方案与 ADR](engineering/technical-design.md) | 什么时候写设计文档 |
| [测试与提测](engineering/testing.md) | 提测准入 |
| [发布与回滚](engineering/release.md) | 版本、发布、回滚 |
| [技术文档规范](engineering/documentation.md) | README、设计文档怎么写 |

## 技术参考（按需查）

- 语言规范：[Java](software/java.md)、[Python](software/python.md)、[TypeScript](software/typescript.md)
- [Docker 概述](docker/overview.md) · [Dockerfile](docker/dockerfile.md) · [Compose](docker/docker-compose.md)
- [CI/CD 概述](cicd/overview.md) · [GitHub Actions](cicd/github-actions.md)

## 制度在哪

组织架构、入组退出、考勤、奖惩、成果署名与保密制度在飞书 CodeLab 成员手册；本仓库不复制，只写 GitHub 上的技术操作。

## License

[MIT](LICENSE)
