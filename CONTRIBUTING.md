# 贡献技术文档

本仓库维护 CodeLab 的组织级技术规范和协作规范。提交前先判断内容是否应留在飞书、放入本仓库，还是放入具体项目仓库。

## 内容边界

适合本仓库：

- 所有项目共用的 Git、GitHub、Review、测试、发布和安全规范
- 工具使用指南、模板说明和跨项目技术实践
- 可复用的技术方案、接口约定和工程检查清单

不适合本仓库：

- 组织架构、角色任免和成员管理
- 入组、退出、考勤、会议和奖惩制度
- 飞书通知、会议纪要和内部管理流程
- 只对单个项目有效的私有实现细节

## 新增页面

1. 在对应目录创建 Markdown 文件。
2. 使用一级标题，标题直接说明主题。
3. 开头说明适用对象、解决的问题和使用场景。
4. 命令必须实际执行或明确标注未验证原因。
5. 更新本仓库 `README.md` 的导航。
6. 提交 PR 并关联 Issue。

## 文档检查

- 标题层级连续，不跳级。
- 内部链接使用相对路径，外部链接可访问。
- 代码块标注语言。
- 示例不包含真实密钥、账号、服务器地址或企业数据。
- 术语与现有文档保持一致。
- 不复制飞书制度原文，只保留 GitHub 上的实现方式。

## 提交规范

分支示例：

```text
docs/add-release-checklist
docs/update-pr-template
```

Commit 示例：

```text
docs(release): add rollback checklist
docs(github): clarify review requirements
```

PR 标题和 Commit 均遵循 Conventional Commits。详细规则见 [.github/CONTRIBUTING.md](https://github.com/nynu-codelab/.github/blob/main/CONTRIBUTING.md)。
