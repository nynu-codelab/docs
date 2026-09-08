# Python 实践

CodeLab 的 Python 用于算法、AI、后端（FastAPI）与自动化。模板见 [python-template](https://github.com/nynu-codelab/templates/tree/main/python-template)。

## 版本与工具

- Python 3.12
- 包管理：**uv**（简单、快，替代 pip + venv）
- 代码规范：ruff（lint + format）
- 测试：pytest

## 标准结构

```text
src/xxx/
├── __init__.py
├── main.py        # 入口（CLI / FastAPI）
├── config.py      # 配置（读取环境变量）
└── ...
tests/
├── test_xxx.py
├── pyproject.toml  # 项目与依赖声明
└── .python-version # 固定 3.12
```

## 日常命令（uv）

```bash
uv sync                    # 安装依赖（读取 pyproject.toml）
uv run python src/main.py  # 运行
uv run pytest              # 测试
uv run ruff check .        # lint
uv run ruff format .       # 格式化
```

## 规范要点

- **配置走环境变量**：`python-dotenv` 或 pydantic-settings 读取 `.env`
- **类型标注**：函数签名加类型，`mypy` 可选
- **依赖声明**：在 `pyproject.toml` 的 `[project] dependencies` 中声明，不用 `requirements.txt`（除非项目特殊）
- **测试覆盖**：核心逻辑必须有 pytest 测试
- **AI 项目**：密钥只放 `.env`，代码不出现真实 key

## FastAPI 快速开始

```python
from fastapi import FastAPI

app = FastAPI(title="codelab api")

@app.get("/api/health")
def health():
    return {"status": "ok"}
```

```bash
uv run uvicorn src.xxx.main:app --reload
```

## 下一步

- 用模板建项目：[templates/python-template](https://github.com/nynu-codelab/templates/tree/main/python-template)
- AI / Agent 项目：[../ai/overview.md](../ai/overview.md)
