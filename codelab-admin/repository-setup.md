# 新仓库权限配置（Repository Setup）

新仓库创建后，按以下四步完成权限与保护配置。

**总原则**：新仓库 = `software`(Write) + `codelab-admin`(Admin) + CODEOWNERS（codelab-admin 审批线）+ main 分支保护 + 安全开关，五件事齐了才能对外开放协作。

## 前置：创建仓库

见 [repository.md](repository.md)：由项目负责人或 `codelab-admin` 在组织中创建，归属 `nynu-codelab`，默认选 **Private**。组织不提供项目模板，骨架按规范手工搭。

## 1. 加 team 权限

Settings → Collaborators and teams：

| Team | 权限 | 说明 |
| --- | --- | --- |
| `@nynu-codelab/software` | Write | 全体研发默认推分支、开 PR |
| `@nynu-codelab/codelab-admin` | Admin | 分支保护、规则集、权限与安全开关（Maintain 不足以管理这些设置） |

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

组织是免费计划，没有组织级规则集，因此这一步每个仓库都必须做，没有"新仓库自动继承"这回事。

Settings → Branches → Add rule，针对 `main`：

- ☑ Require a pull request before merging
- ☑ Require approvals = **1**
- ☑ **Require review from Code Owners（审批人 = CODEOWNERS 中的 codelab-admin）**
- ☑ Require status checks to pass（填上 CI workflow 名）
- ☑ Do not allow bypassing the above settings

`develop` 照抄一份（长期迭代项目）。

## 4. 安全开关

Settings → Code security and analysis，确认全部开启：

- ☑ Secret scanning（密钥扫描）
- ☑ Push protection（推送保护）
- ☑ Dependabot alerts（依赖漏洞告警）
- ☑ Dependabot security updates（安全更新 PR）

新仓库默认可能关闭这些开关，必须手动确认，不要假设它们继承组织设置。

## 5. 不要做的事

- **不直接给个人授仓库权限**——除非要临时隔离某个仓库，否则全走 team。
- **不把 `software` 加成 Admin**——Write 够用，Admin 只给 `codelab-admin`。
- **不在 README 里写“谁负责什么”**——那是 CODEOWNERS 的活，README 只写怎么跑。
- **不把审批线设成 `software`**——合并批准权只属于 `codelab-admin`。
- **不要只依赖规则集或只依赖经典分支保护**——两者并存时要分别核对；组织级规则集管默认分支，仓库级只叠加必需状态检查。
- **不要配一个永远跑不出来的必需状态检查**——检查名必须来自仓库里真实存在的 workflow，否则 PR 永远无法合并。

## 下一步

- 仓库命名与创建：[repository.md](repository.md)
- PR 流程：[../software/github/pull-request.md](../software/github/pull-request.md)
