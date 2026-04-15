# HTTP注意事项

更新时间：2026-04-15

## 基本请求头

绝大多数接口建议至少带上：

```http
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

## Base URL 只填根地址

正确：

```text
https://apihalo.com/v1
```

错误：

```text
https://apihalo.com/v1/chat/completions
```

## 流式响应

如果使用流式输出：

- 需要客户端支持 `text/event-stream`
- `curl` 建议加 `-N`
- 反向代理不要错误缓存流式响应

## Multipart 场景

以下场景常见使用 `multipart/form-data`：

- 音频转写
- 视频生成
- 需要上传本地文件的场景

## 超时与重试

建议：

- 文本请求设置合理超时
- 视频生成使用任务轮询，不要长连接一直等待
- 429、5xx 场景使用指数退避重试

## 大文件上传

如果你的文件较大：

- 优先压缩或裁剪无关内容
- 避免把超大文件直接塞进单次请求
- 先做小文件验证，再上正式文件

## 结论

大多数客户只要正确处理：

- 鉴权
- `Content-Type`
- 流式输出
- 轮询查询

就能稳定接入。
