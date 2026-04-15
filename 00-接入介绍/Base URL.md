# Base URL

更新时间：2026-04-15

## 默认地址

ApiHalo 的默认 OpenAI 兼容地址是：

```text
https://apihalo.com/v1
```

## 什么时候只填域名

如果你的 SDK、插件或客户端会自动补 `/v1`，请填写：

```text
https://apihalo.com
```

## 常见填写方式

### OpenAI SDK

```text
base_url = https://apihalo.com/v1
```

### 第三方工具

- 如果字段名是 `Base URL` 或 `Endpoint`，优先填 `https://apihalo.com/v1`
- 如果工具说明里明确写着“会自动拼接 `/v1`”，就填 `https://apihalo.com`

## 常见错误

错误示例：

- `https://apihalo.com/v1/`
- `https://apihalo.com/v1/chat/completions`
- `https://openrouter.ai/api/v1`

说明：

- Base URL 只填网关根地址，不要直接填某个具体接口路径
- 公开接入不要直接填写其他平台地址

## 常用完整接口示例

- `GET https://apihalo.com/v1/models`
- `POST https://apihalo.com/v1/chat/completions`
- `POST https://apihalo.com/v1/embeddings`
- `POST https://apihalo.com/v1/images/generations`
- `POST https://apihalo.com/v1/audio/transcriptions`
- `POST https://apihalo.com/v1/videos`

## 结论

不确定时，优先填写：

```text
https://apihalo.com/v1
```
