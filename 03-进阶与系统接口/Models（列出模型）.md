# Models（列出模型）

更新时间：2026-04-15

模型列表接口是整套接入文档里最重要的接口之一。无论最终调用的是聊天、向量、图像、视频、Rerank，还是开发工具场景，都应该先查看 `/v1/models`。

## 一、接口地址

```text
GET https://apihalo.com/v1/models
```

## 二、请求示例

```bash
curl https://apihalo.com/v1/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 三、这个接口的作用

调用 `/v1/models` 的主要目的包括：

- 获取当前 Key 真实可用模型
- 获取真实模型 ID
- 判断模型支持的端点类型
- 判断是否适合聊天、图片、视频、Rerank 或 Responses API 等场景

## 四、响应示例

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

## 五、常见返回字段说明

| 字段 | 说明 |
| --- | --- |
| `id` | 模型 ID，正式请求时应直接使用该值 |
| `object` | 对象类型 |
| `owned_by` | 来源标记 |
| `supported_endpoint_types` | 当前模型支持的接口入口类型 |

## 六、`supported_endpoint_types` 怎么看

它表示当前模型可用的接口入口类型。

常见用途：

- 判断是否适合走 `chat/completions`
- 判断是否适合走 `responses`
- 判断是否属于图像、视频、Rerank 等专项能力
- 辅助前端、控制台或调用端做模型分类

常见值说明：

| 值 | 对应含义 |
| --- | --- |
| `openai` | 可用于 `POST /v1/chat/completions` |
| `openai-response` | 可用于 `POST /v1/responses` |
| `openai-response-compact` | 可用于 `POST /v1/responses/compact` |
| `image-generation` | 可用于 `POST /v1/images/generations` |
| `jina-rerank` | 可用于 `POST /v1/rerank` |

其中：

- 普通 SDK、聊天工具通常优先使用 `openai`
- Codex 这类自定义 Provider 场景优先验证 `openai-response`

## 七、正确接入顺序

1. 先调用 `/v1/models`
2. 从结果中选择一个模型 ID
3. 按模型能力选择对应端点
4. 再发起正式请求

## 八、最常见的错误

- 把其他平台的模型总表直接复制到业务里
- 把模型名写死在前端或配置文件中长期不刷新
- 不看 `supported_endpoint_types` 就直接调用某个高级接口

## 九、结论

如果只记住一个接口，请记住 `/v1/models`。
