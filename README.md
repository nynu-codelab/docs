# CodeLab Docs

CodeLab 技术文档中心，面向本科生，回答“CodeLab 项目应该怎么做”。

## Overview

本文档覆盖开发全流程所需知识：Git / GitHub 协作、Docker、CI/CD、各技术栈实践、AI 与硬件方向。所有内容以实践为主，直接对应实验室项目的真实用法，不写教科书式长文。

## Structure

```text
docs/
├── git/          # Git 基础、分支模型、Commit 规范
├── github/       # 仓库、Issue、PR、Code Review 规范
├── docker/       # Docker、Dockerfile、docker-compose
├── cicd/         # CI/CD 与 GitHub Actions
├── software/     # Java / Python / TypeScript 实践
├── ai/           # AI / Agent / RAG
├── algorithm/    # 算法、计算机视觉、工业视觉
└── hardware/     # 树莓派、嵌入式、无人机
```

## Usage

- 新手从 [git/overview.md](git/overview.md) 开始
- 写代码前阅读对应技术栈文档（如 [software/java.md](software/java.md)）
- 用 Docker 时阅读 [docker/overview.md](docker/overview.md)
- 提 PR 前阅读 [github/pull-request.md](github/pull-request.md)

## Contributing

欢迎补充与修正。提交方式见 [.github/CONTRIBUTING.md](https://github.com/nynu-codelab/.github/blob/main/CONTRIBUTING.md)。

## License

[MIT](LICENSE)
