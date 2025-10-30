# 快速上手（建议从这里开始）

目标：在最短时间内完成登录与服务启动，并通过 MCP Inspector 验证工具可用。

## 1. 安装与环境

- 方式一：直接下载二进制（推荐）
  - 从 Releases 下载 `xiaohongshu-mcp-*` 与 `xiaohongshu-login-*`
  - `chmod +x` 后直接执行
- 方式二：源码运行
  - 安装 Go（建议 1.22+），配置 `GOPROXY`
  - 在项目根执行 `go run .` 与 `go run cmd/login/main.go`
- 方式三：Docker
  - `docker pull xpzouying/xiaohongshu-mcp`
  - 使用提供的 `docker-compose.yml` 启动

## 2. 首次登录

- 运行登录工具展示二维码：
  ```bash
  ./xiaohongshu-login-<platform>
  # 或：go run cmd/login/main.go
  ```
- 使用手机 App 扫码登录；登录后会在 `./data` 持久化 Cookies

## 3. 启动服务

```bash
# 默认无头
./xiaohongshu-mcp-<platform>
# 有界面
./xiaohongshu-mcp-<platform> -headless=false
# 自定义端口（默认 18060）
./xiaohongshu-mcp-<platform> -port=18060
```

## 4. 验证 MCP

- CLI 验证：
  ```bash
  curl -X POST http://localhost:18060/mcp \
    -H "Content-Type: application/json" \
    -d '{"jsonrpc":"2.0","method":"initialize","params":{},"id":1}'
  ```
- Inspector：
  ```bash
  npx @modelcontextprotocol/inspector
  # 在浏览器中配置 http://localhost:18060/mcp 并 Connect
  ```

## 5. 客户端接入

- Cursor：在 `.cursor/mcp.json` 配置服务地址
- VSCode：命令面板运行 `MCP: Add Server`，或 `.vscode/mcp.json`
- Cline/Gemini CLI：按各自说明配置 `http://localhost:18060/mcp`

## 6. 常见问题速查

- 登录二维码过期、被“踢下线”、端口占用、图片路径不可达等 → 见 `docs/faq.md`

更多图文动效与演示，见项目根 `README.md`。