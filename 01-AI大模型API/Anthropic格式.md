# Anthropic格式

更新时间：2026-04-15

本页是可选接入页。

只有当你的客户端必须使用 Anthropic `Messages API` 格式，且你的账号已开通对应能力时，才使用本页。

默认情况下，仍然建议优先使用 [OpenAI格式（支持各大原厂模型）](OpenAI格式（支持各大原厂模型）.md)。

## 请求地址

```text
POST https://apihalo.com/v1/messages
```

## 请求头

```http
x-api-key: YOUR_API_KEY
anthropic-version: 2023-06-01
Content-Type: application/json
```

## 请求示例

```bash
curl https://apihalo.com/v1/messages \
  -H "x-api-key: YOUR_API_KEY" \
  -H "anthropic-version: 2023-06-01" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "YOUR_MODEL_ID",
    "max_tokens": 1024,
    "messages": [
      {"role": "user", "content": "你好，请介绍一下自己"}
    ]
  }'
```

## 模型选择

仍然建议先调用：

```bash
curl https://apihalo.com/v1/models \
  -H "x-api-key: YOUR_API_KEY" \
  -H "anthropic-version: 2023-06-01"
```

## 适用建议

- 如果你是新接入，优先用 OpenAI 兼容格式
- 只有在现有系统必须兼容 Anthropic SDK 时，再使用本页
- 如果某个模型在 Anthropic 原生协议下不可用，请改回 OpenAI 兼容格式
