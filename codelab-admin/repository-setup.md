# 新仓库权限配置（Repository Setup）

新仓库创建后，按以下四步完成权限与保护配置。

**总原则**：新仓库 = `software`(Write) + `codelab-admin`(Maintain) + CODEOWNERS（codelab-admin 审批线）+ main 分支保护，四件事齐了就能跑。

## 前置：创建仓库

见 [repository.md](repository.md)：从 templates 模板创建，归属 `nynu-codelab`，默认选 **Private**。

## 1. 加 team 权限

Settings → Collaborators and teams：

| Team | 权限 | 说明 |
| --- | --- | --- |
| `@nynu-codelab/software` | Write | 全体研发默认推分支、开 PR |
| `@nynu-codelab/codelab-admin` | Maintain | 分支保护、权限、仓库设置 |

普通代码仓库**不要**加 `achievement`；只有论文 / 竞赛 / 成果材料类仓库才加它。

## 2. 根目录 CODEOWNERS

**审批线统一为 `codelab-admin`**：任何 PR 改动任何路径，都必须由 `codelab-admin` 团队成员批准，其他团队不能批准合并。

```text
# 默认：所有改动由 codelab-admin（维护团队）批准
* @nynu-codelab/codelab-admin

# 如需让某子目录由专人把关，追加路径行并指向具体 GitHub 用户名
# CODEOWNERS 只认 GitHub login，不写中文名
```

## 3. 分支保护

Settings → Branches → Add rule，针对 `main`：

- ☑ Require a pull request before merging
- ☑ Require approvals = **1**
- ☑ **Require review from Code Owners（审批人 = CODEOWNERS 中的 codelab-admin）**
- ☑ Require status checks to pass（填上 CI workflow 名）
- ☑ Do not allow bypassing the above settings

`develop` 照抄一份（长期迭代项目）。

## 4. 不要做的事

- **不直接给个人授仓库权限**——除非要临时隔离某个仓库，否则全走 team。
- **不把 `software` 加成 Admin**——Write 够用，Admin 只给 `codelab-admin`。
- **不在 README 里写“谁负责什么”**——那是 CODEOWNERS 的活，README 只写怎么跑。
- **不把审批线设成 `software`**——合并批准权只属于 `codelab-admin`。

## 下一步

- 仓库命名与模板：[repository.md](repository.md)
- PR 流程：[../software/github/pull-request.md](../software/github/pull-request.md)
