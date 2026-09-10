# 分支模型（Branching）

CodeLab 项目统一以 `main` 为主线，保持简单、易学。多人长期协作的项目再增加 `develop`。

## 分支结构

默认（适用于绝大多数项目）：

```text
main                    # 稳定分支，始终可运行、可发布
  ├── feature/*         # 新功能
  ├── fix/*             # 修复 Bug
  ├── docs/*            # 文档
  ├── refactor/*        # 重构
  └── chore/*           # 构建、依赖、杂项
```

需要长期迭代、且希望把未验证改动与发布版本隔开时，再增加 `develop` 作为集成分支：`feature/*` 先合入 `develop`，验证通过后由 `develop` 合入 `main`。引入 `develop` 是**项目级决定**，由项目负责人在仓库 README 中写明，不要默认假设它存在。

## 规则

| 分支 | 用途 | 谁可以推 |
| --- | --- | --- |
| `main` | 只存稳定代码 | 只能通过 PR 合并 |
| `develop` | 开发集成（可选，长期项目） | 通过 PR 合并 |
| `feature/*` | 新功能开发 | 负责成员 |
| `fix/*` | 修复 Bug | 负责成员 |
| `docs/*` | 文档修改 | 任何成员 |
| `refactor/*` | 重构 | 负责成员 |

**核心规则：`main` 禁止直接提交，所有改动必须走 PR。**

## 分支命名

```text
feature/login-page
fix/empty-list-error
docs/readme-update
refactor/user-service
```

规则：`类型/简短描述`，描述用短横线连接，全部小写。

## 常用操作

```bash
# 先同步目标分支（默认 main；项目有 develop 时用 develop）
git checkout main
git pull
git checkout -b feature/xxx

# 开发完成后
git add .
git commit -m "feat: xxx"
git push -u origin feature/xxx

# 在 GitHub 上创建 PR，合并回目标分支
```

## 同步目标分支

分支开发久了会落后，定期合并最新的目标分支：

```bash
git checkout main && git pull
git checkout feature/xxx
git merge main           # 或 git rebase main
git push
```

## 什么时候需要 develop

只有满足「多人长期并行开发」或「需要把未验证改动与发布版本隔离」时才引入 `develop`。单人项目和短周期项目直接用 `main` + 功能分支，少一层合并就少一层出错机会；无论用哪种模型，PR + Review 流程都不省略。

## 下一步

- Commit 规范：[commit-convention.md](commit-convention.md)
- PR 流程：[../github/pull-request.md](../github/pull-request.md)
