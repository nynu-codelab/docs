# 新仓库权限配置（Repository Setup）

新仓库创建后，按以下四步完成权限与保护配置。

**总原则**：新仓库 = `software`(Write) + `codelab-admin`(Maintain) + CODEOWNERS 划审批线 + main 分支保护，四件事齐了就能跑。

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

```text
# 默认：业务代码由研发团队审批
* @nynu-codelab/software

# 部署与 CI：由 codelab-admin（运维负责人）把关
/.github/workflows/ @nynu-codelab/codelab-admin
/deploy/             @nynu-codelab/codelab-admin

# 测试资产：由 codelab-admin（测试负责人）把关
/tests/              @nynu-codelab/codelab-admin
/test-data/          @nynu-codelab/codelab-admin
```

当前运维与测试负责人由 `codelab-admin` 兼任；专职负责人到位后，对应行替换为具体 GitHub 用户名——CODEOWNERS 只认 GitHub login，不写中文名。

## 3. 分支保护

Settings → Branches → Add rule，针对 `main`：

- ☑ Require a pull request before merging
- ☑ Require approvals = **1**
- ☑ Require status checks to pass（填上 CI workflow 名）
- ☑ Do not allow bypassing the above settings

`develop` 照抄一份（长期迭代项目）。

## 4. 不要做的事

- **不直接给个人授仓库权限**——除非要临时隔离某个仓库，否则全走 team。
- **不把 `software` 加成 Admin**——Write 够用，Admin 只给 `codelab-admin`。
- **不在 README 里写“谁负责什么”**——那是 CODEOWNERS 的活，README 只写怎么跑。

## 下一步

- 仓库命名与模板：[repository.md](repository.md)
- PR 流程：[../software/github/pull-request.md](../software/github/pull-request.md)
