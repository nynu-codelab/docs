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
4. 由项目负责人或 `codelab-admin` 创建，并设置团队权限
5. 为默认分支启用规则集，至少要求 Pull Request、Code Review 和禁止强推

> 不要从零 `git init` 搭建：模板已经内置统一规范。

## 每个仓库必须包含

- `README.md`：项目一句话简介、如何运行、如何贡献
- `.gitignore`：忽略 IDE 配置、`.env`、构建产物
- `.env.example`：环境变量示例（不填真实值）
- `LICENSE`：按项目类型决定（公共项目 MIT；竞赛 / 企业 / 成果项目先不加）
- CI 配置（`templates` 已内置）

## 可见性

- 公共仓库：面向开源的学习项目、模板、文档
- 私有仓库：竞赛项目、企业合作、未公开成果

拿不准就问项目负责人。

## 团队权限

| 团队 | 职责 |
| --- | --- |
| `codelab-admin` | 组织管理、仓库创建、权限和安全事件处理 |
| `software` | 软件研发部整体协作 |
| `fullstack` | 全栈开发组：前后端、Agent / LLM 应用和接口集成 |
| `qa` | 产品测试组：需求分析、测试用例、提测验收和回归 |
| `devops` | 运维组：部署发布、CI/CD、服务器、数据库和监控 |
| `achievement` | 成果中心：成果归档、竞赛和合作项目协作 |

项目仓库优先按具体项目建立团队并授予最小权限。不要为了方便直接给整个部门开放 `Write` 或 `Admin`。

## 默认分支保护

组织级仓库和正式项目仓库的默认分支应启用 `Protect main` 规则：

- 所有变更必须通过 Pull Request。
- 至少一位 Reviewer 批准，新的 Push 会使旧批准失效。
- 所有 Review 对话解决后才能合并。
- `codelab-admin` 成员可通过 Pull Request bypass 合并自己的 PR，但不能绕过必需状态检查。
- 禁止强制推送和删除默认分支。
- 文档仓库和模板仓库要求 `Markdown Lint`、`Check PR Title` 检查通过。
- 代码项目按技术栈配置 Lint、Test、Build 或安全扫描检查。

规则集用于执行协作规范，不替代测试、Review 或人工判断。

## 下一步

- Issue 怎么写：[issue.md](issue.md)
- PR 流程：[pull-request.md](pull-request.md)
