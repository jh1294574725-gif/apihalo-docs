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

## 你应该如何使用它

- 使用返回结果中的 `data[].id` 作为真实模型 ID
- 使用返回结果中的 `supported_endpoint_types` 判断模型端点类型
- 不要照搬别的平台模型清单

## 常见返回字段

- `id`：模型 ID
- `object`：对象类型
- `owned_by`：来源标记
- `supported_endpoint_types`：当前模型支持的端点类型

## `supported_endpoint_types` 怎么看

你可以把它理解为“这个模型当前支持哪类接口入口”。

常见用途：

- 判断是否适合走 `chat/completions`
- 判断是否属于图像、视频、Rerank 等专项能力
- 辅助前端筛选模型分类

## 正确接入顺序

1. 拉取 `/v1/models`
2. 从结果中选一个模型
3. 再发起正式请求

## 错误示例

- 把 OpenRouter 或其他上游平台的模型总表直接复制到业务里
- 把模型名写死在前端，不做刷新

## 结论

如果你只记住一个接口，请记住 `/v1/models`。
