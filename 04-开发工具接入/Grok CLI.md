# Grok CLI

更新时间：2026-04-15

如果你的 Grok CLI 版本支持自定义 OpenAI 兼容网关，可按本页配置。

## 接入前准备

- ApiHalo API Key
- ApiHalo Base URL：`https://apihalo.com/v1`
- 一个来自 `GET /v1/models` 的真实模型 ID

## 第一步：先获取模型

```bash
curl https://apihalo.com/v1/models \
  -H "Authorization: Bearer YOUR_API_KEY"
```

## 第二步：填写方式

- Endpoint / Base URL：`https://apihalo.com/v1`
- API Key：ApiHalo API Key
- Model：使用 `/v1/models` 返回的模型 ID

如果 CLI 会自动补 `/v1`，Base URL 改填：

```text
https://apihalo.com
```

## 第三步：完成一次简单测试

建议先发起一条最小请求，确认模型可正常返回内容。

## 说明

- 如果 CLI 不支持自定义网关，请不要直接套用本页
- 如果你只是想接入 Grok 系列模型，本质上仍然优先按 OpenAI 兼容方式接入
