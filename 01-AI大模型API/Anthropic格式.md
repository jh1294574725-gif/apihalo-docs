# Anthropic格式

更新时间：2026-04-15

本页是可选接入页。

只有当现有客户端、SDK 或业务系统必须使用 Anthropic `Messages API` 格式，且当前 Key 已开通对应能力时，才建议使用本页。

默认情况下，仍然建议优先使用 [OpenAI格式（支持各大原厂模型）](OpenAI格式（支持各大原厂模型）.md)。

## 一、适用场景

- 系统已经绑定 Anthropic 原生 SDK
- 现有业务逻辑必须使用 `Messages API`
- 目标模型已支持该协议

## 二、接入前准备

| 配置项 | 推荐值 |
| --- | --- |
| API Key | ApiHalo API Key |
| 请求地址 | `https://apihalo.com/v1/messages` |
| 协议版本头 | `anthropic-version: 2023-06-01` |
| 模型名 | 先通过 `/v1/models` 获取 |

## 三、请求地址

```text
POST https://apihalo.com/v1/messages
```

## 四、请求头

```http
x-api-key: YOUR_API_KEY
anthropic-version: 2023-06-01
Content-Type: application/json
```

## 五、请求示例

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

## 六、模型选择方式

建议先调用：

```bash
curl https://apihalo.com/v1/models \
  -H "x-api-key: YOUR_API_KEY" \
  -H "anthropic-version: 2023-06-01"
```

## 七、使用建议

- 新接入优先用 OpenAI 兼容格式
- 只有在系统必须兼容 Anthropic SDK 时，再使用本页
- 如果某个模型在 Anthropic 原生协议下不可用，请改回 OpenAI 兼容格式
