<div align="center">

# CodeLab Docs

`nynu-codelab` 组织统一的工程协作规范：**codelab-admin 怎么维护项目**、**software 怎么协作**。

[![Standards Check](https://github.com/nynu-codelab/docs/actions/workflows/standards.yml/badge.svg)](https://github.com/nynu-codelab/docs/actions/workflows/standards.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

</div>

## 这个仓库管什么

本仓库是组织**协作规范的唯一来源**，只覆盖 GitHub 上的技术与协作实现：

- **项目维护** —— 建仓库、配 team 与分支保护、守安全基线、做项目与技术资产交接。
- **日常协作** —— Git 工作流、分支与 Commit 规范、Issue / PR / Code Review，以及需求 → 发布 → 复盘的工程流程。

不在本仓库的内容见 [本仓库不包含什么](#本仓库不包含什么)。

## 我该看哪一份

| Team | 仓库权限 | 职责 | 入口 |
| --- | --- | --- | --- |
| `codelab-admin` | Admin | 组织负责人、全栈组长：仓库创建、权限、分支保护、规则集与安全开关 | [codelab-admin/](codelab-admin/README.md) |
| `software` | Write | 软件研发部全体成员：日常开发、提 PR、参与评审 | [software/](software/README.md) |
| `achievement` | Write（按需） | 成果中心：竞赛、论文、专利、软著与企业合作类仓库 | 成果归档流程以飞书成员手册为准 |

> `codelab-admin` 必须配 **Admin**：Maintain 无法管理仓库设置、规则集和安全开关，不要按 Maintain 配置。

## 新成员第一步

1. 配好 Git 身份 —— [Git 概述](software/git/overview.md)
2. 找一个 `good first issue` 认领 —— [Issue 规范](software/github/issue.md)
3. 建规范分支、按约定写 Commit —— [分支模型](software/git/branching.md) · [Commit 规范](software/git/commit-convention.md)
4. 提 PR 并等待 CI 与 Review —— [PR 流程](software/github/pull-request.md) · [Code Review](software/github/code-review.md)
5. 全组织通用的最低协作要求见 [CONTRIBUTING.md](https://github.com/nynu-codelab/.github/blob/main/CONTRIBUTING.md)

## 文档地图

### software —— 研发怎么协作

| 文档 | 内容 |
| --- | --- |
| [Git 概述](software/git/overview.md) / [分支模型](software/git/branching.md) / [Commit 规范](software/git/commit-convention.md) | 日常 Git |
| [Issue 规范](software/github/issue.md) | 怎么写 Issue、怎么认领任务 |
| [PR 流程](software/github/pull-request.md) | 怎么提 PR |
| [Code Review](software/github/code-review.md) | 怎么审、怎么被审 |
| [工程流程总览](software/engineering/overview.md) | 需求 → 发布全流程 |
| [技术方案与 ADR](software/engineering/technical-design.md) | 什么时候必须写设计文档 |
| [测试与提测](software/engineering/testing.md) | 测试层次与提测准入 |
| [发布与回滚](software/engineering/release.md) | 版本、发布、回滚 |
| [技术文档规范](software/engineering/documentation.md) | README、设计文档怎么写 |

### codelab-admin —— 项目怎么维护

| 文档 | 内容 |
| --- | --- |
| [新仓库配置](codelab-admin/repository-setup.md) | 加 team、CODEOWNERS、分支保护、安全开关四步 |
| [仓库命名与权限模型](codelab-admin/repository.md) | 三 team 模型、可见性、默认分支保护 |
| [工程安全基线](codelab-admin/security.md) | 密钥、CI、依赖安全；泄露事件响应 |
| [项目与技术资产交接](codelab-admin/handover.md) | 人员变动时仓库、权限、密钥怎么交 |

各目录下的 `README.md` 是该目录更细的索引。

## 本仓库不包含什么

- **组织制度与人事** —— 架构、入组退出、考勤、奖惩、署名与保密，以飞书 CodeLab 成员手册为准。
- **技术栈教程** —— Docker、CI/CD、AI / Agent、算法与硬件方向的资料在飞书知识库维护。
- **项目模板** —— 组织不维护 templates 仓库；新项目按 [codelab-admin/repository.md](codelab-admin/repository.md) 从零搭建，规范一致性由 CI 检查保证。

新增内容前先判断它属于「协作规范」还是「知识库」，不要直接往本仓库堆。

## 改这些规范

本仓库自身的改动同样走 PR：

1. 从 `main` 建 `docs/*` 分支，一个 PR 只解决一个问题。
2. PR 标题遵循 Conventional Commits，例如 `docs: 重构根 README`、`docs(github): 补充 PR 模板说明`。
3. 两个必需状态检查必须通过：**Markdown Lint** 与 **Check PR Title**，配置见 [standards.yml](.github/workflows/standards.yml)。
4. 合并需 `codelab-admin` 以 Code Owner 身份批准 —— 见 [CODEOWNERS](CODEOWNERS)。
5. 新增或移动文档时，同步更新所在目录 `README.md` 的索引。

## 相关仓库与组织级文件

| 位置 | 内容 |
| --- | --- |
| [`nynu-codelab/.github`](https://github.com/nynu-codelab/.github) | 组织级配置：Issue / PR 模板、[SECURITY.md](https://github.com/nynu-codelab/.github/blob/main/SECURITY.md)、[CODE_OF_CONDUCT.md](https://github.com/nynu-codelab/.github/blob/main/CODE_OF_CONDUCT.md)、[SUPPORT.md](https://github.com/nynu-codelab/.github/blob/main/SUPPORT.md) |
| [`codelab-web`](https://github.com/nynu-codelab/codelab-web) | 实验室官网与招新管理系统 |
| [`lab-member-system-docs`](https://github.com/nynu-codelab/lab-member-system-docs) | 新成员上手项目说明 |

## License

[MIT](LICENSE)
