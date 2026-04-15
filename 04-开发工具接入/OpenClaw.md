# OpenClaw

更新时间：2026-04-15

本页适用于支持 `OpenAI` 或 `OpenAI Compatible` 自定义网关的 OpenClaw 版本。

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

### 第 2 步：填写方式

- Provider：`OpenAI` / `OpenAI Compatible` / `Custom`
- Base URL：`https://apihalo.com/v1`
- API Key：ApiHalo API Key
- Model：从 `GET /v1/models` 返回结果中选择

### 第 3 步：完成一次简单测试

建议先发起一条最小请求，确认模型可正常返回内容。

## 三、常见问题

如果客户端会自动补 `/v1`，则 Base URL 改填：

```text
https://apihalo.com
```
