# TypeScript 实践

CodeLab 前端与部分后端（Node）技术栈。模板见 [typescript-template](https://github.com/nynu-codelab/templates/tree/main/typescript-template)。

## 版本与工具

- Node.js LTS（22+）
- TypeScript 严格模式
- ESLint + Prettier（代码规范）
- Vitest（测试）
- 前端框架：Vue 3（默认）/ React（按项目需要）

## 标准结构

```text
src/
├── index.ts        # 入口
├── greet.ts        # 业务模块
└── ...
tests/              # 或 *.test.ts 与源码同目录
├── greet.test.ts
├── package.json
├── tsconfig.json
└── eslint.config.js
```

## 常用命令

```bash
npm install          # 安装依赖
npm run dev          # 本地开发
npm run lint         # ESLint 检查
npm run typecheck    # tsc --noEmit
npm test             # Vitest
npm run build        # tsc 构建
```

## 规范要点

- **严格模式**：`tsconfig.json` 开启 `strict`，避免 `any` 泛滥
- **类型优先**：接口、DTO 都定义类型，不用魔法字符串
- **格式化统一**：Prettier 配置固定，CI 检查
- **依赖管理**：提交 `package-lock.json`，保证可复现
- **环境变量**：`.env` 读取，`.env.example` 提交

## 下一步

- 用模板建项目：[templates/typescript-template](https://github.com/nynu-codelab/templates/tree/main/typescript-template)
- 前后端一体项目：[templates/fullstack-template](https://github.com/nynu-codelab/templates/tree/main/fullstack-template)
