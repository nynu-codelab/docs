# Agent 开发

Agent（智能体）= 大模型 + 工具 + 循环：模型根据目标，调用工具、观察结果、继续行动。

## 核心组成

```text
LLM（大模型）       负责理解与决策
  ↓ 生成动作
Tools（工具）       让模型能操作外部世界：搜索、算数、调 API、读文件
  ↓ 结果返回
循环（Loop）        模型看到结果 → 决定下一步 → 直到完成
```

## 最小结构

```python
class Agent:
    def __init__(self, llm, tools):
        self.llm = llm
        self.tools = {t.name: t for t in tools}

    def run(self, task: str) -> str:
        messages = [{"role": "user", "content": task}]
        for _ in range(10):            # 限制最大步数
            reply = self.llm.chat(messages, tools=self.tools)
            call = reply.tool_call
            if call is None:           # 模型决定结束
                return reply.content
            result = self.tools[call.name].run(**call.args)
            messages.append({"role": "tool", "content": result})
        return "达到最大步数"
```

## 设计要点

- **工具要有清晰的名字和描述**：模型靠描述决定调用哪个
- **工具参数用 JSON Schema**：约束模型输出格式
- **必须有步数上限和超时**：防止死循环
- **日志记录每一步**：模型调用、工具调用、结果，便于调试
- **密钥走 .env**：`LLM_API_KEY=`，不绑定单一供应商

## 常见坑

- 模型返回格式不合法：加 retry + 错误回传
- 工具异常：把异常信息作为结果回传给模型，让它自己调整
- 成本失控：限制步数、限制上下文长度、记录 token

## 在 CodeLab 实践

- 直接使用 [ai-agent-template](https://github.com/nynu-codelab/templates/tree/main/ai-agent-template)：已内置 LLM 抽象、Tool、Agent、日志、测试
- 先做能跑通的小 Agent，再加工具、加记忆、加 RAG

## 下一步

- RAG：[rag.md](rag.md)
- 模板：[templates/ai-agent-template](https://github.com/nynu-codelab/templates/tree/main/ai-agent-template)
