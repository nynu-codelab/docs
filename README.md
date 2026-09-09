# CodeLab 技术与协作规范

本仓库是 CodeLab 在 GitHub 上的技术与协作规范中心，回答“代码和项目应该怎么做”。组织架构、角色职责、入组与权限、会议、考勤、奖惩、成果与保密制度以飞书 CodeLab 成员手册为准。

## 适用范围

本仓库维护：

- Git 与 GitHub 协作流程
- 分支、Commit、Issue、Pull Request 与 Code Review 规范
- 技术方案、接口、测试、部署、发布与复盘文档规范
- Docker、CI/CD、安全与代码质量实践
- Java、Python、TypeScript、AI、算法和硬件方向的技术指南

本仓库不维护：

- 实验室组织架构和角色任免
- 成员入组、退出、考勤和会议制度
- 奖惩、成果署名和保密管理制度
- 飞书中的通知、会议纪要和内部管理流程

## 快速入口

### 协作规范

- [Git 概述](git/overview.md)
- [分支模型](git/branching.md)
- [Commit 规范](git/commit-convention.md)
- [仓库规范](github/repository.md)
- [Issue 规范](github/issue.md)
- [Pull Request 规范](github/pull-request.md)
- [Code Review 规范](github/code-review.md)

### 工程流程

- [工程流程总览](engineering/overview.md)
- [技术方案与 ADR](engineering/technical-design.md)
- [测试与提测](engineering/testing.md)
- [发布与回滚](engineering/release.md)
- [技术文档规范](engineering/documentation.md)
- [工程安全基线](engineering/security.md)

### 基础设施

- [Docker 概述](docker/overview.md)
- [CI/CD 概述](cicd/overview.md)
- [GitHub Actions](cicd/github-actions.md)

### 技术方向

- 软件：[Java](software/java.md)、[Python](software/python.md)、[TypeScript](software/typescript.md)
- AI：[AI 概述](ai/overview.md)、[Agent](ai/agent.md)、[RAG](ai/rag.md)
- 算法：[算法概述](algorithm/overview.md)、[计算机视觉](algorithm/computer-vision.md)、[工业视觉](algorithm/industrial-vision.md)
- 硬件：[硬件概述](hardware/overview.md)、[树莓派](hardware/raspberry-pi.md)、[嵌入式](hardware/embedded.md)、[无人机](hardware/uav.md)

## 文档落点

| 内容 | 维护位置 |
| --- | --- |
| 组织级技术规范和协作规则 | 本仓库 |
| 项目特有的技术方案、接口、部署、测试和复盘 | 项目仓库的 `docs/`，或本仓库 `projects/<repo>/` |
| Issue、PR、Review、CI/CD 和 Release | 对应 GitHub 仓库 |
| 组织制度、人员管理和日常沟通 | 飞书 |

同一规则只维护一个权威版本。GitHub 不复制飞书中的制度文本；如果制度变化会影响技术实现，只在 GitHub 更新对应的操作步骤、模板或检查项。

## 目录结构

```text
docs/
├── git/            # Git 基础、分支和 Commit
├── github/         # 仓库、Issue、PR 和 Code Review
├── engineering/    # 技术方案、测试、发布、文档和安全
├── docker/         # Docker 与 Docker Compose
├── cicd/           # CI/CD 与 GitHub Actions
├── software/       # Java、Python、TypeScript
├── ai/             # AI、Agent、RAG
├── algorithm/      # 算法、计算机视觉、工业视觉
└── hardware/       # 树莓派、嵌入式和无人机
```

## 贡献方式

新增或修改文档时：

1. 确认内容属于技术与协作范围，不重复飞书制度。
2. 创建 `docs/<short-description>` 分支。
3. 保证命令、链接和示例可验证。
4. 提交 Pull Request，并关联 Issue。
5. 等待 CI 和 Review 通过后合并。

完整流程见 [CONTRIBUTING.md](CONTRIBUTING.md) 和 [.github/CONTRIBUTING.md](https://github.com/nynu-codelab/.github/blob/main/CONTRIBUTING.md)。

## License

[MIT](LICENSE)
