# Models（列出模型）

更新时间：2026-04-15

模型列表接口是整个接入文档里最重要的接口之一。

## 请求地址

```text
GET https://apihalo.com/v1/models
```

## 请求示例

```bash
curl https://apihalo.com/v1/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 响应中重点看什么

- 使用返回结果中的 `data[].id` 作为真实模型 ID
- 使用返回结果中的 `supported_endpoint_types` 判断模型端点类型
- 不要照搬别的平台模型清单

## 响应示例

```json
{
  "object": "list",
  "data": [
    {
      "id": "YOUR_MODEL_ID",
      "object": "model",
      "owned_by": "apihalo",
      "supported_endpoint_types": [
        "openai",
        "openai-response"
      ]
    }
  ]
}
```

## 常见返回字段

- `id`：模型 ID
- `object`：对象类型
- `owned_by`：来源标记
- `supported_endpoint_types`：当前模型支持的端点类型

## `supported_endpoint_types` 怎么看

它表示这个模型当前可用的接口入口类型。

常见用途：

- 判断是否适合走 `chat/completions`
- 判断是否属于图像、视频、Rerank 等专项能力
- 辅助前端筛选模型分类

常见值说明：

- `openai`：可用于 `POST /v1/chat/completions`
- `openai-response`：可用于 `POST /v1/responses`
- `openai-response-compact`：可用于 `POST /v1/responses/compact`
- `image-generation`：可用于 `POST /v1/images/generations`
- `jina-rerank`：可用于 `POST /v1/rerank`

其中：

- 普通 SDK、聊天工具通常优先使用 `openai`
- Codex 这类自定义 Provider 场景优先验证 `openai-response`

## 正确接入顺序

1. 拉取 `/v1/models`
2. 从结果中选一个模型
3. 按模型能力选择对应端点
4. 再发起正式请求

## 错误示例

- 把其他平台的模型总表直接复制到业务里
- 把模型名写死在前端，不做刷新

## 结论

如果你只记住一个接口，请记住 `/v1/models`。
