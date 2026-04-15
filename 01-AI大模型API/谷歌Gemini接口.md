# 谷歌Gemini接口

更新时间：2026-04-15

本页是可选接入页。

只有在你的客户端明确要求 Gemini 原生协议时，才使用本页。默认仍然推荐使用 [OpenAI格式（支持各大原厂模型）](OpenAI格式（支持各大原厂模型）.md)。

## 请求地址

```text
POST https://apihalo.com/v1beta/models/{model}:generateContent
```

## 鉴权方式

可以使用：

- `x-goog-api-key: YOUR_API_KEY`

或：

- `?key=YOUR_API_KEY`

## 请求示例

```bash
curl "https://apihalo.com/v1beta/models/YOUR_MODEL_ID:generateContent" \
  -H "x-goog-api-key: YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "contents": [
      {
        "parts": [
          {"text": "你好，请介绍一下自己"}
        ]
      }
    ]
  }'
```

## 模型列出

```bash
curl "https://apihalo.com/v1beta/models?key=YOUR_API_KEY"
```

## 适用建议

- 只有在现有系统已经依赖 Gemini 原生 SDK 时再用本页
- 新系统默认优先用 OpenAI 兼容格式
