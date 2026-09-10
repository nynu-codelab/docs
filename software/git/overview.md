# Git 概述

Git 是 CodeLab 所有项目的版本管理工具。本文介绍入门必需的知识。

## 什么是 Git

Git 是一个分布式版本控制系统，用来记录代码的每一次修改。它的核心概念：

- **Repository（仓库）**：一个项目的所有历史记录
- **Commit（提交）**：一次修改的快照，有唯一的 hash
- **Branch（分支）**：一条独立的开发线
- **Remote（远程）**：远程仓库，如 GitHub

## 安装与配置

安装 Git 后，先配置身份（提交时使用）：

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

> 邮箱建议使用 GitHub 绑定的邮箱，提交记录才能关联到你的账号。

## 常用命令

```bash
git clone <repo-url>        # 克隆仓库
git status                  # 查看状态
git add <file>              # 暂存文件
git commit -m "feat: ..."   # 提交
git pull                    # 拉取远程更新
git push                    # 推送远程
git branch -a               # 查看所有分支
git log --oneline           # 查看提交历史
```

## CodeLab 的用法

- 所有项目代码托管在 [nynu-codelab](https://github.com/nynu-codelab) 组织下
- 不要直接往 `main` 推，按 [branching.md](branching.md) 的分支模型操作
- Commit 信息遵循 [commit-convention.md](commit-convention.md)

## 常见问题

- **提交错了文件**：`git restore --staged <file>` 取消暂存
- **想撤销最后一次提交**：`git reset --soft HEAD~1`（保留改动）
- **改了本地代码想放弃**：`git restore <file>`（会丢失改动，谨慎）

## 下一步

- 分支怎么用：[branching.md](branching.md)
- Commit 怎么写：[commit-convention.md](commit-convention.md)
- 提 PR 的流程：[../github/pull-request.md](../github/pull-request.md)
