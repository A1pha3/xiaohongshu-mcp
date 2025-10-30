# 模块说明（目录级）

- 入口与启动：`main.go`、`app_server.go`
- 路由与中间件：`routes.go`、`middleware.go`
- HTTP 处理器：`handlers_api.go`、`types.go`
- MCP 服务与工具：`mcp_server.go`、`mcp_handlers.go`
- 业务服务：`service.go`
- 浏览器封装：`browser/browser.go`
- 配置与常量：`configs/*`
- 站点动作层：`xiaohongshu/*`（login/publish/search/feeds/feed_detail/comment/like_favorite/user_profile）
- 其他：`pkg/*`（downloader 等）、`cookies/*`

每个模块的详细接口与数据结构，见对应章节与代码走读。
