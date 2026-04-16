# N8N

更新时间：2026-04-16

对于面向客户、可保证接入的方案，推荐只使用 N8N 的 `HTTP Request` 节点接入 ApiHalo。

不再把 N8N 的 `OpenAI` 节点作为标准接法。这样可以避免节点版本差异、字段限制和网关能力差异带来的不确定性。

## 一、接入前准备

- ApiHalo API Key
- 一个来自 `GET /v1/models` 的真实模型 ID

## 二、先获取模型

```bash
curl https://apihalo.com/v1/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

请选择当前 Key 可见的真实模型 ID。

## 三、标准接法：HTTP Request 节点

### 方法

`POST`

### URL

```text
https://apihalo.com/v1/chat/completions
```

### Headers

```json
{
  "Authorization": "Bearer YOUR_API_KEY",
  "Content-Type": "application/json"
}
```

### Body

```json
{
  "model": "YOUR_MODEL_ID",
  "messages": [
    {
      "role": "user",
      "content": "你好"
    }
  ]
}
```

## 四、第一次测试建议

建议第一次先发送一个最小请求：

```json
{
  "model": "YOUR_MODEL_ID",
  "messages": [
    {
      "role": "user",
      "content": "Reply with OK only."
    }
  ]
}
```

## 五、如果需要其他接口

在 N8N 中继续使用 `HTTP Request` 节点即可，只需要更换 URL 和请求体。

常见示例：

- 文本对话：`POST https://apihalo.com/v1/chat/completions`
- Responses API：`POST https://apihalo.com/v1/responses`
- Embeddings：`POST https://apihalo.com/v1/embeddings`
- 图像生成：`POST https://apihalo.com/v1/images/generations`

如果使用 `POST /v1/responses`，请先确认目标模型已经开放该能力。

## 六、最稳的结论

- N8N 面向客户的标准接法，优先只写 `HTTP Request`
- 不要求客户依赖某个特定版本的 `OpenAI` 节点
- 这样写出的工作流，更稳定，也更不受 N8N 版本变化影响

## 七、后续更换上游是否受影响

不受影响。

因为 N8N 工作流调用的是 ApiHalo 的公开地址，而不是你后面的上游渠道地址。
