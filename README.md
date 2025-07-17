[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/bassnova91-supamcp-badge.png)](https://mseep.ai/app/bassnova91-supamcp)

# Supabase MCP Server

## 概述

Supabase MCP Server 是一个基于 Python 的 Model Context Protocol (MCP) 服务器，旨在让 AI 工具（如 Cursor、Claude 等）通过标准协议与 Supabase 数据库进行交互。它支持表数据的查询、插入、更新和删除，所有操作均通过 Supabase 官方 Python SDK 实现，安全、可扩展、易于集成。

- **主要功能**：
  - 查询表记录（支持条件、排序、分页）
  - 插入单条/多条记录
  - 更新记录（支持条件）
  - 删除记录（支持条件）
- **技术栈**：Python 3.10+、FastAPI、supabase-py、Pydantic、Pytest
- **架构**：所有数据库连接参数通过环境变量配置，核心逻辑模块化，便于扩展和维护。

## 目录结构

```
supabase-mcp-server/
├── supa_mcp/
│   ├── server.py           # MCP 服务器主入口，所有工具注册于此
│   ├── tools.py            # 额外工具函数示例
│   ├── config.py           # 环境变量与配置管理
│   ├── supabase_client.py  # Supabase 客户端适配（预留）
│   └── __init__.py
├── tests/
│   └── supa_mcp/
│       └── test_tools.py   # 单元测试（可扩展）
├── requirements.txt        # 依赖包列表
├── Planning.md             # 项目规划与架构说明
├── Task.md                 # 任务追踪与进度
```

## 安装步骤

1. **克隆仓库**
   ```bash
   git clone <your-repo-url>
   cd supabase-mcp-server
   ```

2. **创建虚拟环境并激活**
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **安装依赖**
   ```bash
   pip install -r requirements.txt
   ```

4. **配置环境变量**

   在项目根目录下创建 `.env` 文件，内容如下（请替换为你的 Supabase 项目参数）：

   ```env
   SUPABASE_URL=https://your-project.supabase.co
   SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
   ```

## 在 Cursor 中运行

1. **启动 MCP 服务器**

   在 Cursor 的终端中运行：

   ```bash
   python -m supa_mcp.server
   ```

   或直接：

   ```bash
   python supa_mcp/server.py
   ```

   服务器将以 stdio 方式运行，等待 MCP 客户端（如 Cursor）连接。

2. **在 Cursor 侧连接 MCP Server**

   - 打开 Cursor，选择"连接 MCP 服务器"。
   - 填写本地 MCP 服务器的启动命令（如上）。
   - 连接后即可通过自然语言或代码指令操作 Supabase 数据库。

## 运行测试

本项目采用 Pytest 进行单元测试。测试文件位于 `tests/` 目录下。

```bash
pytest
```

## 常见问题

- **环境变量未配置或错误**：请确保 `.env` 文件存在且内容正确。
- **依赖安装失败**：请使用 Python 3.10 及以上版本，并确保虚拟环境已激活。
- **Supabase 权限问题**：请使用 Service Role Key，避免使用匿名或公开密钥。

## 参考文档

- [Supabase 官方文档](https://supabase.com/docs)
- [supabase-py SDK](https://github.com/supabase-community/supabase-py)
- [Model Context Protocol (MCP)](https://github.com/context-labs/model-context-protocol)

---

如需扩展功能或遇到问题，请查阅 `Planning.md` 和 `Task.md`，或提交 Issue。
