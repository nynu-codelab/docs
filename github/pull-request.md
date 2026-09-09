# Pull Request 规范

PR 是 CodeLab 所有代码进入仓库的唯一方式。PR = 代码 + 说明 + 讨论记录。

## 提 PR 的流程

```text
本地开发完成
  ↓ push 分支
创建 PR（选 base 分支，关联 Issue）
  ↓ 填写模板
CI 自动运行
  ↓ 修复检查失败项
Code Review
  ↓ 根据意见修改
合并（Merge）
```

## 创建 PR

1. Push 你的分支后，GitHub 会自动提示 Create Pull Request
2. `base` 选 `develop`（或项目约定的分支），`compare` 选你的分支
3. 标题遵循 [Commit 规范](../git/commit-convention.md)：`feat(auth): add login page`
4. 按 [PULL_REQUEST_TEMPLATE](https://github.com/nynu-codelab/.github/blob/main/PULL_REQUEST_TEMPLATE.md) 填写
5. 关联 Issue：描述中写 `Closes #12`

## PR 要小

- 一个 PR 解决一个问题，改动控制在可 Review 的范围
- 超大 PR 会被要求拆开
- 无关的格式化、重构不要混进功能 PR

## CI 与 Review

- PR 会触发 CI（Lint / Test / Build），**CI 失败不能合并**
- Reviewer 的评论会以对话形式出现，逐条回复即可
- 修改后 push 新 commit，PR 会自动更新

## 合并

- 由 Reviewer 或作者在通过后合并
- 合并前确认：CI 通过、Review 通过、无未解决的对话
- `codelab-admin` 成员可以合并自己的 PR，但必须通过全部必需 CI，并在 PR 中写明自审结论
- 合并后删除分支（GitHub 会提示）

## 下一步

- Review 怎么看：[code-review.md](code-review.md)
- 提交规范：[../git/commit-convention.md](../git/commit-convention.md)
