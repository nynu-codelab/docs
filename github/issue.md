# Issue 规范

Issue 是 CodeLab 的任务与问题入口。写好 Issue = 沟通清楚。

## 三种模板

组织已配置统一模板，创建 Issue 时选择：

| 模板 | 用在哪里 |
| --- | --- |
| Bug Report | 报 Bug |
| Feature Request | 提新功能 |
| Project Task | 项目开发任务 |

## 写 Issue 的原则

- **一个 Issue 一件事**，便于跟踪和关闭
- 标题明确：`[Bug] 登录后白屏`、`[Task] 实现报表导出`
- 描述完整：别人只看 Issue 就能知道要做什么 / 复现什么
- 善用模板字段，不要留空

## 标签

常用标签：

- `bug`：缺陷
- `enhancement`：新功能
- `task`：开发任务
- `documentation`：文档
- `good first issue`：适合新人的任务（新人优先找这个）

## 认领任务

- 想做什么任务，先在该 Issue 下评论，让项目负责人分配
- 不要同时领多个任务；做完一个再领下一个
- 开始开发后，在 Issue 关联你的 PR（PR 描述里写 `Closes #编号`）

## 规则

- 不要在 Issue 里贴真实密钥（见 [SECURITY](https://github.com/nynu-codelab/.github/blob/main/SECURITY.md)）
- 安全问题**不要**公开创建 Issue，联系管理员
- 已解决的问题及时关闭，并写一句结论

## 下一步

- PR 流程：[pull-request.md](pull-request.md)
- 任务怎么拆：[工程流程总览](../engineering/overview.md)
