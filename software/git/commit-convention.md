# Commit 规范

统一的 Commit 信息让历史清晰、可回溯、可自动生成 changelog。

## 格式

```text
type(scope): description
```

- `type`：提交类型（见下表）
- `scope`：可选，影响的范围，如模块名
- `description`：简短描述，建议英文，首字母小写

## 类型

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

## 好与坏的例子

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

## 小贴士

- 一次 Commit 只做一件事（一个功能 / 一个修复）
- Commit 信息能说明“为什么改”更好：`fix: retry db connection to avoid startup failure`
- 用 `git commit -m` 写单行信息足够；复杂改动用 `-m` 多次分段
- 不要在 Commit 里夹带无关文件的修改

## 下一步

- 分支怎么建：[branching.md](branching.md)
- PR 标题同样遵循本规范（有 CI 自动检查）
