# 约定与规范

- JSON 响应：统一使用 `SuccessResponse` / `ErrorResponse`
- 错误码命名：`<DOMAIN>_<ACTION>_<RESULT>`（如 `PUBLISH_FAILED`）
- 日志字段：方法、路径、账号、状态码；错误附加 `details`
- 目录组织：功能分层清晰；动作层位于 `xiaohongshu/*`
- 参数校验：使用 `binding` tag，必要参数必填
