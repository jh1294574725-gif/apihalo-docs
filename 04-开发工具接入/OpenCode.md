# OpenCode

更新时间：2026-04-15

本页适用于支持自定义 OpenAI 兼容入口的 OpenCode 客户端。

## 接入前准备

- ApiHalo API Key
- ApiHalo Base URL：`https://apihalo.com/v1`
- 一个来自 `GET /v1/models` 的真实模型 ID

## 第一步：获取可用模型

```bash
curl https://apihalo.com/v1/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 第二步：填写连接信息

不同版本的 OpenCode 字段名称可能略有差异，可按下列原则填写：

- Provider：`OpenAI` / `Compatible`
- Base URL：`https://apihalo.com/v1`
- API Key：ApiHalo API Key
- Model：从 `/v1/models` 返回结果中选择

如果客户端会自动补 `/v1`，Base URL 改填：

```text
https://apihalo.com
```

## 第三步：先做一次简单测试

建议先发起一条最小请求，确认模型可正常返回内容。

## 注意事项

- 如果模型切换后不可用，请重新拉取一次 `/v1/models`
- 不要写死其他平台的模型名
