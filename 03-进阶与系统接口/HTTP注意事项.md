# HTTP注意事项

更新时间：2026-04-15

本页用于说明公开接口调用时最容易忽略的 HTTP 层注意事项。

## 一、最基本的请求头

绝大多数接口建议至少带上：

```http
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

## 二、Base URL 只填根地址

正确示例：

```text
https://apihalo.com/v1
```

错误示例：

```text
https://apihalo.com/v1/chat/completions
```

## 三、流式响应注意事项

如果使用流式输出：

- 客户端需要支持 `text/event-stream`
- `curl` 建议加 `-N`
- 反向代理、网关、CDN 不要错误缓存流式响应

## 四、Multipart 场景

以下场景常见使用 `multipart/form-data`：

- 音频转写
- 视频生成
- 上传本地文件的场景

## 五、超时与重试

建议如下：

- 文本请求设置合理超时
- 视频生成使用任务轮询，不要长连接一直等待
- 遇到 `429`、`5xx` 时使用指数退避重试

## 六、大文件上传建议

如果文件较大：

- 优先压缩或裁剪无关内容
- 避免把超大文件直接塞进单次请求
- 建议先做小文件验证，再上正式文件

## 七、结论

大多数客户只要正确处理以下 4 项，就能稳定接入：

- 鉴权
- `Content-Type`
- 流式输出
- 异步轮询查询
