# software：研发协作规范

面向 `nynu-codelab` 组织中 **software** team（软件研发，Write 权限）。一份文档覆盖日常协作全部规范：Git、Issue / PR / Code Review，以及需求 → 发布 → 复盘的工程流程。按目录跳转，或直接全文阅读。

## 目录

- [Git 概述](#git-概述)
- [分支模型](#分支模型)
- [Commit 规范](#commit-规范)
- [Issue 规范](#issue-规范)
- [Pull Request 规范](#pull-request-规范)
- [Code Review](#code-review)
- [工程流程总览](#工程流程总览)
- [技术方案与 ADR](#技术方案与-adr)
- [测试与提测](#测试与提测)
- [发布与回滚](#发布与回滚)
- [技术文档规范](#技术文档规范)

## Git 概述

Git 是 CodeLab 所有项目的版本管理工具。本节介绍入门必需的知识。

### 什么是 Git

Git 是一个分布式版本控制系统，用来记录代码的每一次修改。它的核心概念：

- **Repository（仓库）**：一个项目的所有历史记录
- **Commit（提交）**：一次修改的快照，有唯一的 hash
- **Branch（分支）**：一条独立的开发线
- **Remote（远程）**：远程仓库，如 GitHub

### 安装与配置

安装 Git 后，先配置身份（提交时使用）：

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

> 邮箱建议使用 GitHub 绑定的邮箱，提交记录才能关联到你的账号。

### 常用命令

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

### CodeLab 的用法

- 所有项目代码托管在 [nynu-codelab](https://github.com/nynu-codelab) 组织下
- 不要直接往 `main` 推，按 [分支模型](#分支模型) 操作
- Commit 信息遵循 [Commit 规范](#commit-规范)

### 常见问题

- **提交错了文件**：`git restore --staged <file>` 取消暂存
- **想撤销最后一次提交**：`git reset --soft HEAD~1`（保留改动）
- **改了本地代码想放弃**：`git restore <file>`（会丢失改动，谨慎）

## 分支模型

CodeLab 项目统一以 `main` 为主线，保持简单、易学。多人长期协作的项目再增加 `develop`。

### 分支结构

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

### 规则

| 分支 | 用途 | 谁可以推 |
| --- | --- | --- |
| `main` | 只存稳定代码 | 只能通过 PR 合并 |
| `develop` | 开发集成（可选，长期项目） | 通过 PR 合并 |
| `feature/*` | 新功能开发 | 负责成员 |
| `fix/*` | 修复 Bug | 负责成员 |
| `docs/*` | 文档修改 | 任何成员 |
| `refactor/*` | 重构 | 负责成员 |

**核心规则：`main` 禁止直接提交，所有改动必须走 PR。**

### 分支命名

```text
feature/login-page
fix/empty-list-error
docs/readme-update
refactor/user-service
```

规则：`类型/简短描述`，描述用短横线连接，全部小写。

### 常用操作

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

### 同步目标分支

分支开发久了会落后，定期合并最新的目标分支：

```bash
git checkout main && git pull
git checkout feature/xxx
git merge main           # 或 git rebase main
git push
```

### 什么时候需要 develop

只有满足「多人长期并行开发」或「需要把未验证改动与发布版本隔离」时才引入 `develop`。单人项目和短周期项目直接用 `main` + 功能分支，少一层合并就少一层出错机会；无论用哪种模型，PR + Review 流程都不省略。

## Commit 规范

统一的 Commit 信息让历史清晰、可回溯、可自动生成 changelog。

### 格式

```text
type(scope): description
```

- `type`：提交类型（见下表）
- `scope`：可选，影响的范围，如模块名
- `description`：简短描述，建议英文，首字母小写

### 类型

| type | 含义 | 例子 |
| --- | --- | --- |
| `feat` | 新功能 | `feat(auth): add login page` |
| `fix` | 修复 Bug | `fix(api): fix null pointer on empty list` |
| `docs` | 文档 | `docs: update readme` |
| `style` | 格式调整 | `style: format code` |
| `refactor` | 重构 | `refactor: extract user service` |
| `perf` | 性能优化 | `perf: cache hot query` |
| `test` | 测试 | `test: add calculator tests` |
| `build` | 构建相关 | `build: bump spring boot to 3.3` |
| `ci` | CI 配置 | `ci: add lint job` |
| `chore` | 杂项 | `chore: update gitignore` |

### 好与坏的例子

```text
# 好
feat(auth): add jwt login
fix: handle empty list in report api
docs: add docker quickstart

# 不好
update code
修复一些问题
asdf
```

### 小贴士

- 一次 Commit 只做一件事（一个功能 / 一个修复）
- Commit 信息能说明"为什么改"更好：`fix: retry db connection to avoid startup failure`
- 用 `git commit -m` 写单行信息足够；复杂改动用 `-m` 多次分段
- 不要在 Commit 里夹带无关文件的修改
- PR 标题同样遵循本规范（有 CI 自动检查）

## Issue 规范

Issue 是 CodeLab 的任务与问题入口。写好 Issue = 沟通清楚。

### 模板

组织已配置统一模板，创建 Issue 时选择：

| 模板 | 用在哪里 |
| --- | --- |
| Bug Report | 报 Bug |
| Feature Request | 提新功能 |
| Project Task | 项目开发任务 |
| Documentation | 文档改进 |
| Technical Debt | 技术债登记 |

### 写 Issue 的原则

- **一个 Issue 一件事**，便于跟踪和关闭
- 标题明确：`[Bug] 登录后白屏`、`[Task] 实现报表导出`
- 描述完整：别人只看 Issue 就能知道要做什么 / 复现什么
- 善用模板字段，不要留空

### 标签

常用标签：

- `bug`：缺陷
- `enhancement`：新功能
- `task`：开发任务
- `documentation`：文档
- `good first issue`：适合新人的任务（新人优先找这个）

### 认领任务

- 想做什么任务，先在该 Issue 下评论，让项目负责人分配
- 不要同时领多个任务；做完一个再领下一个
- 开始开发后，在 Issue 关联你的 PR（PR 描述里写 `Closes #编号`）

### 规则

- 不要在 Issue 里贴真实密钥（见 [SECURITY](https://github.com/nynu-codelab/.github/blob/main/SECURITY.md)）
- 安全问题**不要**公开创建 Issue，联系管理员
- 已解决的问题及时关闭，并写一句结论

## Pull Request 规范

PR 是 CodeLab 所有代码进入仓库的唯一方式。PR = 代码 + 说明 + 讨论记录。

### 提 PR 的流程

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

### 创建 PR

1. Push 你的分支后，GitHub 会自动提示 Create Pull Request
2. `base` 选目标分支：项目有 `develop` 时选 `develop`，否则选 `main`（以仓库 README 的约定为准）；`compare` 选你的分支
3. 标题遵循 [Commit 规范](#commit-规范)：`feat(auth): add login page`
4. 按 [PULL_REQUEST_TEMPLATE](https://github.com/nynu-codelab/.github/blob/main/PULL_REQUEST_TEMPLATE.md) 填写
5. 关联 Issue：描述中写 `Closes #12`

### PR 要小

- 一个 PR 解决一个问题，改动控制在可 Review 的范围
- 超大 PR 会被要求拆开
- 无关的格式化、重构不要混进功能 PR

### CI 与 Review

- PR 会触发 CI（Lint / Test / Build），**CI 失败不能合并**
- Reviewer 的评论会以对话形式出现，逐条回复即可
- 修改后 push 新 commit，PR 会自动更新

### 合并

- 由 Reviewer 或作者在通过后合并
- 合并前确认：CI 通过、Review 通过、无未解决的对话
- 合并后删除分支（GitHub 会提示）

## Code Review

Code Review 是 CodeLab 保证代码质量的核心环节，也是新人学习最快的途径。

### 为什么 Review

- 发现 Bug、隐患、坏味道
- 传递项目规范与经验
- 让代码不是"一个人的代码"

### Reviewer 怎么看

1. **先看整体**：这个 PR 解决了什么问题？方案是否合理？
2. **再抠细节**：逻辑、边界情况、异常处理、命名、安全性
3. **重点检查**：
   - 有没有硬编码密钥、泄露敏感信息
   - 有没有明显性能问题（N+1 查询、死循环）
   - 有没有破坏兼容性（API / 数据库变更是否说明）
   - 测试是否覆盖关键逻辑

### 评论怎么写

- 对事不对人：说"这里有个 bug"，不说"你写错了"
- 给出原因和建议，不只是"改一下"
- 用 GitHub 的 suggestion 功能直接给修改建议

示例：

```text
这里当列表为空时会 NPE，建议先判空。
```

### 作者怎么回应

- 每个评论都回复：同意就改并说明，不同意就解释理由
- 不要默默忽略评论
- 修改后 push，评论对话保持可追溯

### 新人友好

- 新人的 PR 由项目负责人 Review，重在培养规范意识
- `good first issue` 适合新人练手
- Review 是互相学习，不是考试

## 工程流程总览

本节把实验室的开发流程转换为 GitHub 上可执行的产物。制度要求以飞书为准；具体如何记录、提交、检查和发布以本仓库和项目仓库为准。

### 六个阶段

| 阶段 | GitHub 实现载体 | 完成标准 |
| --- | --- | --- |
| 需求评审 | Issue、需求文档、验收标准、里程碑 | 范围、优先级、验收标准和排期明确 |
| 技术评审 | 技术方案、ADR、接口契约、迁移方案 | 方案、风险、兼容性和回滚方式有结论 |
| 联调 | OpenAPI / Mock、联调环境、联调 Issue | 接口契约一致，数据链路打通 |
| 提测 | 测试计划、测试用例、Bug Issue、测试报告 | 准入条件满足，质量结论明确 |
| 上线 | Release、变更记录、部署 Checklist、回滚方案 | 发布可追踪，验证和回滚路径明确 |
| 复盘 | 复盘文档、改进 Issue、技术债 | 问题和改进项有负责人、期限和跟踪记录 |

### 需求到 Issue

需求评审通过后，把可交付工作拆成 Issue：

- 一个 Issue 只描述一个可验收结果。
- 标题使用 `[Task]`、`[Bug]`、`[Feature]`、`[Docs]` 或 `[Debt]` 前缀。
- 描述中写清背景、范围、非目标、验收标准和依赖。
- 涉及跨仓库工作时，在相关仓库分别建立 Issue 并互相链接。
- 估算应说明假设和不确定性，不把未确认的工作写成承诺。

Issue 写法见 [Issue 规范](#issue-规范)。

### 技术方案到 PR

涉及系统架构、接口、数据库、部署方式或重要依赖变更时，先提交技术方案：

1. 在 Issue 中说明问题和约束。
2. 在项目 `docs/design/` 或本仓库 `projects/<repo>/` 提交方案。
3. 通过 Pull Request 评审方案。
4. 评审通过后再开始实现，必要时把方案拆成多个实现 Issue。

技术方案结构见 [技术方案与 ADR](#技术方案与-adr)。

### 开发与验证

- 从 `develop` 或 `main` 创建规范分支。
- 每个 Commit 只包含一个逻辑变化。
- 本地执行项目定义的 Lint、测试和构建。
- 涉及接口时同步维护 OpenAPI 或等价契约。
- 涉及数据库时提供向前迁移和回滚方案。
- 不提交真实配置、密钥和敏感数据。

### 提测与上线

提测前至少满足：

- 代码已合入 `develop` 或约定的集成分支。
- CI 构建、Lint 和测试通过。
- 冒烟用例通过。
- 已知问题和未覆盖范围已记录。

上线前至少满足：

- Release 版本和变更摘要已准备。
- 部署步骤、环境变量和数据迁移已确认。
- 监控、日志和健康检查可观察。
- 回滚条件和执行步骤明确。
- 关键变更已通知相关成员。

细节见 [测试与提测](#测试与提测)、[发布与回滚](#发布与回滚)。

### 复盘

项目交付或重要里程碑结束后，复盘文档至少包含：

- 目标和实际结果
- 做得好、做得不好的具体事实
- 问题和根因
- 改进项、负责人和期限
- 需要转为 Issue 的技术债或流程改进

复盘不是追责记录。改进项必须在 GitHub 中有对应 Issue 或文档，避免只停留在会议结论。

### Definition of Done

一个任务只有同时满足以下条件才算完成：

- 验收标准全部满足。
- 代码已通过 CI 和 Review。
- 必要测试已补充并通过。
- 接口、配置、部署或迁移说明已更新。
- 风险和回滚方式已记录。
- 相关 Issue 已关闭，后续工作已建立新 Issue。

## 技术方案与 ADR

技术方案用于在编码前确认问题、约束和取舍。小改动可以直接在 PR 描述中说明；涉及架构、接口、数据库、部署或重要依赖时，应单独提交设计文档。

### 何时必须写

- 新增或重构核心模块。
- 修改对外 API、数据模型或数据库结构。
- 引入重要框架、中间件或第三方服务。
- 改变部署、发布、监控或回滚方式。
- 存在多个方案且取舍会影响后续维护。

### 存放位置

| 类型 | 位置 |
| --- | --- |
| 跨项目规范或通用方案 | 本仓库对应章节 |
| 单项目方案 | 项目仓库 `docs/design/` |
| 需要集中展示的项目方案 | 本仓库 `projects/<repo>/design/` |

设计文档通过 Pull Request 提交和评审。评审结论留在 PR 中，不另外维护无法追溯的聊天记录。

### 推荐结构

```markdown
# 方案标题

## 背景与问题

## 目标

## 非目标

## 现状与约束

## 候选方案

## 决策

## 接口与数据变更

## 兼容性与迁移

## 安全、性能与可观测性

## 测试计划

## 发布与回滚

## 未决问题
```

### 写作要求

- 先写问题和约束，再写方案，不从技术选型倒推需求。
- 至少列出两个候选方案；只有一个方案时说明原因。
- 明确目标和非目标，避免范围持续膨胀。
- 接口变更给出请求、响应、错误码和兼容策略。
- 数据变更说明迁移顺序、数据校验和回滚条件。
- 记录被拒绝的方案及原因，减少后续重复讨论。
- 未决问题要有负责人和处理期限。

### ADR

当决策会影响长期维护时，可把结论单独整理为 ADR：

```text
docs/adr/0001-use-postgresql.md
docs/adr/0002-standardize-api-errors.md
```

ADR 只记录已经作出的决策、背景、后果和替代方案，不替代完整设计文档。

### 评审清单

- [ ] 问题、目标和非目标清晰
- [ ] 方案满足约束，风险和取舍已说明
- [ ] 接口、数据和部署影响已覆盖
- [ ] 兼容性和迁移方案可执行
- [ ] 测试与回滚方式明确
- [ ] 安全、性能和监控风险已评估
- [ ] 评审结论和未决事项已记录

## 测试与提测

测试的目标是让缺陷尽早暴露，并让交付结果可重复验证。已建立 Lint 和自动化测试框架的项目必须在 CI 中执行；尚未建立的项目至少执行类型检查、构建和现有测试，并创建 `technical debt` Issue 跟踪缺口，不能静默跳过。

### 测试层次

| 层级 | 关注内容 | 常见工具 |
| --- | --- | --- |
| 单元测试 | 函数、类和模块的边界与错误处理 | JUnit、pytest、Vitest |
| 集成测试 | 数据库、外部服务、消息和接口协作 | Testcontainers、pytest、Spring Boot Test |
| 端到端测试 | 关键用户流程和跨端链路 | Playwright、Cypress |
| 手工验收 | 无法稳定自动化的交互和视觉检查 | 测试用例和验收清单 |

不要求每个项目都覆盖所有层级，但关键路径必须有可重复验证方式。

### 测试命名与结构

- 测试名描述行为和预期，例如 `reject_empty_email`。
- 一个测试只验证一个主要行为。
- 测试数据使用固定 fixture 或工厂，不依赖个人环境。
- 外部服务优先使用 Mock、Stub 或测试容器。
- 不把真实账号、生产数据和密钥写入测试。

### 缺陷修复

修复 Bug 时：

1. 先用测试或最小复现脚本证明问题存在。
2. 修复后确保该测试通过。
3. 检查是否存在同类问题。
4. 在 PR 中说明根因、修复范围和回归验证。

### 提测准入

- [ ] 代码已合入 `develop` 或约定的集成分支
- [ ] CI 的 Lint、测试和构建通过
- [ ] 冒烟用例通过
- [ ] 测试环境可访问，配置和版本明确
- [ ] 功能范围、已知问题和回归范围已记录
- [ ] 数据库迁移和回滚步骤已准备

### 测试报告

测试报告至少包含：

- 测试版本、Commit 或 Tag
- 环境、依赖和部署方式
- 测试范围和未覆盖范围
- 用例结果和缺陷列表
- 阻塞问题、风险和结论
- 建议上线或退回的条件

### Bug Issue

缺陷统一使用 Bug Report 模板，至少提供：

- 复现步骤
- 预期行为和实际行为
- 环境与版本
- 日志、截图或录屏
- 影响范围和严重程度
- 已尝试的排查方法

缺陷修复通过 PR 关联 Bug Issue，不直接修改主分支。

## 发布与回滚

发布是把已验证的变更交付到目标环境的过程。每次发布都必须有版本、变更记录、验证方式和回滚方案。

### 版本约定

优先使用 Semantic Versioning：

```text
MAJOR.MINOR.PATCH
```

- `MAJOR`：不兼容的 API 或行为变更
- `MINOR`：向后兼容的新功能
- `PATCH`：向后兼容的缺陷修复

Tag 示例：

```text
v1.4.0
v1.4.1
```

### 发布前

- [ ] 目标 Commit 已通过 CI、测试和 Review
- [ ] Release 说明列出新增、修复、破坏性变更和迁移步骤
- [ ] 配置、密钥和环境变量已确认，仓库中没有真实值
- [ ] 数据库迁移已完成备份、验证和回滚演练
- [ ] 部署脚本和镜像版本可追踪
- [ ] 监控、日志和健康检查可用
- [ ] 回滚条件、负责人和执行步骤明确
- [ ] 相关成员已收到发布通知

### 发布过程

1. 冻结发布范围，记录目标 Commit。
2. 构建并发布带唯一版本的镜像或制品。
3. 执行数据库迁移和配置变更。
4. 部署到预发布或灰度环境。
5. 执行冒烟测试和关键指标检查。
6. 按计划扩大流量或部署到生产环境。
7. 创建 Git Tag 和 GitHub Release。
8. 记录发布时间、版本、负责人和验证结果。

### Release 内容

Release 至少包含：

- 版本号和发布日期
- 变更摘要
- 破坏性变更和迁移说明
- 已知问题
- 验证结果
- 回滚方式

Release 说明由 PR 作者和维护者共同确认，不能只写"更新代码"。

### 回滚

回滚方案必须在发布前准备，而不是故障发生后临时决定。

- 明确触发条件，例如错误率、延迟、数据异常或关键功能不可用。
- 明确回滚命令、制品版本、数据库处理和责任人。
- 数据迁移优先采用向前兼容方案，避免不可逆变更。
- 回滚后执行健康检查和数据校验。
- 在 Issue 或复盘文档中记录故障时间线、影响和改进项。

### 热修复

热修复也应走分支、PR、CI 和 Review。紧急情况下可以缩短流程，但不能跳过安全检查和变更记录。修复完成后合并回主分支，并补充回归测试。

## 技术文档规范

技术文档是代码的一部分，应随代码一起评审、版本化和更新。GitHub 维护技术实现；飞书维护组织制度和人事信息。

### 文档类型

| 类型 | 内容 | 建议位置 |
| --- | --- | --- |
| README | 项目目标、运行方式、目录和常见操作 | 仓库根目录 |
| 设计文档 | 架构、方案、取舍和风险 | `docs/design/` |
| ADR | 已确认的重要技术决策 | `docs/adr/` |
| 接口文档 | API、事件、错误码和示例 | `docs/api/` 或 OpenAPI 文件 |
| 部署文档 | 环境、配置、发布、监控和回滚 | `docs/deploy/` |
| 测试文档 | 测试计划、用例和报告 | `docs/testing/` |
| 复盘文档 | 结果、问题、根因和改进项 | `docs/retrospective/` |
| 组织级规范 | 跨项目协作和技术标准 | 本仓库 |

### 写作要求

- 标题直接说明主题，不使用空泛口号。
- 开头说明读者、目的、适用范围和前置条件。
- 命令可复制执行，路径和版本明确。
- 代码块标注语言。
- 外部链接说明用途，内部链接使用锚点。
- 不写真实账号、密钥、服务器地址或企业数据。
- 变更行为时同步更新文档，不用"稍后补充"代替交付。

### README 最低要求

每个代码仓库的 README 至少包含：

1. 项目一句话说明
2. 适用场景和主要功能
3. 环境要求
4. 安装、启动和测试命令
5. 配置说明和 `.env.example`
6. 目录结构
7. 贡献方式
8. 许可证或可见性说明

### 文档评审

- 新增或修改设计、接口和部署文档时通过 PR 提交。
- 代码与文档不一致时，先判断哪个是权威来源，再修正另一边。
- 示例命令应在干净环境中验证。
- 文档变更需要 Reviewer 确认读者能按步骤完成操作。
