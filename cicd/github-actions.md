# GitHub Actions 实践

GitHub Actions 是 CodeLab 的 CI 引擎：代码推到 GitHub 后自动执行检查。

## 一个 Workflow 长什么样

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [develop]
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.12"
      - run: pip install -r requirements.txt
      - run: pytest
```

## 三要素

- **on**：何时触发（push / pull_request / 定时 schedule）
- **jobs**：任务（并行或串行）
- **steps**：步骤（checkout、装依赖、跑测试……）

## CodeLab 的用法

- 新项目直接用 [templates](https://github.com/nynu-codelab/templates) 自带的 `ci.yml`，改一改即可
- 公共工作流放在 [.github 仓库](https://github.com/nynu-codelab/.github/tree/main/workflows)，支持复用的部分抽出来
- 不要在 workflow 里写死密钥，用 **Secrets**：

```yaml
- run: echo "${{ secrets.GHCR_TOKEN }}" | docker login ghcr.io -u ${{ github.actor }} --password-stdin
```

Secrets 在仓库 Settings → Secrets 中配置，值不可见。

## 组织级共享 Workflow

公共工作流放在 `.github/workflows/` 后，各项目可以复用：

```yaml
jobs:
  ci:
    uses: nynu-codelab/.github/.github/workflows/python-ci.yml@main
```

> 如果复用明显增加理解成本，优先在项目内直接写 workflow，保持简单。

## 常见问题

- 跑失败先看 Actions 页面的日志
- 权限问题：workflow 需要 `permissions` 声明（模板已配好）
- 想跳过 CI：commit message 含 `[skip ci]`（少用）

## 下一步

- 整体管线：[overview.md](overview.md)
- Docker 构建与推送：[../docker/overview.md](../docker/overview.md)
