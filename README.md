# CodeLab Docs

本仓库只放**协作规范**：**codelab-admin 怎么维护项目**、**software（软件研发）怎么协作提 PR**。组织制度（架构、入组退出、考勤、奖惩、署名与保密）在飞书 CodeLab 成员手册，本仓库不复制。

`nynu-codelab` 组织维护三个 team，与本仓库的对应关系如下：

| Team | 在仓库中的权限 | 看哪份文档 |
| --- | --- | --- |
| codelab-admin | Admin（组织负责人、组长） | [codelab-admin/](codelab-admin/README.md) |
| software | Write（软件研发部全体成员） | [software/](software/README.md) |
| achievement | Write（仅成果类仓库，按需授予） | 成果归档流程以飞书成员手册为准 |

> `codelab-admin` 需要 Admin 才能管理仓库设置、规则集和安全开关；Maintain 不具备这些权限，因此不要按 Maintain 配置。

## 本仓库不包含什么

本仓库只维护**协作规范**，不放技术栈教程，也不放项目模板。Docker、CI/CD、AI / Agent、算法与硬件方向的资料在飞书知识库维护；新项目按 [codelab-admin/repository.md](codelab-admin/repository.md) 从零搭建，规范一致性由 CI 检查保证。需要新增教程类内容时，先确认它属于「协作规范」还是「知识库」，不要直接往本仓库堆。

## 我是 codelab-admin → 项目维护

[进入 codelab-admin/](codelab-admin/README.md)：新仓库配置、仓库权限模型、工程安全基线、项目与技术资产交接。

## 我是 software 开发者 → 怎么协作

[进入 software/](software/README.md)：Git 工作流、Issue / PR / Code Review、工程流程（技术方案、测试、发布、文档）。

## License

[MIT](LICENSE)
