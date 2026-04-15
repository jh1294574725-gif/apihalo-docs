# N8N

更新时间：2026-04-15

N8N 通常按 OpenAI 节点或 HTTP Request 节点接入。

## 一、接入前准备

- ApiHalo API Key
- ApiHalo Base URL：`https://apihalo.com/v1`
- 一个来自 `GET /v1/models` 的真实模型 ID

## 二、快速接入

### 第 1 步：先获取模型

```bash
curl https://apihalo.com/v1/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### 第 2 步：方式一，OpenAI 节点

如果你的 N8N 版本支持自定义 OpenAI Base URL：

- Base URL：`https://apihalo.com/v1`
- API Key：ApiHalo API Key
- Model：从 `/v1/models` 返回结果选择

### 第 3 步：方式二，HTTP Request 节点

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

## 三、测试建议

第一次接入时，建议先让工作流发送一条简单请求，例如：

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

## 四、建议

- 第一次先用 HTTP Request 节点验证最稳
- 验证通过后，再封装成自己的工作流模板
