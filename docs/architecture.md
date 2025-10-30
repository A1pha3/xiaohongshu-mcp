# 架构设计与数据流

- 整体架构：HTTP(REST) + MCP(Streamable HTTP)
- 关键组件：`AppServer`、`XiaohongshuService`、`MCP Server`、`handlers`、`routes`、`configs`、`browser`、`xiaohongshu/*`

## 1. 组件关系（Mermaid）

```mermaid
flowchart LR
  Client[AI/CLI Clients] -->|HTTP| REST[REST API]
  Client -->|MCP| MCPServer[MCP Server]
  REST --> Handlers[handlers_api]
  MCPServer --> MCPHandlers[mcp_handlers]
  Handlers --> Service[XiaohongshuService]
  MCPHandlers --> Service
  Service --> Actions[xiaohongshu Actions]
  Service --> Browser[Browser Wrapper]
  Browser --> Cookies[(cookies store)]
  Service --> Respond[Success/Error Response]
```

## 2. 请求生命周期（Sequence）

```mermaid
sequenceDiagram
  participant C as Client
  participant R as Gin Router/Handlers
  participant S as XiaohongshuService
  participant A as Actions
  participant B as Browser
  C->>R: POST /api/v1/publish
  R->>S: Validate & Dispatch
  S->>A: NewPublishImageAction.Publish
  A->>B: Navigate, Upload, Submit
  B-->>A: Result
  A-->>S: Domain Result
  S-->>R: SuccessResponse
  R-->>C: 200 OK
```

## 3. 错误与日志

- 统一响应：`SuccessResponse` / `ErrorResponse`
- 日志分层：入口、服务、动作层关键字段（方法、路径、账号、耗时、错误详情）

## 4. 会话与状态

- 会话持久：`./data` cookies 存储，首次登录后自动加载
- 浏览器封装：`browser.NewBrowser` 管理实例、语言/字体设置、下载目录

## 5. 依赖关系与扩展

- Service 依赖 Actions 与 Browser；Handlers/MCPHandlers 依赖 Service
- 新增能力时保持分层：入口 -> 处理器 -> 服务 -> 动作 -> 浏览器/外部
