# 仓库规范（Repository）

CodeLab 组织下的仓库如何创建、命名和管理。

## 命名

- 小写字母、数字、短横线，如 `smart-farm-backend`
- 项目名 + 后缀区分：`xxx-backend`、`xxx-frontend`、`xxx-docs`
- 不用中文、不用大写、不用下划线

## 创建新仓库

组织不维护"复制即用"的项目模板：模板会和真实项目脱节，改一次规范就得同步改一遍模板，也容易让人以为"套了模板就等于合规"。规范靠 CI 检查，不靠复制。

组织已关闭成员自助建仓（Members can create repositories = off），仓库统一由组织所有者创建。

1. 由组织所有者（`codelab-admin` 成员）在组织中创建仓库，归属选 `nynu-codelab`，默认选 **Private**
2. 按下面的命名规则命名，并在 `/main` 前先配好保护规则
3. 搭最小骨架：`README.md`（怎么跑）、`.gitignore`、`.env.example`
4. 在 Actions 页面用组织工作流模板添加标准检查（`.github` 仓库的 `workflow-templates/`），再按技术栈补充 lint / test / build
5. 按 [repository-setup.md](repository-setup.md) 完成 team 权限、CODEOWNERS、分支保护与安全开关

> 顺序很重要：先配保护规则和 CI，再有第一个 commit。反过来做，第一个 PR 就会踩到"检查名不存在"或"没人能批准"这类坑。

## 每个仓库必须包含

- `README.md`：项目一句话简介、如何运行、如何贡献
- `.gitignore`：忽略 IDE 配置、`.env`、构建产物
- `.env.example`：环境变量示例（不填真实值）
- `LICENSE`：按项目类型决定（公共项目 MIT，含纯文档仓库；竞赛 / 企业 / 成果项目先不加）
- CI 配置：至少包含组织标准检查（Markdown Lint、PR 标题），再按技术栈补 lint / test / build

每一项都按仓库实际情况核对，缺项在 PR 里说明原因，不要默默省略。

## 可见性

- 公共仓库：面向开源的学习项目、文档
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

组织当前是免费计划，**不支持组织级规则集**（组织级规则集是 GitHub Team 功能），所以每个新仓库都要单独配置规则集和分支保护。这就是 [repository-setup.md](repository-setup.md) 必须逐步执行的原因——不要假设新仓库会自动继承保护。

配置完成后，`main` 的行为是：不能删除、不能强推、必须走 PR、至少 1 位 `codelab-admin` 批准、必需状态检查通过。

> 升级到 GitHub Team 后，应把公共规则抽成组织级规则集，仓库级只保留该仓库特有的必需状态检查，避免每个新仓库重复配置。

## 下一步

- 新仓库权限配置：[repository-setup.md](repository-setup.md)
- Issue 怎么写：[../software/github/issue.md](../software/github/issue.md)
- PR 流程：[../software/github/pull-request.md](../software/github/pull-request.md)
