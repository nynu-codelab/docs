# 分支模型（Branching）

CodeLab 所有项目使用统一的分支模型，保持简单、易学。

## 分支结构

```text
main                    # 稳定分支，始终可运行、可发布
  └── develop           # 开发分支，日常集成分支
       ├── feature/*    # 新功能
       ├── fix/*        # 修复 Bug
       ├── docs/*       # 文档
       └── refactor/*   # 重构
```

## 规则

| 分支 | 用途 | 谁可以推 |
| --- | --- | --- |
| `main` | 只存稳定代码 | 只能通过 PR 合并 |
| `develop` | 开发集成 | 通过 PR 合并 |
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
# 基于 develop 创建功能分支
git checkout develop
git pull
git checkout -b feature/xxx

# 开发完成后
git add .
git commit -m "feat: xxx"
git push -u origin feature/xxx

# 在 GitHub 上创建 PR，合并到 develop
```

## 同步开发分支

分支开发久了会落后，定期合并最新的 develop：

```bash
git checkout develop && git pull
git checkout feature/xxx
git merge develop        # 或 git rebase develop
git push
```

## 小项目可以简化

小型项目（单人 / 短周期）可以只用 `main` + `feature/*`，跳过 `develop`，但要保持 PR + Review 流程。

## 下一步

- Commit 规范：[commit-convention.md](commit-convention.md)
- PR 流程：[../github/pull-request.md](../github/pull-request.md)
