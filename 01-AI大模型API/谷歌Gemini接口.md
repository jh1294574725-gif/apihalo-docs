# 谷歌Gemini接口

更新时间：2026-04-15

本页是可选接入页。

只有在现有客户端明确要求 Gemini 原生协议时，才建议使用本页。默认仍然推荐使用 [OpenAI格式（支持各大原厂模型）](OpenAI格式（支持各大原厂模型）.md)。

## 一、适用场景

- 已经使用 Gemini 原生 SDK
- 现有系统必须调用 Gemini 原生协议
- 目标模型已经开放 Gemini 原生能力

## 二、接入前准备

| 配置项 | 推荐值 |
| --- | --- |
| API Key | ApiHalo API Key |
| 请求地址 | `https://apihalo.com/v1beta/models/{model}:generateContent` |
| 模型名 | 先通过 `/v1beta/models` 或 `/v1/models` 获取 |

```text
# 基础配置
Request URL = "https://apihalo.com/v1beta/models/{model}:generateContent"
API Key = "你的 ApiHalo API Key"
Model = "请替换为 /v1beta/models 或 /v1/models 返回的真实模型 ID"
```

## 三、请求地址

```text
POST https://apihalo.com/v1beta/models/{model}:generateContent
```

## 四、鉴权方式

可以使用以下任一方式：

- `x-goog-api-key: YOUR_API_KEY`
- `?key=YOUR_API_KEY`

## 五、请求示例

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

## 六、模型列出

```bash
curl "https://apihalo.com/v1beta/models?key=YOUR_API_KEY"
```

## 七、使用建议

- 只有在系统已经依赖 Gemini 原生 SDK 时再使用本页
- 新系统默认优先用 OpenAI 兼容格式
