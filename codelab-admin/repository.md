# 仓库规范（Repository）

CodeLab 组织下的仓库如何创建、命名和管理。

## 命名

- 小写字母、数字、短横线，如 `smart-farm-backend`
- 项目名 + 后缀区分：`xxx-backend`、`xxx-frontend`、`xxx-docs`
- 不用中文、不用大写、不用下划线

## 创建新仓库

1. 在 [templates](https://github.com/nynu-codelab/templates) 找到对应模板
2. 使用 **Use this template** 创建新仓库（自动继承 README、.gitignore、CI 等）
3. 仓库归属选择 `nynu-codelab`
4. 由项目负责人或 `codelab-admin` 创建，并按 [repository-setup.md](repository-setup.md) 配置权限

> 不要从零 `git init` 搭建：模板已经内置统一规范。

## 每个仓库必须包含

- `README.md`：项目一句话简介、如何运行、如何贡献
- `.gitignore`：忽略 IDE 配置、`.env`、构建产物
- `.env.example`：环境变量示例（不填真实值）
- `LICENSE`：按项目类型决定（公共项目 MIT，含纯文档仓库；竞赛 / 企业 / 成果项目先不加）
- CI 配置（`templates` 已内置）

每一项都按仓库实际情况核对，缺项在 PR 里说明原因，不要默默省略。

## 可见性

- 公共仓库：面向开源的学习项目、模板、文档
- 私有仓库：竞赛项目、企业合作、未公开成果

拿不准就问项目负责人。

## 团队权限

组织只维护三个 team：

| Team | 仓库权限 | 职责 |
| --- | --- | --- |
| `codelab-admin` | Admin | 组织管理、仓库创建、权限、分支保护、规则集与安全开关（组织负责人 + 全栈组长） |
| `software` | Write | 全体研发，所有代码仓库的默认读写权限 |
| `achievement` | Write（按需） | 成果中心：成果归档、竞赛、论文、专利、软著与企业合作；仅授给成果类仓库 |

项目仓库默认给 `software` Write、`codelab-admin` Admin；工作边界（哪个仓库必须谁批准）写在该仓库的 `CODEOWNERS` 中，不按部门预设子组。完整步骤见 [repository-setup.md](repository-setup.md)。

`codelab-admin` 实际需要 **Admin**（组织负责人是仓库管理员）；Maintain 无法管理规则集与安全开关。批量授权用 team、不要给个人开权限，例外情况在 Issue 中说明。

## 规则集与分支保护

组织级规则集对所有仓库的默认分支生效，新仓库自动继承，无需逐个配置。仓库级规则集只用来叠加该仓库特有的必需状态检查。详见 [repository-setup.md](repository-setup.md)。

## 下一步

- 新仓库权限配置：[repository-setup.md](repository-setup.md)
- Issue 怎么写：[../software/github/issue.md](../software/github/issue.md)
- PR 流程：[../software/github/pull-request.md](../software/github/pull-request.md)
