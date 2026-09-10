# CodeLab Docs

CodeLab 技术文档中心，面向本科生，回答“CodeLab 项目应该怎么做”。

## Overview

本文档覆盖开发全流程所需知识：Git / GitHub 协作、工程流程（技术方案、测试、发布、安全）、Docker、CI/CD、各技术栈实践、AI 与硬件方向。所有内容以实践为主，直接对应实验室项目的真实用法，不写教科书式长文。

## Structure

```text
docs/
├── git/          # Git 基础、分支模型、Commit 规范
├── github/       # 仓库、Issue、PR、Code Review 规范
├── engineering/  # 工程流程：技术方案、测试、发布、交接、安全
├── docker/       # Docker、Dockerfile、docker-compose
├── cicd/         # CI/CD 与 GitHub Actions
├── software/     # Java / Python / TypeScript 实践
├── ai/           # AI / Agent / RAG
├── algorithm/    # 算法、计算机视觉、工业视觉
└── hardware/     # 树莓派、嵌入式、无人机
```

## 工程流程

- [工程流程总览](engineering/overview.md)
- [技术方案与 ADR](engineering/technical-design.md)
- [测试与提测](engineering/testing.md)
- [发布与回滚](engineering/release.md)
- [项目与技术资产交接](engineering/handover.md)
- [技术文档规范](engineering/documentation.md)
- [工程安全基线](engineering/security.md)

## Usage

- 新手从 [git/overview.md](git/overview.md) 开始
- 写代码前阅读对应技术栈文档（如 [software/java.md](software/java.md)）
- 用 Docker 时阅读 [docker/overview.md](docker/overview.md)
- 提 PR 前阅读 [github/pull-request.md](github/pull-request.md)
- 需求到发布全流程看 [工程流程总览](engineering/overview.md)

## Contributing

欢迎补充与修正。提交方式见 [.github/CONTRIBUTING.md](https://github.com/nynu-codelab/.github/blob/main/CONTRIBUTING.md)。

## License

[MIT](LICENSE)
